作者：Raynor
链接：https://www.zhihu.com/question/22017267/answer/26468016
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

计算机网络计算机网络分为3块：1. 硬件网卡，网线，交换机这些，用来处理数据的。2. 协议数据在网络中通信如何组织？如何识别？如何保证数据的正确性？这2块我就不多说了。3. 操作系统这就是如何把计算机网络和操作系统结合起来的问题了。对于操作系统来说，网卡也是一种硬件资源。但是网络不单只是一种硬件，而是一种媒体入口。比如操作系统管理硬盘，当然不是简单的记一下硬盘有多大，然后一切操作都交给硬盘芯片去做，更多的需要组织硬盘的扇区，分区，记录文件和扇区/偏移的关系等等。操作系统对于网络来说也是如此，要记录自身在网络的标识（ip），可被他人访问的入口（port），以及对方的信息（remote ip/port）。连接，断开，数据确认等操作也是由协议控制。传递自身消息给对方，类似访问硬盘一样把内存中的数据传递给网卡缓存，再发消息给网卡让网卡去传数据，而是否发送成功这些保证不再由硬件中断信号反馈，而是通过网络协议完成。接收对方消息，也是接收到网卡中断，再把数据从网卡缓存移动到内存中，再通过协议给予对方反馈。简单来说就是这样，如果以后有时间，我再把osi七层协议中的内容和操作系统的交互再详述一遍吧。网络方面的就推荐《tcp/ip详解》，《uinx网络高级编程》吧。