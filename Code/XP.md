# ExtremeProgramming

一套软件开发方法是由一系列与开发相关的规则、规范和惯例。重量级的开发方法严格定义了许多的规则、流程和相关的文档工作。灵巧的轻量级开发方法，其规则和文档相对较少，流程更加灵活，实施起来相对较容易。

它列出的每个方法和思想做到极限、做到最好

* 沟通（Communication）：加强交流
* 简单（Simplicity）从简单做起
* 反馈（Feedback）寻求反馈
* 勇气（Courage）勇于实事求是
* 遵守（Respect）

## 特点

* 增量和反复式的开发----一次小的改进跟着一个小的改进。
* 反复性，通常是自动重复的单元测试，回归测试。参见JUnit。
* 结对程序设计
* 在程序设计团队中的用户交互（在场的客户）
* 软件重构
* 共享的代码所有权
* 简单
* 反馈
* 用隐喻来组织系统
* 可以忍受的速度

## 流程

* 需求分析：不仅仅是用户需求，应该是开发中遇到的所有的需求。比如，你首先要知道做这个项目是为了解决什么问题；测试案例中应该输入什么数据……为了清楚地知道这些需求，你经常要和客户、项目经理等交流。
* 设计：编码前，肯定有个计划告诉你要做什么，结构是怎样等等。你一定要按照这个来做，否则可能会一团糟。
* 编码：如果在项目截止日，你的程序不能跑起来或达不到客户的要求，你就拿不到钱。
* 测试：目的是让你知道，什么时候算是完成了。如果你聪明，你就应该先写测试，这样可以及时知道你是否真地完成了。否则，你经常会不知道，到底有哪些功能是真正完成了，离预期目标还差多远。

## 权利和义务

* 定义每个用户需求的商业优先级；
* 制订总体计划，包括用多少投资、经过多长时间、达到什么目的；
* 在项目开发过程中的每个工作周，都能让投资获得最大的收益；
* 通过重复运行你所指定的功能测试，准确地掌握项目进展情况；
* 能随时改变需求、功能或优先级，同时避免昂贵的再投资；能够根据各种变化及时调整项目计划；
* 能够随时取消项目；项目取消时，以前的开发工作不是一堆垃圾，已开发完的功能是合乎要求的，正在进行或未完成的的工作则应该是不难接手的。
* 知道要做什么，以及要优先做什么；
* 工作有效率；
* 有问题或困难时，能得到客户、同事、上级的回答或帮助；
* 对工作做评估，并根据周围情况的变化及时重新评估；
* 积极承担工作，而不是消极接受分配；

## 核心实践

* 团队协作(Whole Team)：所有参与者（开发人员、客户、测试人员等）一起工作在一个开放的场所中，他们是同一个团队的成员。这个场所的墙壁上随意悬挂着大幅的、显著的图表以及其他一些显示他们进度的东西。必须至少有一个人对用户需求非常清晰，能够提出需求、决定各个需求的商业价值（优先级）、根据需求等的变化调整项目计划等
* 规划策略(The Planning Game)；：计划是持续的、循序渐进的。每2周，开发人员就为下2周估算候选特性的成本，而客户则根据成本和商务价值来选择要实现的特性。
    - 软件发布计划（ReleasePlanning）。客户阐述需求，开发人员估算开发成本和风险。客户根据开发成本、风险和每个需求的重要性，制订一个大致的项目计划。最初的项目计划没有必要（也没有可能）非常准确，因为每个需求的开发成本、风险及其重要性都不是一成不变的。而且，这个计划会在实施过程中被不断地调整以趋精确。
    - 周期开发计划（IterationPlanning）。开发过程中，应该有很多阶段计划（比如每三个星期一个计划）。开发人员可能在某个周期对系统进行内部的重整和优化（代码和设计），而在某个周期增加了新功能，或者会在一个周期内同时做两方面的工作。但是，经过每个开发周期，用户都应该能得到一个已经实现了一些功能的系统。而且，每经过一个周期，客户就会再提出确定下一个周期要完成的需求。在每个开发周期中，开发人员会把需求分解成一个个很小的任务，然后估计每个任务的开发成本和风险。
* 结对编程(Pair programming)：所有的产品软件都是由两个程序员、并排坐在一起在同一台机器上构建的。
* 重构(Refactoring)：随时利用重构方法改进已经腐化的代码，保持代码尽可能的干净、具有表达力。
* 简单设计(Simple Design)：团队保持设计恰好和当前的系统功能相匹配。它通过了所有的测试，不包含任何重复，表达出了编写者想表达的所有东西，并且包含尽可能少的代码。用最简单的办法实现每个小需求，前提是按照这些简单设计开发出来的软件必须通过测试。这些设计只要能满足系统和客户在当下的需求就可以了，不需要任何画蛇添足的设计，而且所有这些设计都将在后续的开发过程中就被不断地重整和优化。
* 代码集体所有权(Collective Code Ownership)：任何结对的程序员都可以在任何时候改进任何代码。没有程序员对任何一个特定的模块或技术单独负责，每个人都可以参与任何其它方面的开发。
* 持续集成(Continuous Integration)：团队总是使系统完整地被集成。一个人拆入（Check in）后，其它所有人责任代码集成。
* 每周40小时工作制（40-hour Week）
* 编码规范（Code Standards）：系统中所有的代码看起来就好像是被单独一人编写的。
* 系统隐喻（System Metaphor）：将整个系统联系在一起的全局视图；它是系统的未来影像，是它使得所有单独模块的位置和外观变得明显直观。如果模块的外观与整个隐喻不符，那么你就知道该模块是错误的。
* 测试驱动开发(Testing-Driven Development)：编写单元测试是一个验证行为，更是一个设计行为。同样，它更是一种编写文档的行为。编写单元测试避免了相当数量的反馈循环，尤其是功能验证方面的反馈循环。程序员以非常短的循环周期工作，他们先增加一个失败的测试，然后使之通过。
* 小型发布（Small Release）
* 客户测试(Customer Tests)：作为选择每个所期望的特性的一部分，客户可以根据脚本语言来定义出自动验收测试来表明该特性可以工作。

## 实践

* 测试驱动开发—TDD是你的商业安全网。因为测试是在编码之前完成的，所以写完的测试一定会运行失败，接下来再写代码使测试可以通过。TDD保证你的产品功能，不管公司和技术团队实现的是大规模的变更还是小规模的变更。
* 结对编程—让2名开发人员写同一段代码，使用同一个键盘和同一台显示器。因为结对大大降低了浪费的时间和缺陷，所以能带来更高质量的代码，并带来高水平的协作。
    - 愿不愿意暴露自己编程的思路和技术水平，思维的透明化
    - 当Driver在写代码时，不能频繁地被打断
    - 一直霸者开发
    - 两个人的水平应该差不太多
* 集体代码所有制和持续集成—如果每段代码不只有一个人熟悉，那么就不会有什么交流瓶颈了。把代码持续集成到一个主干可以避免重复和不匹配的代码。
* 重构—在当时的情况下，写的代码是解决已知问题的。通常，团队巧妙地解决了他们的问题，然后持续重构和修改代码，确保代码库能以最为高效的方式不断满足业务最新的需要。

## 概念

* UserStory：开发人员要求客户把所有的需求写成一个个独立的小故事，每个只需要几天时间就可以完成。开发过程中，客户可以随时提出新的UserStory，或者更改以前的UserStory。
* StoryEstimates和开发速度：开发小组对每个UserStory进行估算，并根据每个开发周期（Iteration）中的实际情况反复计算开发速度。这样，开发人员和客户能知道每个星期到底能开发多少UserStory。
* ReleasePlan和ReleaseScope：整个开发过程中，开发人员将不断地发布新版本。开发人员和客户一起确定每个发布所包含的UserStory。
* Iteration（开发周期，或称迭代）和IterationPlan：在一个Release过程中，开发人员要求客户选择最有价值的UserStory作为未来一两个星期的开发内容。
* TheSeed：第一个迭代（Iteration）完成后，提交给客户的系统。虽然这不是最终的产品，但它已经实现了几个客户认为是最重要的Story，开发人员将逐步在其基础上增加新的模块。
* ContinuousIntegration（整合）：把开发完的UserStory的模块一个个拼装起来，一步步接近乃至最终完成最终产品。
* 验收测试（功能测试）：对于每个UserStory，客户将定义一些测试案例，开发人员将使运行这些测试案例的过程自动化。
* UnitTest（单元测试）：在开始写程序前，程序员针对大部分类的方法，先写出相应的测试程序。
* Refactoring(重构)：去掉代码中的冗余部分，增加代码的可重用性和伸缩性。