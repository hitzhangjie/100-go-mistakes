# 100个Go常见错误及如何避免

📖 _100个Go常见错误及如何避免 的源代码和社区空间，于2022年8月份由Manning创建发布。

## ❤️ 赞助该仓库

如果您的公司正在招聘？请您考虑 [赞助](https://github.com/sponsors/teivah?frequency=one-time&sponsor=teivah) 该仓库，并在这里介绍让更多Go开发者了解贵公司的工作机会。

## 📖 本书介绍

如果您是一名Go开发者，想要提高自己的技能，那么这本书非常适合你。《100个Go常见错误及如何避免》从实用示例出发，涵盖了从并发、错误处理到测试和代码组织等广泛的主题。通过阅读本书，你将学会编写出更符合Go惯例、更具效率和可维护性的代码，成为一名熟练的Go开发者。

![](inside-cover.png)

### 推荐语

> 这本书应该是所有Golang开发者在开始编写生产代码之前必读的书籍......本书之于Golang，犹如Joshua Bloch所著的传奇书籍《Effective Java》之于Java。

– _Neeraj Shah_

> 如果Go开发者不读这本书，那将会是他犯的第101个错误。

– _Anupam Sengupta_

### ✍️ 关于作者

Teiva Harsanyi是Google的高级软件工程师。他在多个领域工作过，包括保险、交通运输以及像航空调度管理这样的安全性至关重要的行业。他对Go语言以及如何设计和实现可靠的系统充满了热情。

### 从哪里购买?

* _100个Go常见错误及如何避免(🇬🇧 英文版: 纸质书, 电子书, 或 有声书):
  * [Manning](https://www.manning.com/books/100-go-mistakes-and-how-to-avoid-them)
  * [O’Reilly](https://www.oreilly.com/library/view/100-go-mistakes/9781617299599/)
  * Amazon: [.com](https://www.amazon.com/dp/1617299596), [.co.uk](https://www.amazon.co.uk/dp/B0BBSNJR6B), [.de](https://www.amazon.de/dp/B0BBHQD8BQ), [.fr](https://www.amazon.fr/100-Mistakes-How-Avoid-Them/dp/1617299596), [.in](https://www.amazon.in/dp/B0BBHQD8BQ), [.co.jp](https://www.amazon.co.jp/dp/B0BBHQD8BQ), [.es](https://www.amazon.es/dp/B0BBHQD8BQ), [.it](https://www.amazon.it/dp/B0BBHQD8BQ), [.com.br](https://www.amazon.com.br/dp/B0BBHQD8BQ)

* _Go言語100Tips 開発者にありがちな間違いへの対処法_ (🇯🇵 日本版):
  * Amazon: [.co.jp](https://www.amazon.co.jp/exec/obidos/ASIN/4295017531/)

## 💡 常见的Go错误

本节简要总结了本书讲述的100个Go常见错误，同时本节也对社区开放，如果您相信有一个Go常见错误应该被添加进来，请您发起 [常见错误issue](https://github.com/teivah/100-go-mistakes/issues/new?assignees=&labels=community+mistake&template=community_mistake.md&title=)。

- [100个Go常见错误及如何避免](#100个go常见错误及如何避免)
  - [❤️ 赞助该仓库](#️-赞助该仓库)
  - [📖 本书介绍](#-本书介绍)
    - [推荐语](#推荐语)
    - [✍️ 关于作者](#️-关于作者)
    - [从哪里购买?](#从哪里购买)
  - [💡 常见的Go错误](#-常见的go错误)
    - [代码及工程组织](#代码及工程组织)
      - [意外的变量隐藏 (#1)](#意外的变量隐藏-1)
      - [不必要的代码嵌套 (#2)](#不必要的代码嵌套-2)
      - [误用init函数 (#3)](#误用init函数-3)
      - [滥用getters/setters (#4)](#滥用getterssetters-4)
      - [接口污染 (#5)](#接口污染-5)
      - [将接口定义在实现方一侧 (#6)](#将接口定义在实现方一侧-6)
      - [将接口作为返回值 (#7)](#将接口作为返回值-7)
      - [`any` 没传递任何信息 (#8)](#any-没传递任何信息-8)
      - [困惑何时该用范型 (#9)](#困惑何时该用范型-9)
      - [未意识到类型嵌套的可能问题 (#10)](#未意识到类型嵌套的可能问题-10)
      - [不使用function option模式 (#11)](#不使用function-option模式-11)
      - [工程组织不合理 (工程结构和包的组织) (#12)](#工程组织不合理-工程结构和包的组织-12)
      - [创建工具包 (#13)](#创建工具包-13)
      - [忽略了包名冲突 (#14)](#忽略了包名冲突-14)
      - [代码缺少文档 (#15)](#代码缺少文档-15)
      - [不使用linters检查 (#16)](#不使用linters检查-16)
    - [数据类型](#数据类型)
      - [八进制字面量引发的困惑 (#17)](#八进制字面量引发的困惑-17)
      - [未注意可能的整数溢出 (#18)](#未注意可能的整数溢出-18)
      - [没有透彻理解浮点数 (#19)](#没有透彻理解浮点数-19)
      - [不理解slice的长度和容量 (#20)](#不理解slice的长度和容量-20)
      - [不高效的slice初始化 (#21)](#不高效的slice初始化-21)
      - [困惑于nil和空slice (#22)](#困惑于nil和空slice-22)
      - [没有适当检查slice是否为空 (#23)](#没有适当检查slice是否为空-23)
      - [没有正确拷贝slice (#24)](#没有正确拷贝slice-24)
      - [slice append带来的预期之外的副作用 (#25)](#slice-append带来的预期之外的副作用-25)
      - [slice和内存泄漏 (#26)](#slice和内存泄漏-26)
      - [不高效的map初始化 (#27)](#不高效的map初始化-27)
      - [map和内存泄漏 (#28)](#map和内存泄漏-28)
      - [不正确的值比较 (#29)](#不正确的值比较-29)
    - [控制结构](#控制结构)
      - [忽略了 `range` 循环变量是一个拷贝 (#30)](#忽略了-range-循环变量是一个拷贝-30)
      - [忽略了 `range` 循环中迭代目标值的计算方式 (channels 和 arrays) (#31)](#忽略了-range-循环中迭代目标值的计算方式-channels-和-arrays-31)
      - [忽略了 `range` 循环中指针元素的影响 `range` loops (#32)](#忽略了-range-循环中指针元素的影响-range-loops-32)
      - [map迭代过程中的错误假设（遍历顺序 和 迭代过程中插入）(#33)](#map迭代过程中的错误假设遍历顺序-和-迭代过程中插入33)
      - [忽略了 `break` 语句是如何工作的 (#34)](#忽略了-break-语句是如何工作的-34)
      - [在循环中使用 `defer`  (#35)](#在循环中使用-defer--35)
    - [字符串](#字符串)
      - [没有理解rune (#36)](#没有理解rune-36)
      - [不正确的字符串遍历 (#37)](#不正确的字符串遍历-37)
      - [误用trim函数 (#38)](#误用trim函数-38)
      - [不经优化的字符串拼接操作 (#39)](#不经优化的字符串拼接操作-39)
      - [无用的字符串转换 (#40)](#无用的字符串转换-40)
      - [子字符串和内存泄漏 (#41)](#子字符串和内存泄漏-41)
    - [函数和方法](#函数和方法)
      - [不知道使用哪种接收器类型 (#42)](#不知道使用哪种接收器类型-42)
      - [从不使用命名的返回值 (#43)](#从不使用命名的返回值-43)
      - [使用命名的返回值时预期外的副作用 (#44)](#使用命名的返回值时预期外的副作用-44)
      - [返回一个nil接收器 (#45)](#返回一个nil接收器-45)
      - [使用文件名作为函数入参 (#46)](#使用文件名作为函数入参-46)
      - [忽略 `defer` 语句中参数、接收器值的计算方式 (参数值计算, 指针, 和 value类型接收器) (#47)](#忽略-defer-语句中参数接收器值的计算方式-参数值计算-指针-和-value类型接收器-47)
    - [错误管理](#错误管理)
      - [Panicking (#48)](#panicking-48)
      - [未考虑何时才应该包装error (#49)](#未考虑何时才应该包装error-49)
      - [不正确的错误类型比较 (#50)](#不正确的错误类型比较-50)
      - [不正确的错误对象值比较 (#51)](#不正确的错误对象值比较-51)
      - [处理同一个错误两次 (#52)](#处理同一个错误两次-52)
      - [不处理错误 (#53)](#不处理错误-53)
      - [不处理 `defer` 中的错误 (#54)](#不处理-defer-中的错误-54)
    - [并发编程: 基础](#并发编程-基础)
      - [混淆并发和并行 (#55)](#混淆并发和并行-55)
      - [认为并发总是更快 (#56)](#认为并发总是更快-56)
      - [不清楚何时使用channels或mutexes (#57)](#不清楚何时使用channels或mutexes-57)
      - [不明白竞态问题 (数据竞态 vs. 竞态条件 和 Go内存模型) (#58)](#不明白竞态问题-数据竞态-vs-竞态条件-和-go内存模型-58)
      - [不理解不同工作负载类型对并发的影响 (#59)](#不理解不同工作负载类型对并发的影响-59)
      - [误解了Go contexts (#60)](#误解了go-contexts-60)
    - [并发编程: 实践](#并发编程-实践)
      - [传递不合适的context (#61)](#传递不合适的context-61)
      - [启动了一个goroutine但是不知道它何时会停止 (#62)](#启动了一个goroutine但是不知道它何时会停止-62)
      - [不注意处理 goroutines 和 循环中的迭代变量 (#63)](#不注意处理-goroutines-和-循环中的迭代变量-63)
      - [使用select + channels 时误以为分支选择顺序是确定的 (#64)](#使用select--channels-时误以为分支选择顺序是确定的-64)
      - [不正确使用通知 channels (#65)](#不正确使用通知-channels-65)
      - [不使用 nil channels (#66)](#不使用-nil-channels-66)
      - [不清楚该如何确定 channel size (#67)](#不清楚该如何确定-channel-size-67)
      - [忘记了字符串格式化可能带来的副作用（例如 etcd 数据竞争和死锁）(#68)](#忘记了字符串格式化可能带来的副作用例如-etcd-数据竞争和死锁68)
      - [使用 append 不当导致数据竞争 (#69)](#使用-append-不当导致数据竞争-69)
      - [误用 mutexes 和 slices、maps (#70)](#误用-mutexes-和-slicesmaps-70)
      - [误用 `sync.WaitGroup` (#71)](#误用-syncwaitgroup-71)
      - [忘记使用 `sync.Cond` (#72)](#忘记使用-synccond-72)
      - [不使用 `errgroup` (#73)](#不使用-errgroup-73)
      - [拷贝一个 `sync` 下的类型 (#74)](#拷贝一个-sync-下的类型-74)
    - [标准库](#标准库)
      - [使用了错误的 time.Duration (#75)](#使用了错误的-timeduration-75)
      - [`time.After` 和内存泄漏 (#76)](#timeafter-和内存泄漏-76)
      - [JSON处理中的常见错误 (#77)](#json处理中的常见错误-77)
      - [常见的 SQL 错误 (#78)](#常见的-sql-错误-78)
      - [不关闭临时资源（HTTP 请求体、`sql.Rows` 和 `os.File`) (#79)](#不关闭临时资源http-请求体sqlrows-和-osfile-79)
      - [响应HTTP请求后没有返回语句 (#80)](#响应http请求后没有返回语句-80)
      - [直接使用默认的HTTP client和server (#81)](#直接使用默认的http-client和server-81)
    - [测试](#测试)
      - [不对测试进行分类 （build tags, 环境变量，短模式）(#82)](#不对测试进行分类-build-tags-环境变量短模式82)
      - [不打开 race 开关 (#83)](#不打开-race-开关-83)
      - [不打开测试的执行模式开关 (parallel 和 shuffle) (#84)](#不打开测试的执行模式开关-parallel-和-shuffle-84)
      - [不使用表驱动的测试 (#85)](#不使用表驱动的测试-85)
      - [在单元测试中执行sleep操作 (#86)](#在单元测试中执行sleep操作-86)
      - [没有高效地处理 time API (#87)](#没有高效地处理-time-api-87)
      - [不使用测试相关的工具包 (`httptest` 和 `iotest`) (#88)](#不使用测试相关的工具包-httptest-和-iotest-88)
      - [不正确的基准测试 (#89)](#不正确的基准测试-89)
      - [没有去探索go test所有的特性 (#90)](#没有去探索go-test所有的特性-90)
      - [不使用模糊测试 (社区反馈错误)](#不使用模糊测试-社区反馈错误)
    - [优化技术](#优化技术)
      - [不理解CPU cache (#91)](#不理解cpu-cache-91)
      - [写的并发处理逻辑会导致false sharing (#92)](#写的并发处理逻辑会导致false-sharing-92)
      - [没有考虑指令级的并行 (#93)](#没有考虑指令级的并行-93)
      - [不了解数据对齐 (#94)](#不了解数据对齐-94)
      - [不了解 stack vs. heap (#95)](#不了解-stack-vs-heap-95)
      - [不知道如何减少内存分配次数 (API调整, compiler optimizations, and `sync.Pool`) (#96)](#不知道如何减少内存分配次数-api调整-compiler-optimizations-and-syncpool-96)
      - [不注意使用内联 (#97)](#不注意使用内联-97)
      - [不使用Go问题诊断工具 (#98)](#不使用go问题诊断工具-98)
      - [不理解GC是如何工作的 (#99)](#不理解gc是如何工作的-99)
      - [不了解Docker或者K8S对运行的Go应用的性能影响 (#100)](#不了解docker或者k8s对运行的go应用的性能影响-100)
  - [🌎 外部资源](#-外部资源)
    - [英文资料](#英文资料)
    - [中文资料](#中文资料)
    - [日本资料](#日本资料)
    - [葡萄牙资料](#葡萄牙资料)

### 代码及工程组织

#### 意外的变量隐藏 (#1)

Avoiding shadowed variables can help prevent mistakes like referencing the wrong variable or confusing readers.

避免变量隐藏（外部作用域变量被内部作用域同名变量隐藏），有助于避免变量引用错误，有助于他人阅读理解。

#### 不必要的代码嵌套 (#2)

避免不必要的、过多的嵌套层次，并且让正常代码路径尽量左对齐（而不是放在分支路径中），有助于构建可读性更好的代码。

#### 误用init函数 (#3)

初始化变量时，请记住 init 函数具有有限的错误处理能力，并且会使状态处理和测试变得更加复杂。在大多数情况下，初始化应该作为特定函数来处理。

#### 滥用getters/setters (#4)

在Go语言中，强制使用getter和setter方法并不符合Go惯例。在实践中，应该找到效率和盲目遵循某些惯用法之间的平衡点。

#### 接口污染 (#5)

抽象应该被发现，而不是被创造。为了避免不必要的复杂性，需要时才创建接口，而不是预见到需要它，或者至少可以证明这种抽象是有价值的。

#### 将接口定义在实现方一侧 (#6)

将接口保留在引用方一侧（而不是实现方一侧）可以避免不必要的抽象。

#### 将接口作为返回值 (#7)

为了避免在灵活性方面受到限制，大多数情况下函数不应该返回接口，而应该返回具体的实现。相反，函数应该尽可能地使用接口作为参数。

#### `any` 没传递任何信息 (#8)

只有在需要接受或返回任意类型时，才使用 `any`，例如 `json.Marshal`。其他情况下，因为 `any` 不提供有意义的信息，可能会导致编译时问题，如允许调用者调用方法处理任意类型数据。

#### [困惑何时该用范型](https://teivah.medium.com/when-to-use-generics-in-go-36d49c1aeda) (#9)

使用泛型，可以通过类型参数分离具体的数据类型和行为，避免写很多重复度很高的代码。然而，不要过早地使用泛型、类型参数，只有在你看到真正需要时才使用。否则，它们会引入不必要的抽象和复杂性。

#### 未意识到类型嵌套的可能问题 (#10)

使用类型嵌套也可以避免写一些重复代码，然而，在使用时需要确保不会导致不合理的可见性问题，比如有些字段应该对外隐藏不应该被暴漏。

#### 不使用function option模式 (#11)

为了设计并提供更友好的API（可选参数），为了更好地处理选项，应该使用function option模式。

#### 工程组织不合理 (工程结构和包的组织) (#12)

遵循像 project-layout 的建议来组织Go工程是一个不错的方法，特别是你正在寻找一些类似的经验、惯例来组织一个新的Go工程的时候。

#### 创建工具包 (#13)

命名是软件设计开发中非常重要的一个部分，创建一些名如 `common`、`util`、`shared` 之类的包名并不会给读者带来太大价值，应该将这些包名重构为更清晰、更聚焦的包名。

#### 忽略了包名冲突 (#14)

To avoid naming collisions between variables and packages, leading to confusion or perhaps even bugs, use unique names for each one. If this isn’t feasible, use an import alias to change the qualifier to differentiate the package name from the variable name, or think of a better name.

为了避免变量名和包名之间的冲突，导致混淆或甚至错误，应为每个变量和包使用唯一的名称。如果这不可行，可以考虑使用导入别名 `import importAlias 'importPath'`，以区分包名和变量名，或者考虑一个更好的变量名。

#### 代码缺少文档 (#15)

为了让使用方、维护人员能更清晰地了解你的代码的意图，导出的元素（函数、类型、字段）需要添加godoc注释。

#### 不使用linters检查 (#16)

为了改善代码质量、整体代码的一致性，应该使用linters、formatters。

### 数据类型

#### 八进制字面量引发的困惑 (#17)

在阅读现有代码时，请记住以 0 开头的整数字面量是八进制数。此外，为了提高可读性，可以通过在前面加上 0o 来显式地表示八进制整数。

#### 未注意可能的整数溢出 (#18)

在 Go 中整数上溢出和下溢是静默处理的，所以你可以实现自己的函数来捕获它们。

#### 没有透彻理解浮点数 (#19)

比较浮点数时，通过比较二者的delta值是否介于一定的范围内，能让你写出可移植性更好的代码。

在进行加法或减法时，将具有相似数量级的操作分成同一组以提高精度 (过早指数对齐丢失精度)。此外，在进行加法和减法之前，应先进行乘法和除法 (加减法误差会被乘除放大)。

#### [不理解slice的长度和容量](https://teivah.medium.com/slice-length-vs-capacity-in-go-af71a754b7d8) (#20)

理解slice的长度和容量的区别，是一个Go开发者的核心知识点之一。slice的长度指的是slice已经存储的元素的数量，而容量指的是slice当前底层开辟的数组最多能容纳的元素的数量。

#### 不高效的slice初始化 (#21)

当创建一个slice时，如果其长度可以预先确定，那么可以在定义时指定它的长度和容量。这可以改善后期append时一次或者多次的内存分配操作，从而改善性能。对于map的初始化也是这样的。

#### 困惑于nil和空slice (#22)

为了避免常见的对nil和empty slice处理行为的混淆，例如在使用 encoding/json 或 reflect 包时，你需要理解 nil 和 empty slice的区别。两者都是长度为零、容量为零的切片，但是 nil 切片不需要分配内存。

#### 没有适当检查slice是否为空 (#23)

检查一个slice的是否包含任何元素，可以检查其长度，不管slice是nil还是empty，检查长度都是有效的。这个检查方法也适用于map。

为了设计更明确的API，API不应区分nil和空切片。

#### 没有正确拷贝slice (#24)

使用 `copy` 拷贝一个slice元素到另一个slice时，需要记得，实际拷贝的元素数量是二者slice长度中的较小值。

#### slice append带来的预期之外的副作用 (#25)

如果两个不同的函数操作的slice复用了相同的底层数组，它们对slice执行append操作时可能会产生冲突。使用copy来完整复制一个slice或者使用完整的slice表达式[low:high:max]限制最大容量，有助于避免产生冲突。当想对一个大slice进行shrink操作时，两种方式中，只有copy才可以避免内存泄漏。

#### slice和内存泄漏 (#26)

对于slice元素为指针，或者slice元素为struct但是该struct含有指针字段，当通过slice[low:high]操作取subslice时，对于那些不可访问的元素可以显示设置为nil来避免内存泄露。

#### 不高效的map初始化 (#27)

见 [#21](#inefficient-slice-initialization-21).

#### [map和内存泄漏](https://teivah.medium.com/maps-and-memory-leaks-in-go-a85ebe6e7e69) (#28)

一个map的buckets占用的内存只会增长，不会缩减。因此，如果它导致了一些内存占用的问题，你需要尝试不同的选项来解决，比如重新创建一个map代替原来的（原来的map会被GC掉），或者map[keyType]valueType中的valueType使用指针代替长度固定的数组或者sliceHeader来缓解过多的内存占用。

#### 不正确的值比较 (#29)

Go中比较两个类型值时，如果是可比较类型，那么可以使用 `==` 或者 `!=` 运算符进行比较，比如：booleans、numerals、strings、pointers、channels，以及字段全部是可比较类型的structs。其他情况下，你可以使用 `reflect.DeepEqual` 来比较，用反射的话会牺牲一点性能，也可以使用自定义的实现和其他库来完成。

### 控制结构

#### 忽略了 `range` 循环变量是一个拷贝 (#30) 

`range` 循环中的循环变量是遍历容器中元素值的一个拷贝。因此，如果元素值是一个struct并且想在 `range` 中修改它，可以通过索引值来访问并修改它，或者使用经典的for循环+索引值的写法（除非遍历的元素是一个指针）。

#### 忽略了 `range` 循环中迭代目标值的计算方式 (channels 和 arrays) (#31)

传递给 `range` 操作的迭代目标对应的表达式的值，只会在循环执行前被计算一次，理解这个有助于避免犯一些常见的错误，例如不高效的channel赋值操作、slice迭代操作。

#### 忽略了 `range` 循环中指针元素的影响 `range` loops (#32)

这里其实强调的是 `range` 迭代过程中，迭代变量实际上是一个拷贝，假设给另外一个容器元素（指针类型）赋值，且需要对迭代变量取地址转换成指针再赋值的话，这里潜藏着一个错误，就是for循环迭代变量是 per-variable-per-loop 而不是 per-variable-per-iteration。如果是通过局部变量（用迭代变量来初始化）或者使用索引值来直接引用迭代的元素，将有助于避免拷贝指针(迭代变量的地址)之类的bug。

#### map迭代过程中的错误假设（遍历顺序 和 迭代过程中插入）(#33)

使用map时，为了能得到确定一致的结果，应该记住Go中的map数据结构：
* 不会按照key对data进行排序，遍历时不是按key有序的；
* 遍历时的顺序，也不是按照插入时的顺序；
* 没有一个确定性的遍历顺序，每次遍历顺序是不同的；
* 不能保证迭代过程中新插入的元素，在当前迭代中能够被遍历到；

#### 忽略了 `break` 语句是如何工作的 (#34)

配合label使用 `break` 和 `continue`，能够跳过一个特定的语句，在某些循环中存在 `switch`和`select`语句的场景中就比较有帮助。

#### 在循环中使用 `defer`  (#35)

在循环中使用defer不能在每轮迭代结束时执行defer语句，但是将循环逻辑提取到函数内部会在每次迭代结束时执行 defer 语句。

### 字符串

#### 没有理解rune (#36)

理解rune类型对应的是一个unicode码点，每一个unicode码点其实是一个多字节的序列，不是一个byte。这应该是Go开发者的核心知识点之一，理解了这个有助于更准确地处理字符串。

#### 不正确的字符串遍历 (#37)

使用 `range` 操作符对一个string进行遍历实际上是对string对应的 `[]rune` 进行遍历，迭代变量中的索引值，表示的当前rune对应的 `[]byte` 在整个 `[]byte(string)` 中的起始索引。如果要访问string中的某一个rune（比如第三个），首先要将字符串转换为 `[]rune` 然后再按索引值访问。

#### 误用trim函数 (#38)

`strings.TrimRight`/`strings.TrimLeft` 移除在字符串尾部或者开头出现的一些runes，函数会指定一个rune集合，出现在集合中的rune将被从字符串移除。而 `strings.TrimSuffix`/`strings.TrimPrefix` 是移除字符串的一个后缀/前缀。

#### 不经优化的字符串拼接操作 (#39)

对一个字符串列表进行遍历拼接操作，应该通过 `strings.Builder` 来完成，以避免每次迭代拼接时都分配一个新的string对象出来。

#### 无用的字符串转换 (#40)

`bytes` 包提供了一些和 `strings` 包相似的操作，可以帮助避免 []byte/string 之间的转换。

#### 子字符串和内存泄漏 (#41)

使用一个子字符串的拷贝，有助于避免内存泄漏，因为对一个字符串的s[low:high]操作返回的子字符串，其使用了和原字符串s相同的底层数组。

### 函数和方法

#### 不知道使用哪种接收器类型 (#42)

对于接收器类型是采用value类型还是pointer类型，应该取决于下面这几种因素，比如：方法内是否会对它进行修改，它是否包含了一个不能被拷贝的字段，以及它表示的对象有多大。如果有疑问，接收器可以考虑使用pointer类型。

#### 从不使用命名的返回值 (#43)

使用命名的返回值，是一种有效改善函数、方法可读性的方法，特别是返回值列表中有多个类型相同的参数。另外，因为返回值列表中的参数是经过零值初始化过的，某些场景下也会简化函数、方法的实现。但是需要注意它的一些潜在副作用。

#### 使用命名的返回值时预期外的副作用 (#44)

见 [#43](#从不使用命名的返回值-43).

使用命名的返回值，因为它已经被初始化了零值，需要注意在某些情况下异常返回时是否需要给它赋予一个不同的值，比如返回值列表定义了一个有名参数 `err error`，需要注意 `return err` 时是否正确地对 `err` 进行了赋值。

#### 返回一个nil接收器 (#45)

当返回一个interface参数时，需要小心，不要返回一个nil指针，而是应该显示返回一个nil值。否则，可能会发生一些预期外的问题，因为调用方会收到一个非nil的值。

#### 使用文件名作为函数入参 (#46)

设计函数时使用 `io.Reader` 类型作为入参，而不是文件名，将有助于改善函数的可复用性、易测试性。

#### 忽略 `defer` 语句中参数、接收器值的计算方式 (参数值计算, 指针, 和 value类型接收器) (#47)

为了避免 `defer` 语句执行时就立即计算对defer要执行的函数的参数进行计算，可以考虑将要执行的函数放到闭包里面，然后通过指针传递参数给闭包内函数（或者通过闭包捕获外部变量），来解决这个问题。

### 错误管理

#### Panicking (#48)

使用 `panic` 是Go中一种处理错误的方式，但是只能在遇到不可恢复的错误时使用，例如：通知开发人员一个强依赖的模块加载失败了。

#### 未考虑何时才应该包装error (#49)

Wrapping（包装）错误允许您标记错误、提供额外的上下文信息。然而，包装错误会创建潜在的耦合，因为它使得原来的错误对调用者可见。如果您想要防止这种情况，请不要使用包装错误的方式。

#### 不正确的错误类型比较 (#50)

如果你使用 Go 1.13 引入的特性 `fmt.Errorf` + `%w` 来包装一个错误，当进行错误比较时，如果想判断该包装后的错误是不是指定的错误类型，就需要使用 `errors.As`，如果想判断是不是指定的error对象就需要用 `errors.Is`。

#### 不正确的错误对象值比较 (#51)

见 [#50](#不正确的错误类型比较-50).

为了表达一个预期内的错误，请使用错误值的方式，并通过 `==` 或者 `errors.Is` 来比较。而对于意外错误，则应使用特定的错误类型（可以通过 `errors.As` 来比较）。

#### 处理同一个错误两次 (#52)

大多数情况下，错误仅需要处理一次。打印错误日志也是一种错误处理。因此，当函数内发生错误时，应该在打印日志和返回错误中选择其中一种。包装错误也可以提供问题发生的额外上下文信息，也包括了原来的错误（可考虑交给调用方负责打日志）。

#### 不处理错误 (#53)

不管是在函数调用时，还是在一个 `defer` 函数执行时，如果想要忽略一个错误，应该显示地通过 `_` 来忽略（可注明忽略的原因）。否则，将来的读者就会感觉到困惑，忽略这个错误是有意为之还是无意中漏掉了。

#### 不处理 `defer` 中的错误 (#54)

大多数情况下，你不应该忽略 `defer` 函数执行时返回的错误，或者显示处理它，或者将它传递给调用方处理，可以根据情景进行选择。如果你确定要忽略这个错误，请显示使用 `_` 来忽略。

### 并发编程: 基础

#### 混淆并发和并行 (#55)

理解并发（concurrency）、并行（parallelism）之间的本质区别是Go开发人员必须要掌握的。并发是关于结构设计上的，并行是关于具体执行上的。

#### [认为并发总是更快](https://teivah.medium.com/concurrency-isnt-always-faster-in-go-de325168907c) (#56)

要成为一名熟练的开发人员，您必须意识到并非所有场景下都是并发的方案更快。对于任务中的最小工作负载部分，对它们进行并行化处理并不一定就有明显收益或者比串行化方案更快。对串行化、并发方案进行benchmark测试，是验证假设的好办法。

#### 不清楚何时使用channels或mutexes (#57)

了解 goroutine 之间的交互也可以在选择使用channels或mutexes时有所帮助。一般来说，并行的 goroutine 需要同步，因此需要使用mutexes。相反，并发的 goroutine 通常需要协调和编排，因此需要使用channels。

#### 不明白竞态问题 (数据竞态 vs. 竞态条件 和 Go内存模型) (#58)

掌握并发意味着要认识到数据竞争（data races）和竞态条件（race conditions）是两个不同的概念。数据竞争，指的是有多个goroutines同时访问相同内存区域时，没有必要的同步控制，且其中至少有一个goroutine是执行的写操作。同时要认识到，没有发生数据竞争不代表程序的执行是确定性的、没问题的。当在某个特定的操作顺序或者特定的事件发生顺序下，如果最终的行为是不可控的，这就是竞态条件。

> ps：数据竞争是竞态条件的子集，竞态条件不仅局限于访存未同步，它可以发生在更高的层面。`go test -race` 检测的是数据竞争，需要同步来解决，而开发者还需要关注面更广的竞态条件，它需要对多个goroutines的执行进行编排。

理解 Go 的内存模型以及有关顺序和同步的底层保证是防止可能的数据竞争和竞态条件的关键。

#### 不理解不同工作负载类型对并发的影响 (#59)

当创建一定数量的goroutines是，需要考虑工作负载的类型。如果工作负载是CPU密集型的，那么goroutines数量应该接近于 `GOMAXPROCS` 的值（该值取决于主机处理器核心数）。如果工作负载是IO密集型的，goroutines数量就需要考虑多种因素，比如外部系统（考虑请求、响应速率）。

#### 误解了Go contexts (#60)

Go 的上下文（context）也是 Go 并发编程的基石之一。上下文允许您携带截止时间、取消信号和键值列表。

### 并发编程: 实践

#### 传递不合适的context (#61)

当我们传递了一个context，我们需要知道这个context什么时候可以被取消，这点很重要，例如：一个HTTP请求处理器在发送完响应后取消context。

> ps: 实际上context表达的是一个动作可以持续多久之后被停止。

#### 启动了一个goroutine但是不知道它何时会停止 (#62)

避免goroutine泄漏，要有这种意识，当创建并启动一个goroutine的时候，应该有对应的设计让它能正常退出。

#### 不注意处理 goroutines 和 循环中的迭代变量 (#63)

为了避免goroutines和循环中的迭代变量问题，可以考虑创建局部变量并将迭代变量赋值给局部变量，或者goroutine调用带参数的函数，将迭代变量值作为参数值传入，来代替goroutine调用闭包。

#### 使用select + channels 时误以为分支选择顺序是确定的 (#64)

要明白，`select` 多个channels时，如果多个channels上的操作都就绪，那么会随机选择一个 `case` 分支来执行，因此要避免有分支选择顺序是从上到下的这种错误预设，这可能会导致设计上的bug。

#### 不正确使用通知 channels (#65)

发送通知时使用 `chan struct{}` 类型。

> ps: 先明白什么是通知channels，一个通知channels指的是只是用来做通知，而其中传递的数据没有意义，或者理解成不传递数据的channels，这种称为通知channels。其中传递的数据的类型struct{}更合适。

#### 不使用 nil channels (#66)

使用 nil channels 应该是并发处理方式中的一部分，例如，它能够帮助禁用 `select` 语句中的特定的分支。

#### 不清楚该如何确定 channel size (#67)

根据指定的场景仔细评估应该使用哪一种 channel 类型（带缓冲的，不带缓冲的）。只有不带缓冲的 channels 可以提供强同步保证。

使用带缓冲的 channels 时如果不确定 size 该如何设置，可以先设为1，如果有合理的理由再去指定 channels size。

> ps: 根据disruptor这个高性能内存消息队列的实践，在某种读写pacing下，队列要么满要么空，不大可能处于某种介于中间的稳态。

#### 忘记了字符串格式化可能带来的副作用（例如 etcd 数据竞争和死锁）(#68)

意识到字符串格式化可能会导致调用现有函数，这意味着需要注意可能的死锁和其他数据竞争问题。

> ps: 核心是要关注 `fmt.Sprintf` + `%v` 进行字符串格式化时 `%v` 具体到不同的类型值时，实际上执行的操作是什么。比如 `%v` 这个placeholder对应的值时一个 `context.Context`，那么会就遍历其通过 `context.WithValue` 附加在其中的 values，这个过程可能涉及到数据竞争问题。书中提及的另一个导致死锁的案例本质上也是一样的问题，只不过又额外牵扯到了 `sync.RWMutex` 不可重入的问题。

#### 使用 append 不当导致数据竞争 (#69)

调用 `append` 不总是没有数据竞争的，因此不要在一个共享的 `slice` 上并发地执行 `append`。

#### 误用 mutexes 和 slices、maps (#70)

请记住 slices 和 maps 引用类型，有助于避免常见的数据竞争问题。

> ps: 这里实际是因为错误理解了 slices 和 maps，导致写出了错误的拷贝 slices 和 maps 的代码，进而导致锁保护无效、出现数据竞争问题。

#### 误用 `sync.WaitGroup` (#71)

正确地使用 `sync.WaitGroup` 需要在启动 goroutines 之前先调用 `Add` 方法。

#### 忘记使用 `sync.Cond` (#72)

你可以使用 `sync.Cond` 向多个 goroutines 发送重复的通知。

#### 不使用 `errgroup` (#73)

你可以使用 `errgroup` 包来同步一组 goroutines 并处理错误和上下文。

#### 拷贝一个 `sync` 下的类型 (#74)

`sync` 包下的类型不应该被拷贝。

### 标准库

#### 使用了错误的 time.Duration (#75)

注意有些函数接收一个 `time.Duration` 类型的参数时，尽管直接传递一个整数是可以的，但最好还是使用 time API 中的方法来传递 duration，以避免可能造成的困惑、bug。

> ps: 重点是注意 time.Duration 定义的是 nanoseconds 数。

#### `time.After` 和内存泄漏 (#76)

避免在重复执行很多次的函数 （如循环中或HTTP处理函数）中调用 `time.After`，这可以避免内存峰值消耗。由 `time.After` 创建的资源仅在计时器超时才会被释放。

#### JSON处理中的常见错误 (#77)

* 类型嵌套导致的预料外的行为

  要当心在Go结构体中嵌入字段，这样做可能会导致诸如嵌入的 `time.Time` 字段实现 `json.Marshaler` 接口，从而覆盖默认的json序列。

* JSON 和 单调时钟

  当对两个 `time.Time` 类型值进行比较时，需要记住 `time.Time` 包含了一个墙上时钟（wall clock）和一个单调时钟 （monotonic clock），而使用 `==` 运算符进行比较时会同时比较这两个。

* Map 键对应值为 `any`

  当提供一个map用来unmarshal JSON数据时，为了避免不确定的value结构我们会使用 `any` 来作为value的类型而不是定义一个struct，这种情况下需要记得数值默认会被转换为 `float64`。

#### 常见的 SQL 错误 (#78)

* 忘记了 `sql.Open` 并没有与db服务器建立实际连接 

  需要调用 `Ping` 或者 `PingContext` 方法来测试配置并确保数据库是可达的。

* 忘记了使用连接池

  作为生产级别的应用，访问数据库时应该关注配置数据库连接池参数。

* 没有使用 prepared 语句

  使用 SQL prepared 语句能够让查询更加高效和安全。

* 误处理 null 值

  使用 `sql.NullXXX` 类型处理表中的可空列。

* 不处理行迭代时的错误

  调用 `sql.Rows` 的 `Err` 方法来确保在准备下一个行时没有遗漏错误。

#### 不关闭临时资源（HTTP 请求体、`sql.Rows` 和 `os.File`) (#79)

最终要注意关闭所有实现 `io.Closer` 接口的结构体,以避免可能的泄漏。

#### 响应HTTP请求后没有返回语句 (#80)

为了避免在HTTP处理函数中出现某些意外的问题，如果想在发生 `http.Error` 后让HTTP处理函数停止，那么就不要忘记使用`return`语句来阻止后续代码的执行。

#### 直接使用默认的HTTP client和server (#81)

对于生产级别的应用，不要使用默认的HTTP client和server实现。这些实现缺少超时和生产环境中应该强制使用的行为。

### 测试

#### 不对测试进行分类 （build tags, 环境变量，短模式）(#82)

对测试进行必要的分类，可以借助 build tags、环境变量以及短模式，来使得测试过程更加高效。你可以使用 build tags 或环境变量来创建测试类别（例如单元测试与集成测试），并区分短测试与长时间测试，来决定执行哪种类型的。

> ps: 了解下go build tags，以及 `go test -short`。

#### 不打开 race 开关 (#83)

打开 `-race` 开关在编写并发应用时非常重要。这能帮助你捕获可能的数据竞争,从而避免软件bug。

#### 不打开测试的执行模式开关 (parallel 和 shuffle) (#84)

打开开关 `-parallel` 有助于加速测试的执行，特别是测试中包含一些需要长期运行的用例的时候。

打开开关 `-shuffle` 能够打乱测试用例执行的顺序，避免一个测试依赖于某些不符合真实情况的预设，有助于及早暴漏bug。

#### 不使用表驱动的测试 (#85)

表驱动的测试是一种有效的方式,可以将一组相似的测试分组在一起,以避免代码重复和使未来的更新更容易处理。

#### 在单元测试中执行sleep操作 (#86)

使用同步的方式、避免sleep，来尽量减少测试的不稳定性和提高鲁棒性。如果无法使用同步手段,可以考虑重试的方式。

#### 没有高效地处理 time API (#87)

理解如何处理使用 time API 的函数，是使测试更加稳定的另一种方式。您可以使用标准技术，例如将时间作为隐藏依赖项的一部分来处理，或者要求客户端提供时间。

#### 不使用测试相关的工具包 (`httptest` 和 `iotest`) (#88)

这个 `httptest` 包对处理HTTP应用程序很有帮助。它提供了一组实用程序来测试客户端和服务器。

这个 `iotest` 包有助于编写 io.Reader 并测试应用程序是否能够容忍错误。

#### [不正确的基准测试](https://teivah.medium.com/how-to-write-accurate-benchmarks-in-go-4266d7dd1a95) (#89)

* 不要重置或者暂停timer

  使用 time 方法来保持基准测试的准确性。

* 做出错误的微基准测试假设

  增加 `benchtime` 或者使用 `benchstat` 等工具可以有助于微基准测试。

  小心微基准测试的结果,如果最终运行应用程序的系统与运行微基准测试的系统不同。

* 对编译期优化要足够小心

  确保测试函数是否会产生一些副作用，防止编译器优化欺骗你得到的基准测试结果。

* 被观察者效应所欺骗

  为了避免被观察者效应欺骗,强制重新创建CPU密集型函数使用的数据。

#### 没有去探索go test所有的特性 (#90)

* 代码覆盖率

  使用 `-coverprofile` 参数可以快速查看代码的测试覆盖情况，方便快速查看哪个部分需要更多的关注。

* 在一个不同包中执行测试

  单元测试组织到一个独立的包中，对于对外层暴漏的接口，需要写一些测试用例。测试应该关注公开的行为，而非内部实现细节。

* Utility 函数

  处理错误时,使用 `*testing.T` 变量而不是经典的 `if err != nil` 可以让代码更加简洁易读。

* 设置和销毁

  你可以使用setup和teardown函数来配置一个复杂的环境，比如在集成测试的情况下。

#### 不使用模糊测试 (社区反馈错误)

模糊测试是一种高效的策略，使用它能检测出随机、意料外的和一些恶意的数据输入，来完成一些复杂的操作。

见: [@jeromedoucet](https://github.com/jeromedoucet)

### 优化技术

#### 不理解CPU cache (#91)

* CPU架构

  理解CPU缓存的使用对于优化CPU密集型应用很重要，因为L1缓存比主存快50到100倍。

* Cache line

  意识到 cache line 概念对于理解如何在数据密集型应用中组织数据非常关键。CPU 并不是一个一个字来获取内存。相反，它通常复制一个 64字节长度的 cache line。为了获得每个 cache line 的最大效用，需要实施空间局部性。

* 一系列struct元素构成的slice vs. 多个slice字段构成的struct

* 概率性的问题 

  提高CPU执行代码时的可预测性，也是优化某些函数的一个有效方法。比如，固定步长或连续访问对CPU来说是可预测的，但非连续访问（例如链表）就是不可预测的。

* cache放置策略

  要注意现代缓存是分区的（set associative placement，组相连映射），要注意避免使用 `critical stride`，这种步长情况下只能利用 cache 的一小部分。

  > critical stride，这种类型的步长，指的是内存访问的步长刚好等于 cache 大小。这种情况下，只有少部分 cacheline 被利用。

#### 写的并发处理逻辑会导致false sharing (#92)

了解 CPU 缓存的较低层的 L1、L2 cache 不会在所有核间共享，编写并发处理逻辑时能避免写出一些降低性能的问题，比如伪共享（false sharing）。内存共享只是一种假象。

#### 没有考虑指令级的并行 (#93)

使用指令级并行（ILP）优化代码的特定部分，以允许CPU尽可能执行更多可以并行执行的指令。识别指令的数据依赖问题（data hazards）是主要步骤之一。

#### 不了解数据对齐 (#94)

记住Go中基本类型与其自身大小对齐，例如，按降序从大到小重新组织结构体的字段可以形成更紧凑的结构体（减少内存分配，更好的空间局部性），这有助于避免一些常见的错误。

#### 不了解 stack vs. heap (#95)

了解堆和栈之间的区别是开发人员的核心知识点，特别是要去优化一个Go程序时。栈分配的开销几乎为零，而堆分配则较慢，并且依赖GC来清理内存。

#### 不知道如何减少内存分配次数 (API调整, compiler optimizations, and `sync.Pool`) (#96)

减少内存分配次数也是优化Go应用的一个重要方面。这可以通过不同的方式来实现,比如仔细设计API来避免不必要的拷贝，以及使用 `sync.Pool` 来对待分配对象进行池化。

#### 不注意使用内联 (#97)

使用快速路径的内联技术来更加有效地减少调用函数的摊销时间。

#### [不使用Go问题诊断工具](https://medium.com/@teivah/profiling-and-execution-tracing-in-go-a5e646970f5b) (#98)

了解Go profilng工具、执行时tracer来辅助判断一个应用程序是否正常，以及列出需要优化的部分。

#### 不理解GC是如何工作的 (#99)

理解如何调优GC能够带来很多收益，例如有助于更高效地处理突增的负载。

#### 不了解Docker或者K8S对运行的Go应用的性能影响 (#100)

为了避免CPU throttling（CPU限频）问题，当我们在Docker和Kubernetes部署应用时，要知道Go语言对CFS(完全公平调度器)无感知。

## 🌎 外部资源

### 英文资料

* How to make mistakes in Go - Go Time #190: [Episode](https://changelog.com/gotime/190), [Spotify](https://open.spotify.com/episode/0K1DImrxHCy6E7zVY4AxMZ?si=akroInsPQ1mM5B5V2tHLUw&dl_branch=1)
* [8LU - 100% Test Coverage](https://youtu.be/V3FBDav6wgQ?t=1210)
* [Some Tips I learned from 100 Mistakes in Go](https://raygervais.dev/articles/2023/04/100_mistakes_in_go/)
* [What can be summarized from 100 Go Mistakes?](https://www.sobyte.net/post/2023-05/summarized-from-100-go-mistakes/)

### 中文资料

* [深度阅读之《100 Go Mistakes and How to Avoid Them](https://qcrao.com/post/100-go-mistakes-reading-notes/)
* [100 Go Mistakes 随记](https://zhuanlan.zhihu.com/p/592602656)
* [我为什么放弃Go语言？](https://juejin.cn/post/7241452578125824061)

### 日本资料

* [最近読んだGo言語の本の紹介：100 Go Mistakes and How to Avoid Them](https://qiita.com/kentaro_suzuki/items/c9c31dc81217f237433c)
* [『100 Go Mistakes and How to Avoid Them』を読む](https://zenn.dev/yukibobier/books/066f07c8a59fa0)
* [100 Go Mistakes 随记 - 01 Code and project organization](https://zhuanlan.zhihu.com/p/592602656)

### 葡萄牙资料

* [Um ÓTIMO livro para programadores Go](https://www.youtube.com/watch?v=34XShL_jWD4)
