# 软件工程

## 《加速：构建和扩展高性能技术组织》

* 大项目的开发效率低？
    - 代码复杂度:不真正理解系统，也就不会感到自己是代码的主人。你会很犹豫要不要重构，过时的代码开始累积，技术债务就这样出现了。长此以往，开发变得越来越不愉快和令人无法满意，最终导致人才流失。后面接手的新人，更难于重构那些遗留下来的代码。
    - 团队原因
        + 交流成本开始指数式上升
        + 保持扁平化管理，也会越来越困难
* 代码解耦：软件解耦，拆分成组件或者模块，防止各个部分紧密地耦合在一起。每个组件和模块，都可以独立开发，通过公开的接口被其它部分调用。
* 团队解耦：可以参考互联网的架构
    * 独立的节点
        - 遵守公开的通信协议。
        - 不需要了解其它节点的内部实现，就可以与之通信。
        - 节点之间不直接共享状态，只通过通信交换数据。
        - 每个节点单独开发和部署。
    * 标准
        + 每个子团队都可以独立运作，不依赖外部人员
        + 子团队内部的运作，不需要被外部知道
        + 子团队之间的协调，应该按照公开的协议和规则，最好能够自动完成，避免私下协商
    - 团队解耦注意点
        + 子团队的人数不宜过多，每个子团队最好不要超过5个人
        + 子团队应该是一个小型的全功能软件开发组织
            + 按照软件的业务功能分组，每组负责一个全流程的软件大功能，设计、编码、测试、部署、支持等人员都在同一组。这样才能做到解耦，以及独立的交付和重构。每组内部使用什么工具、如何实现某个功能，都是自己决定，各组之间不需要共享内部细节，也不依赖别组的工作
        - 大团队应该保障子团队的自主权，按照子团队提供的功能和商业价值，进行资源分配
        - 软件架构师的角色很重要
            + 软件架构师的关注点，不应该是团队使用的工具和技术，而是各种服务与整个系统运行状况之间的协议和通信，保证代码和团队可以正确解耦
        + 代码解耦和团队解耦的关系： 理想情况下，代码解耦与团队解耦保持一致，形成一对一的关系，一个子团队负责一个独立的模块。实际运作中，一个子团队负责几个模块也可以，但是一个模块不能由多个子团队来参与。
        - 通信（模块之间的、子团队之间的）尽量规范化，争取做到过程简单、文档充分，最好有规范的 API，这样无需任何人员交流，就能建立通信

## 《规模：生物，城市和公司的普遍法则》