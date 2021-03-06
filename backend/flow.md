# [Flow](https://github.com/area9innovation/flow9/)

Platform for safe, easy and productive programming of complex, multi-platform apps with a modern user interface

* 一个稳定、成熟的平台，不仅提供了编程语言、增量编译器、多后端，而且还提供了一个功能强大的标准库，包括一个一流的 UI 库。
* 语法非常简单，易于学习、读写，并且基于函数语言家族中的清晰语义，使用了大多数程序员都熟悉的 C 风格语法。
* 一种实用的语言，具有可以利用类型推断的静态类型，但在需要时也支持动态类型。它提供了开箱即用的安全性和防故障能力。它鼓励函数式代码，但在需要时也支持可能带来副作用的引用
* 轻量级的、强大的基于表达式的语法。Flow 的语法有 255 行，包括注释，总共 25 个关键词。
* 类型系统很简单，但是仍然支持类型推断、子类型和动态类型。抽象数据类型允许通过编译器的强类型检查对数据进行自然建模。
* 一致的标准库。因为 Flow 是一种函数式语言，所以标准库就是围绕这个范式设计的。特别是，我们大量使用函数式反应式编程来处理交互性。这意味着各个部分可以很好地组合在一起，即使对于 UI 代码，也具有很高的组合性。
* 代码通常很容易理解，部分原因是没有混合多种范式及其交互。没有重载、没有隐式转换、空指针或方法重载。当你阅读代码时，可以确切地看到它做了什么，因为语法和语义是一致的，并且不随上下文而改变。
* 将 HTML 视为一级目标。上述语言不能自然地在浏览器中运行。其中一些提供了实验性的 WebAssembly 目标，但是这些目标需要比较大的运行时，因此需要大量的下载。令人惊讶的是，它们的运行速度比 JS 慢很多倍，而且 UI 工具包没有移植到浏览器中。因此，使用这些语言不容易编写包含浏览器在内的多平台代码。
