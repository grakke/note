# [lucene-solr](https://github.com/apache/lucene-solr)

Apache Lucene is a high-performance, full featured text search engine library written in Java. <https://lucene.apache.org/>

* 一种高性能、可伸缩的信息搜索（IR）库，在2000年开源，最初由鼎鼎大名的Doug Cutting开发，是基于Java实现的高性能的开源项目
* 采用基于倒排表的设计，非常高效地实现文本查找，底层采用了分段存储模式，在读写时几乎完全避免了锁的出现，大大提升了读写性能
* 一个工具包，不是一个完整的全文检索引擎,目的:为软件开发人员提供一个简单易用工具包，方便在目标系统中实现全文检索的功能，或者是以此为基础建立起完整的全文检索引擎

## 索引原理

* 从词出发，记载了这个词在哪些文档中出现过，由两部分组成——词典和倒排表

## 词典 Term Dictionary

* 词条 Term： 索引里面最小存储和查询单元，对于英文是一个单词，对于中文一般指分词后的一个词
* 词条 Term 集合
  - 搜索引擎通常索引单位是单词，词典是由文档集合中出现过的所有单词构成的字符串集合
  - 词典内每条索引项:记载单词本身一些信息以及指向“倒排列表”指针
* 有很多种词典结构，各有各的优缺点，最简单如排序数组，通过二分查找来检索数据，更快的有哈希表，磁盘查找有B树、B+树，但一个能支持TB级数据的倒排索引结构需要在时间和空间上有个平衡
* 要求：
  - 查询速度
  - 内存占用
  - 内存+磁盘结合

## 倒排表 Post list

* 记录的是某个词在哪些文档里出现过以及出现的位置
* 每条记录称为一个倒排项 Posting,不单是文档编号，还存储了词频等信息
* **倒排文件 Inverted File**：所有单词倒排表往往顺序地存储在磁盘的某个文件里，存储倒排索引的物理文件
* 段 Segment：索引中最小独立存储单元。一个索引文件由一个或者多个段组成。在Luence中的段有不变性，段一旦生成，在其上只能有读操作，不能有写操作

## 倒排索引：关键词到文档 ID 的映射，每个关键词都对应一个倒排表，倒排表由一系列倒排文件组成，这些文件中都出现了关键词

* 通过分词器将每个文档内容域拆分成单独的词（词条或Term），创建一个包含所有不重复词条的排序列表，然后列出每个词条出现在哪个文档.由属性值来确定记录的位置的结构就是倒排索引
* 词典和倒排文件是分两部分存储的，词典存储在内存中而倒排文件存储在磁盘
* 倒排索引中词项根据字典顺序升序排列

## 分段存储

* 早期的Lucene中当写入数据时会为整个文档集合建立一个很大的倒排索引，并将其写入磁盘中，如果索引有更新，就需要重新全量创建一个索引来替换原来的索引。这种方式在数据量很大时效率很低，并且由于创建一次索引的成本很高，所以对数据的更新不能过于频繁，也就不能保证实效性
* 引入了段(Segment)的概念（将一个索引文件拆分为多个子文件，其中每个子文件称为段[Segment]），每个段都是一个独立的可被搜索的数据集，并且段具有不变性，一旦索引的数据被写入硬盘，就不可修改
* 过程
* 新增：当有新的数据需要创建索引时，由于段的不变性，所以会新建一个段来存储新增的数据
* 删除：当删除数据时，由于数据所在的段只可读，不可写，所以Lucene在索引文件新增一个.del的文件，用来专门存储被删除的数据id。当查询时，被删除的数据还是可以被查到的，只是在进行文档链表合并时，才把已经删除的数据过滤掉。被删除的数据在进行段合并时才会被真正被移除
* 更新：更新的操作其实就是删除和新增操作的组合(delete & insert)，先在.del文件中标记旧数据的删除，再在新段中添加一条更新后的数据
* 段不可变性优点：
  - 不需要锁：因为数据不会更新，所以不用考虑多线程下的读写不一致情况
  - 可以常驻内存：段在被加载到内存后，由于具有不变性，所以只要内存的空间足够大，就可以长时间驻存，大部分查询请求会直接访问内存，而不需要访问磁盘，使得查询的性能有很大的提升
  - 缓存友好：在段的声明周期内始终有效，不需要在每次数据更新时被重建
  - 增量创建：分段可以做到增量创建索引，可以轻量级地对数据进行更新，由于每次创建的成本很低，所以可以频繁地更新数据，使系统接近实时更新
* 段不可变性缺点：
  - 删除：当对数据进行删除时，旧数据不会被马上删除，而是在.del文件中被标记为删除。旧数据只能等到段更新时才能真正地被移除，这样会有大量的空间浪费
  - 更新：更新数据由删除和新增这两个动作组成。若有一条数据频繁更新，则会有大量的空间浪费
  - 新增：由于索引具有不变性，所以每次新增数据时，都需要新增一个段来存储数据。当段的数量太多时，对服务器的资源（如文件句柄）的消耗会非常大，查询的性能也会受到影响
  - 过滤：在查询后需要对已经删除的旧数据进行过滤，这增加了查询的负担
* 为了提升写的性能，Lucene并没有每新增一条数据就增加一个段，而是采用延迟写的策略，每当有新增的数据时，就将其先写入内存中，然后批量写入磁盘中
  - 若有一个段被写到硬盘，就会生成一个提交点，提交点就是一个用来记录所有提交后的段信息的文件
* 一个段一旦拥有了提交点，就说明这个段只有读权限，失去了写权限；相反，当段在内存中时，就只有写数据的权限，而不具备读数据的权限，所以也就不能被查询了
* 段合并策略
  - 在索引中会存储大量的段，非常影响服务器的稳定性以及查询的性能。因此在Lucene中会根据段的大小将段进行分组，然后将同一组的段进行合并，且主要只对中小段进行合并，既可以避免大段合并消耗过多资源也可以很好的控制索引中段的数量
  - mergeFactor：每次合并时参与合并的最少数量，当同一组的段的数量达到该值时开始合并，默认值为10。
  - SegmentSize：段的实际大小，单位为字节。
  - minMergeSize：小于该值的段会被分到一组，这样可以加速小片段的合并。
  - maxMergeSize：若有一段的文本数量大于该值，就不再参与合并，因为大段合并会消耗更多的资源

## 写索引

* 暂驻内存：新数据被写入时，并没有被直接写到硬盘中，而是被暂时写到内存中
  - 默认是一秒钟，或者当内存中数据量达到一定阶段时，再批量提交到磁盘中，默认提交时间和数据量的大小是可以通过参数控制的
  - 通过延时写的策略，可以减少数据往磁盘上写的次数，从而提升整体的写入性能，降低磁盘压力。此时该内存中的数据不能被检索到
* 持久化：在达到触发条件以后，会将内存中缓存的数据一次性写入磁盘中，并生成提交点，此时该段数据可以被检索到
* 释放内存：释放内存并等待新的数据写入
* 当内存中的数据还没有持久化到磁盘中的时候如果集群出现故障，那么内存中的数据就会丢失无法恢复，因此在Elasticsearch中新增了事务日志用以保证数据安全