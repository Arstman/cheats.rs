+++
weight = 1
sort_by = "weight"
template = "index.html"
insert_anchor_links = "right"
+++

<img id="logo" class="hide_on_small" src="logo.png" alt="煮熟的大闸蟹~"></img>
<pagetitle>Rust 语言备忘清单</pagetitle>
<subtitle><span id="subtitle" onclick="advance_subtitle()">{{ date() }}</span></subtitle>


<blockquote class="legend">

<symbol-legend class="short">

《Rust 程序设计语言》{{ book(page="") }}
《通过例子学 Rust》{{ ex(page="") }}
《标准库文档》{{ std(page="std") }}
《Rust 秘典》{{ nom(page="") }}
《Rust 参考手册》{{ ref(page="") }}

</symbol-legend>

<symbol-legend class="long">

<twocolumn>
<column>

**可点击凡例** <br>
<br> <legend-symbol> {{ book(page="") }} </legend-symbol>《Rust 程序设计语言》
<br> <legend-symbol> {{ ex(page="") }} </legend-symbol>《通过例子学 Rust》
<br> <legend-symbol> {{ std(page="std") }} </legend-symbol>《标准库文档》
<br> <legend-symbol> {{ nom(page="") }} </legend-symbol>《Rust 秘典》（死灵书）
<br> <legend-symbol> {{ ref(page="") }} </legend-symbol>《Rust 参考手册》
<br> <legend-symbol> {{ rfc(page="") }} </legend-symbol>官方 **RFC** 文档
<br> <legend-symbol> {{ link(url="https://cheats.rs.kingfree.moe") }} </legend-symbol>**外部链接**
<br> <legend-symbol> {{ above(target="#") }} </legend-symbol>参见**上文**
<br> <legend-symbol> {{ below(target="#") }} </legend-symbol>参见**下文**

</column>
<column>

**其他凡例** <br>
<br> <legend-symbol> {{ deprecated() }}   </legend-symbol>**已废弃**
<br> <legend-symbol> {{ edition(ed="'18") }} </legend-symbol>要求**最低版本**
<br> <legend-symbol> {{ experimental() }} </legend-symbol>要求 **Rust nightly** (或未完成)
<br> <legend-symbol> {{ bad() }}   </legend-symbol>特意的**错误示例**或**缺陷代码**
<br> <legend-symbol> {{ esoteric() }}   </legend-symbol>**晦涩**、少用或难懂的特性
<br> <legend-symbol> {{ hot() }}   </legend-symbol>**常用特性**
<br> <legend-symbol> {{ todo() }} </legend-symbol>**缺少链接**或解释
<br> <legend-symbol> {{ opinionated() }} </legend-symbol>**作者见解**

</column>
</twocolumn>
</symbol-legend>

<div style="text-align: right; height: 1px;">
    <span class="expander" style="font-size: 10px; position: relative; top: -20px;">
        <a href="javascript:toggle_legend();">➕</a>
    </span>
</div>

</blockquote>


<noprint>
<page-controls>
    <!-- <a id="" href="" style="float: left; margin-left:5px;">X-Ray Mode 👓</a> -->
    <a id="toggle_ligatures" href="javascript:toggle_ligatures()">连字 (<code>..=, =></code>)</a>
    <a id="expand_everything" class="hide_on_small" href="javascript:toggle_expand_all()">全部展开</a>
    <a href="javascript:toggle_night_mode()">深色模式 &#x1f4a1;</a>
</page-controls>
</noprint>

<noprint>
<toc><column>

**语言架构**
* [数据结构](#data-structures)
* [引用和指针](#references-pointers)
* [函数和行为](#functions-behavior)
* [控制流程](#control-flow)
* [代码组织](#organizing-code)
* [类型别名和转换](#type-aliases-and-casts)
* [宏和属性](#macros-attributes)
* [模式匹配](#pattern-matching)
* [泛型和约束](#generics-constraints)
* [Higher-Ranked Items](#higher-ranked-items)
* [字符串和字符](#strings-chars)
* [Documentation](#documentation)
* [其他](#miscellaneous)

**增强设施**
* [The Abstract Machine](#the-abstract-machine)
* [语法糖](#language-sugar)
* [Memory & Lifetimes](#memory-lifetimes)


**数据类型**
* [基本类型](#basic-types)
* [自定义类型](#custom-types)
* [引用和指针](#references-pointers-ui)
* [闭包](#closures-data)
* [标准库类型](#standard-library-types)

**附录**
* [外链和服务](#links-services)
* [打印 PDF](#printing-pdf)

</column>

<column>

**标准库**
* [One-Liners](#one-liners)
* [Thread Safety](#thread-safety)
* [Iterators](#iterators)
* [Number Conversions](#number-conversions)
* [字符串转换](#string-conversions)
* [String Output](#string-output)


**工具**
* [项目结构](#project-anatomy)
* [Cargo](#cargo)
* [交叉编译](#cross-compilation)
* [Tooling Directives](#tooling-directives)


**Working with Types**
* [Types, Traits, Generics](#types-traits-generics)
* [Type Zoo](#type-zoo)
* [Type Conversions](#type-conversions)


**编码指南**
* [Rust 惯用法](#idiomatic-rust)
* [Async-Await 101](#async-await-101)
* [API 中的闭包](#closures-in-apis)
* [Unsafe, Unsound, Undefined](#unsafe-unsound-undefined)
* [API 稳定性](#api-stability)

</column>

</toc>

<noprint>

## 你好, Rust！

如果你之前从来没用过 Rust，或者你想试点什么东西，都可以在这里跑一下：

<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-hello-1" name="tab-hello" checked/>
<label for="tab-hello-1"><b>Hello World</b></label>
<panel><div>
<div id="hellostatic">

```rust
fn main() {
    println!("Hello, world!");
}
```


</div>
<div id="helloplay"></div>
<div id="helloinfo">由 <a href="https://play.rust-lang.org/" target="_blank" rel="noopener">play.rust-lang.org <sup>🔗</sup></a> 提供</div>
<div id="helloctrl"><a href="javascript:show_playground(true);">▶️ 编译运行</a></div>
</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-hello-3" name="tab-hello">
<label for="tab-hello-3"><b>Strengths</b></label>
<panel><div>

**Things Rust does measurably really well**

- Compiled code [about same performance](https://benchmarksgame-team.pages.debian.net/benchmarksgame/box-plot-summary-charts.html) as C / C++, and excellent [memory and energy efficiency](https://dl.acm.org/doi/10.1145/3136014.3136031).
- Can [avoid 70% of all safety issues](https://www.chromium.org/Home/chromium-security/memory-safety) present in C / C++, and most memory issues.
- Strong type system prevents [data races](https://doc.rust-lang.org/nomicon/races.html), brings ['fearless concurrency'](https://blog.rust-lang.org/2015/04/10/Fearless-Concurrency.html) (amongst others).
- Seamless C interop, and [dozens of supported platforms](https://doc.rust-lang.org/rustc/platform-support.html) (based on LLVM).
- ["Most loved language"](https://insights.stackoverflow.com/survey/2021#technology-most-loved-dreaded-and-wanted) for 6 years in a row.
- Modern tooling: `cargo` (builds _just work_), `clippy` (450+ code quality lints), `rustup` (easy toolchain mgmt).

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-hello-4" name="tab-hello">
<label for="tab-hello-4"><b>Weaknesses</b></label>
<panel><div>

**Points you might run into**

- Steep learning curve;<sup>1</sup> compiler enforcing (esp. memory) rules that would be "best practices" elsewhere.
- Missing Rust-native libs in some domains, target platforms (esp. embedded), IDE features.<sup>1</sup>
- Longer compile times than "similar" code in other languages.<sup>1</sup>
- No formal language specification, can prevent legal use in some domains (aviation, medical, &hellip;).
- Careless (use of `unsafe` in) libraries can secretly break safety guarantees.

<sup>1</sup> Compare [Rust Survey](https://blog.rust-lang.org/2020/04/17/Rust-survey-2019.html#why-not-use-rust).
</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-hello-5" name="tab-hello">
<label for="tab-hello-5"><b>Installation</b></label>
<panel><div>

**Download**
- Get installer from [**rustup.rs**](https://rustup.rs/) (highly recommended for any platform)


**IDEs**
- [IntelliJ](https://www.jetbrains.com/idea/) (free) or [CLion](https://www.jetbrains.com/clion/) (paid) with [**IntelliJ Rust**](https://intellij-rust.github.io/)
- [Visual Studio Code](https://code.visualstudio.com/) with [**rust-analyzer**](https://rust-analyzer.github.io/)


</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-hello-6" name="tab-hello">
<label for="tab-hello-6"><b>First Steps</b></label>
<panel><div>

<!-- Note - Please ONLY submit PRs linking to high-quality, "permanent" sites
            dedicated to learning Rust that work in a browser, are moderately
            condensed, and have a public Git repo and issue tracker.
            Also, this section should be very short <=3 entries, so it should only list
            "the best of their kind".
             -->

**Modular Beginner Resources**
- [**Tour of Rust**](https://tourofrust.com/TOC_en.html) - Live code and explanations, side by side.
- [**Rust in Easy English**](https://dhghomon.github.io/easy_rust/Chapter_3.html) - 60+ concepts, simple English, example-driven.

In addition, have a look at the usual suspects. {{ book(page="") }} {{ ex(page="") }} {{ std(page="std") }}


> **Opinion** {{ opinionated() }} &mdash; If you have never seen or used any Rust it might be good to visit one of the links above before continuing; the next chapter might feel a bit terse otherwise.

</div></panel></tab>

</tabs>
</noprint>


### 数据结构 {#data-structures}

数据类型和内存位置由关键字定义。

<fixed-2-column>

| 示例 | 说明 |
|---------|-------------|
| `struct S {}` | 定义包含命名字段的**结构体**{{ book(page="ch05-00-structs.html") }} {{ ex(page="custom_types/structs.html") }} {{ std(page="std/keyword.struct.html") }} {{ ref(page="expressions/struct-expr.html") }}。 |
| {{ tab() }} `struct S { x: T }` | 定义包含 `T` 类型命名字段 `x` 的结构体。 |
| {{ tab() }} `struct S` &#8203;`(T);` | 定义 `T` 类型数字字段 `.0` 的“元组”结构体。 |
| {{ tab() }} `struct S;` | 定义一个**零大小**{{ nom(page="exotic-sizes.html#zero-sized-types-zsts")}} 单元的结构体。已优化不占空间。 |
| `enum E {}` | 定义**枚举**{{ book(page="ch06-01-defining-an-enum.html") }} {{ ex(page="custom_types/enum.html#enums") }} {{ ref(page="items/enumerations.html") }}。参见[数字数据类型](https://en.wikipedia.org/wiki/Algebraic_data_type)和[标签联合](https://en.wikipedia.org/wiki/Tagged_union)。 |
| {{ tab() }}  `enum E { A, B`&#8203;`(), C {} }` | 定义变体枚举，它可以是单元 `A`、元组 `B` &#8203;`()` 或者结构体风格的 `C{}`。 |
| {{ tab() }}  `enum E { A = 1 }` | 如果所有变体都是单元值，则允许判别式值，可用于 FFI。 |
| `union U {}` | 不安全的 C 风格**联合体**{{ ref(page="items/unions.html") }}，用于兼容 FFI。{{ esoteric() }} |
| `static X: T = T();`  | 具有静态 `'static` 生命周期的**全局变量** {{ book(page="ch19-01-unsafe-rust.html#accessing-or-modifying-a-mutable-static-variable") }} {{ ex(page="custom_types/constants.html#constants") }} {{ ref(page="items/static-items.html#static-items") }}，内存位置独立。 |
| `const X: T = T();`  | 定义**常量** {{ book(page="ch03-01-variables-and-mutability.html#differences-between-variables-and-constants") }} {{ ex(page="custom_types/constants.html") }} {{ ref(page="items/constant-items.html") }}。使用时会临时复制一份。 |
| `let x: T;`  | 在栈{{ note( note="1") }}上分配 `T` 大小的字节并命名为 `x`。一旦分配，不可修改。 |
| `let mut x: T;`  | 类似 `let`，但具有**可变性** {{ book(page="ch03-01-variables-and-mutability.html") }} {{ ex(page="variable_bindings/mut.html") }}，允许修改和可变借用。{{ note( note="2") }} |
| {{ tab() }} `x = y;` | 将 `y` 移动到 `x`，如果 `T` 不满足 `Copy`{{ std(page="std/marker/trait.Copy.html") }}，`y` 将不再可用，否则会复制一份 `y`。|

</fixed-2-column>

<footnotes>

<sup>1</sup> 同步代码中，**域变量** {{ book(page="ch03-01-variables-and-mutability.html") }} {{ ex(page="variable_bindings.html") }} {{ ref(page="variables.html") }} 生存在栈上。但对于 `async {}`，这些变量将会成为异步状态机的一部分，最终可能是在堆上。<br>
<sup>2</sup> 注意术语_可变_和_不可变_并不准确. 尽管你有一个不可变绑定或者共享引用，它也有可能包含一个 Cell {{ std(page="std/cell/index.html") }}，它仍支持 _内部可变性_。

</footnotes>


{{ tablesep() }}

下面列出了如何创建和访问数据结构，包括一些**神奇的**类型。

<fixed-2-column>

| 示例 | 说明 |
|---------|-------------|
| `S { x: y }` | 创建 `struct S {}`，或 `use` 的 `enum E::S {}` 字段 `x` 设置为 `y`。 |
| `S { x }` | 同上，但字段 `x` 会设置为局部变量 `x`。 |
| `S { ..s }` | 用 `s` 填充剩余字段，常配合 [Default](https://doc.rust-lang.org/std/default/trait.Default.html) 使用。 |
| `S { 0: x }` | 类似下面的 `S` &#8203;`(x)` 但是用结构体语法初始化字段 `.0`。  |
| `S`&#8203; `(x)` | 创建 `struct S` &#8203;`(T)`，或 `use` 的 `enum E::S`&#8203; `()` 其中字段 `.0` 设置为 `x`。 |
| `S` | 表示 `struct S;` 或以 `S` 为值创建 `use` 来的 `enum E::S`。 |
| `E::C { x: y }` | 创建枚举变体 `C`。 上面的方法依然可用。 |
| `()` | 空元组，既是字面量也是类型，又称**单元**。 {{ std(page="std/primitive.unit.html") }} |
| `(x)` | 括号表达式。 |
| `(x,)` | 单元素**元组**表达式。 {{ ex(page="primitives/tuples.html") }} {{ std(page="std/primitive.tuple.html") }} {{ ref(page="expressions/tuple-expr.html") }} |
| `(S,)` | 单元素元组类型。 |
| `[S]` | 未指明长度的数组类型，如**切片**。{{ std(page="std/primitive.slice.html") }}  {{ ex(page="primitives/array.html") }}  {{ ref(page="types.html#array-and-slice-types") }} 不能生存在栈上。 {{ note( note="*") }} |
| `[S; n]` | 元素类型为 `S` 定长为 `n` 的**数组类型**{{ ex(page="primitives/array.html") }}  {{ std(page="std/primitive.array.html") }}。 |
| `[x; n]` | 由 `n` 个 `x` 的副本构成的数组实例。 {{ ref(page="expressions/array-expr.html") }} |
| `[x, y]` | 由给定元素 `x` 和 `y` 构成的数组实例。 |
| `x[0]` | 索引，下标为 `usize`。 可重载 [Index](https://doc.rust-lang.org/std/ops/trait.Index.html) 和 [IndexMut](https://doc.rust-lang.org/std/ops/trait.IndexMut.html)。 |
| {{ tab() }} `x[..]` | 范围索引。此处为_全部范围_，又见下 `x[a..b]`、`x[a..=b]`、……  |
| `a..b` | **左闭右开区间**，{{ std(page="std/ops/struct.Range.html") }} {{ ref(page="expressions/range-expr.html") }} 如 `1..3` 表示 `1, 2`。  |
| `..b` | 右开区间 **RangeTo** {{ std(page="std/ops/struct.RangeTo.html") }} 不指定起点。  |
| `a..=b` | **闭区间**，{{ std(page="std/ops/struct.RangeInclusive.html") }} `1..=3` 表示 `1, 2, 3`。 |
| `..=b` | 右闭区间 **RangeFrom** {{ std(page="std/ops/struct.RangeFrom.html") }} 不指定起点。  |
| `..` | **全区间**，{{ std(page="std/ops/struct.RangeFull.html") }} 常表示_整个集合_。   |
| `s.x` | 命名**字段访问**{{ ref(page="expressions/field-expr.html") }}，如果 `x` 不是 `S` 的一部分的话则会尝试 [Deref](https://doc.rust-lang.org/std/ops/trait.Deref.html)。 |
| `s.0` | 数字字段访问，用于元组类型 `S` &#8203;`(T)`。 |

</fixed-2-column>

<footnotes>

<sup>*</sup> 目前，可以参考{{ rfc( page ="1909-unsized-rvalues.html") }}中的[已知问题](https://github.com/rust-lang/rust/issues/48055)。

</footnotes>


### 引用和指针 {#references-pointers}

为非所有者内存赋予访问权限。参见 [泛型和约束](#generics-constraints)。


<fixed-2-column>

| 示例 | 说明 |
|---------|-------------|
| `&S` | 共享 **引用** {{ book(page="ch04-02-references-and-borrowing.html") }} {{ std(page="std/primitive.reference.html") }} {{ nom(page="references.html")}} {{ ref(page="types.html#pointer-types")}} (用于存储_任意_`&s`). |
| {{ tab() }} `&[S]` | 特殊的切片引用，包含地址和长度 (`address`, `length`). |
| {{ tab() }} `&str` | 特殊的字符串引用，包含地址和长度 (`address`, `length`). |
| {{ tab() }} `&mut S` | 允许修改的独占引用 (参见 `&mut [S]`, `&mut dyn S`, &hellip;). |
| {{ tab() }} `&dyn T` | 特殊的 **trait 对象** {{ book(page="ch17-02-trait-objects.html#using-trait-objects-that-allow-for-values-of-different-types") }} 引用，包含地址和虚表 (`address`, `vtable`). |
| `&s` | 共享**借用** {{ book(page="ch04-02-references-and-borrowing.html") }} {{ ex(page="scope/borrow.html") }} {{ std(page="std/borrow/trait.Borrow.html") }} (_该_ `s` 的地址、长度、虚表等, 如 `0x1234`). |
| {{ tab() }} `&mut s` | 具有**可变性**的独占借用. {{ ex(page="scope/borrow/mut.html") }} |
| `*const S` | 不可变的**裸指针类型** {{ book(page="ch19-01-unsafe-rust.html#dereferencing-a-raw-pointer") }} {{ std(page="std/primitive.pointer.html") }} {{ ref(page="types.html#raw-pointers-const-and-mut") }}，内存不安全 |
| {{ tab() }} `*mut S` | 可变的裸指针类型，内存不安全。 |
| {{ tab() }} `&raw const s` | Create raw pointer w/o going through reference; _c_. `ptr:addr_of!()` {{ std(page="std/ptr/macro.addr_of.html") }} {{ experimental() }} {{ esoteric() }}  |
| {{ tab() }} `&raw mut s` | Same, but mutable. {{ experimental() }} Raw ptrs. are needed for unaligned, packed fields. {{ esoteric() }} |
| `ref s` | **引用绑定**, {{ ex(page="scope/borrow/ref.html") }} 创建绑定的引用类型. {{ deprecated() }}|
| {{ tab() }} `let ref r = s;` | 等价于 `let r = &s`. |
| {{ tab() }} `let S { ref mut x } = s;` | Mutable ref binding (`let x = &mut s.x`), shorthand destructuring {{ below( target = "#pattern-matching") }} version. |
| `*r` | **Dereference** {{ book(page="ch15-02-deref.html") }} {{ std(page="std/ops/trait.Deref.html") }} {{ nom(page="vec-deref.html") }} a reference `r` to access what it points to. |
| {{ tab() }} `*r = s;` | 如果 `r` 是一个可变引用，则将 `s` 移动或复制到目标内存。 |
| {{ tab() }} `s = *r;` | 如果 `r` 可 `Copy`，则将 `r` 引用的内容复制到 `s`。 |
| {{ tab() }} `s = *my_box;` | `Box` 有一个[特例](https://www.reddit.com/r/rust/comments/b4so6i/what_is_exactly/ej8xwg8/) ，即便它不可 `Copy`，也仍会从 Box 里面移动出来。 |
| `'a`  | **生命周期参数**，{{ book(page="ch10-00-generics.html") }} {{ ex(page="scope/lifetime.html")}} {{ nom(page="lifetimes.html") }} {{ ref(page="items/generics.html#type-and-lifetime-parameters")}}，为静态分析声明一块代码的持续时间。 |
| {{ tab() }}  `&'a S`  | 仅支持生存时间不短于 `'a` 的地址 `s` 。 |
| {{ tab() }}  `&'a mut S`  | 同上，但允许改变地址指向的内容。 |
| {{ tab() }}  `struct S<'a> {}`  | 表明 `S` 包含一个生命周期为 `'a` 的地址。由 `S` 的创建者决定 `'a`。 |
| {{ tab() }} `trait T<'a> {}` | 表明一个实现了 `impl T for S` 的 `S` 可能会包含地址。 |
| {{ tab() }}  `fn f<'a>(t: &'a T)`  | 同上，用于函数。调用者决定 `'a`。 |
| `'static`  | 特殊的生命周期，生存在程序的整个执行过程中。 |

</fixed-2-column>




###  函数和行为 {#functions-behavior}

定义代码单元及其抽象。

<fixed-2-column>

| 示例 | 说明 |
|---------|-------------|
| `trait T {}`  | 定义 **trait** {{ book(page="ch10-02-traits.html") }} {{ ex(page="trait.html") }} {{ ref(page="items/traits.html") }}，它是一系列可被实现的通用行为. |
| `trait T : R {}` | `T` 是**父 trait** {{ ref(page="items/traits.html#supertraits") }} `R` 的子 trait。任何要 `impl T` 的 `S` 都必须先 `impl R`。 |
| `impl S {}`  | 类型 `S` 的函数**实现** {{ ref(page="items/implementations.html") }}，如方法。 |
| `impl T for S {}`  | 为类型 `S` 实现 trait `T`. |
| `impl !T for S {}` | 禁用自动推导的 **auto trait**. {{ nom(page="send-and-sync.html") }} {{ ref(page="special-types-and-traits.html#auto-traits") }} {{ experimental() }} {{ esoteric() }} |
| `fn f() {}`  | 定义一个**函数**{{ book(page="ch03-03-how-functions-work.html") }}  {{ ex(page="fn.html") }} {{ ref(page="items/functions.html") }}，或在 `impl` 里关联一个函数。 |
| {{ tab() }} `fn f() -> S {}`  | 同上，但会返回一个 `S` 类型的值。 |
| {{ tab() }} `fn f(&self) {}`  | 定义一个方法。{{ book(page="ch05-03-method-syntax.html") }}  {{ ex(page="fn/methods.html") }}例如，在 `impl S {}` 中. |
| `const fn f() {}`  | 编译期常量函数 `fn`。如 `const X: u32 = f(Y)`. {{ edition(ed="'18") }}|
| `async fn f() {}`  | **异步** {{ ref(page="items/functions.html#async-functions") }} {{ edition(ed="'18") }} function transformation, {{ below(target="#async-await-101") }} 函数转写。令 `f` 返回一个 `impl` **`Future`**. {{ std(page="std/future/trait.Future.html") }} |
| {{ tab() }} `async fn f() -> S {}`  | 同上，但令 `f` 返回 `impl Future<Output=S>`。 |
| {{ tab() }} `async { x }`  | 用在函数内部，使 `{ x }` 变得 `impl Future<Output=X>`。 |
| `fn() -> S`  | **函数指针**{{ book(page="ch19-05-advanced-functions-and-closures.html#function-pointers") }} {{ std(page="std/primitive.fn.html") }} {{ ref(page="types.html#function-pointer-types") }}，内存存放的可调用地址。 |
| `Fn() -> S`  | **可调用 Trait**{{ book(page="ch19-05-advanced-functions-and-closures.html#returning-closures") }} {{ std(page="std/ops/trait.Fn.html") }}（又见 `FnMut` 和 `FnOnce`），可由闭包或函数等实现。 |
| <code>&vert;&vert; {} </code> | **闭包** {{ book(page="ch13-01-closures.html") }} {{ ex(page="fn/closures.html") }} {{ ref(page="expressions/closure-expr.html")}} ，将会借用它所有的**捕获**。{{ below(target="#closures-data") }} {{ ref(page="types/closure.html#capture-modes") }}  (如局部变量). |
| {{ tab() }} <code>&vert;x&vert; {}</code> | 有传入参数 `x` 的闭包。 |
| {{ tab() }} <code>&vert;x&vert; x + x</code> | 没有块表达式的闭包，仅可由单个表达式组成。 |
| {{ tab() }} <code>move &vert;x&vert; x + y </code> | 闭包，将会获取它所有捕获的所有权。 |
| {{ tab() }} <code> return &vert;&vert; true </code> | 闭包，看起来像是逻辑或，但这里表示返回一个闭包。 |
| `unsafe` | **不安全代码**。{{ below(target="#unsafe-unsound-undefined") }} {{ book(page="ch19-01-unsafe-rust.html#unsafe-superpowers") }} {{ ex(page="unsafe.html#unsafe-operations") }} {{ nom(page="meet-safe-and-unsafe.html") }} {{ ref(page="unsafe-blocks.html#unsafe-blocks") }} 。如果你喜欢在周五晚上调试段错误的话~ |
| {{ tab() }} `unsafe fn f() {}` | Means "_calling can cause UB, {{ below(target="#unsafe-unsound-undefined") }} **YOU must check** requirements_". |
| {{ tab() }} `unsafe trait T {}` | Means "_careless impl. of `T` can cause UB_; **implementor must check**".  |
| {{ tab() }} `unsafe { f(); }` | Guarantees to compiler "_**I have checked** requirements, trust me_".  |
| {{ tab() }} `unsafe impl T for S {}` | Guarantees _`S` is well-behaved w.r.t `T`_; people may use `T` on `S` safely.  |

</fixed-2-column>


### 控制流程 {#control-flow}

在函数中控制执行。

<fixed-2-column>

| 示例 | 说明 |
|---------|-------------|
| `while x {}`  | **循环** {{ ref(page="expressions/loop-expr.html#predicate-loops") }}，当表达式 `x` 为真时运行。 |
| `loop {}`  | **无限循环** {{ ref(page="expressions/loop-expr.html#infinite-loops") }} 直到 `break`。可以用 `break x` 来 yield 一个值出来。 |
| `for x in iter {}` | 在 **迭代器** 上循环的语法糖。{{ book(page="ch13-02-iterators.html") }} {{ std(page="std/iter/index.html") }} {{ ref(page="expressions/loop-expr.html#iterator-loops") }} |
| `if x {} else {}`  | **条件分支** {{ ref(page="expressions/if-expr.html") }}。如果表达式为真则……否则…… |
| `'label: loop {}` | **循环标签** {{ ex(page="flow_control/loop/nested.html") }} {{ ref(page="expressions/loop-expr.html#loop-labels")}}，用于嵌套循环的流程控制。 |
| `break`  | **Break 表达式** {{ ref(page="expressions/loop-expr.html#break-expressions") }}，用于退出循环。 |
| {{ tab() }} `break x`  | 同上，但将 `x` 作为循环表达式的值（仅在 `loop` 中有效）。 |
| {{ tab() }} `break 'label`  | 不单单退出的是当前循环，而是最近一个标记有 `'label` 的循环。 |
| {{ tab() }} `break 'label x`  |  Same, but make `x` the value of the enclosing loop marked with `'label`. |
| `continue `  | **Continue 表达式** {{ ref(page="expressions/loop-expr.html#continue-expressions") }}，用于继续该循环的下一次迭代。 |
| `continue 'label`  | 同上，但继续的是最近标记有 `'label` 的循环迭代。 |
| `x?` | 如果 `x` 是 [Err](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err) 或 [None](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None)，**返回并向上传播**。{{ book(page="ch09-02-recoverable-errors-with-result.html#propagating-errors") }} {{ ex(page="error/result/enter_question_mark.html") }} {{ std(page="std/result/index.html#the-question-mark-operator-") }} {{ ref(page="expressions/operator-expr.html#the-question-mark-operator")}} |
| `x.await` | Only works inside `async`. Yield flow until **`Future`** {{ std(page="std/future/trait.Future.html") }} or Stream `x` ready. {{ ref(page="expressions/await-expr.html#await-expressions") }} {{ edition(ed="'18") }} |
| `return x`  | 从函数中提前返回。然而以表达式结束的方式更惯用。 |
| `f()` | 调用 `f`（如函数、闭包、函数指针或 `Fn` 等）。 |
| `x.f()` | 调用成员函数（方法），要求 `f` 以 `self`、`&self` 等作为第一个参数。 |
| {{ tab() }} `X::f(x)` | 同 `x.f()`。除非 `impl Copy for X {}`，否则 `f` 仅可调用一次。 |
| {{ tab() }} `X::f(&x)` | 同 `x.f()`。 |
| {{ tab() }} `X::f(&mut x)` | 同 `x.f()`。 |
| {{ tab() }} `S::f(&x)` | 同 `x.f()`，仅当 `X` 实现了对 `S` 的 [Deref](https://doc.rust-lang.org/std/ops/trait.Deref.html)。这里 `x.f()` 会去找 `S` 的方法。 |
| {{ tab() }} `T::f(&x)` | 同 `x.f()`，仅当 `X impl T`。这里 `x.f()` 会去找作用域内 `T` 的方法。 |
| `X::f()` | 调用关联函数。比如 `X::new()`。 |
| {{ tab() }} `<X as T>::f()` | 调用为 `X` 实现了的 trait 方法 `T::f()。 |
</fixed-2-column>



### 代码组织 {#organizing-code}

将项目分割成小的单元并最小化相关依赖。

<fixed-2-column>

| 示例 | 说明 |
|---------|-------------|
| `mod m {}`  | 定义**模块**{{ book(page="ch07-02-defining-modules-to-control-scope-and-privacy.html") }} {{ ex(page="mod.html#modules") }} {{ ref(page="items/modules.html#modules") }}，其中的定义在 `{}` 内. {{ below(target="#project-anatomy") }} |
| `mod m;`  | 定义模块，其中的定义在 `m.rs` 或 `m/mod.rs`. {{ below(target="#project-anatomy") }}|
| `a::b` | 命名空间**路径**{{ ex(page="mod/use.html") }} {{ ref(page="paths.html")}}，表示 `a`（`mod` 或 `enum` 等） 里面的元素 `b`。 |
| {{ tab() }} `::b` | 相对于当前 crate 根下搜索 `b` 。{{ deprecated() }} |
| {{ tab() }} `crate::b` | 相对于当前 crate 根下搜索 `b`。{{ edition(ed="'18") }} |
| {{ tab() }} `self::b`  | 相对于当前模块下搜索 `b`。 |
| {{ tab() }} `super::b`  | 相对于父级模块下搜索 `b`。 |
| `use a::b;`  | **Use** {{ ex(page="mod/use.html#the-use-declaration") }} {{ ref(page="items/use-declarations.html") }} 声明，将 `b` 直接引入到当前作用域，以后就不需要再加 `a` 前缀了。 |
| `use a::{b, c};` | 同上，但同时将 `b` 和 `c` 都引入。 |
| `use a::b as x;`  | 将 `b` 引入作用域但命名为 `x`。比如 `use std::error::Error as E`。 |
| `use a::b as _;`  | 将 `b` 匿名的引入作用域，用于含有冲突名称的 trait。 |
| `use a::*;`  | 将 `a` 里面的所有元素都引入作用域。仅推荐在 `a` 为 **prelude** 的情况下使用。{{ link(url="https://stackoverflow.com/questions/36384840/what-is-the-prelude" ) }} |
| `pub use a::b;`  | 将 `a::b` 引入作用域，并再次从当前位置导出。 |
| `pub T`  | 控制 `T` 的**可见性** {{ book(page="ch07-02-defining-modules-to-control-scope-and-privacy.html") }}。“如果父级路径公开，我也公开”。 |
| {{ tab() }} `pub(crate) T` | 可见性仅<sup>1</sup>在当前 crate 内。 |
| {{ tab() }} `pub(self) T`  | 可见性仅<sup>1</sup>在当前模块内。 |
| {{ tab() }} `pub(super) T`  | 可见性仅<sup>1</sup>在父级以下。 |
| {{ tab() }} `pub(in a::b) T`  | 可见性仅<sup>1</sup>在 `a::b` 内。 |
| `extern crate a;` | 声明依赖一个外部 **crate** {{ book(page="ch02-00-guessing-game-tutorial.html#using-a-crate-to-get-more-functionality") }} {{ ex(page="crates/link.html#extern-crate") }} {{ ref(page="items/extern-crates.html#extern-crate-declarations") }} {{ deprecated() }}。换用 `use a::b` {{ edition(ed="'18") }}。  |
| `extern "C" {}`  | _声明_ **FFI** 的外部依赖和 ABI（如 `"C"`）。 {{ book(page="ch19-01-unsafe-rust.html#using-extern-functions-to-call-external-code") }} {{ ex(page="std_misc/ffi.html#foreign-function-interface") }} {{ nom(page="ffi.html#calling-foreign-functions") }} {{ ref(page="items/external-blocks.html#external-blocks") }} |
| `extern "C" fn f() {}`  | _定义_ FFI 导出成 ABI（如 `"C"`）的函数。 |

</fixed-2-column>

<footnotes>

<sup>1</sup> Items in child modules always have access to any item, regardless if `pub` or not.

</footnotes>


### 类型别名和转换 {#type-aliases-and-casts}

类型名称的简写，以及转为其他类型的方法。

<fixed-2-column>

| 示例 | 说明 |
|---------|-------------|
| `type T = S;`  | 创建**类型别名**{{ book(page="ch19-04-advanced-types.html#creating-type-synonyms-with-type-aliases") }} {{ ref(page="items/type-aliases.html?highlight=alias#type-aliases") }}。这里表示 `S` 的另一个名字。 |
| `Self`  | **当前实现类型**{{ ref(page="types.html#self-types") }} 的别名。如 `fn new() -> Self`。 |
| `self`  | `fn f(self) {}` 的方法主体。同 `fn f(self: Self) {}`。 |
|  {{ tab() }}  `&self`  | 同上，但将借用指向自己的引用。同 `f(self: &Self)`。 |
|  {{ tab() }}  `&mut self`  | 同上，但是可变借用。同 `f(self: &mut Self)`。 |
|  {{ tab() }}  `self: Box<Self>`  | [任意自型](https://github.com/withoutboats/rfcs/blob/arbitray-receivers/text/0000-century-of-the-self-type.md)，为智能指针增加方法（`my_box.f_of_self()`）。 |
| `S as T`  | **消歧义**{{ book(page="ch19-03-advanced-traits.html#fully-qualified-syntax-for-disambiguation-calling-methods-with-the-same-name") }} {{ ref(page="expressions/call-expr.html#disambiguating-function-calls") }}，将类型 `S` 作为 trait `T` 看待。比如 `<X as T>::f()`。 |
| `S as R`  | 在 `use` 里，将 `S` 导入为 `R`。如 `use a::b as x`。 |
| `x as u32`  | 裸**转换**{{ ex(page="types/cast.html#casting") }} {{ ref(page="expressions/operator-expr.html#type-cast-expressions") }}，会发生截断和一些位上的意外。<sup>1</sup> {{ nom(page="casts.html") }} |

</fixed-2-column>

<footnotes>

<sup>1</sup> See [Type Conversions](#type-conversions) below for all the ways to convert between types.

</footnotes>



### 宏和属性 {#macros-attributes}

实际编译前的代码预展开。

<fixed-2-column>

| 示例 |  说明 |
|---------|---------|
| `m!()` |  **宏** {{book(page="ch19-06-macros.html")}} {{std(page="std/index.html#macros")}} {{ref(page="macros.html")}} 咒语。也作 `m!{}` 或 `m![]`（取决于宏本身）。 |
| `#[attr]`  | 外部**属性**{{ex(page="attribute.html")}} {{ref(page="attributes.html")}}。注解接下来的内容。 |
| `#![attr]` | Inner attribute, annotating the _upper_, surrounding item. |

</fixed-2-column>

{{ tablesep() }}

<fixed-2-column class="color-header special_example">

| Inside Macros |  Explanation |
|---------|---------|
| `$x:ty`  | Macro capture (here a type); see **tooling directives** {{ below(target="#tooling-directives") }} for details. |
| `$x` |  Macro substitution, e.g., use the captured `$x:ty` from above. |
| `$(x),*` | Macro repetition "zero or more times" in macros by example. |
| {{ tab() }} `$(x),?` | Same, but "zero or one time". |
| {{ tab() }} `$(x),+` | Same, but "one or more times". |
| {{ tab() }} `$(x)<<+` | In fact separators other than `,` are also accepted. Here: `<<`. |


</fixed-2-column>



### 模式匹配 {#pattern-matching}

函数参数、`match` 或 `let` 表达式中的构造。


<fixed-2-column>

| 示例 | 说明 |
|---------|-------------|
| `match m {}` | **模式匹配**{{ book(page="ch06-02-match.html") }} {{ ex(page="flow_control/match.html") }} {{ ref(page="expressions/match-expr.html") }}，下面跟匹配分支。参见 下表。 |
| `let S(x) = get();`  | 显然，`let` 也和下表的模式匹配类似。 |
|  {{ tab() }} `let S { x } = s;` | 仅将 `x` 绑定到值 `s.x`。 |
|  {{ tab() }} `let (_, b, _) = abc;` | 仅将 `b` 绑定到值 `abc.1`。 |
|  {{ tab() }} `let (a, ..) = abc;` | 也可以将“剩余的”都忽略掉。 |
|  {{ tab() }} `let (.., a, b) = (1, 2);` | Specific bindings take precedence over 'the rest', here `a` is `1`, `b` is `2`. |
|  {{ tab() }} `let s @ S { x } = get();`  | Bind `s` to `S` while `x` is bound to `s.x`, **pattern binding**, {{ book(page="ch18-03-pattern-syntax.html#-bindings") }} {{ ex(page="flow_control/match/binding.html#binding") }} {{ ref(page="patterns.html#identifier-patterns") }} _c_. below {{ esoteric() }} |
|  {{ tab() }} `let w @ t @ f = get();`  | Stores 3 copies of `get()` result in each `w`, `t`, `f`. {{ esoteric() }} |
|  {{ tab() }} `let Some(x) = get();` | **Won't** work {{ bad() }} if pattern can be **refuted**, {{ ref(page="expressions/if-expr.html#if-let-expressions") }} use `if let` instead. |
|  {{ tab() }} `let Some(x) = get();` | **不可用** {{ bad() }}，因为模式可能会 **不匹配** {{ ref(page="expressions/if-expr.html#if-let-expressions") }}。换用 `if let`。 |
| `if let Some(x) = get() {}`  | 如果模式匹配则执行该分支（如某个 `enum` 变体）。语法糖<sup>*</sup>。 |
| `fn f(S { x }: S)`  | 类似于 `let`，模式匹配也可用在函数参数上。这里，`f(s)` 的 `x` 被绑定到 `s.x`。{{ esoteric() }}|

</fixed-2-column>


<footnotes>

<sup>*</sup> 展开后是 `match get() { Some(x) => {}, _ => () }`。

</footnotes>



{{ tablesep() }}

`match` 表达式的模式匹配分支。左列的分支也可用于 `let` 表达式。

<fixed-2-column class="color-header special_example">

| 匹配分支 | 说明 |
|---------|-------------|
|  `E::A => {}` | 匹配枚举变体 `A`。参见**模式匹配**。{{ book(page="ch06-02-match.html") }} {{ ex(page="flow_control/match.html") }} {{ ref(page="expressions/match-expr.html") }} |
|  `E::B ( .. ) => {}` | 匹配枚举元组变体 `B`，通配所有下标。 |
|  `E::C { .. } => {}` | 匹配枚举结构变体 `C`，通配所有字段。 |
|  `S { x: 0, y: 1 } => {}` | 匹配含特定值的结构体（仅匹配 `s` 的 `s.x` 为 `0` 且 `s.y` 为 `1` 的情况）。 |
|  `S { x: a, y: b } => {}` | 匹配为**任意**(!)值的该类型结构体，并绑定 `s.x` 到 `a`，绑定 `s.y` 到 `b`。 |
|  {{ tab() }} `S { x, y } => {}` | 同上，但将 `s.x` 和 `s.y` 分别简写地绑定为 `x` 和 `y`。 |
|  `S { .. } => {}` | 匹配任意值的该类型结构体。 |
|  `D => {}` | 匹配枚举变体 `E::D`。仅当 `D` 已由 `use` 引入。 |
|  `D => {}` | 匹配任意事物并绑定到 `D`。如果 `D` 没被 `use` 进来，怕不是个 `E::D` 的假朋友。{{ bad() }} |
|  `_ => {}` | 通配所有，或者所有剩下的。 |
| <code>0 &vert; 1 => {}</code> | Pattern alternatives, **or-patterns**. {{ rfc( page ="2535-or-patterns.html") }}|
| {{ tab() }}  <code>E::A &vert; E::Z </code> | Same, but on enum variants. |
| {{ tab() }}  <code>E::C {x} &vert; E::D {x}</code> | Same, but bind `x` if all variants have it. |
| {{ tab() }}  <code>Some(A &vert; B)</code> | Same, can also match alternatives deeply nested. |
|  `(a, 0) => {}` | 匹配元组，绑定第一个值到 `a`，要求第二个是 `0`。 |
|  `[a, 0] => {}` | **切片模式**{{ ref(page="patterns.html?highlight=slice,pattern#slice-patterns") }} {{ link(url="https://doc.rust-lang.org/edition-guide/rust-2018/slice-patterns.html") }}。绑定第一个值到 `a`，要求第二个是 `0`。 |
|  {{ tab() }} `[1, ..] => {}` | 匹配以 `1` 开始的数组，剩下的不管。**子切片模式**。{{ todo() }} |
|  {{ tab() }} `[1, .., 5] => {}` | 匹配以 `1` 开始以 `5` 结束的数组。 |
|  {{ tab() }} `[1, x @ .., 5] => {}` | 同上，但将 `x` 绑定到中间部分的切片上（见匹配绑定）  |
|  {{ tab() }} `[a, x @ .., b] => {}` | Same, but match any first, last, bound as `a`, `b` respectively.  |
|  `1 .. 3 => {}` | **Range pattern**, {{ book(page="ch18-03-pattern-syntax.html#matching-ranges-of-values-with-") }} {{ ref(page="patterns.html#range-patterns") }} here matches `1` and `2`; partially unstable. {{ experimental() }} |
|  {{ tab() }} `1 ..= 3 => {}` | Inclusive range pattern, matches `1`, `2` and `3`. |
|  {{ tab() }} `1 .. => {}` | Open range pattern, matches `1` and any larger number.  |
| `x @ 1..=5 => {}` | 绑定匹配到 `x`，即**模式绑定**{{ book(page="ch18-03-pattern-syntax.html#-bindings") }} {{ ex(page="flow_control/match/binding.html#binding") }} {{ ref(page="patterns.html#identifier-patterns") }}。这里 `x` 可以是 `1`、`2` 直到 `5`。  |
| {{ tab() }} `Err(x @ Error {..}) => {}` | Also works nested, here `x` binds to `Error`, esp. useful with `if` below. |
| `S { x } if x > 10 => {}`  | 模式**匹配条件**{{ book(page="ch18-03-pattern-syntax.html#extra-conditionals-with-match-guards")}} {{ ex(page="flow_control/match/guard.html#guards")}} {{ ref(page="expressions/match-expr.html#match-guards") }}。该匹配会要求这个条件也为真。 |

</fixed-2-column>



<!-- This is more relevant for let D = ... cases, https://www.reddit.com/r/rust/comments/a1846o/rust_quiz_26_medium_to_hard_rust_questions_with/eaop291/ -->
<!-- |  `D => {}` | Match struct if `D` unit `struct D;`| -->



### 泛型和约束 {#generics-constraints}

Generics combine with type constructors, traits and functions to give your users more flexibility.

<fixed-2-column>

| 示例 | 说明 |
|---------|-------------|
| `S<T>`  | **泛型**{{ book(page="ch10-01-syntax.html") }} {{ ex(page="generics.html") }}，类型参数 `T` 是占位符。 |
| `S<T: R>`  | 类型短 **trait 约束**{{ book(page="ch10-02-traits.html#using-trait-bounds-to-conditionally-implement-methods") }} {{ ex(page="generics/bounds.html") }}说明。（`R` _必须_是个实际的 trait）。 |
| {{ tab() }} `T: R, P: S`  | **独立 trait 约束**（这里一个对 `T`，一个对 `P`）。 |
| {{ tab() }} `T: R, S`  | 编译错误{{ bad() }}。可以用下面的 `R + S` 代替。 |
| {{ tab() }} `T: R + S`  | **合并 trait 约束**{{ book(page="ch10-02-traits.html#specifying-multiple-trait-bounds-with-the--syntax") }} {{ ex(page="generics/multi_bounds.html") }}。`T` 必须同时满足 `R` 和 `S`。 |
| {{ tab() }} `T: R + 'a`  | 同上，但有生命周期。`T` 必须满足 `R`；如果 `T` 有生命周期，则必须长于 `'a`。 |
| {{ tab() }} `T: ?Sized` | Opt out of a pre-defined trait bound, here `Sized`. {{ todo() }} |
| {{ tab() }} `T: 'a` | 类型**生命周期约束**{{ ex(page="scope/lifetime/lifetime_bounds.html") }}。`T` 应长于 `'a`。 |
| {{ tab() }} `T: 'static` | Same; does esp. _not_ mean value `t` _will_ {{ bad() }} live `'static`, only that it could. |
| {{ tab() }} `'b: 'a` | Lifetime `'b` must live at least as long as (i.e., _outlive_) `'a` bound. |
| `S<const N: usize>` | **Generic const bound**; {{ todo() }} user of type `S` can provide constant value `N`. |
| {{ tab() }} `S<10>` | Where used, const bounds can be provided as primitive values. |
| {{ tab() }} `S<{5+5}>` | Expressions must be put in curly brackets. |
| `S<T> where T: R`  | Almost same as `S<T: R>` but more pleasant to read for longer bounds. |
| {{ tab() }} `S<T> where u8: R<T>`  | Also allows you to make conditional statements involving _other_ types. |
| `S<T = R>` | **Default parameters**; {{ book(page="ch19-03-advanced-traits.html#default-generic-type-parameters-and-operator-overloading") }} bit easier to use, but still flexible. |
| {{ tab() }} `S<const N: u8 = 0>` | Default parameter for constants; e.g., in `f(x: S) {}` param `N` is `0`. |
| {{ tab() }} `S<T = u8>` | Default parameter for types, e.g., in `f(x: S) {}` param `T` is `u8`. |
| `S<'_>` | Inferred **anonymous lifetime**; asks compiler to _'figure it out'_ if obvious.  |
| `S<_>` | Inferred **anonymous type**, e.g., as `let x: Vec<_> = iter.collect()`  |
| `S::<T>` | **Turbofish** {{ std(page="std/iter/trait.Iterator.html#method.collect")}} 消歧义类型调用。如 `f::<u32>()` |
| `trait T<X> {}`  | `X` 的 trait 泛型。可以有多个 `impl T for S`（每个 `X` 一个）。 |
| `trait T { type X; }`  | 定义**关联类型**{{ book(page="ch19-03-advanced-traits.html#specifying-placeholder-types-in-trait-definitions-with-associated-types") }} {{ ref(page="items/associated-items.html#associated-types") }} `X`。仅可有一个 `impl T for S` 。 |
| {{ tab() }} `type X = R;`  | 设置关联类型。仅在 `impl T for S { type X = R; }` 内。 |
| `impl<T> S<T> {}`  | 实现 `S<T>` 任意类型 `T` 的功能。 |
| `impl S<T> {}`  | 实现确定 `S<T>` 的功能。如 `S<u32>`。 |
| `fn f() -> impl T`  | **Existential 类型** {{ book(page="ch10-02-traits.html#returning-types-that-implement-traits") }}。返回一个对调用者未知的但 `impl T`的 `S`。 |
| `fn f(x: &impl T)`  | Trait 约束，“**impl trait**”{{ book(page="ch10-02-traits.html#trait-bound-syntax") }}。和 `fn f<S:T>(x: &S)` 有点类似。 |
| `fn f(x: &dyn T)`  | **动态分发**标记{{ book(page="ch17-02-trait-objects.html#using-trait-objects-that-allow-for-values-of-different-types") }} {{ ref(page="types.html#trait-objects") }}。`f` 不再单态。 |
| `fn f() where Self: R`  | 在 `trait T {}` 中标记 `f` 仅可由实现了 `impl R` 的类型访问。 |
| {{ tab() }} `fn f() where Self: Sized;`  | Using `Sized` can opt `f` out of `dyn T` trait object vtable, enabling trait obj. |
| {{ tab() }} `fn f() where Self: R {}`  | Other `R` useful w. dflt. methods (non dflt. would need be impl'ed anyway). |
</fixed-2-column>



### Higher-Ranked Items {{ esoteric() }} {#higher-ranked-items}

_Actual_ types and traits, abstract over something, usually lifetimes.

<fixed-2-column>

| Example | Explanation |
|---------|-------------|
| `for<'a>` | Marker for **higher-ranked bounds.** {{ nom(page="hrtb.html")}} {{ ref(page="trait-bounds.html#higher-ranked-trait-bounds")}} {{ esoteric() }} |
| {{ tab() }} `trait T: for<'a> R<'a> {}` | Any `S` that `impl T` would also have to fulfill `R` for any lifetime. |
| `fn(&'a u8)` | _Fn. ptr._ type holding fn callable with **specific** lifetime `'a`. |
| `for<'a> fn(&'a u8)` | **Higher-ranked type**<sup>1</sup> {{ link(url="https://github.com/rust-lang/rust/issues/56105") }} holding fn callable with **any** _lt._; subtype of above. |
| {{ tab() }} `fn(&'_ u8)` | Same; automatically expanded to type `for<'a> fn(&'a u8)`. |
| {{ tab() }} `fn(&u8)` | Same; automatically expanded to type `for<'a> fn(&'a u8)`. |
| `dyn for<'a> Fn(&'a u8)` | Higher-ranked (trait-object) type, works like `fn` above. |
| {{ tab() }} `dyn Fn(&'_ u8)` | Same; automatically expanded to type `dyn for<'a> Fn(&'a u8)`. |
| {{ tab() }} `dyn Fn(&u8)` | Same; automatically expanded to type `dyn for<'a> Fn(&'a u8)`. |

<footnotes>

 <sup>1</sup> Yes, the `for<>` is part of the type, which is why you write `impl T for for<'a> fn(&'a u8)` below.

</footnotes>

</fixed-2-column>


<div class="color-header special_example">
{{ tablesep() }}

| Implementing Traits | Explanation |
|---------|-------------|
| `impl<'a> T for fn(&'a u8) {}` | For fn. pointer, where call accepts **specific** _lt._ `'a`, impl trait `T`.|
| `impl T for for<'a> fn(&'a u8) {}` | For fn. pointer, where call accepts **any** _lt._, impl trait `T`. |
| {{ tab() }} `impl T for fn(&u8) {}` | Same, short version. |

</div>


### 字符串和字符 {#strings-chars}

Rust 提供了若干种创建字符串和字符字面量的办法。


<fixed-2-column>

| 示例 | 说明 |
|--------|-------------|
| `"..."` | UTF-8 **字符串字面量**{{ ref(page="tokens.html#string-literals")}}。会将 `\n` 等看作换行 `0xA` 等。 |
| `r"..."` | UTF-8 **裸字符串字面量**{{ ref(page="tokens.html#raw-string-literals")}}。不会处理 `\n` 等。 |
| `r#"..."#` 等 | UTF-8 裸字符串字面量。但可以包含 `"`。 |
| `b"..."` | **字节串字面量**{{ ref(page="tokens.html#byte-and-byte-string-literals")}}，由 ASCII `[u8]` 组成。不是字符串。 |
| `br"..."`、`br#"..."#` 等 | 裸字节串字面量，ASCII `[u8]`。说明见上。 |
| `'🦀'` | **字符字面量**{{ ref(page="tokens.html#character-and-string-literals")}}，固定的 4 字节 Unicode “**字符**”。{{ std(page="std/primitive.char.html") }} |
| `b'x'` | ASCII **字节字面量**。{{ ref(page="tokens.html#byte-literals")}} |
</fixed-2-column>

<footnotes>

<sup>1</sup> Supports multiple lines out of the box. Just keep in mind `Debug`{{ below(target="#string-output") }} (e.g., `dbg!(x)` and `println!("{x:?}")`) might render them as `\n`, while `Display`{{ below(target="#string-output") }} (e.g., `println!("{x}")`) renders them _proper_.

</footnotes>


### Documentation

Debuggers hate him. Avoid bugs with this one weird trick.


<fixed-2-column>

| 示例 | 说明 |
|--------|-------------|
| `///` | Outer line **doc comment**, {{ book(page="ch14-02-publishing-to-crates-io.html#making-useful-documentation-comments") }} {{ ex(page="meta/doc.html#documentation") }} {{ ref(page="comments.html#doc-comments")}} use these on types, traits, functions, &hellip; |
| `//!` | Inner line doc comment, mostly used at start of file to document module. |
| `//` | 行内注释。用于文档代码流内或_内部组件_。 |
| `/*...*/` | 块级注释。 |
| `/**...*/` | 外部块级文档注释. |
| `/*!...*/` | 内部块级文档注释. |

</fixed-2-column>

<footnotes>

Tooling directives {{ below(target="#tooling-directives") }} outlines what you can do inside doc comments.

</footnotes>



### 其他 {#miscellaneous}

这些小技巧不属于其他分类但最好了解一下。

<fixed-2-column>

| 示例 | 说明 |
|---------|-------------|
| `!` | 永远为空的 **never 类型**。{{ experimental() }} {{ book(page="ch19-04-advanced-types.html#the-never-type-that-never-returns") }} {{ ex(page="fn/diverging.html#diverging-functions") }} {{ std(page="std/primitive.never.html") }} {{ ref(page="types.html#never-type") }} |
| `_` | 无名变量绑定。如 <code>&vert;x, _&vert; {}</code>。|
| {{ tab() }} `let _ = x;`  | Unnamed assignment is no-op, does **not** {{ bad() }} move out `x` or preserve scope! |
| `_x` | 变量绑定，明确标记该变量未使用。 |
| `1_234_567` | 为了易读加入的数字分隔符。 |
| `1_u8` | **数字字面量**的类型说明符。{{ ex(page="types/literals.html#literals") }} {{ ref(page="tokens.html#number-literals") }}（又见 `i8`、`u16`等）。 |
| `0xBEEF`, `0o777`, `0b1001`  | 十六进制（`0x`）、八进制（`0o`）和二进制（`0b`) 整型字面量。 |
| `r#foo` | **原始标识符** {{ book(page="appendix-01-keywords.html#raw-identifiers") }} {{ ex(page="compatibility/raw_identifiers.html#raw-identifiers") }}。用于版本兼容。 {{ esoteric() }} |
| `x;` | **语句**{{ ref(page="statements.html")}}终止符。见**表达式**{{ ex(page="expression.html") }} {{ ref(page="expressions.html")}}。 |

</fixed-2-column>




### 通用操作符

Rust 支持大部分其他语言也有的通用操作符（`+`, `*`, `%`, `=`, `==`...）。因为这在 Rust 里没什么太大差别所以这里不列出来了。Rust 也支持**运算符重载**。{{ std(page="std/ops/index.html")}}


---

<magic>

# 增强设施

Arcane knowledge that may do terrible things to your mind, highly recommended.

## The Abstract Machine

Like `C` and `C++`, Rust is based on an _abstract machine_.


<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-abstract-machine-1" name="tab-group-abstract-machine" checked>
<label for="tab-abstract-machine-1"><b>Overview</b></label>
<panel><div>


<div style="text-align: center;">

<mini-zoo class="zoo" style="text-align: center;">
    <entry>
        <machine class="bad">Rust</machine>
    </entry>
    <code style="text-align:center;">→</code>
    <entry>
        <machine class="bad">CPU</machine>
    </entry>
    <br/>
    <note>{{bad()}} Less correctish.</note>
</mini-zoo>

<mini-zoo class="zoo" style="text-align: center; margin-left: 80px;">
    <entry>
        <machine class="good">Rust</machine>
    </entry>
    <code style="text-align:center">→</code>
    <entry style="width: 120px;">
        <machine class="good">Abstract Machine</machine>
    </entry>
    <code style="text-align:center">→</code>
    <entry>
        <machine class="good">CPU</machine>
    </entry>
    <br/>
    <note>More correctish.</note>
</mini-zoo>

</div>


{{ tablesep() }}


The abstract machine
- is not a runtime, and does not have any runtime overhead, but is a _computing model abstraction_,
- contains concepts such as memory regions (_stack_, ...), execution semantics, ...
- _knows_ and _sees_ things your CPU might not care about,
- forms a contract between programmer and machine,
- and **exploits all of the above for optimizations**.


</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-abstract-machine-2" name="tab-group-abstract-machine">
<label for="tab-abstract-machine-2"><b>Misconceptions</b></label>
<panel><div>

<div class="color-header abstract-machine">

Things people may incorrectly assume they _should get away with_ if Rust targeted CPU directly, and _more correct_ counterparts:

{{ tablesep() }}

| Without AM | With AM |
|---------|-------------|
| `0xffff_ffff` would make a valid `char`. {{ bad() }} | Memory more than just bits.  |
| `0xff` and `0xff` are same pointer. {{ bad() }} | Pointers can come from different _domains_.  |
| Any r/w pointer on `0xff` always fine. {{ bad() }} | Read and write reference may not exist same time.  |
| Null reference is just `0x0` in some register. {{ bad() }} | Holding `0x0` in reference summons Cthulhu.  |

</div>
</div></panel></tab>


</tabs>

<!--  -->
<!-- > Practically this means: -->
<!-- > - before assuming your **CPU** will do `A` when writing `B` you need positive proof **via documentation**(!), -->
<!-- > - if you don't have that any physical behavior is _coincidental_, -->
<!-- > - violate the abtract machine's contract and the optimizer makes your CPU do something **entirely else** &mdash; **undefined behavior**.{{ below(target="#unsafe-unsound-undefined")}} -->
<!--  -->


## 语法糖 {#language-sugar}

如果有什么东西让你觉得，“不该能用的啊”，那可能就是这里的原因。


<div class="color-header language-sugar">


| 名称 | 说明 |
|--------| -----------|
| **Coercions** {{ nom(page="coercions.html") }} | _Weakens_ types to match signature, e.g., `&mut T` to `&T`; _c_. _type conversions_. {{ below(target="#type-conversions") }}  |
| **Deref** {{ nom(page="vec-deref.html") }} {{ link(url="https://stackoverflow.com/questions/28519997/what-are-rusts-exact-auto-dereferencing-rules") }} | [Derefs](https://doc.rust-lang.org/std/ops/trait.Deref.html) `x: T` until `*x`, `**x`, &hellip; compatible with some target `S`. |
| **Prelude** {{ std(page="std/prelude/index.html") }} | Automatic import of basic items, e.g., `Option`, `drop`, ...
| **重新借用** | 即便 `x: &mut T` 不能复制，也可以移动一个新的 `&mut *x` 代替。 |
| **Lifetime Elision** {{ book(page="ch10-03-lifetime-syntax.html#lifetime-elision") }} {{ nom(page="lifetime-elision.html#lifetime-elision") }} {{ ref(page="lifetime-elision.html#lifetime-elision") }} | Automatically annotates `f(x: &T)` to `f<'a>(x: &'a T)`.|
| **Method Resolution** {{ ref(page="expressions/method-call-expr.html") }} | Derefs or borrow `x` until `x.f()` works. |
| **Match Ergonomics** {{ rfc(page="2005-match-ergonomics.html") }} | Repeatedly dereferences [scrutinee](https://doc.rust-lang.org/stable/reference/glossary.html#scrutinee) and adds `ref` and `ref mut` to bindings. |
| **Rvalue Static Promotion** {{ rfc(page="1414-rvalue_static_promotion.html") }} | Makes references to constants `'static`, e.g., `&42`, `&None`, `&mut []`. |


</div>

{{ tablesep() }}

> **Opinion** {{ opinionated() }} &mdash; The features above will make your life easier, but might hinder your understanding. If any (type-related) operation ever feels _inconsistent_ it might be worth revisiting this list.


## Memory & Lifetimes


Why moves, references and lifetimes are how they are.


<tabs class="lifetimes">

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-lt-1" name="tab-lt" checked>
<label for="tab-lt-1"><b>Types & Moves</b></label>
<panel>
<div>


<lifetime-section>
<lifetime-example>
    <section-header>Application Memory</section-header>
    <memory-row>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 57px;">S(1)</value>
        </values>
        <labels>
            <label class="" style="right: 10px;">&nbsp;</label>
        </labels>
        <subtext>Application Memory</subtext>
    </memory-row>
</lifetime-example>
<explanation>

- Application memory is just array of bytes on low level.
- Operating environment usually segments that, amongst others, into:
    - **stack** (small, low-overhead memory,<sup>1</sup> most _variables_ go here),
    - **heap** (large, flexible memory, but always handled via stack proxy like `Box<T>`),
    - **static** (most commonly used as resting place for `str` part of `&str`),
    - **code** (where bitcode of your functions reside).
- Most tricky part is tied to **how stack evolves**, which is **our focus**.

<footnotes>

<sup>1</sup> For fixed-size values stack is trivially managable: _take a few bytes more while you need them, discarded once you leave_. However, giving out pointers to these _transient_ locations form the very essence of why _lifetimes_ exist; and are the subject of the rest of this chapter.

</footnotes>

</explanation>
</lifetime-section>



<lifetime-section>
<lifetime-example class="not-first">
    <section-header>Variables</section-header>
    <memory-row>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 57px;">S(1)</value>
            <value class="t byte2" style="left: 97.5px;">S(1)</value>
        </values>
        <labels>
            <label class="byte2 hide" style="left: 57px;"><code>a</code></label>
            <label class="byte2" style="left: 97.5px;"><code>t</code></label>
        </labels>
        <subtext>Variables</subtext>
        <!-- <subtext><code>let t = S(1);</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
let t = S(1);
```

- Reserves memory location with name `t` of type `S` and the value `S(1)` stored inside.
- If declared with `let` that location lives on stack. <sup>1</sup>
- Note the **linguistic ambiguity**,<sup>2</sup> in the term **_variable_**, it can mean the:
    1. **name** of the location in the source file ("rename that variable"),
    1. **location** in a compiled app, `0x7` ("tell me the address of that variable"),
    1. **value** contained within, `S(1)` ("increment that variable").
- Specifically towards the compiler `t` can mean **location of** `t`, here `0x7`, and **value within** `t`, here `S(1)`.

<footnotes>

<sup>1</sup> Compare above,{{ above(target="#data-structures" ) }} true for fully synchronous code, but `async` stack frame might placed it on heap via runtime.

</footnotes>


</explanation>
</lifetime-section>


<lifetime-section>
<lifetime-example class="not-first">
    <section-header>Move Semantics</section-header>
    <memory-row>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 57px;">S(1)</value>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code>a</code></label>
            <label class="byte2" style="left: 97.5px;"><code>t</code></label>
        </labels>
        <subtext>Moves</subtext>
        <!-- <subtext><code>let a = t;</code></subtext> -->
    </memory-row>
</lifetime-example>

<explanation>

```
let a = t;
```

- This will **move** value within `t` to location of `a`, or copy it, if `S` is `Copy`.
- After move location `t` is **invalid** and cannot be read anymore.
    - Technically the bits at that location are not really _empty_, but _undefined_.
    - If you still had access to `t` (via `unsafe`) they might still _look_ like valid `S`, but
    any attempt to use them as valid `S` is undefined behavior. {{ below(target="#unsafe-unsound-undefined") }}
- We do not cover `Copy` types explicitly here. They change the rules a bit, but not much:
    - They won't be dropped.
    - They never leave behind an 'empty' variable location.

</explanation>
</lifetime-section>



<lifetime-section>
<lifetime-example class="not-first">
    <section-header>Type Safety</section-header>
    <memory-row>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <failed style="left: 231.5px;"><value class="atomic byte4">M { ... }</value></failed>
            <denied style="left: 141px;">⛔</denied>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code></code></label>
            <label class="byte2" style="left: 170px;"><code>c</code></label>
        </labels>
        <subtext>Type Safety</subtext>
        <!-- <subtext><code>let c: S = M::new();</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>


```
let c: S = M::new();
```

- The **type of a variable** serves multiple important purposes, it:
    1. dictates how the underlying bits are to be interpreted,
    1. allows only well-defined operations on these bits
    1. prevents random other values or bits from being written to that location.
- Here assignment fails to compile since the bytes of `M::new()` cannot be converted to form of type `S`.
- **Conversions between types will _always_ fail** in general, **unless explicit rule allows it** (coercion, cast, &hellip;).

</explanation>
</lifetime-section>


<lifetime-section>
<lifetime-example class="not-first">
    <section-header>Scope & Drop</section-header>
    <memory-row>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <drop><value class="t byte2" style="left: 57px;">S(1)</value><droparrow style="left:37px;">▼</droparrow></drop>
            <value class="t byte2 hide" style="left: 87.5px;">C(2)</value>
            <drop><value class="t byte2" style="left: 128px;">S(2)</value><droparrow style="left:107px;">▼</droparrow></drop>
            <failed style="left: -27.5px;"><value class="t byte2" style="left: 128px;">S(3)</value></failed>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code></code></label>
            <label class="byte2" style="left: 97.5px;"><code>t</code></label>
            <!-- <label class="byte2" style="left: 136.5px;"><code>c</code></label> -->
        </labels>
        <subtext>Scope & Drop</subtext>
        <!-- <subtext><code>{ let a = ...; }</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
{
    let mut c = S(2);
    c = S(3);  // <- Drop called on `c` before assignment.
    let t = S(1);
    let a = t;
}   // <- Scope of `a`, `t`, `c` ends here, drop called on `a`, `c`.
```

- Once the 'name' of a non-vacated variable goes out of (drop-)**scope**, the contained value is **dropped**.
    - Rule of thumb: execution reaches point where name of variable leaves `{}`-block it was defined in
    - In detail more tricky, esp. temporaries, &hellip;
- Drop also invoked when new value assigned to existing variable location.
- In that case **`Drop::drop()`** is called on the location of that value.
    - In the example above `drop()` is called on `a`, twice on `c`, but not on `t`.
- Most non-`Copy` values get dropped most of the time; exceptions include `mem::forget()`, `Rc` cycles, `abort()`.

</explanation>
</lifetime-section>


</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-lt-2" name="tab-lt">
<label for="tab-lt-2"><b>Call Stack</b></label>
<panel><div>

<lifetime-section>
<lifetime-example>
    <section-header>Stack Frame</section-header>
    <memory-row>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 57px;">S(1)</value>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code>a</code></label>
            <label class="byte2" style="left: 97.5px;"><code>x</code></label>
        </labels>
        <subtext>Function Boundaries</subtext>
        <!-- <subtext><code>fn f(x: S) {}</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
fn f(x: S) { ... }

let a = S(1); // <- We are here
f(a);
```

- When a **function is called**, memory for parameters (and return values) are reserved on stack.<sup>1</sup>
- Here before `f` is invoked value in `a` is moved to 'agreed upon' location on stack, and during `f` works like 'local variable' `x`.

<footnotes>

<sup>1</sup> Actual location depends on calling convention, might practically not end up on stack at all, but that doesn't change mental model.

</footnotes>

</explanation>
</lifetime-section>


<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 131px;">S(1)</value>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code>a</code></label>
            <label class="byte2" style="left: 97.5px;"><code>x</code></label>
            <label class="byte2" style="left: 136px;"><code>x</code></label>
        </labels>
        <subtext>Nested Functions</subtext>
        <!-- <subtext><code>fn f(x: S) { ... f(x) ... }</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
fn f(x: S) {
    if once() { f(x) } // <- We are here (before recursion)
}

let a = S(1);
f(a);
```

- **Recursively calling** functions, or calling other functions, likewise extends the stack frame.
- Nesting too many invocations (esp. via unbounded recursion) will cause stack to grow, and eventually to overflow, terminating the app.

</explanation>
</lifetime-section>


<lifetime-section>

<lifetime-example class="not-first">
    <section-header>Validity of Variables</section-header>
    <memory-row>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t" style="opacity: 0.4;"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 131px;">S(1)</value>
            <value class="atomic byte4" style="left: 190px;">M { }</value>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code>a</code></label>
            <label class="byte2" style="left: 97.5px;"><code>x</code></label>
            <label class="byte2" style="left: 174px;"><code>m</code></label>
        </labels>
        <subtext>Repurposing Memory</subtext>
        <!-- <subtext><code>f(x); let m = M::new();</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
fn f(x: S) {
    if once() { f(x) }
    let m = M::new() // <- We are here (after recursion)
}

let a = S(1);
f(a);
```

- Stack that previously held a certain type will be repurposed across (even within) functions.
- Here, recursing on `f` produced second `x`, which after recursion was partially reused for `m`.

> Key take away so far, there are multiple ways how memory locations that previously held a valid value of a certain type stopped doing so in the meantime.
> As we will see shortly, this has implications for pointers.

</explanation>
</lifetime-section>

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-lt-3" name="tab-lt">
<label for="tab-lt-3"><b>References & Pointers</b></label>
<panel><div>

<lifetime-section>
<lifetime-example>
    <section-header class="arrowed">Reference Types</section-header>
    <memory-row>
        <arrows>
            <arrow style="left: 62px; width: 176px;">&nbsp;<tip>▼</tip></arrow>
        </arrows>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 57px;">S(1)</value>
            <value class="ptr byte4" style="left: 171px;">0x3</value>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code>a</code></label>
            <label class="byte4" style="left: 171px;"><code>r</code></label>
        </labels>
        <subtext>References as Pointers</subtext>
        <!-- <subtext><code>let r = &mut a;</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
let a = S(1);
let r: &S = &a;
```

- A **reference type** such as `&S` or `&mut S` can hold the **location of** some `s`.
- Here type `&S`, bound as name `r`, holds _location of_ variable `a` (`0x3`), that must be type `S`, obtained via `&a`.
- If you think of variable `c` as _specific location_, reference **`r` is a _switchboard for locations_**.
- The type of the reference, like all other types, can often be inferred, so we might omit it from now on:
    ```
    let r: &S = &a;
    let r = &a;
    ```
<!-- - References on their own are **never** concerned with the _value within_ the location they point to. -->

</explanation>
</lifetime-section>


<lifetime-section>
<lifetime-example class="not-first">
    <section-header class="arrowed">(Mutable) References</section-header>
    <memory-row>
        <arrows>
            <arrow style="left: 62px; width: 176px;">&nbsp;<tip>▼</tip></arrow>
        </arrows>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 57px;">S(2)</value>
            <value class="ptr byte4" style="left: 171px;">0x3</value>
            <value class="t byte2" style="left: 213px;">S(1)</value>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code>a</code></label>
            <label class="byte4" style="left: 171px;"><code>r</code></label>
            <label class="byte4" style="left: 193px;"><code>d</code></label>
        </labels>
        <subtext>Access to Non-Owned Memory</subtext>
        <!-- <subtext><code>let d = r.clone(); *r = S(2);</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
let mut a = S(1);
let r = &mut a;
let d = r.clone();  // Valid to clone (or copy) from r-target.
*r = S(2);          // Valid to set new S value to r-target.
```


- References can **read from**  (`&S`) and also **write to** (`&mut S`) location they point to.
- The *dereference* `*r` means to neither use the _location of_ or _value within_ `r`, but the **location `r` points to**.
- In example above, clone `d` is created from `*r`, and `S(2)` written to `*r`.
    - Method `Clone::clone(&T)` expects a reference itself, which is why we can use `r`, not `*r`.
    - On assignment `*r = ...` old value in location also dropped (not shown above).

</explanation>
</lifetime-section>


<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <arrows>
            <arrow style="left: 62px; width: 176px;">&nbsp;<tip>▼</tip></arrow>
        </arrows>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 57px;">S(2)</value>
            <value class="ptr byte4" style="left: 171px;">0x3</value>
            <value class="atomic byte4" style="top:-36px; left: 20px;">M { x }</value>
            <denied style="left: -71px; top:-36px;">⛔</denied>
            <denied style="left: -131px;">⛔</denied>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code>a</code></label>
            <label class="byte4" style="left: 171px;"><code>r</code></label>
            <label class="byte4" style="left: 193px;"><code>d</code></label>
        </labels>
        <subtext>References Guard Referents</subtext>
        <!-- <subtext><code>let d = *r; *r = M::new();</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
let mut a = ...;
let r = &mut a;
let d = *r;       // Invalid to move out value, `a` would be empty.
*r = M::new();    // invalid to store non S value, doesn't make sense.
```

- While bindings guarantee to always _hold_ valid data, references guarantee to always _point to_ valid data.
- Esp. `&mut T` must provide same guarantees as variables, and some more as they can't dissolve the target:
    - They do **not allow writing invalid** data.
    - They do **not allow moving out** data (would leave target empty w/o owner knowing).

</explanation>
</lifetime-section>




<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <arrows>
            <arrow style="left: 62px; width: 176px; border-color: red;">&nbsp;<tip style="color: red">▼</tip></arrow>
        </arrows>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 57px;">C(2)</value>
            <value class="ptr byte4 unsafe" style="left: 171px;">0x3</value>
        </values>
        <labels>
            <label class="byte2 hide" style="left: 57px;"><code>c</code></label>
            <label class="byte4" style="left: 171px;"><code>p</code></label>
        </labels>
        <subtext>Raw Pointers</subtext>
        <!-- <subtext><code>let p: *const S = ...;</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
let p: *const S = questionable_origin();
```

- In contrast to references, pointers come with almost no guarantees.
- They may point to invalid or non-existent data.
- Dereferencing them is `unsafe`, and treating an invalid `*p` as if it were valid is undefined behavior. {{ below(target="#unsafe-unsound-undefined") }}

</explanation>
</lifetime-section>

</div></panel></tab>




<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-lt-10" name="tab-lt">
<label for="tab-lt-10"><b>Lifetime Basics</b></label>
<panel><div>


<lifetime-section>
<lifetime-example>
    <memory-row>
        <memory-backdrop class="past" style="padding-left: 7px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop class="past" style="padding-left: 3px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 57px;">C(2)</value>
            <value class="ptr byte4 hide" style="left: 171px;">0x3</value>
        </values>
        <labels>
            <!-- <label class="byte2" style="left: 37px;"><code>'a</code></label>
            <label class="byte4" style="left: 59px;"><code>'b: 'c</code></label>
            <label class="byte2" style="left: 81px;"><code>'c</code></label>
            <label class="byte4" style="left: 139px;"><code>'d</code></label> -->
        </labels>
        <subtext>"Lifetime" of Things</subtext>
        <!-- <subtext><code>f(); g(); h();</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

- Every entity in a program has some (temporal / spatial) room where it is relevant, i.e., _alive_.
- Loosely speaking, this _alive time_ can be<sup>1</sup>
    1. the **LOC** (lines of code) where an **item is available** (e.g., a module name).
    1. the **LOC** between when a _location_ is **initialized** with a value, and when the location is **abandoned**.
    1. the **LOC** between when a location is first **used in a certain way**, and when that **usage stops**.
    1. the **LOC (or actual time)** between when a _value_ is created, and when that value is dropped.
- Within the rest of this section, we will refer to the items above as the:
    1. **scope** of that item, irrelevant here.
    1. **scope** of that variable or location.
    1. **lifetime**<sup>2</sup> of that usage.
    1. **lifetime** of that value, might be useful when discussing open file descriptors, but also irrelevant here.
- Likewise, lifetime parameters in code, e.g., `r: &'a S`, are
    - concerned with LOC any **location r _points to_** needs to be accessible or locked;
    - unrelated to the 'existence time' (as LOC) of `r` itself (well, it needs to exist shorter, that's it).
- `&'static S` means address must be _valid during all lines of code_.

> <sup>1</sup> There is sometimes ambiguity in the docs differentiating the various _scopes_ and _lifetimes_.
> We try to be pragmatic here, but suggestions are welcome.
>
> <sup>2</sup> _Live lines_ might have been a more appropriate term ...

</explanation>
</lifetime-section>




<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <memory-backdrop class="past" style="padding-left: 7px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop class="past" style="padding-left: 3px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <arrows>
            <arrow style="left: 192px; width: 120px;">&nbsp;<tip>▼</tip></arrow>
        </arrows>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 38px;">S(0)</value>
            <value class="t byte2 hide" style="left: 79px;">S(1)</value>
            <value class="t byte2" style="left: 119px;">S(2)</value>
            <value class="ptr byte4" style="left: 177px;">0xa</value>
        </values>
        <labels>
            <label class="byte2 hide" style="left: 37px;"><code>a</code></label>
            <label class="byte2 hide" style="left: 78px;"><code>b</code></label>
            <label class="byte2" style="left: 118px;"><code>c</code></label>
            <label class="byte4" style="left: 177px;"><code>r</code></label>
        </labels>
        <subtext>Meaning of <code>r: &'c S</code></subtext>
        <!-- <subtext><code>r: &mut 'c S</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

- Assume you got a `r: &'c S` from somewhere it means:
    - `r` holds an address of some `S`,
    - any address `r` points to must and will exist for at least `'c`,
    - the variable `r` itself cannot live longer than `'c`.



</explanation>
</lifetime-section>



<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <memory-backdrop class="past" style="padding-left: 7px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop class="past" style="padding-left: 3px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <arrows>
            <arrow style="left: 118px; width: 193px;">&nbsp;<tip>▼</tip></arrow>
        </arrows>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 38px;">S(0)</value>
            <value class="t byte2" style="left: 79px;">S(3)</value>
            <value class="t byte2" style="left: 119px;">S(2)</value>
            <value class="ptr byte4" style="left: 177px;">0x6</value>
            <denied style="left: -125px; top:-25px;">⛔</denied>
        </values>
        <labels>
            <label class="byte2" style="left: 37px;"><code>a</code></label>
            <label class="byte2" style="left: 78px;"><code>b</code></label>
            <label class="byte2" style="left: 118px;"><code>c</code></label>
            <label class="byte4" style="left: 177px;"><code>r</code></label>
        </labels>
        <subtext>Typelikeness of Lifetimes</subtext>
        <!-- <subtext><code>r = &mut b;</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
{
    let b = S(3);
    {
        let c = S(2);
        let r: &'c S = &c;      // Does not quite work since we can't name lifetimes of local
        {                       // variables in a function body, but very same principle applies
            let a = S(0);       // to functions next page.

            r = &a;             // Location of `a` does not live sufficient many lines -> not ok.
            r = &b;             // Location of `b` lives all lines of `c` and more -> ok.
        }
    }
}
```

- Assume you got a `mut r: &mut 'c S` from somewhere.
    - That is, a mutable location that can hold a mutable reference.
- As mentioned, that reference must guard the targeted memory.
- However, the **`'c` part**, like a type, also **guards what is allowed into `r`**.
- Here assiging `&b` (`0x6`) to `r` is valid, but `&a` (`0x3`) would not, as only `&b` lives equal or longer than `&c`.

</explanation>
</lifetime-section>




<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <memory-backdrop class="past" style="padding-left: 7px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop class="past" style="padding-left: 3px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <arrows>
            <arrow style="left: 118px; width: 193px;">&nbsp;<tip>▼</tip></arrow>
        </arrows>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t borrowed"></byte>
            <byte class="t borrowed"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 38px;">S(0)</value>
            <value class="t byte2" style="left: 79px;">&nbsp;</value>
            <value class="t byte2 hide" style="left: 119px;">S(2)</value>
            <value class="ptr byte4" style="left: 177px;">0x6</value>
            <failed style="left: -40px;"><value class="t bytes">S(4)</value></failed>
            <denied style="left: -83px;">⛔</denied>
        </values>
        <labels>
            <label class="byte2 hide" style="left: 37px;"><code>a</code></label>
            <label class="byte2" style="left: 78px;"><code>b</code></label>
            <label class="byte2 hide" style="left: 118px;"><code>c</code></label>
            <label class="byte4 hide" style="left: 177px;"><code></code></label>
        </labels>
        <subtext>Borrowed State</subtext>
    </memory-row>
</lifetime-example>
<explanation>

```
let mut b = S(0);
let r = &mut b;

b = S(4);   // Will fail since `b` in borrowed state.

print_byte(r);
```

- Once the address of a variable is taken via `&b` or `&mut b` the variable is marked as **borrowed**.
- While borrowed, the content of the address cannot be modified anymore via original binding `b`.
- Once address taken via `&b` or `&mut b` stops being used (in terms of LOC) original binding `b` works again.


</explanation>
</lifetime-section>

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-lt-11" name="tab-lt">
<label for="tab-lt-11"><b>Lifetimes in Functions</b></label>
<panel>
<div>


<lifetime-section>
<lifetime-example>
    <memory-row>
        <memory-backdrop class="past" style="padding-left: 7px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop class="past" style="padding-left: 3px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t borrowed"></byte>
            <byte class="t borrowed"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t borrowed"></byte>
            <byte class="t borrowed"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 38px;">S(0)</value>
            <value class="t byte2" style="left: 79px;">S(1)</value>
            <value class="t byte2" style="left: 119px;">S(2)</value>
            <value class="ptr byte4" style="left: 177px;">?</value>
            <value class="ptr byte4" style="left: 201px;">0x6</value>
            <value class="ptr byte4" style="left: 224px;">0xa</value>
        </values>
        <labels>
            <label class="byte2 hide" style="left: 37px;"><code>a</code></label>
            <label class="byte4" style="left: 59px;"><code>b</code></label>
            <label class="byte2" style="left: 81px;"><code>c</code></label>
            <label class="byte4" style="left: 139px;"><code>r</code></label>
            <label class="byte4" style="left: 165px;"><code>x</code></label>
            <label class="byte4" style="left: 188px;"><code>y</code></label>
        </labels>
        <subtext>Function Parameters</subtext>
        <!-- <subtext><code>let r = f(&b, &c);</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
fn f(x: &S, y:&S) -> &u8 { ... }

let b = S(1);
let c = S(2);

let r = f(&b, &c);
```

- When calling functions that take and return references two interesting things happen:
    - The used local variables are placed in a borrowed state,
    - But it is during compilation unknown which address will be returned.



</explanation>
</lifetime-section>




<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <memory-backdrop class="past" style="padding-left: 7px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop class="past" style="padding-left: 3px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t maybe-borrowed"></byte>
            <byte class="t maybe-borrowed"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t maybe-borrowed"></byte>
            <byte class="t maybe-borrowed"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 38px;">S(0)</value>
            <value class="t byte2" style="left: 79px;">S(1)</value>
            <value class="t byte2" style="left: 119px;">S(2)</value>
            <value class="ptr byte4" style="left: 177px;">?</value>
            <value class="ptr byte4 hide" style="left: 201px;">0x6</value>
            <value class="ptr byte4 hide" style="left: 224px;">0xa</value>
        </values>
        <labels>
            <label class="byte2" style="left: 37px;"><code>a</code></label>
            <label class="byte4" style="left: 59px;"><code>b</code></label>
            <label class="byte2" style="left: 81px;"><code>c</code></label>
            <label class="byte4" style="left: 139px;"><code>r</code></label>
            <label class="byte4 hide" style="left: 165px;"><code>x</code></label>
            <label class="byte4 hide" style="left: 188px;"><code>y</code></label>
        </labels>
        <subtext>Problem of 'Borrowed' Propagation</subtext>
        <!-- <subtext><code>let a = b;</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
let b = S(1);
let c = S(2);

let r = f(&b, &c);

let a = b;   // Are we allowed to do this?
let a = c;   // Which one is _really_ borrowed?

print_byte(r);
```

- Since `f` can return only one address, not in all cases `b` and `c` need to stay locked.
- In many cases we can get quality-of-life improvements.
    - Notably, when we know one parameter _couldn't_ have been used in return value anymore.


</explanation>
</lifetime-section>



<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <memory-backdrop class="past" style="padding-left: 7px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop class="past" style="padding-left: 3px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <arrows>
            <arrow style="left: 210px; width: 102px;">&nbsp;<tip>▼</tip></arrow>
        </arrows>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t borrowed"></byte>
            <byte class="t borrowed"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 38px;">S(1)</value>
            <value class="t byte2 hide" style="left: 79px;">S(1)</value>
            <value class="t byte2" style="left: 119px;">S(2)</value>
            <value class="ptr byte4" style="left: 177px;">y + _</value>
            <value class="ptr byte4 hide" style="left: 201px;">0x6</value>
            <value class="ptr byte4 hide" style="left: 224px;">0xa</value>
        </values>
        <labels>
            <label class="byte2" style="left: 37px;"><code>a</code></label>
            <label class="byte4" style="left: 59px;"><code>b</code></label>
            <label class="byte2" style="left: 81px;"><code>c</code></label>
            <label class="byte4" style="left: 139px;"><code>r</code></label>
            <label class="byte4 hide" style="left: 165px;"><code>x</code></label>
            <label class="byte4 hide" style="left: 188px;"><code>y</code></label>
        </labels>
        <subtext>Lifetimes Propagate Borrowed State</subtext>
        <!-- <subtext><code>f(x: &'x S, y: &'y S) -> &'y u8</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
fn f<'b, 'c>(x: &'b S, y: &'c S) -> &'c u8 { ... }

let b = S(1);
let c = S(2);

let r = f(&b, &c); // We know returned reference is `c`-based, which must stay locked,
                   // while `b` is free to move.

let a = b;

print_byte(r);
```

- Lifetime parameters in signatures, like `'c` above, solve that problem.
- Their primary purpose is:
    - **outside the function**, to explain based on which input address an output address could be generated,
    - **within the function**, to guarantee only addresses that live at least `'c` are assigned.
- The actual lifetimes `'b`, `'c` are transparently picked by the compiler at **call site**, based on the borrowed variables the developer gave.
- They are **not** equal to the _scope_ (which would be LOC from initialization to destruction) of `b` or `c`, but only a minimal subset of their scope called _lifetime_, that is, a minmal set of LOC based on how long `b` and `c` need to be borrowed to perform this call and use the obtained result.
- In some cases, like if `f` had `'c: 'b` instead, we still couldn't distinguish and both needed to stay locked.

</explanation>
</lifetime-section>




<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <memory-backdrop class="past" style="padding-left: 7px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop class="past" style="padding-left: 3px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 38px;">S(2)</value>
            <value class="t byte2 hide" style="left: 79px;">S(1)</value>
            <value class="t byte2 hide" style="left: 119px;">S(2)</value>
            <value class="ptr byte4 hide" style="left: 177px;">y + 1</value>
            <value class="ptr byte4 hide" style="left: 201px;">0x6</value>
            <value class="ptr byte4 hide" style="left: 224px;">0xa</value>
        </values>
        <labels>
            <label class="byte2" style="left: 37px;"><code>a</code></label>
            <label class="byte4 hide" style="left: 59px;"><code>b</code></label>
            <label class="byte2" style="left: 81px;"><code>c</code></label>
            <label class="byte4 hide" style="left: 139px;"><code>r</code></label>
            <label class="byte4 hide" style="left: 165px;"><code>x</code></label>
            <label class="byte4 hide" style="left: 188px;"><code>y</code></label>
        </labels>
        <!-- <subtext><code>{ let r = ... }</code></subtext> -->
        <subtext>Unlocking</subtext>
    </memory-row>
</lifetime-example>
<explanation>

```
let mut c = S(2);

let r = f(&c);
let s = r;
                    // <- Not here, `s` prolongs locking of `c`.

print_byte(s);

let a = c;          // <- But here, no more use of `r` or `s`.


```
- A variable location is _unlocked_ again once the last use of any reference that may point to it ends.

</explanation>
</lifetime-section>

</div></panel></tab>
</tabs>


<footnotes>

↕️ Examples expand by clicking.

</footnotes>



{{ tablesep() }}


</magic>


---


# 数据类型

通用数据类型的内存表示。


## 基本类型 {#basic-types}

语言核心内建的必要类型。


#### 数字类型 {{ ref(page="types/numeric.html") }}

<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>u8</code>, <code>i8</code></name>
    <visual class="bytes">
        <byte><code></code></byte>
    </visual>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced" >
    <name><code>u16</code>, <code>i16</code></name>
    <visual class="bytes">
        <byte><code></code></byte>
        <byte><code></code></byte>
    </visual>
</datum>


<!-- NEW ENTRY -->
<datum  class="spaced">
    <name><code>u32</code>, <code>i32</code></name>
    <visual class="bytes">
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
    </visual>
</datum>


<!-- NEW ENTRY -->
<datum  class="spaced">
    <name><code>u64</code>, <code>i64</code></name>
    <visual class="bytes">
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
    </visual>
</datum>


<!-- NEW ENTRY -->
<datum  class="spaced">
    <name><code>u128</code>, <code>i128</code></name>
    <visual class="bytes">
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
    </visual>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>f32</code></name>
    <visual class="float">
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
    </visual>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>f64</code></name>
    <visual class="float">
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
    </visual>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>usize</code>, <code>isize</code></name>
    <visual class="sized">
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte style="border-color: #888;"><code></code></byte>
        <byte style="border-color: #888;"><code></code></byte>
        <byte style="border-color: #aaa;"><code></code></byte>
        <byte style="border-color: #aaa;"><code></code></byte>
        <byte style="border-color: #aaa;"><code></code></byte>
        <byte style="border-color: #aaa;"><code></code></byte>
    </visual>
    <zoom>
        与平台的 <code>ptr</code> 一致
    </zoom>
</datum>



<br/>


{{ tablesep() }}


<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-numeric-1" name="tab-group-numeric" checked>
<label for="tab-numeric-1"><b>无符号类型</b></label>
<panel><div>



|类型|最大值|
|---|---|
|`u8`| `255` |
|`u16` | `65_535` |
|`u32`| `4_294_967_295` |
|`u64`| `18_446_744_073_709_551_615` |
|`u128`| `340_282_366_920_938_463_463_374_607_431_768_211_455` |
|`usize`| Depending on platform pointer size, same as `u16`, `u32`, or `u64`. |


</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-numeric-3" name="tab-group-numeric">
<label for="tab-numeric-3"><b>Signed Types</b></label>
<panel><div>



|类型|最大值|
|---|---|
|`i8`| `127` |
|`i16` | `32_767` |
|`i32`| `2_147_483_647` |
|`i64`| `9_223_372_036_854_775_807` |
|`i128`| `170_141_183_460_469_231_731_687_303_715_884_105_727` |
|`isize`| Depending on platform pointer size, same as `i16`, `i32`, or `i64`. |

{{ tablesep() }}

|类型|最小值|
|---|---|
|`i8`| `-128` |
|`i16` | `-32_768` |
|`i32`| `-2_147_483_648` |
|`i64`| `-9_223_372_036_854_775_808` |
|`i128`| `-170_141_183_460_469_231_731_687_303_715_884_105_728` |
|`isize`| Depending on platform pointer size, same as `i16`, `i32`, or `i64`. |


</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-numeric-2" name="tab-group-numeric">
<label for="tab-numeric-2"><b>浮点类型</b>{{ esoteric() }}</label>
<panel><div>


`f32` 的位表示<sup>*</sup>：

<!-- NEW ENTRY -->
<datum style="opacity:0.7; margin-bottom:10px;">
    <visual class="float">
    <bitgroup>
        <bit><code>S</code></bit>
    </bitgroup>
    <bitgroup>
        <bit><code>E</code></bit>
        <bit><code>E</code></bit>
        <bit><code>E</code></bit>
        <bit><code>E</code></bit>
        <bit><code>E</code></bit>
        <bit><code>E</code></bit>
        <bit><code>E</code></bit>
        <bit><code>E</code></bit>
    </bitgroup>
    <bitgroup>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
    </bitgroup>
    </visual>
</datum>

{{ tablesep() }}

说明：

| f32 | S (1) | E (8) | F (23) | 值 |
|------| ---------| ---------| ---------| ---------|
| 规格化数 | ± | 1 to 254 | 任意 | ±(1.F)<sub>2</sub> * 2<sup>E-127</sup>  |
| 非规格化数 | ± | 0 | 非零 | ±(0.F)<sub>2</sub> * 2<sup>-126</sup>  |
| 零 | ± | 0 | 0 | ±0  |
| 无穷大 | ± | 255 | 0 | ±∞  |
| NaN | ± | 255 | 非零 | NaN  |

{{ tablesep() }}

类似地，<code>f64</code> 如下：

| f64 | S (1) | E (11) | F (52) | 值 |
|------| ---------| ---------| ---------| ---------|
| 规格化数 | ± | 1 to 2046 | 任意 | ±(1.F)<sub>2</sub> * 2<sup>E-1023</sup>  |
| 非规格化数 | ± | 0 | 非零 | ±(0.F)<sub>2</sub> * 2<sup>-1022</sup>  |
| 零 | ± | 0 | 0 | ±0  |
| 无穷大 | ± | 2047 | 0 | ±∞  |
| NaN | ± | 2047 | 非零 | NaN  |


<footnotes>
    <sup>*</sup> 浮点类型遵循 <a href="https://en.wikipedia.org/wiki/IEEE_754-2008_revision">IEEE 754-2008</a> 规范，并取决于平台大小端序。
</footnotes>

</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-numeric-4" name="tab-group-numeric">
<label for="tab-numeric-4"><b>Casting Pitfalls</b> {{ bad() }}</label>
<panel><div class="">


| Cast<sup>1</sup> | Gives | Note |
| --- | --- | --- |
| `3.9_f32 as u8` | `3` | Truncates, consider `x.round()` first. |
| `314_f32 as u8` | `255` | Takes closest available number. |
| `f32::INFINITY as u8` | `255` | Same, treats `INFINITY` as _really_ large number.|
| `f32::NAN as u8` | `0` | - |
| `_314 as u8` | `58` | Truncates excess bits. |
| `_200 as i8` | `56` | - |
| `_257 as i8` | `-1` | - |

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-numeric-5" name="tab-group-numeric">
<label for="tab-numeric-5"><b>Arithmetical Pitfalls</b> {{ bad() }}</label>
<panel><div class="">

| Operation<sup>1</sup> | Gives | Note |
| --- | --- | --- |
| `200_u8 / 0_u8` | Compile error. | - |
| `200_u8 / _0` <sup>d</sup> | Panic. | Regular math may panic; here: division by zero. |
| `200_u8 / _0` <sup>r</sup> | Panic. | Same. |
| `200_u8 + 200_u8` |  Compile error. | - |
| `200_u8 + _200` <sup>d</sup> | Panic. | Consider `checked_`, `wrapping_`, ... instead. {{ std(page="std/primitive.isize.html#method.checked_add") }}|
| `200_u8 + _200` <sup>r</sup> | `144` | In release mode this will overflow. |
| `1_u8 / 2_u8` | `0` | Other integer division truncates. |
| `0.8_f32 + 0.1_f32` | `0.90000004` | - |
| `1.0_f32 / 0.0_f32` | `f32::INFINITY` | - |
| `0.0_f32 / 0.0_f32` | `f32::NAN` | - |
| `x < f32::NAN` | `false` | `NAN` comparisons always return false. |
| `x > f32::NAN` | `false` | - |
| `f32::NAN == f32::NAN` | `false` | - |

</div></panel></tab>


<!-- End tabs -->
</tabs>

<!-- End overflow prevention -->
</div></div>


<footnotes>

<sup>1</sup> Expression `_100` means anything that might contain the value `100`, e.g., `100_i32`, but is opaque to compiler.<br/>
<sup>d</sup> Debug build.<br/>
<sup>r</sup> Release build.<br/>

</footnotes>


{{ tablesep() }}



#### 文字类型 {{ ref(page="types/textual.html") }}


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>char</code></name>
    <visual class="char">
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
    </visual>
    <description>任意 UTF-8 标量</description>
</datum>



<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>str</code></name>
    <visual>
        <note>...</note>
        <byte class="bytes"><code>U</code></byte>
        <byte class="bytes"><code>T</code></byte>
        <byte class="bytes"><code>F</code></byte>
        <byte class="bytes"><code>-</code></byte>
        <byte class="bytes"><code>8</code></byte>
        <note>... 未指明条目</note>
    </visual>
    <description>很少单独见到，常用 <code>&str</code> 代替</description>
</datum>


{{ tablesep() }}

<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-textual-3" name="tab-group-textual" checked>
<label for="tab-textual-3"><b>Basics</b></label>
<panel><div>

| Type | Description |
|---------|-------------|
| `char` | Always 4 bytes and only holds a single Unicode **scalar value** {{ link(url="https://www.unicode.org/glossary/#unicode_scalar_value") }}. |
| `str` | An `u8`-array of unknown length guaranteed to hold **UTF-8 encoded code points**. |

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-textual-1" name="tab-group-textual">
<label for="tab-textual-1"><b>Usage</b></label>
<panel><div>



<!-- Notice how:

- `char` is always 4 bytes and only holds a single Unicode **scalar value** {{ link(url="https://www.unicode.org/glossary/#unicode_scalar_value") }}, thus possibly wasting space.
- `str` is a byte-array of unknown length guaranteed to hold **UTF-8 encoded code points** (but harder to index).
 -->

| Chars | Description |
|---------|-------------|
| `let c = 'a';` | Often a `char` (unicode scalar) can coincide with your intuition of _character_. |
| `let c = '❤';` | It can also hold many Unicode symbols. |
| `let c = '❤️';` | But not always. Given emoji is **two** `char` (see Encoding) and **can't** {{ bad() }} be held by `c`.<sup>1</sup> |
| `c = 0xffff_ffff;` | Also, chars are **not allowed** {{ bad() }} to hold arbitrary bit patterns. |

<footnotes>
    <sup>1</sup> Fun fact, due to the <a href="https://en.wikipedia.org/wiki/Zero-width_joiner">Zero-width joiner</a> (⨝) what the user <i>perceives as a character</i> can get even more unpredictable: 👨‍👩‍👧 is in fact 5 chars 👨⨝👩⨝👧, and rendering engines are free to either show them fused as one, or separately as three, depending on their abilities.
</footnotes>


{{ tablesep() }}

| Strings | Description |
|---------|-------------|
| `let s = "a";` | A `str` is usually never held directly, but as `&str`, like `s` here. |
| `let s = "❤❤️";` | It can hold arbitrary text, has variable length per _c._, and is hard to index. |


</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-textual-2" name="tab-group-textual">
<label for="tab-textual-2"><b>Encoding</b>{{ esoteric() }}</label>
<panel><div>


`let s = "I ❤ Rust"; ` <br>
`let t = "I ❤️ Rust";`

| Variant | Memory Representation<sup>2<sup> |
|---------|-------------|
| `s.as_bytes()` | `49` `20` <span class="force-code-color same-black"><b>`e2 9d a4`</b> </span> `20 52 75 73 74` <sup>3<sup> |
| `s.chars()`<sup>1<sup> | `49 00 00 00 20 00 00 00` <span class="force-code-color same-black"><b>`64 27 00 00` </b></span> `20 00 00 00 52 00 00 00 75 00 00 00 73 00` &hellip; |
| `t.as_bytes()` | `49` `20` <span class="force-code-color same-black"><b>`e2 9d a4`</b> </span> <span class="force-code-color same-red"><b>`ef b8 8f`</b></span> `20 52 75 73 74` <sup>4<sup> |
| `t.chars()`<sup>1<sup> | `49 00 00 00 20 00 00 00` <span class="force-code-color same-black"><b>`64 27 00 00`</b></span> <span class="force-code-color same-red"><b>`0f fe 01 00`</b></span> `20 00 00 00 52 00 00 00 75 00` &hellip; |

{{ tablesep() }}

<footnotes>
    <sup>1</sup> Result then collected into array and transmuted to bytes.<br>
    <sup>2</sup> Values given in hex, on x86.<br>
    <sup>3</sup> Notice how <code>❤</code>, having <a href="https://codepoints.net/U+2764">Unicode Code Point (U+2764)</a>, is represented as <span class="force-code-color same-black"><b>64 27 00 00</b></span> inside the <code>char</code>, but got <a href="https://en.wikipedia.org/wiki/UTF-8#Description">UTF-8 encoded to</a> <span class="force-code-color same-black"><b>e2 9d a4</b></span> in the <code>str</code>.<br>
    <sup>4</sup> Also observe how the emoji <a href="https://emojipedia.org/red-heart/">Red Heart <code>❤️</code></a>, is a combination of <code>❤</code> and the <a href="https://codepoints.net/U+FE0F">U+FE0F Variation Selector</a>, thus <code>t</code> has a higher char count than <code>s</code>.
</footnotes>

{{ tablesep() }}


<footnotes>

> <sup>💬</sup> For what seem to be browser bugs Safari and Edge render the hearts in Footnote 3 and 4 wrong, despite being able to differentiate them correctly in `s` and `t` above.

</footnotes>

</div></panel></tab>


<!-- End tabs -->
</tabs>


{{ tablesep() }}


## 自定义类型 {#custom-types}

用户定义的基本类型。它实际的<b>内存布局</b>{{ ref(page="type-layout.html") }}取决于<b>表示法</b>{{ ref(page="type-layout.html#representations") }}，还有对齐。


<!-- NEW ENTRY -->
<datum class="spaced">
    <name class="nogrow"><code>T</code></name>
    <name class="hidden">x</name>
    <visual>
       <framed class="any t"><code>T</code></framed>
    </visual>
    <description>Sized {{ below(target = "#sized-types") }} </description>
</datum>

<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>T: ?Sized</code></name>
    <visual>
       <framed class="any unsized"><code>T</code></framed>
    </visual>
    <description>Maybe DST {{ below(target = "#sized-types") }} </description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>[T; n]</code></name>
    <visual>
       <framed class="any t"><code>T</code></framed>
       <framed class="any t"><code>T</code></framed>
       <framed class="any t"><code>T</code></framed>
       <note>... n times</note>
    </visual>
    <description>Fixed array of <code>n</code> elements.</description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>[T]</code></name>
    <visual>
       <note>...</note>
       <framed class="any t"><code>T</code></framed>
       <framed class="any t"><code>T</code></framed>
       <framed class="any t"><code>T</code></framed>
       <note>... unspecified times</note>
    </visual>
    <description><b>Slice type</b> of unknown-many elements. Neither <br> <code>Sized</code> (nor carries <code>len</code> information), and most<br> often lives behind reference as <code>&[T]</code>. {{ below(target="#references-pointers-ui") }}</description>
</datum>

<!-- NEW ENTRY -->
<datum style="margin-right:70px;">
    <name class="nogrow"><code>struct S; </code></name>
    <name class="hidden"><code>;</code></name>
    <visual style="width: 15px;" class="zst">
        <code></code>
    </visual>
    <description>Zero-Sized {{ below(target = "#sized-types") }} </description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>(A, B, C)</code></name>
    <visual style="width: 182px;">
       <framed class="any"><code>A</code></framed>
       <framed class="any" style="width: 100px;"><code>B</code></framed>
       <framed class="any" style="width: 50px;"><code>C</code></framed>
    </visual>
    <andor>or maybe</andor>
    <visual style="width: 182px;">
       <framed class="any" style="width: 100px;"><code>B</code></framed>
       <framed class="any"><code>A</code></framed>
       <framed class="any" style="width: 50px;"><code>C</code></framed>
    </visual>
    <description>Unless a representation is forced <br>(e.g., via <code>#[repr(C)]</code>), type layout<br> unspecified.</description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>struct S { b: B, c: C } </code></name>
    <visual style="width: 166px;">
       <framed class="any" style="width: 100px;"><code>B</code></framed>
       <framed class="any" style="width: 50px;"><code>C</code></framed>
    </visual>
    <andor>or maybe</andor>
    <visual>
       <framed class="any" style="width: 50px;"><code>C</code></framed>
       <pad><code style="">↦</code></pad>
       <framed class="any" style="width: 100px;"><code>B</code></framed>
    </visual>
    <description>Compiler may also add padding.</description>
</datum>



<blockquote>
<footnotes>

Also note, two types `A(X, Y)` and `B(X, Y)` with exactly the same fields can still have differing layout; never `transmute()` without representation guarantees.

</footnotes>
</blockquote>



{{ tablesep() }}

这些**合并类型**存有其一种子类型的值：

<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>enum E { A, B, C }</code></name>
    <visual class="enum" style="text-align: left;">
        <pad><code>标签</code></pad>
        <framed class="any">
            <code>A</code>
        </framed>
    </visual>
    <andor>排他性或</andor>
    <visual class="enum" style="text-align: left;">
        <pad><code>标签</code></pad>
        <framed class="any" style="width: 100px;">
            <code>B</code>
        </framed>
    </visual>
    <andor>排他性或</andor>
    <visual class="enum" style="text-align: left;">
        <pad><code>标签</code></pad>
        <framed class="any" style="width: 50px;">
            <code>C</code>
        </framed>
    </visual>
    <description>
        安全地保存 A、B 或 C。<br>又名“标签联合”，尽管编译器会忽略标签。
    </description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>union { ... }</code></name>
    <visual style="text-align: left;">
        <framed class="any">
            <code>A</code>
        </framed>
    </visual>
    <andor>不安全或</andor>
    <visual style="text-align: left;">
        <framed class="any" style="width: 100px;">
            <code>B</code>
        </framed>
    </visual>
    <andor>不安全或</andor>
    <visual style="text-align: left;">
        <framed class="any" style="width: 50px;">
            <code>C</code>
        </framed>
    </visual>
    <description>
        不安全地以多种方式解释同一块内存。<br>结果可能是未定义的。
    </description>
</datum>



## 引用和指针 {#references-pointers-ui}

References give safe access to other memory, raw pointers `unsafe` access.
The respective `mut` types are identical.


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>&'a T</code></name>
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <payload>
            <code>meta</code><sub>2/4/8</sub>
        </payload>
    </visual>
    <memory-entry>
        <memory-link style="left:46%;">|</memory-link>
        <memory class="anymem">
            <framed class="any unsized"><code>T</code></framed>
        </memory>
    </memory-entry>
    <description>Must target some valid <code>t</code> of <code>T</code>, <br> and any such target must exist for <br> at least <code>'a</code>.</description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>*const T</code></name>
    <visual class="unsafe">
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <payload>
            <code>meta</code><sub>2/4/8</sub>
        </payload>
    </visual>
    <zoom>
        没有任何保证。
    </zoom>
</datum>

<br/>


### Pointer Meta {#pointer-meta}

Many reference and pointer types can carry an extra field, **pointer metadata**. {{ std(page="nightly/std/ptr/trait.Pointee.html#pointer-metadata") }}
It can be the element- or byte-length of the target, or a pointer to a <i>vtable</i>. Pointers with meta are called **fat**, otherwise **thin**.

<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>&'a T</code></name>
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
    </visual>
    <memory-entry>
        <memory-link style="left:46%;">|</memory-link>
        <memory class="anymem">
            <framed class="any t"><code>T</code></framed>
        </memory>
    </memory-entry>
    <description>No meta for <br>sized target.<br>(pointer is thin).</description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>&'a T</code></name>
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <sized>
            <code>len</code><sub>2/4/8</sub>
        </sized>
    </visual>
    <memory-entry>
        <memory-link style="left:46%;">|</memory-link>
        <memory class="anymem">
            <framed class="any unsized"><code>T</code></framed>
        </memory>
    </memory-entry>
    <description>If <code>T</code> is a DST <code>struct</code> such as<br> <code>S { x: [u8] }</code>
    meta field <code>len</code> is <br>length of dyn. sized content.</description>
</datum>



<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>&'a [T]</code></name>
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <sized>
            <code>len</code><sub>2/4/8</sub>
        </sized>
    </visual>
    <memory-entry class="double">
        <memory-link style="left:24%;">|</memory-link>
        <memory class="anymem">
            ...
            <framed class="any" style="width: 30px;"><code>T</code></framed>
            <framed class="any" style="width: 30px;"><code>T</code></framed>
            ...
        </memory>
    </memory-entry>
    <description>Regular <b>slice reference</b> (i.e., the <br>reference type of a slice type <code>[T]</code>) {{ above (target="#custom-types") }} <br>often seen as <code>&[T]</code> if <code>'a</code> elided.</description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>&'a str</code></name>
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <sized>
            <code>len</code><sub>2/4/8</sub>
        </sized>
    </visual>
    <memory-entry class="double">
        <memory-link style="left:24%;">|</memory-link>
        <memory class="anymem">
            ...
            <byte class="bytes"><code>U</code></byte>
            <byte class="bytes"><code>T</code></byte>
            <byte class="bytes"><code>F</code></byte>
            <byte class="bytes"><code>-</code></byte>
            <byte class="bytes"><code>8</code></byte>
            ...
        </memory>
    </memory-entry>
    <description><b>String slice reference</b> (i.e., the <br>reference type of string type <code>str</code>),<br> with meta <code>len</code> being byte length.</description>
</datum>

<br>

<!-- NEW ENTRY -->
<datum class="spaced" style="padding-bottom: 165px;">
    <name><code>&'a dyn Trait</code></name>
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <ptr>
            <code>ptr</code><sub>2/4/8</sub>
        </ptr>
    </visual>
    <memory-entry>
        <memory-link style="left:49%;">|</memory-link>
        <memory class="anymem">
            <framed class="any unsized"><code>T</code></framed>
        </memory>
    </memory-entry>
    <memory-entry style="width:220px; position: absolute;">
        <memory-link style="left:22%;">|</memory-link>
        <memory class="static-vtable" style="width: 210px;">
            <table>
                <tr class="vtable"><td><code>*Drop::drop(&mut T)</code></td></tr>
                <tr class="vtable"><td><code>size</code></td></tr>
                <tr class="vtable"><td><code>align</code></td></tr>
                <tr class="vtable"><td><code>*Trait::f(&T, ...)</code></td></tr>
                <tr class="vtable"><td><code>*Trait::g(&T, ...)</code></td></tr>
            </table>
        </memory>
        <description>Meta points to vtable, where <code>*Drop::drop()</code>, <code>*Trait::f()</code>, ... are pointers to their respective <code>impl</code> for <code>T</code>.</description>
    </memory-entry>

</datum>


## 闭包 {#closures-data}

闭包是一个临时函数，定义闭包时，它会自动管理数据**捕获**{{ ref(page="types/closure.html#capture-modes") }}环境中访问的内容。例如：
<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>move |x| x + y.f() + z</code></name>
    <visual>
       <framed class="any" style="width: 100px;"><code>Y</code></framed>
       <framed class="any" style="width: 50px;"><code>Z</code></framed>
    </visual>
    <zoom>匿名闭包类型 C1</zoom>
    <!-- <description>Also produces anonymous <br><code>f<sub>c1</sub> (c: C1, x: T)</code>. Details depend<br> which <code>FnOnce</code>, <code>FnMut</code>, <code>Fn</code> is allowed.</description> -->
</datum>



<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>|x| x + y.f() + z</code></name>
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
    </visual>
    <zoom>匿名闭包类型 C2</zoom>
    <memory-entry>
        <memory-link style="left:44%;">|</memory-link>
        <memory class="anymem">
            <framed class="any" style="width: 30px;"><code>Y</code></framed>
        </memory>
    </memory-entry>
    <memory-entry>
        <memory-link style="left:44%;">|</memory-link>
        <memory class="anymem">
            <framed class="any" style="width: 30px;"><code>Z</code></framed>
        </memory>
    </memory-entry>
    <!-- <description>Similar, but captured context by<br> reference. Details might differ <br> depending on types involved.</description> -->
</datum>

<!-- Little hack as description below was too cluttered. -->
<!-- <datum>
    <name>&nbsp;</name>
    <description>
    Also produces anonymous <code>fn</code> such as <code>f_c1 (C1, X)</code> or <br>
    <code>f_c2 (&C2, X)</code>. Details depend which <code>FnOnce</code>, <code>FnMut</code>, <code>Fn</code> ...<br>
    is supported, based on properties of captured types.
    </description>
</datum> -->

<blockquote>
<footnotes>

Also produces anonymous <code>fn</code> such as <code>f<sub>c1</sub>(C1, X)</code> or <code>f<sub>c2</sub>(&C2, X)</code>. Details depend which <code>FnOnce</code>, <code>FnMut</code>, <code>Fn</code> ... is supported, based on properties of captured types.

</footnotes>
</blockquote>



## 标准库类型 {#standard-library-types}

Rust 标准库为上面提到的基本类型扩展了更多有用的类型，并定义了一些特殊的语义。一些通用类型如下：


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>UnsafeCell&lt;T&gt;</code></name>
    <visual class="cell">
           <framed class="any unsized"><code>T</code></framed>
    </visual>
    <description>魔术类型，允许<br>别名可变性。</description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>Cell&lt;T&gt;</code></name>
    <visual>
           <framed class="any unsized celled"><code>T</code></framed>
    </visual>
    <description>允许 <code>T</code> 的<br>移动进出。</description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>RefCell&lt;T&gt;</code></name>
    <visual>
        <sized class="celled"><code>borrowed</code></sized>
        <framed class="any unsized celled"><code>T</code></framed>
    </visual>
    <description>Also support dynamic<br>
    borrowing of <code>T</code>. Like <code>Cell</code> this<br>
    is <code>Send</code>, but not <code>Sync</code>.</description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>AtomicUsize</code></name>
    <visual class="atomic">
        <ptr class="atomic">
            <code>usize</code><sub>2/4/8</sub>
        </ptr>
    </visual>
    <description>其他原子类型类似</description>
</datum>


<!-- NEW ENTRY -->
<datum>
    <name><code>Result&lt;T, E&gt;</code></name>
    <visual class="enum" style="text-align: left;">
        <pad><code>Tag</code></pad>
        <framed class="any" style="width: 50px;">
            <code>E</code>
        </framed>
    </visual>
    <andor>or</andor>
    <visual class="enum" style="text-align: left;">
        <pad><code>Tag</code></pad>
        <framed class="any" style="width: 100px;">
            <code>T</code>
        </framed>
    </visual>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>Option&lt;T&gt;</code></name>
    <visual class="enum" style="text-align: left;">
        <pad><code>Tag</code></pad>
    </visual>
    <andor>or</andor>
    <visual class="enum">
        <pad><code>Tag</code></pad>
        <framed class="any" style="width: 100px;">
            <code>T</code>
        </framed>
    </visual>
    <description>Tag may be omitted for <br> certain T, e.g., <code>NonNull</code>.</description>
</datum>



{{ tablesep() }}


#### 通用堆存储器


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>Box&lt;T&gt;</code></name>
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <payload>
            <code>meta</code><sub>2/4/8</sub>
        </payload>
    </visual>
    <memory-entry>
        <memory-link style="left:49%;">|</memory-link>
        <memory class="heap">
        <framed class="any unsized"><code>T</code></framed>
        </memory>
    </memory-entry>
    <description>For some <code>T</code> stack proxy may carry <br>meta{{ above (target="#custom-types") }} (e.g., <code>Box<[T]></code>).</description>
</datum>

<spacer>
</spacer>

<!-- NEW ENTRY -->
<datum>
    <name><code>Vec&lt;T&gt;</code></name>
    <!-- For some reason we need the width for mobile not to line break -->
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <sized>
            <code>capacity</code><sub>2/4/8</sub>
        </sized>
        <sized>
            <code>len</code><sub>2/4/8</sub>
        </sized>
    </visual>
    <memory-entry class="double">
        <memory-link style="left:25%;">|</memory-link>
        <memory class="heap capacity">
            <div>
                <framed class="any t"><code>T</code></framed>
                <framed class="any t"><code>T</code></framed>
                <note>... len</note>
            </div>
            <capacity>← <note>capacity</note> →</capacity>
        </memory>
    </memory-entry>
</datum>


{{ tablesep() }}


#### 所有字符串


<!-- NEW ENTRY -->
<datum>
    <name><code>String</code></name>
    <!-- For some reason we need the width for mobile not to line break -->
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <sized>
            <code>capacity</code><sub>2/4/8</sub>
        </sized>
        <sized>
            <code>len</code><sub>2/4/8</sub>
        </sized>
    </visual>
    <memory-entry class="double">
        <memory-link style="left:25%;">|</memory-link>
        <memory class="heap">
            <div>
                <byte class="bytes"><code>U</code></byte>
                <byte class="bytes"><code>T</code></byte>
                <byte class="bytes"><code>F</code></byte>
                <byte class="bytes"><code>-</code></byte>
                <byte class="bytes"><code>8</code></byte>
                <note>... len</note>
            </div>
            <capacity>← <note>capacity</note> →</capacity>
        </memory>
    </memory-entry>
    <description>Observe how <code>String</code> differs from <code>&str</code> and <code>&[char]</code>.</description>
</datum>

<spacer>
</spacer>

<!-- NEW ENTRY -->
<datum>
    <name><code>CString</code></name>
    <!-- For some reason we need the width for mobile not to line break -->
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <sized>
            <code>len</code><sub>2/4/8</sub>
        </sized>
    </visual>
    <memory-entry class="double">
        <memory-link style="left:25%;">|</memory-link>
        <memory class="heap">
            <div>
                <byte class="bytes"><code>A</code></byte>
                <byte class="bytes"><code>B</code></byte>
                <byte class="bytes"><code>C</code></byte>
                <note>... len ...</note>
                <byte class="bytes"><code>␀</code></byte>
            </div>
        </memory>
    </memory-entry>
    <description>以空字符结束，但中间没有空字符。</description>
</datum>


<spacer>
</spacer>

<!-- NEW ENTRY -->
<datum>
    <name><code>OsString</code> {{ todo() }}</name>
    <!-- For some reason we need the width for mobile not to line break -->
    <visual class="platformdefined">
        平台定义
    </visual>
    <memory-entry class="double">
        <memory-link style="left:25%;">|</memory-link>
        <memory class="heap">
            <div>
                <byte class="bytes"><code>?</code></byte>
                <byte class="bytes"><code>?</code></byte>
                /
                <word class="bytes"><code>?</code></word>
                <word class="bytes"><code>?</code></word>
            </div>
        </memory>
    </memory-entry>
    <description>Encapsulates how operating system<br> represents strings (e.g., UTF-16 on <br>Windows).</description>
</datum>

<spacer>
</spacer>

<!-- NEW ENTRY -->
<datum>
    <name><code>PathBuf</code> {{ todo() }}</name>
    <!-- For some reason we need the width for mobile not to line break -->
    <visual class="platformdefined">
        <payload>
            <code>OsString</code>
        </payload>
    </visual>
    <memory-entry class="double">
        <memory-link style="left:40%;">|</memory-link>
        <memory class="heap">
            <div>
                <byte class="bytes"><code>?</code></byte>
                <byte class="bytes"><code>?</code></byte>
                /
                <word class="bytes"><code>?</code></word>
                <word class="bytes"><code>?</code></word>
            </div>
        </memory>
    </memory-entry>
    <description>Encapsulates how operating system<br> represents paths.</description>
</datum>


{{ tablesep() }}

#### 共享所有权

如果类型 `T` 不包含 `Cell`，那它也会包含以下 `Cell` 类型的变体以允许共享实际可变性。

<!-- NEW ENTRY -->
<datum>
    <name><code>Rc&lt;T&gt;</code></name>
    <visual style="width: 180px;">
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <payload>
            <code>meta</code><sub>2/4/8</sub>
        </payload>
    </visual>
    <div>
        <memory-entry class="quad">
            <memory-link style="left:15%;">|</memory-link>
            <memory class="heap">
                <sized class="celled"><code>strng</code><sub>2/4/8</sub></sized>
                <sized class="celled"><code>weak</code><sub>2/4/8</sub></sized>
                <framed class="any unsized"><code>T</code></framed>
            </memory>
        </memory-entry>
    </div>
    <description>在同一个线程上共享 <code>T</code> 的所有权。需要嵌套 <code>Cell</code>
    或 <br><code>RefCell</code> 以允许修改。它既不是 <code>Send</code> 也不是 <code>Sync</code> 的。</description>
</datum>


<!-- NEW ENTRY -->
<datum>
    <name><code>Arc&lt;T&gt;</code></name>
    <visual style="width: 180px;">
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <payload>
            <code>meta</code><sub>2/4/8</sub>
        </payload>
    </visual>
    <div style="width: 0px;">
        <memory-entry class="quad">
            <memory-link style="left:15%;">|</memory-link>
            <memory class="heap">
                <sized class="atomicx"><code>strong</code><sub>2/4/8</sub></sized>
                <sized class="atomicx"><code>weak</code><sub>2/4/8</sub></sized>
                <framed class="any unsized"><code>T</code></framed>
            </memory>
        </memory-entry>
    </div>
    <description>同左。但如果 T 是 <code>Send</code> 且 <code>Sync</code> 的，则允许在线程间共享。</description>
</datum>

<br>

<!-- NEW ENTRY -->
<datum>
    <name><code>Mutex&lt;T&gt;</code> / <code>RwLock&lt;T&gt;</code></name>
    <visual style="width: 230px;">
        <ptr><code>ptr</code><sub>2/4/8</sub></ptr>
        <sized class="atomicx"><code>poison</code><sub>2/4/8</sub></sized>
        <framed class="any unsized celled"><code>T</code></framed>
    </visual>
    <memory-entry>
        <memory-link style="left:45%;">|</memory-link>
        <memory class="heap">
            <code>lock</code>
        </memory>
    </memory-entry>
    <description>Needs to be held in <code>Arc</code> to be shared between<br> threads,
    always <code>Send</code> and <code>Sync</code>. Consider using <br> <a href="https://crates.io/crates/parking_lot">parking_lot</a> instead (faster, no heap usage).
    </description>
</datum>



---


# Standard Library


## One-Liners

Snippets that are common, but still easy to forget. See **Rust Cookbook** {{ link(url="https://rust-lang-nursery.github.io/rust-cookbook/") }} for more.


<!--
PRs for this section are very welcome. Idea is:
- Should be `std` only for now, no 3rd party libs (maybe exception for `rand`?)
- "Most people" should have encountered the problem
- Is not just a trival method on an 'obvious' struct (e.g., Sort a slice by `x.sort()` is probably too obvious.)
-->

<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">


<tabs>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-api-2" name="tab-api-sized" checked>
<label for="tab-api-2"><b>Strings</b></label>
<panel><div class="color-header one-liners cheats">

| Intent | Snippet |
|---------|-------------|
| Concatenate strings (any `Display`{{ below(target="#string-output") }} that is). <sup>1</sup>  {{ edition(ed="'21") }} | `format!("{x}{y}")` |
| Split by separator pattern. {{ std(page="std/str/pattern/trait.Pattern.html") }} {{ link(url="https://stackoverflow.com/a/38138985") }} | `s.split(pattern)` |
| {{ tab() }} ... with `&str` | `s.split("abc")` |
| {{ tab() }} ... with `char` | `s.split('/')` |
| {{ tab() }} ... with closure | `s.split(char::is_numeric)`|
| Split by whitespace. | `s.split_whitespace()` |
| Split by newlines. | `s.lines()` |
| Split by regular expression.<sup>2</sup> | ` Regex::new(r"\s")?.split("one two three")` |

<footnotes>

<sup>1</sup> Allocates; might not be fastest solution if `x` is `String` already.<br>
<sup>2</sup> Requires [regex](https://crates.io/crates/regex) crate.

</footnotes>


</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-api-1" name="tab-api-sized">
<label for="tab-api-1"><b>I/O</b></label>
<panel><div class="color-header one-liners cheats">

| Intent | Snippet |
|---------|-------------|
| Create a new file | `File::create(PATH)?` |
| {{ tab() }}  Same, via OpenOptions | `OpenOptions::new().create(true).write(true).truncate(true).open(PATH)?` |

<!-- <footnotes>

<sup>*</sup> We're a bit short on space here, <code>t</code> means true.

</footnotes> -->

</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-api-4" name="tab-api-sized">
<label for="tab-api-4"><b>Macros</b></label>
<panel><div class="color-header one-liners cheats">

| Intent | Snippet |
|---------|-------------|
| Macro w. variable arguments | `macro_rules! var_args { ($($args:expr),*) => {{ }} }` |
| {{ tab() }} Using `args`, e.g., calling `f` multiple times. | {{ tab() }} ` $( f($args); )*` |

</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-api-3" name="tab-api-sized">
<label for="tab-api-3"><b>Esoterics</b>{{ esoteric() }}</label>
<panel><div class="color-header one-liners cheats">

| Intent | Snippet |
|---------|-------------|
| Cleaner closure captures | <code>wants_closure({ let c = outer.clone(); move &vert;&vert; use_clone(c) })</code> |
| Fix inference in '`try`' closures | <code>iter.try_for_each(&vert;x&vert; { Ok::<(), Error>(()) })?;</code> |
| Iterate _and_ edit `&mut [T]` if `T` Copy. | `Cell::from_mut(mut_slice).as_slice_of_cells()` |
| Get subslice with length. | `&original_slice[offset..][..length]` |
| Canary to ensure trait `T` is object safe. | `const _: Option<&dyn T> = None;` |


</div></panel></tab>


</tabs>


</div></div>



## 线程安全 {#thread-safety}


<!-- Shamelessly stolen from https://www.reddit.com/r/rust/comments/ctdkyr/understanding_sendsync/exk8grg/ -->
<table class="sendsync">
    <thead>
        <tr><th>例</th><th><code>Send</code><sup>*</sup></th><th><code>!Send</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>Sync</code><sup>*</sup></td><td><i>多数类型</i> ... <code>Mutex&lt;T&gt;</code>, <code>Arc&lt;T&gt;</code><sup>1,2</sup></td><td><code>MutexGuard&lt;T&gt;</code><sup>1</sup>, <code>RwLockReadGuard&lt;T&gt;</code><sup>1</sup></td></tr>
        <tr><td><code>!Sync</code></td><td><code>Cell&lt;T&gt;</code><sup>2</sup>, <code>RefCell&lt;T&gt;</code><sup>2</sup></td><td><code>Rc&lt;T&gt;</code>, <code>&dyn Trait</code>, <code>*const T</code><sup>3</sup>, <code>*mut T</code><sup>3</sup></td></tr>
    </tbody>
</table>

<footnotes>

<sup>*</sup> **`T: Send`** 表示实例 `t` 可以移动到另一个线程；**`T: Sync`** 表示 `&t` 可以移动到另一个线程。<br>
<sup>1</sup> 如果 `T` 为 `Sync`。 <br>
<sup>2</sup> 如果 `T` 为 `Send`。
<sup>3</sup> If you need to send a raw pointer, create newtype `struct Ptr(*const u8)` and `unsafe impl Send for Ptr {}`. Just ensure you _may_ send it.

</footnotes>



## 迭代器 {#iterators}

<tabs class="color-header std-green">

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-trait-iter-1" name="tab-group-trait-iter" checked>
<label for="tab-trait-iter-1"><b>Obtaining Iterators</b></label>
<panel><div>



**Basics**

Assume you have a collection `c` of type `C`:

* **`c.into_iter()`** &mdash; Turns collection `c` into an **`Iterator`** {{ std(page="std/iter/trait.Iterator.html") }} `i` and **consumes**<sup>*</sup> `c`. Requires **`IntoIterator`** {{ std(page="std/iter/trait.IntoIterator.html") }} for `C` to be implemented. Type of item depends on what `C` was. 'Standardized' way to get Iterators.
* **`c.iter()`** &mdash; Courtesy method **some** collections provide, returns **borrowing** Iterator, doesn't consume `c`.
* **`c.iter_mut()`** &mdash; Same, but **mutably borrowing** Iterator that allow collection to be changed.


**The Iterator**

Once you have an `i`:

* **`i.next()`** &mdash; Returns `Some(x)` next element `c` provides, or `None` if we're done.


**For Loops**

* **`for x in c {}`** &mdash; Syntactic sugar, calls `c.into_iter()` and loops `i` until `None`.

<footnotes>

<sup>*</sup> If it looks as if it doesn't consume `c` that's because type was `Copy`. For example, if you call `(&c).into_iter()` it will invoke `.into_iter()` on `&c` (which will consume the reference and turn it into an Iterator), but `c` remains untouched.

</footnotes>

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-trait-iter-2" name="tab-group-trait-iter">
<label for="tab-trait-iter-2"><b>Implementing Iterators</b></label>
<panel><div>

**Basics**

Let's assume you have a `struct Collection<T> {}`.


* **`struct IntoIter<T> {}`** &mdash; Create a struct to hold your iteration status (e.g., an index) for value iteration.
* **`impl Iterator for IntoIter {}`** &mdash; Implement `Iterator::next()` so it can produce elements.

<mini-zoo class="zoo" style="">
    <entry class="wide">
        <type class="generic dotted"><code>Collection&lt;T&gt;</code></type>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-right: 20px;">
    <entry class="wide">
        <type class="generic dotted"><code>IntoIter&lt;T&gt;</code></type>
        <trait-impl class="">⌾ <code style="">Iterator</code></trait-impl>
        <associated-type class="grayed"><code>Item = T;</code></associated-type>
    </entry>
</mini-zoo>


---


**Shared & Mutable Iterators**

* **`struct Iter<T> {}`** &mdash; Create struct holding `&Collection<T>` for shared iteration.
* **`struct IterMut<T> {}`** &mdash; Similar, but holding `&mut Collection<T>` for mutable iteration.
* **`impl Iterator for Iter<T> {}`** &mdash; Implement shared iteration.
* **`impl Iterator for IterMut<T> {}`** &mdash; Implement mutable iteration.

In addition, you might want to add convenience methods:

- `Collection::iter(&self) -> Iter`,
- `Collection::iter_mut(&mut self) -> IterMut`.



<mini-zoo class="zoo" style="margin-right: 20px;">
    <entry class="wide">
        <type class="generic dotted"><code>Iter&lt;T&gt;</code></type>
        <trait-impl class="">⌾ <code style="">Iterator</code></trait-impl>
        <associated-type class="grayed"><code>Item = &T;</code></associated-type>
    </entry>
</mini-zoo>


<mini-zoo class="zoo" style="margin-right: 20px;">
    <entry class="wide">
        <type class="generic dotted"><code>IterMut&lt;T&gt;</code></type>
        <trait-impl class="">⌾ <code style="">Iterator</code></trait-impl>
        <associated-type class="grayed"><code>Item = &mut T;</code></associated-type>
    </entry>
</mini-zoo>

---

**Making Loops Work**
* **`impl IntoIterator for Collection {}`** &mdash; Now `for x in c {}` works.
* **`impl IntoIterator for &Collection {}`** &mdash; Now `for x in &c {}` works.
* **`impl IntoIterator for &mut Collection {}`** &mdash; Now `for x in &mut c {}` works.

<mini-zoo class="zoo" style="">
    <entry class="wide">
        <type class="generic dotted"><code>Collection&lt;T&gt;</code></type>
        <trait-impl class="">⌾ <code style="">IntoIterator</code></trait-impl>
        <associated-type class="grayed"><code>Item = T;</code></associated-type>
        <associated-type class="grayed"><code>To = IntoIter&lt;T&gt;</code></associated-type>
        <note>Iterate over <code>T</code>.</note>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="">
    <entry class="wide">
        <type class="generic dotted grayed"><code>&Collection&lt;T&gt;</code></type>
        <trait-impl class="">⌾ <code style="">IntoIterator</code></trait-impl>
        <associated-type class="grayed"><code>Item = &T;</code></associated-type>
        <associated-type class="grayed"><code>To = Iter&lt;T&gt;</code></associated-type>
        <note>Iterate over <code>&T</code>.</note>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="">
    <entry class="wide">
        <type class="generic dotted grayed"><code>&mut Collectn&lt;T&gt;</code></type>
        <trait-impl class="">⌾ <code style="">IntoIterator</code></trait-impl>
        <associated-type class="grayed"><code>Item = &mut T;</code></associated-type>
        <associated-type class="grayed"><code>To = IterMut&lt;T&gt;</code></associated-type>
        <note>Iterate over <code>&mut T</code>.</note>
    </entry>
</mini-zoo>

</div></panel></tab>


</tabs>



<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">
<div class="color-header number">


## Number Conversions


As-<b style="">correct</b>-as-it-currently-gets number conversions.

| ↓ Have / Want → | `u8` &hellip; `i128` |  `f32` / `f64` | String |
| --- | --- |  --- |--- |
| `u8` &hellip; `i128` | `u8::try_from(x)?` <sup>1</sup> |  `x as f32` <sup>3</sup> | `x.to_string()` |
| `f32` / `f64` | `x as u8` <sup>2</sup> |  `x as f32` | `x.to_string()` |
| `String` | `x.parse::<u8>()?` | `x.parse::<f32>()?` | `x` |


<footnotes>

<sup>1</sup> If type true subset `from()` works directly, e.g., `u32::from(my_u8)`. <br/>
<sup>2</sup> Truncating (`11.9_f32 as u8` gives `11`) and saturating (`1024_f32 as u8` gives `255`); _c_. below. <br/>
<sup>3</sup> Might misrepresent number (`u64::MAX as f32`) or produce `Inf` (`u128::MAX as f32`).

</footnotes>


<!-- end overflow -->
</div>
</div>
</div>



## String Conversions


If you **want** a string of type &hellip;

<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">


<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-1" name="tab-group-str" checked>
<label for="tab-str-1"><code>String</code></label>
<panel><div class="stringconversion">

| If you **have** `x` of type &hellip;| Use this &hellip; |
| --- | --- |
|`String`|`x`|
|`CString`|`x.into_string()?` |
|`OsString`|`x.to_str()?.to_string()`|
|`PathBuf`|`x.to_str()?.to_string()`|
|`Vec<u8>` <sup>1</sup> |`String::from_utf8(x)?`|
|`&str`|`x.to_string()` <sup>`i`</sup> |
|`&CStr`|`x.to_str()?.to_string()` |
|`&OsStr`|`x.to_str()?.to_string()`|
|`&Path`|`x.to_str()?.to_string()`|
|`&[u8]` <sup>1</sup> |`String::from_utf8_lossy(x).to_string()`|

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-2" name="tab-group-str" >
<label for="tab-str-2"><code>CString</code></label>
<panel><div class="stringconversion">

| If you **have** `x` of type &hellip;| Use this &hellip; |
| --- | --- |
|`String`|`CString::new(x)?`|
|`CString`|`x`|
|`OsString` <sup>2</sup>|`CString::new(x.to_str()?)?`|
|`PathBuf`|`CString::new(x.to_str()?)?`|
|`Vec<u8>` <sup>1</sup> |`CString::new(x)?`|
|`&str`|`CString::new(x)?`|
|`&CStr`|`x.to_owned()` <sup>`i`</sup> |
|`&OsStr` <sup>2</sup> |`CString::new(x.to_os_string().into_string()?)?`|
|`&Path`|`CString::new(x.to_str()?)?`|
|`&[u8]` <sup>1</sup> |`CString::new(Vec::from(x))?`|
|`*mut c_char` <sup>3</sup> |`unsafe { CString::from_raw(x) }`|

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-3" name="tab-group-str" >
<label for="tab-str-3"><code>OsString</code></label>
<panel><div class="stringconversion">

| If you **have** `x` of type &hellip;| Use this &hellip; |
| --- | --- |
|`String`|`OsString::from(x)` <sup>`i`</sup> |
|`CString`|`OsString::from(x.to_str()?)`|
|`OsString`|`x`|
|`PathBuf`|`x.into_os_string()`|
|`Vec<u8>` <sup>1</sup> | {{ todo() }} |
|`&str`|`OsString::from(x)` <sup>`i`</sup>|
|`&CStr`|`OsString::from(x.to_str()?)`|
|`&OsStr`|`OsString::from(x)` <sup>`i`</sup>|
|`&Path`|`x.as_os_str().to_owned()`|
|`&[u8]` <sup>1</sup> | {{ todo() }} |

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-35" name="tab-group-str" >
<label for="tab-str-35"><code>PathBuf</code></label>
<panel><div class="stringconversion">

| If you **have** `x` of type &hellip;| Use this &hellip; |
| --- | --- |
|`String`|`PathBuf::from(x)` <sup>`i`</sup>|
|`CString`|`PathBuf::from(x.to_str()?)`|
|`OsString`|`PathBuf::from(x)` <sup>`i`</sup>|
|`PathBuf`|`x`|
|`Vec<u8>` <sup>1</sup> | {{ todo() }} |
|`&str`|`PathBuf::from(x)` <sup>`i`</sup>|
|`&CStr`|`PathBuf::from(x.to_str()?)`|
|`&OsStr`|`PathBuf::from(x)` <sup>`i`</sup>|
|`&Path`|`PathBuf::from(x)` <sup>`i`</sup>|
|`&[u8]` <sup>1</sup> | {{ todo() }} |

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-4" name="tab-group-str" >
<label for="tab-str-4"><code>Vec&lt;u8&gt;</code></label>
<panel><div class="stringconversion">

| If you **have** `x` of type &hellip;| Use this &hellip; |
| --- | --- |
|`String`|`x.into_bytes()`|
|`CString`|`x.into_bytes()`|
|`OsString`| {{ todo() }} |
|`PathBuf`| {{ todo() }} |
|`Vec<u8>` <sup>1</sup> |`x`|
|`&str`|`Vec::from(x.as_bytes())`|
|`&CStr`|`Vec::from(x.to_bytes_with_nul())`|
|`&OsStr`| {{ todo() }} |
|`&Path`| {{ todo() }} |
|`&[u8]` <sup>1</sup> |`x.to_vec()`|

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-5" name="tab-group-str" >
<label for="tab-str-5"><code>&str</code></label>
<panel><div class="stringconversion">

| If you **have** `x` of type &hellip;| Use this &hellip; |
| --- | --- |
|`String`|`x.as_str()`|
|`CString`|`x.to_str()?`|
|`OsString`|`x.to_str()?`|
|`PathBuf`|`x.to_str()?`|
|`Vec<u8>` <sup>1</sup> |`std::str::from_utf8(&x)?`|
|`&str`|`x`|
|`&CStr`|`x.to_str()?`|
|`&OsStr`|`x.to_str()?`|
|`&Path`|`x.to_str()?`|
|`&[u8]` <sup>1</sup> |`std::str::from_utf8(x)?`|

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-6" name="tab-group-str" >
<label for="tab-str-6"><code>&CStr</code></label>
<panel><div class="stringconversion">

| If you **have** `x` of type &hellip;| Use this &hellip; |
| --- | --- |
|`String`|`CString::new(x)?.as_c_str()`|
|`CString`|`x.as_c_str()`|
|`OsString` <sup>2</sup>|`x.to_str()?`|
|`PathBuf`| {{ todo() }}<sup>,4</sup> |
|`Vec<u8>` <sup>1</sup><sup>,5</sup> |`CStr::from_bytes_with_nul(&x)?`|
|`&str`| {{ todo() }}<sup>,4</sup> |
|`&CStr`|`x`|
|`&OsStr` <sup>2</sup>| {{ todo() }} |
|`&Path`| {{ todo() }} |
|`&[u8]` <sup>1</sup><sup>,5</sup> |`CStr::from_bytes_with_nul(x)?`|
|`*const c_char` <sup>1</sup> |`unsafe { CStr::from_ptr(x) }`|

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-8" name="tab-group-str" >
<label for="tab-str-8"><code>&OsStr</code></label>
<panel><div class="stringconversion">

| If you **have** `x` of type &hellip;| Use this &hellip; |
| --- | --- |
|`String`|`OsStr::new(&x)`|
|`CString`| {{ todo() }} |
|`OsString`|`x.as_os_str()`|
|`PathBuf`|`x.as_os_str()`|
|`Vec<u8>` <sup>1</sup> | {{ todo() }} |
|`&str`|`OsStr::new(x)`|
|`&CStr`| {{ todo() }} |
|`&OsStr`|`x`|
|`&Path`|`x.as_os_str()`|
|`&[u8]` <sup>1</sup> | {{ todo() }} |

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-85" name="tab-group-str" >
<label for="tab-str-85"><code>&Path</code></label>
<panel><div class="stringconversion">

| If you **have** `x` of type &hellip;| Use this &hellip; |
| --- | --- |
|`String`|`Path::new(x)` <sup>`r`</sup>|
|`CString`|`Path::new(x.to_str()?)` |
|`OsString`|`Path::new(x.to_str()?)` <sup>`r`</sup>|
|`PathBuf`|`Path::new(x.to_str()?)` <sup>`r`</sup>|
|`Vec<u8>` <sup>1</sup> | {{ todo() }} |
|`&str`|`Path::new(x)` <sup>`r`</sup>|
|`&CStr`|`Path::new(x.to_str()?)` |
|`&OsStr`|`Path::new(x)` <sup>`r`</sup>|
|`&Path`|`x`|
|`&[u8]` <sup>1</sup> | {{ todo() }} |

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-7" name="tab-group-str" >
<label for="tab-str-7"><code>&[u8]</code></label>
<panel><div class="stringconversion">

| If you **have** `x` of type &hellip;| Use this &hellip; |
| --- | --- |
|`String`|`x.as_bytes()`|
|`CString`|`x.as_bytes()`|
|`OsString`| {{ todo() }} |
|`PathBuf`| {{ todo() }} |
|`Vec<u8>` <sup>1</sup> |`&x`|
|`&str`|`x.as_bytes()`|
|`&CStr`|`x.to_bytes_with_nul()`|
|`&OsStr`| `x.as_bytes()` <sup>2</sup> |
|`&Path`| {{ todo() }} |
|`&[u8]` <sup>1</sup> |`x`|

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-9" name="tab-group-str" >
<label for="tab-str-9"><b>Other</b></label>
<panel><div class="stringconversion">

| You **want** | And **have** `x` | Use this &hellip; |
| --- | --- | --- |
|<b>`*const c_char`</b>|<b>`CString`</b>|`x.as_ptr()`|


</div></panel></tab>

<!-- End tabs -->
</tabs>

<!-- End overflow protection -->
</div></div>


<footnotes>

<sup>i</sup> Short form `x.into()` possible if type can be inferred. <br>
<sup>r</sup> Short form `x.as_ref()` possible if type can be inferred.

<sup>1</sup> You should, or must if call is `unsafe`, ensure raw data comes with a valid representation for the string type (e.g., UTF-8 data for a `String`). {{ link(url="https://people.gnome.org/~federico/blog/correctness-in-rust-reading-strings.html") }}


<sup>2</sup> Only on some platforms `std::os::<your_os>::ffi::OsStrExt` exists with helper methods to get a raw `&[u8]` representation of the underlying `OsStr`. Use the rest of the table to go from there, e.g.:

```
use std::os::unix::ffi::OsStrExt;
let bytes: &[u8] = my_os_str.as_bytes();
CString::new(bytes)?
```

<sup>3</sup> The `c_char` **must** have come from a previous `CString`. If it comes from FFI see `&CStr` instead.

<sup>4</sup> No known shorthand as `x` will lack terminating `0x0`. Best way to probably go via `CString`.

<sup>5</sup> Must ensure vector actually ends with `0x0`.

</footnotes>


## String Output

How to convert types into a `String`, or output them.

<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-strop-1" name="tab-group-strop" checked>
<label for="tab-strop-1"><b>APIs</b></label>
<panel><div class="color-header undefined-color-3">

Rust has, among others, these APIs to convert types to stringified output, collectively called _format_ macros:

| Macro | Output | Notes |
| --- | --- | --- |
|`format!(fmt)` | `String` | Bread-and-butter "to `String`" converter. |
|`print!(fmt)`| Console | Writes to standard output. |
|`println!(fmt)`| Console | Writes to standard output. |
|`eprint!(fmt)`| Console | Writes to standard error. |
|`eprintln!(fmt)`| Console | Writes to standard error. |
|`write!(dst, fmt)` | Buffer | Don't forget to also `use std::io::Write;` |
|`writeln!(dst, fmt)` | Buffer | Don't forget to also `use std::io::Write;` |

{{ tablesep() }}

| Method | Notes |
| --- | --- |
|`x.to_string()` {{ std(page="std/string/trait.ToString.html") }} | Produces `String`, implemented for any `Display` type. |

{{ tablesep() }}

Here `fmt` is string literal such as `"hello {}"`, that specifies output (compare "Formatting" tab) and additional parameters.


</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-strop-2" name="tab-group-strop">
<label for="tab-strop-2"><b>Printable Types</b></label>
<panel><div class="color-header undefined-color-3">

In `format!` and friends, types convert via trait `Display` `"{}"` {{ std(page="std/fmt/trait.Display.html") }} or `Debug` `"{:?}"` {{ std(page="std/fmt/trait.Debug.html") }} , non exhaustive list:

| Type | Implements |  |
| --- | --- | --- |
|`String`| `Debug, Display` | |
|`CString`| `Debug` | |
|`OsString`| `Debug` | |
|`PathBuf`| `Debug` |  |
|`Vec<u8>` | `Debug` | |
|`&str`|`Debug, Display` | |
|`&CStr`|`Debug` | |
|`&OsStr`| `Debug` | |
|`&Path`| `Debug` | |
|`&[u8]` |`Debug` | |
|`bool` |`Debug, Display` | |
|`char` |`Debug, Display` | |
|`u8` &hellip; `i128` |`Debug, Display` | |
|`f32`, `f64` |`Debug, Display` | |
|`!` |`Debug, Display` | |
|`()` |`Debug` | |

{{ tablesep() }}

In short, pretty much everything is `Debug`; more _special_ types might need special handling or conversion {{ above(target="#string-conversions" ) }} to `Display`.

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-strop-3" name="tab-group-strop">
<label for="tab-strop-3"><b>Formatting</b></label>
<panel><div>

Each argument designator in format macro is either empty `{}`, `{argument}`, or follows a basic [**syntax**](https://doc.rust-lang.org/std/fmt/index.html#syntax):


```
{ [argument] ':' [[fill] align] [sign] ['#'] [width [$]] ['.' precision [$]] [type] }
```

<div class="color-header undefined-color-3">

| Element |  Meaning |
|---------| ---------|
| `argument` |  Number (`0`, `1`, ...), argument {{ edition(ed="'21") }} or name,{{ edition(ed="'18") }} e.g., `print!("{x}")`. |
| `fill` | The character to fill empty spaces with (e.g., `0`), if `width` is specified. |
| `align` | Left (`<`), center (`^`), or right (`>`), if width is specified. |
| `sign` | Can be `+` for sign to always be printed. |
| `#` | [Alternate formatting](https://doc.rust-lang.org/std/fmt/index.html#sign0), e.g. prettify `Debug`{{ std(page="std/fmt/trait.Debug.html") }} formatter `?` or prefix hex with `0x`. |
| `width` | Minimum width (&geq; 0), padding with `fill` (default to space). If starts with `0`, zero-padded. |
| `precision` | Decimal digits (&geq; 0) for numerics, or max width for non-numerics. |
| `$` | Interpret `width` or `precision` as argument identifier instead to allow for dynamic formatting. |
| **`type`** | `Debug`{{ std(page="std/fmt/trait.Debug.html") }} (`?`) formatting, hex (`x`), binary (`b`), octal (`o`), pointer (`p`), exp (`e`) ... [see more](https://doc.rust-lang.org/std/fmt/index.html#traits). |

</div>


{{ tablesep() }}


<div class="color-header undefined-color-3">

| Format Example | Explanation |
|---------|-------------|
| `{}` | Print the next argument using `Display`.{{ std(page="std/fmt/trait.Display.html") }} |
| `{x}` | Same, but use variable `x` from scope. {{ edition(ed="'21") }} |
| `{:?}` | Print the next argument using `Debug`.{{ std(page="std/fmt/trait.Debug.html") }} |
| `{2:#?}` | Pretty-print the 3<sup>rd</sup> argument with `Debug`{{ std(page="std/fmt/trait.Debug.html") }} formatting. |
| `{val:^2$}` | Center the `val` named argument, width specified by the 3<sup>rd</sup> argument. |
| `{:<10.3}` | Left align with width 10 and a precision of 3.|
| `{val:#x}` | Format `val` argument as hex, with a leading `0x` (alternate format for `x`). |

</div>

{{ tablesep() }}


<div class="color-header undefined-color-3">

| Full Example | Explanation |
|---------|-------------|
| `println!("{}", x)` | Print `x` using `Display`{{ std(page="std/fmt/trait.Display.html") }} on std. out and append new line. {{ edition(ed="'15") }} |
| `println!("{x}")` | Same, but use variable `x` from scope. {{ edition(ed="'21") }}  |
| `format!("{a:.3} {b:?}")` | Convert `PI` with 3 digits, add space, b with `Debug` {{ std(page="std/fmt/trait.Debug.html") }}, return `String`.  {{ edition(ed="'21") }} |

</div>


</div></panel></tab>


</tabs>

{{ tablesep() }}




---

# 工具链


## 项目结构 {#project-anatomy}

Basic project layout, and common files and folders, as used by `cargo`. {{ below(target="#cargo") }}

<div class="color-header red">

| Entry | Code |
|--------| ---- |
| 📁 `.cargo/` | **Project-local cargo configuration**, may contain **`config.toml`**. {{ link( url="https://doc.rust-lang.org/cargo/reference/config.html") }} {{ esoteric() }} |
| 📁 `benches/` | Benchmarks for your crate, run via **`cargo bench`**, requires nightly by default. <sup>*</sup> {{ experimental() }} |
| 📁 `examples/` | Examples how to use your crate, they see your crate like external user would.  |
| {{ tab() }} `my_example.rs` | Individual examples are run like **`cargo run --example my_example`**. |
| 📁 `src/` | Actual source code for your project. |
| {{ tab() }} `main.rs` | Default entry point for applications, this is what **`cargo run`** uses. |
| {{ tab() }} `lib.rs` | Default entry point for libraries. This is where lookup for `my_crate::f()` starts. |
| 📁 `src/bin/` | Place for additional binaries, even in library projects. |
| {{ tab() }} `x.rs` | Additional binary, run with `cargo run --bin x`. |
| 📁 `tests/` | Integration tests go here, invoked via **`cargo test`**. Unit tests often stay in `src/` file. |
| `.rustfmt.toml` | In case you want to [**customize**](https://rust-lang.github.io/rustfmt/) how **`cargo fmt`** works. |
| `.clippy.toml` | Special configuration for certain [**clippy lints**](https://rust-lang.github.io/rust-clippy/master/index.html), utilized via **`cargo clippy`**  {{ esoteric() }} |
| `build.rs` |  **Pre-build script**, {{ link(url="https://doc.rust-lang.org/cargo/reference/build-scripts.html") }} useful when compiling C / FFI, ... |
| <code class="ignore-auto language-bash">Cargo.toml</code> | Main **project manifest**, {{ link(url="https://doc.rust-lang.org/cargo/reference/manifest.html") }} Defines dependencies, artifacts ... |
| <code class="ignore-auto language-bash">Cargo.lock</code> | Dependency details for reproducible builds; add to `git` for apps, not for libs. |
| `rust-toolchain.toml` |  Define **toolchain override**{{ link(url="https://rust-lang.github.io/rustup/overrides.html" )}} (channel, components, targets) for this project. |
</div>

<footnotes>

<sup>*</sup> stable 可以考虑 [Criterion](https://github.com/bheisler/criterion.rs).

</footnotes>


{{ tablesep() }}


**Minimal examples** for various entry points might look like:

<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-anatomy-1" name="tab-group-anatomy" checked>
<label for="tab-anatomy-1"><b>应用程序</b></label>
<panel><div>


<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```
// src/main.rs (默认应用程序入口点)

fn main() {
    println!("Hello, world!");
}
```

</div></div></div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-anatomy-2" name="tab-group-anatomy" >
<label for="tab-anatomy-2"><b>库</b></label>
<panel><div>

<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```
// src/lib.rs (默认库入口点)

pub fn f() {}      // 根下的公共条目，可被外部访问。

mod m {
    pub fn g() {}  // 根下非公开 (`m` 不公开)，
}                  // 所以 crate 外不可访问。
```
</div></div></div></panel></tab>





<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-anatomy-3" name="tab-group-anatomy" >
<label for="tab-anatomy-3"><b>Unit Tests</b></label>
<panel><div>

<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```
// src/my_module.rs (any file of your project)

fn f() -> u32 { 0 }

#[cfg(test)]
mod test {
    use super::f;           // Need to import items from parent module. Has
                            // access to non-public members.
    #[test]
    fn ff() {
        assert_eq!(f(), 0);
    }
}
```
</div></div></div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-anatomy-4" name="tab-group-anatomy" >
<label for="tab-anatomy-4"><b>Integration Tests</b></label>
<panel><div>

<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```
// tests/sample.rs (sample integration test)

#[test]
fn my_sample() {
    assert_eq!(my_crate::f(), 123); // Integration tests (and benchmarks) 'depend' to the crate like
}                                   // a 3rd party would. Hence, they only see public items.
```
</div></div></div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-anatomy-5" name="tab-group-anatomy" >
<label for="tab-anatomy-5"><b>Benchmarks</b></label>
<panel><div>


<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```
// benches/sample.rs (sample benchmark)

#![feature(test)]   // #[bench] is still experimental

extern crate test;  // Even in '18 this is needed ... for reasons.
                    // Normally you don't need this in '18 code.

use test::{black_box, Bencher};

#[bench]
fn my_algo(b: &mut Bencher) {
    b.iter(|| black_box(my_crate::f())); // `black_box` prevents `f` from being optimized away.
}
```
</div></div></div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-anatomy-6" name="tab-group-anatomy" >
<label for="tab-anatomy-6"><b>Build Scripts</b></label>
<panel><div>

<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```
// build.rs (sample pre-build script)

fn main() {
    // You need to rely on env. vars for target; `#[cfg(...)]` are for host.
    let target_os = env::var("CARGO_CFG_TARGET_OS");
}
```

<sup>*</sup>[See here for list](https://doc.rust-lang.org/cargo/reference/environment-variables.html#environment-variables-cargo-sets-for-build-scripts) of environment variables set.

</div></div></div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-anatomy-25" name="tab-group-anatomy" >
<label for="tab-anatomy-25"><b>Proc Macros</b>{{ esoteric() }}</label>
<panel><div>


<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```
// src/lib.rs (default entry point for proc macros)

extern crate proc_macro;  // Apparently needed to be imported like this.

use proc_macro::TokenStream;

#[proc_macro_attribute]   // Can now be used as `#[my_attribute]`
pub fn my_attribute(_attr: TokenStream, item: TokenStream) -> TokenStream {
    item
}
```


```
// Cargo.toml

[package]
name = "my_crate"
version = "0.1.0"

[lib]
proc-macro = true
```


</div></div></div></panel></tab>


</tabs>



{{ tablesep() }}


Module trees and imports:

<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-module-import-1" name="tab-group-module-import" checked>
<label for="tab-module-import-1"><b>Module Trees</b></label>
<panel><div>


<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

**Modules** {{ book(page="ch07-02-defining-modules-to-control-scope-and-privacy.html") }} {{ ex(page="mod.html#modules") }} {{ ref(page="items/modules.html#modules") }} and **source files** work as follows:

- **Module tree** needs to be explicitly defined, is **not** implicitly built from **file system tree**. {{ link(url="http://www.sheshbabu.com/posts/rust-module-system/") }}
- **Module tree root** equals library, app, &hellip; entry point (e.g., `lib.rs`).

Actual **module definitions** work as follows:
- A **`mod m {}`** defines module in-file, while **`mod m;`** will read `m.rs` or `m/mod.rs`.
- Path of `.rs` based on **nesting**, e.g., `mod a { mod b { mod c; }}}` is either `a/b/c.rs` or `a/b/c/mod.rs`.
- Files not pathed from module tree root via some `mod m;` won't be touched by compiler! {{ bad() }}

<!-- - **Visibility** of items (e.g., functions, fields) between modules governed by: "Is there visible path to item?"
    - Visibility like `pub fn f() {}` does not mean "`f` is public", but "`f` at most public if all parents public`. -->


</div></div></div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-module-import-2" name="tab-group-module-import">
<label for="tab-module-import-2"><b>Namespaces</b>{{ esoteric() }}</label>
<panel><div>


Rust has three kinds of **namespaces**:

<table>
    <thead>
        <tr>
            <th>Namespace <i>Types</i></th>
            <th>Namespace <i>Functions</i></th>
            <th>Namespace <i>Macros</i></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>mod X {}</code></td>
            <td><code>fn X() {}</code></td>
            <td><code>macro_rules! X { ... }</code></td>
        </tr>
        <tr>
            <td><code>X</code> (crate)</td>
            <td><code>const X: u8 = 1;</code></td>
            <td><code></code></td>
        </tr>
        <tr>
            <td><code>trait X {}</code></td>
            <td><code>static X: u8 = 1;</code></td>
            <td><code></code></td>
        </tr>
        <tr>
            <td><code>enum X {}</code></td>
            <td><code></code></td>
            <td><code></code></td>
        </tr>
        <tr>
            <td><code>union X {}</code></td>
            <td><code></code></td>
            <td><code></code></td>
        </tr>
        <tr>
            <td><code>struct X {}</code></td>
            <td><code></code></td>
            <td><code></code></td>
        </tr>
        <tr>
            <td colspan="2" style="text-align: center;"><code>struct X;</code><sup>1</sup></td>
            <td></td>
        </tr>
        <tr>
            <td colspan="2" style="text-align: center;"><code>struct X();</code><sup>1</sup></td>
            <td></td>
        </tr>
    </tbody>
</table>

<footnotes>

<sup>1</sup> Counts in <i>Types</i> and in <i>Functions</i>.

</footnotes>

- In any given scope, for example within a module, only one item item per namespace can exist, e.g.,
    - `enum X {}` and `fn X() {}` can coexist
    - `struct X;` and `const X` cannot coexist
- With a `use my_mod::X;` all items called `X` will be imported.

> Due to naming conventions (e.g., `fn` and `mod` are lowercase by convention) and _common sense_ (most developers just don't name all things `X`) you won't have to worry about these _kinds_ in most cases. They can, however, be a factor when designing macros.


</div></panel></tab>


</tabs>


{{ tablesep() }}



## Cargo

Commands and tools that are good to know.


<div class="color-header tooling">

| 命令 | 说明 |
|--------| ---- |
| `cargo init` | 基于最新的版本创建新项目。 |
| <code>cargo <span class="cargo-prefix">b</span>uild</code> | Build the project in debug mode (<code>--<span class="cargo-prefix">r</span>elease</code> for all optimization). |
| <code>cargo <span class="cargo-prefix">c</span>heck</code> | Check if project would compile (much faster). |
| <code>cargo <span class="cargo-prefix">t</span>est</code> | Run tests for the project. |
| <code>cargo <span class="cargo-prefix">d</span>oc --open</code> | Locally generate documentation for your code and dependencies. |
| <code>cargo <span class="cargo-prefix">r</span>un</code> | Run your project, if a binary is produced (main.rs). |
| {{ tab() }} `cargo run --bin b` | Run binary `b`. Unifies features with other dependents (can be confusing). |
| {{ tab() }} `cargo run -p w` | Run main of sub-workspace `w`. Treats features more as you would expect. |
| `cargo tree` | Show dependency graph. |
| <code>cargo +{nightly, stable} ...</code>  | Use given toolchain for command, e.g., for 'nightly only' tools. |
| `cargo +nightly ...` | Some nightly-only commands (substitute `...` with command below) |
| {{ tab() }}  <code>build -Z timings</code> | Show what crates caused your build to take so long, highly useful. {{ experimental() }} {{ hot() }} |
| {{ tab() }} `rustc -- -Zunpretty=expanded` |  Show expanded macros. {{ experimental() }} |
| `rustup doc` | Open offline Rust documentation (incl. the books), good on a plane! |

</div>

<footnotes>

Here <code>cargo <span class="cargo-prefix">b</span>uild</code> means you can either type `cargo build` or just `cargo b`; and <code>--<span class="cargo-prefix">r</span>elease</code> means it can be replaced with `-r`.

</footnotes>


{{ tablesep() }}


These are optional `rustup` components.
Install them with `rustup component add [tool]`.


<div class="color-header tooling">

| 工具 | 说明 |
|--------| ---- |
| `cargo clippy` | 额外([lints](https://rust-lang.github.io/rust-clippy/master/)) 检查通用 API 误用和非惯用代码。{{ link(url = "https://github.com/rust-lang/rust-clippy") }} |
| `cargo fmt` | 自动代码格式化。(`rustup component add rustfmt`) {{ link(url = "https://github.com/rust-lang/rustfmt") }} |

</div>

{{ tablesep() }}

更多 cargo 插件可以在[**这里**](https://crates.io/categories/development-tools::cargo-plugins?sort=downloads) 找到。


{{ tablesep() }}


## 交叉编译 {#cross-compilation}

<!-- <div class="steps"> -->

<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

🔘 检查[目标是否支持](https://forge.rust-lang.org/release/platform-support.html)。

🔘 安装目标依赖：**`rustup target install X`**。

🔘 安装本地工具链（取决于目标可能需要**链接**）。

应从目标供应商（Google、Apple 等）获取这些资源。也可能不支持本地宿主环境（比如，Windows 不支持 iOS 工具链）。

**某些工具链需要额外的构建步骤**（比如 Android 的 `make-standalone-toolchain.sh`）。

🔘 修改 **`~/cargo/.config`** 如下：

```
[target.aarch64-linux-android]
linker = "[PATH_TO_TOOLCHAIN]/aarch64-linux-android/bin/aarch64-linux-android-clang"
```

   或者

```
[target.aarch64-linux-android]
linker = "C:/[PATH_TO_TOOLCHAIN]/prebuilt/windows-x86_64/bin/aarch64-linux-android21-clang.cmd"
```

🔘 Set **environment variables** (optional, wait until compiler complains before setting):

```
set CC=C:\[PATH_TO_TOOLCHAIN]\prebuilt\windows-x86_64\bin\aarch64-linux-android21-clang.cmd
set CXX=C:\[PATH_TO_TOOLCHAIN]\prebuilt\windows-x86_64\bin\aarch64-linux-android21-clang.cmd
set AR=C:\[PATH_TO_TOOLCHAIN]\prebuilt\windows-x86_64\bin\aarch64-linux-android-ar.exe
...
```

Whether you set them depends on how compiler complains, not necessarily all are needed.

> Some platforms / configurations can be **extremely sensitive** how paths are specified (e.g., `\` vs `/`) and quoted.


✔️ Compile with **`cargo build --target=X`**


<!-- End overflow area -->
</div>
</div>

<!-- End steps  -->
<!-- </div> -->

{{ tablesep() }}




## Tooling Directives

Special tokens embedded in source code used by tooling or preprocessing.

<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-preprocessing-1" name="tab-group-preprocessing" checked>
<label for="tab-preprocessing-1"><b>Macros</b></label>
<panel><div class="color-header undefined-color-3">

<fixed-2-column class="color-header special_example">

<!-- Tool: **Preprocessor (Automatic)** -->


<!-- ```
macro_rules! my_macro {
    ($x:ty) => { ... }
}
``` -->

Inside a **declarative** {{ book(page="ch19-06-macros.html#declarative-macros-with-macro_rules-for-general-metaprogramming") }} **macro by example** {{book(page="ch19-06-macros.html")}} {{ex(page="macros.html#macro_rules")}} {{ref(page="macros-by-example.html")}} `macro_rules!` implementation these work:

| Within Macros |  Explanation |
|---------|---------|
| `$x:ty`  | Macro capture (here a type). |
| {{ tab() }} `$x:item`    | An item, like a function, struct, module, etc. |
| {{ tab() }} `$x:block`   | A block `{}` of statements or expressions, e.g., `{ let x = 5; }` |
| {{ tab() }} `$x:stmt`    | A statement, e.g., `let x = 1 + 1;`, `String::new();` or `vec![];` |
| {{ tab() }} `$x:expr`    | An expression, e.g., `x`, `1 + 1`, `String::new()` or `vec![]` |
| {{ tab() }} `$x:pat`     | A pattern, e.g., `Some(t)`, `(17, 'a')` or `_`. |
| {{ tab() }} `$x:ty`      | A type, e.g., `String`, `usize` or `Vec<u8>`. |
| {{ tab() }} `$x:ident`   | An identifier, for example in `let x = 0;` the identifier is `x`. |
| {{ tab() }} `$x:path`    | A path (e.g. `foo`, `::std::mem::replace`, `transmute::<_, int>`). |
| {{ tab() }} `$x:literal` | A literal (e.g. `3`, `"foo"`, `b"bar"`, etc.). |
| {{ tab() }} `$x:lifetime` | A lifetime (e.g. `'a`, `'static`, etc.). |
| {{ tab() }} `$x:meta`    | A meta item; the things that go inside `#[...]` and `#![...]` attributes. |
| {{ tab() }} `$x:vis`    | A visibility modifier;  `pub`, `pub(crate)`, etc. |
| {{ tab() }} `$x:tt`      | A single token tree, [see here](https://stackoverflow.com/a/40303308) for more details. |
| `$crate` | Special hygiene variable, crate where macros is defined. {{ todo() }} |

</fixed-2-column>

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-preprocessing-2" name="tab-group-preprocessing">
<label for="tab-preprocessing-2"><b>Documentation</b></label>
<panel><div class="color-header undefined-color-2">

<fixed-2-column  class="color-header special_example">

<!-- ```
/// Accepts an [`S`].
///
/// ```rust
///     f(s);
/// ```
``` -->

Inside a **doc comment** {{ book(page="ch14-02-publishing-to-crates-io.html#making-useful-documentation-comments") }} {{ ex(page="meta/doc.html#documentation") }} {{ ref(page="comments.html#doc-comments")}} these work:

| Within Doc Comments | Explanation |
|--------|-------------|
| ` ```...``` ` | Include a [**doc test**](https://doc.rust-lang.org/rustdoc/documentation-tests.html) (doc code running on `cargo test`). |
| ` ```X,Y ...``` ` | Same, and include optional configurations; with `X`, `Y` being ... |
| {{ tab() }} <code style="color: gray;">rust</code> | Make it explicit test is written in Rust; implied by Rust tooling. |
| {{ tab() }} <code style="color: gray; opacity: 0.3;">-</code> | Compile test. Run test. Fail if panic. **Default behavior**. |
| {{ tab() }} <code style="color: gray;">should_panic</code> | Compile test. Run test. Execution should panic. If not, fail test. |
| {{ tab() }} <code style="color: gray;">no_run</code> | Compile test. Fail test if code can't be compiled, Don't run test. |
| {{ tab() }} <code style="color: gray;">compile_fail</code> | Compile test but fail test if code _can_ be compiled. |
| {{ tab() }} <code style="color: gray;">ignore</code> | Do not compile. Do not run. Prefer option above instead. |
| {{ tab() }} <code style="color: gray;">edition2018</code> | Execute code as Rust '18; default is '15. |
| `#` | Hide line from documentation (` ```   # use x::hidden; ``` `). |
| <code>[&#96;S&#96;]</code> | Create a link to struct, enum, trait, function, &hellip; `S`. |
| <code>[&#96;S&#96;]&#40;crate::S&#41;</code> | Paths can also be used, in the form of markdown links. |


</fixed-2-column>


</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-preprocessing-7" name="tab-group-preprocessing">
<label for="tab-preprocessing-7"><b><code>#![globals]</code></b></label>
<panel><div class="color-header undefined-color-3">

<!-- ```
// Attributes usually found in toplevel project file.
#![no_std]
#![feature(xxx)]
``` -->
<fixed-3-column  class="color-header special_example">

Attributes affecting the whole crate or app:

| Opt-Out's   | On | Explanation |
|--------|---| ----------|
| `#![no_std]` | `C` | Don't (automatically) import **`std`**{{ std(page="std/") }} ; use **`core`**{{ std(page="core/") }} instead. {{ ref(page="names/preludes.html#the-no_std-attribute") }} |
| `#![no_implicit_prelude]` | `CM` | Don't add **`prelude`**{{ std(page="std/prelude/index.html") }}, need to manually import `None`, `Vec`, ... {{ ref(page="names/preludes.html#the-no_implicit_prelude-attribute") }} |
| `#![no_main]` |  `C` | Don't emit `main()` in apps if you do that yourself. {{ ref(page="crates-and-source-files.html#the-no_main-attribute") }}|

<!-- | `#![no_builtins]` | `C` | Does ... something ... probably important. {{ todo() }} {{ ref(page="attributes/codegen.html#the-no_builtins-attribute") }}| -->

{{ tablesep() }}

| Opt-In's   | On | Explanation |
|--------|---| ----------|
| `#![feature(a, b, c)]` | `C` | Rely on features that may never get stabilized, _c._ [**Unstable Book**](https://doc.rust-lang.org/unstable-book/the-unstable-book.html). {{ experimental() }} |

{{ tablesep() }}

| Builds | On | Explanation |
|--------|---| ----------|
| `#![windows_subsystem = "x"]` | `C` | On Windows, make a `console` or `windows` app. {{ ref(page="runtime.html#the-windows_subsystem-attribute") }} {{ esoteric() }} |
| `#![crate_name = "x"]` | `C`  | Specifiy current crate name, e.g., when not using `cargo`. {{ todo() }} {{ ref(page="crates-and-source-files.html#the-crate_name-attribute") }} {{ esoteric() }} |
| `#![crate_type = "bin"]` | `C`  | Specifiy current crate type (`bin`, `lib`, `dylib`, `cdylib`, ...). {{ ref(page="linkage.html") }} {{ esoteric() }} |
| `#![recursion_limit = "123"]` | `C` | Set _compile-time_ recursion limit for deref, macros, ... {{ ref(page="attributes/limits.html#the-recursion_limit-attribute") }} {{ esoteric() }} |
| `#![type_length_limit = "456"]` | `C` | Limits maximum number of type substitutions. {{ ref(page="attributes/limits.html#the-type_length_limit-attribute") }} {{ esoteric() }} |


{{ tablesep() }}

| Handlers | On | Explanation |
|--------|---|----------|
| `#[panic_handler]` | `F` | Make some `fn f(&PanicInfo) -> !` app's **panic handler**. {{ ref(page="runtime.html#the-panic_handler-attribute") }} |
| `#[global_allocator]` | `S` | Make static item impl. `GlobalAlloc` {{ std(page="alloc/alloc/trait.GlobalAlloc.html") }} **global allocator**. {{ ref(page="runtime.html#the-global_allocator-attribute") }}|


</fixed-3-column>


</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-preprocessing-4" name="tab-group-preprocessing">
<label for="tab-preprocessing-4"><b><code>#[code]</code></b></label>
<panel><div class="color-header undefined-color-3">

Attributes primarily governing emitted code:

<fixed-3-column  class="color-header special_example">

| Developer UX | On | Explanation |
|-------|---|-------------|
| `#[non_exhaustive]` | `T` | Future-proof `struct` or `enum`; hint it may grow in future. {{ ref(page="attributes/type_system.html#the-non_exhaustive-attribute") }}|
| `#[path = "x.rs"]` | `M` | Get module from non-standard file. {{ ref(page="items/modules.html#the-path-attribute") }}|

{{ tablesep() }}

| Codegen | On | Explanation |
|-------|---|-------------|
| `#[inline]` | `F` | Nicely suggest compiler should inline function at call sites. {{ ref(page="attributes/codegen.html#the-inline-attribute") }}|
| `#[inline(always)]` | `F` | Emphatically threaten compiler to inline call, or else. {{ ref(page="attributes/codegen.html#the-inline-attribute") }}|
| `#[inline(never)]` | `F` | Instruct compiler to feel disappointed if it still inlines the function. {{ ref(page="attributes/codegen.html#the-inline-attribute") }} |
| `#[cold]` | `F` | Hint that function probably isn't going to be called. {{ ref(page="codegen.html#the-cold-attribute") }}|
| `#[target_feature(enable="x")]` | `F` | Enable CPU feature (e.g., `avx2`) for code of `unsafe fn`. {{ ref(page="attributes/codegen.html#the-target_feature-attribute") }}|
| `#[track_caller]` | `F` | Allows `fn` to find **`caller`**{{ std(page="core/panic/struct.Location.html#method.caller") }} for better panic messages. {{ ref(page="attributes/codegen.html#the-track_caller-attribute") }}|
| `#[repr(X)]`<sup>1</sup>  | `T`  | Use another representation instead of the default **`rust`** {{ ref(page="type-layout.html#the-default-representation") }} one: |
| {{ tab() }} `#[repr(C)]` | `T`  | Use a C-compatible (f. FFI), predictable (f. `transmute`) layout. {{ ref(page="type-layout.html#the-c-representation") }}|
| {{ tab() }} `#[repr(C, u8)]` | `enum`  | Give `enum` discriminant the specified type. {{ ref(page="type-layout.html#the-c-representation") }}|
| {{ tab() }} `#[repr(transparent)]` | `T`  | Give single-element type same layout as contained field. {{ ref(page="type-layout.html#the-transparent-representation") }}|
| {{ tab() }} `#[repr(packed(1))]` | `T`  | Lower alignment of struct and contained fields, mildly UB prone. {{ ref(page="type-layout.html#the-alignment-modifiers") }}|
| {{ tab() }} `#[repr(align(8))]` | `T`  | Raise alignment of struct to given value, e.g., for SIMD types. {{ ref(page="type-layout.html#the-alignment-modifiers") }}|

<!-- {{ tablesep() }}

| Representation | On | Explanation |
|-------|---|-------------|
| `-` | `T`  | In absence of `#[repr]` the **`rust` representation** is used {{ ref(page="type-layout.html#the-default-representation") }} |
| `#[repr(C)]` | `T`  | Use a predictable, C-compatible representation. {{ ref(page="type-layout.html#the-c-representation") }}|
| `#[repr(C, u8)]` | `enum`  | Give `enum` discriminant the specified type. {{ ref(page="type-layout.html#the-c-representation") }}|
| `#[repr(transparent)]` | `T`  | Give single-element type same layout as contained field. {{ ref(page="type-layout.html#the-transparent-representation") }}|
| `#[repr(packed(1))]` | `T`  | Lower alignment of struct and contained fields, mildly UB prone. {{ ref(page="type-layout.html#the-alignment-modifiers") }}|
| `#[repr(align(8))]` | `T`  | Raise alignment of struct to given value, e.g., for SIMD types. {{ ref(page="type-layout.html#the-alignment-modifiers") }}| -->

<footnotes>

<sup>1</sup> Some representation modifiers can be combined, e.g., `#[repr(C, packed(1))]`.

</footnotes>

{{ tablesep() }}

| Linking | On | Explanation |
|-------|---|-------------|
| `#[no_mangle]` | `*` | Use item name directly as symbol name, instead of mangling.  {{ ref(page="abi.html#the-no_mangle-attribute") }}|
| `#[no_link]` | `X` | Don't link `extern crate` when only wanting macros. {{ ref(page="items/extern-crates.html#the-no_link-attribute") }}|
| `#[link(name="x", kind="y")]` | `X`  | Native lib to link against when looking up symbol. {{ ref(page="items/external-blocks.html#the-link-attribute") }}|
| `#[link_name = "foo"]` | `F`  | Name of symbol to search for resolving `extern fn`. {{ ref(page="items/external-blocks.html#the-link_name-attribute") }}|
| `#[link_section = ".sample"]` | `FS`  | Section name of object file where item should be placed. {{ ref(page="abi.html#the-link_section-attribute") }}|
| `#[export_name = "foo"]` | `FS` | Export a `fn` or `static` under a different name. {{ ref(page="abi.html#the-export_name-attribute") }}|
| `#[used]` | `S`  | Don't optimize away `static` variable despite it looking unused. {{ ref(page="abi.html#the-used-attribute") }}|



</fixed-3-column>

</div></panel></tab>




<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-preprocessing-3" name="tab-group-preprocessing">
<label for="tab-preprocessing-3"><b><code>#[quality]</code></b></label>
<panel><div class="color-header undefined-color-3">

Attributes used by Rust tools to improve code quality:

<fixed-3-column  class="color-header special_example">

| Code Patterns | On | Explanation |
|-------|---|-------------|
| `#[allow(X)]` | `*` | Instruct `rustc` / `clippy` to ... ignore class `X` of possible issues. {{ ref(page="attributes/diagnostics.html#lint-check-attributes") }} |
| `#[warn(X)]` <sup>1</sup> | `*` |  ... emit a warning, mixes well with `clippy` lints. {{ hot() }} {{ ref(page="attributes/diagnostics.html#lint-check-attributes") }} |
| `#[deny(X)]` <sup>1</sup> | `*` |  ... fail compilation. {{ ref(page="attributes/diagnostics.html#lint-check-attributes") }} |
| `#[forbid(X)]` <sup>1</sup> | `*` | ... fail compilation and prevent subsequent `allow` overrides. {{ ref(page="attributes/diagnostics.html#lint-check-attributes") }} |
| `#[deprecated = "msg"]` | `*` | Let your users know you made a design mistake. {{ ref(page="diagnostics.html#the-deprecated-attribute") }}|
| `#[must_use = "msg"]` | `FTX` |  Makes compiler check return value is _processed_ by caller. {{ hot() }} {{ ref(page="attributes/diagnostics.html#the-must_use-attribute") }}|

<footnotes>

<sup>1</sup> There is some debate which one is the _best_ to ensure high quality crates. Actively maintained multi-dev crates probably benefit from more aggressive `deny` or `forbid` lints; less-regularly updated ones probably more from conservative use of `warn` (as future compiler or `clippy` updates may suddenly break otherwise working code with minor issues).

</footnotes>

{{ tablesep() }}

</fixed-3-column>

<fixed-3-column  class="color-header special_example">

| Tests | On | Explanation |
|-------|---|-------------|
| `#[test]` | `F` | Marks the function as a test, run with `cargo test`. {{ hot() }} {{ ref(page="attributes/testing.html#the-test-attribute") }}|
| `#[ignore = "msg"]` | `F` | Compiles but does not execute some `#[test]` for now. {{ ref(page="attributes/testing.html#the-ignore-attribute") }}|
| `#[should_panic]` | `F` | Test must `panic!()` to actually succeed. {{ ref(page="attributes/testing.html#the-ignore-attribute") }}|
| `#[bench]` | `F` | Mark function in `bench/` as benchmark for `cargo bench`. {{ experimental() }} {{ ref(page="") }}|

{{ tablesep() }}


| Formatting | On | Explanation |
|-------|---|-------------|
| `#[rustfmt::skip]` |  `*` | Prevent `cargo fmt` from cleaning up item. {{ link(url="https://github.com/rust-lang/rustfmt") }}|
| `#![rustfmt::skip::macros(x)]` |  `CM` | ... from cleaning up macro `x`. {{ link(url="https://github.com/rust-lang/rustfmt") }}|
| `#![rustfmt::skip::attributes(x)]` |  `CM` | ... from cleaning up attribute `x`. {{ link(url="https://github.com/rust-lang/rustfmt") }}|

</fixed-3-column>

{{ tablesep() }}

<fixed-3-column class="color-header special_example extra-wide">


| Documentation | On | Explanation |
|-------|---|-------------|
| `#[doc = "Explanation"]` | `*` | Same as adding a `///` doc comment. {{ link(url="https://doc.rust-lang.org/rustdoc/the-doc-attribute.html") }} |
| `#[doc(alias = "other")]` | `*` | Provide another name users can search for in the docs. {{ link(url="https://github.com/rust-lang/rust/issues/50146") }} |
| `#[doc(hidden)]` | `*` | Prevent item from showing up in docs. {{ link(url="https://doc.rust-lang.org/rustdoc/the-doc-attribute.html#dochidden") }} |
| `#![doc(html_favicon_url = "")]` | `C` | Sets the `favicon` for the docs. {{ link(url="https://doc.rust-lang.org/rustdoc/the-doc-attribute.html#html_favicon_url") }}|
| `#![doc(html_logo_url  = "")]` | `C` | The logo used in the docs. {{ link(url="https://doc.rust-lang.org/rustdoc/the-doc-attribute.html#html_logo_url") }}|
| `#![doc(html_playground_url  = "")]` | `C` | Generates `Run` buttons and uses given service. {{ link(url="https://doc.rust-lang.org/rustdoc/the-doc-attribute.html#html_playground_url") }}|
| `#![doc(html_root_url  = "")]` | `C` | Base URL for links to external crates. {{ link(url="https://doc.rust-lang.org/rustdoc/the-doc-attribute.html#html_root_url") }}|
| `#![doc(html_no_source)]` | `C` | Prevents source from being included in docs. {{ link(url="https://doc.rust-lang.org/rustdoc/the-doc-attribute.html#html_no_source") }}|

<!-- | `#![doc(issue_tracker_base_url  = "")]` | `C` | Mostly for `std::`, where issue numbers link. {{ link(url="https://doc.rust-lang.org/rustdoc/the-doc-attribute.html#issue_tracker_base_url") }}| -->

</fixed-3-column>




</div></panel></tab>




<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-preprocessing-8" name="tab-group-preprocessing">
<label for="tab-preprocessing-8"><b><code>#[macros]</code></b></label>
<panel><div class="color-header undefined-color-3">

<fixed-3-column  class="color-header special_example">

Attributes related to the creation and use of macros:

| Macros By Example | On | Explanation |
|-------|---|-------------|
| `#[macro_export]` |  `!` | Export `macro_rules!` as `pub` on crate level {{ ref(page="macros-by-example.html#path-based-scope") }}|
| `#[macro_use]` | `MX` | Let macros persist past modules; or import from `extern crate`. {{ ref(page="macros-by-example.html#the-macro_use-attribute") }}|

{{ tablesep() }}

| Proc Macros | On | Explanation |
|-------|---|-------------|
| `#[proc_macro]` | `F`  | Mark `fn` as **function-like** procedural macro callable as `m!()`. {{ ref(page="procedural-macros.html#function-like-procedural-macros") }}|
| `#[proc_macro_derive(Foo)]` | `F`  | Mark `fn` as **derive macro** which can `#[derive(Foo)]`. {{ ref(page="procedural-macros.html#derive-macros") }}|
| `#[proc_macro_attribute]` | `F`  | Mark `fn` as **attribute macro** which can understand new `#[x]`. {{ ref(page="procedural-macros.html#attribute-macros") }}|

{{ tablesep() }}

| Derives | On | Explanation |
|-------|---|-------------|
| `#[derive(X)]` | `T` | Let some proc macro provide a goodish `impl` of `trait X`. {{ hot() }} {{ ref(page="") }}|

<!-- | `#[derive(Eq)]` |  | xxx{{ ref(page="") }}|
| `#[derive(PartialEq)]` | |  xxx|
| `#[derive(Ord)]` | |  xxx|
| `#[derive(PartialOrd)]` | |  xxx|
| `#[derive(Clone)]` | |  xxx|
| `#[derive(Copy)]` | |  xxx|
| `#[derive(Hash)]` | |  xxx|
| `#[derive(Default)]` | |  xxx|
| `#[derive(Debug)]` | |  xxx| -->


</fixed-3-column>


</div></panel></tab>






<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-preprocessing-5" name="tab-group-preprocessing">
<label for="tab-preprocessing-5"><b><code>#[cfg]</code></b></label>
<panel><div class="color-header undefined-color-3">

Attributes governing conditional compilation:

<fixed-3-column class="color-header special_example extra-wide">

| Config Attributes | On | Explanation |
|-------|---|-------------|
| `#[cfg(X)]` | `*` | Include item if configuration `X` holds. {{ ref(page="conditional-compilation.html#the-cfg-attribute") }}|
| `#[cfg(all(X, Y, Z))]` | `*` | Include item if all options hold. {{ ref(page="conditional-compilation.html#conditional-compilation") }}|
| `#[cfg(any(X, Y, Z))]` | `*` | Include item if at least one option holds. {{ ref(page="conditional-compilation.html#conditional-compilation") }}|
| `#[cfg(not(X))]` | `*` | Include item if `X` does not hold. {{ ref(page="conditional-compilation.html#conditional-compilation") }}|
| `#[cfg_attr(X, foo = "msg")]` | `*` | Apply `#[foo = "msg"]` if configuration `X` holds. {{ ref(page="conditional-compilation.html#the-cfg_attr-attribute") }}|

{{ tablesep() }}

> ⚠️ Note, options can generally be set multiple times, i.e., the same key can show up with multiple values. One can expect `#[cfg(target_feature = "avx")]` **and** `#[cfg(target_feature = "avx2")]` to be true at the same time.

{{ tablesep() }}

| Known Options | On | Explanation |
|-------|---|-------------|
| `#[cfg(target_arch = "x86_64")]` | `*` | The CPU architecture crate is compiled for. {{ ref(page="conditional-compilation.html#target_arch") }}|
| `#[cfg(target_feature = "avx")]` | `*` | Whether a particular class of instructions is available. {{ ref(page="conditional-compilation.html#target_feature") }}|
| `#[cfg(target_os = "macos")]` | `*` | Operating system your code will run on. {{ ref(page="conditional-compilation.html#target_os") }}|
| `#[cfg(target_family = "unix")]` | `*` | Family operating system belongs to. {{ ref(page="conditional-compilation.html#target_family") }}|
| `#[cfg(target_env = "msvc")]` | `*` | How DLLs and functions are interfaced with on OS. {{ ref(page="conditional-compilation.html#target_env") }}|
| `#[cfg(target_endian = "little")]` | `*` | Main reason your cool new zero-cost protocol fails. {{ ref(page="conditional-compilation.html#target_endian") }}|
| `#[cfg(target_pointer_width = "64")]` | `*` | How many bits pointers, `usize` and CPU words have. {{ ref(page="conditional-compilation.html#target_pointer_width") }}|
| `#[cfg(target_vendor = "apple")]` | `*` |  Manufacturer of target. {{ ref(page="conditional-compilation.html#target_vendor") }}|
| `#[cfg(debug_assertions)]` | `*` | Whether `debug_assert!()` and friends would panic. {{ ref(page="conditional-compilation.html#debug_assertions") }}|
| `#[cfg(proc_macro)]` | `*` | Wheter crate compiled as proc macro. {{ ref(page="conditional-compilation.html#proc_macro") }}|
| `#[cfg(test)]` | `*` | Whether compiled with `cargo test`. {{ hot() }} {{ ref(page="conditional-compilation.html#test") }}|
| `#[cfg(feature = "serde")]` | `*` | When your crate was compiled with feature `serde`. {{ hot() }} {{ ref(page="conditional-compilation.html#conditional-compilation") }}|

</fixed-3-column>



</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-preprocessing-6" name="tab-group-preprocessing">
<label for="tab-preprocessing-6"><b><code>build.rs</code></b></label>
<panel><div class="color-header undefined-color-3">

Environment variables and outputs related to the pre-build script.

<fixed-2-column class="color-header special_example extra-wide">

| Input Environment | Explanation {{ link(url="https://doc.rust-lang.org/cargo/reference/environment-variables.html") }} |
|-------|-------------|
| `CARGO_FEATURE_X` |  Environment variable set for each feature `x` activated.  |
| {{ tab() }} `CARGO_FEATURE_SERDE` |  If feature `serde` were enabled. |
| {{ tab() }} `CARGO_FEATURE_SOME_FEATURE` | If feature `some-feature` were enabled; dash `-` converted to `_`. |
| `CARGO_CFG_X` | Exposes cfg's; joins mult. opts. by `,` and converts `-` to `_`.|
| {{ tab() }} `CARGO_CFG_TARGET_OS=macos` |  If `target_os` were set to `macos`. |
| {{ tab() }} `CARGO_CFG_TARGET_FEATURE=avx,avx2` |  If `target_feature` were set to `avx` and `avx2`. |
| `OUT_DIR` |  Where output should be placed. |
| `TARGET` |  Target triple being compiled for. |
| `HOST` |  Host triple (running this build script). |
| `PROFILE` |  Can be `debug` or `release`. |

<footnotes>

Available in `build.rs` via `env::var()?`. List not exhaustive.

</footnotes>

</fixed-2-column>

<fixed-2-column class="color-header special_example extra-wide">

{{ tablesep() }}

| Output String | Explanation {{ link(url="https://doc.rust-lang.org/cargo/reference/build-scripts.html") }} |
|-------|-------------|
| `cargo:rerun-if-changed=PATH` | (Only) run this `build.rs` again if `PATH` changed. |
| `cargo:rerun-if-env-changed=VAR` | (Only) run this `build.rs` again if environment `VAR` changed. |
| `cargo:rustc-link-lib=[KIND=]NAME` | Link native library as if via `-l` option. |
| `cargo:rustc-link-search=[KIND=]PATH` | Search path for native library as if via `-L` option. |
| `cargo:rustc-flags=FLAGS` | Add special flags to compiler. {{ todo() }} |
| `cargo:rustc-cfg=KEY[="VALUE"]` | Emit given `cfg` option to be used for later compilation. |
| `cargo:rustc-env=VAR=VALUE ` | Emit var accessible via `env!()` in crate during compilation. |
| `cargo:rustc-cdylib-link-arg=FLAG ` | When building a `cdylib`, pass linker flag. |
| `cargo:warning=MESSAGE` | Emit compiler warning. |

<footnotes>

Emitted from `build.rs` via `println!()`. List not exhaustive.

</footnotes>

</fixed-2-column>

</div></panel></tab>


</tabs>


<footnotes>

For the _On_ column in attributes: <br>
`C` means on crate level (usually given as `#![my_attr]` in the top level file). <br>
`M` means on modules. <br>
`F` means on functions. <br>
`S` means on static. <br>
`T` means on types. <br>
`X` means something special. <br>
`!` means on macros. <br>
`*` means on almost any item. <br>

</footnotes>


---

# Working with Types


## Types, Traits, Generics

Allowing users to _bring their own types_ and avoid code duplication.

<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-types-1" name="tab-group-types" checked>
<label for="tab-types-1"><b>Types & Traits</b></label>
<panel><div>


<!-- Section -->
<generics-section id="ttg-types">
<header>Types</header>
<description>

<mini-zoo class="zoo">
    <entry>
        <type class="primitive"><code>u8</code></type>
    </entry>
    <entry>
        <type class="composed"><code>String</code></type>
    </entry>
    <entry>
        <type class="composed"><code>Device</code></type>
    </entry>
</mini-zoo>

- Set of values with given semantics, layout, &hellip;

<mini-table>

| Type |   Values |
| --- | --- |
| `u8`  |  <code>{ 0<sub>u8</sub>, 1<sub>u8</sub>, ..., 255<sub>u8</sub> }</code> |
| `char`  | `{ 'a', 'b', ... '🦀' }` |
| `struct S(u8, char)`  | <code>{ (0<sub>u8</sub>, 'a'), ... (255<sub>u8</sub>, '🦀') }</code> |

<subtitle>Sample types and sample values.</subtitle>

</mini-table>

</description>
</generics-section>


<!-- Section -->
<generics-section id="ttg-equivalence">
<header>Type Equivalence and Conversions</header>
<description>

<mini-zoo class="zoo">
    <entry>
        <type class="primitive"><code>u8</code></type>
    </entry>
    <entry>
        <type class="primitive"><code>&u8</code></type>
    </entry>
    <entry>
        <type class="primitive"><code>&mut u8</code></type>
    </entry>
    <entry>
        <type class="primitive"><code>[u8; 1]</code></type>
    </entry>
    <entry>
        <type class="composed"><code>String</code></type>
    </entry>
</mini-zoo>



<!-- - Question: which of the types above is different from all others?
    - Trick question: all of these types are totally different -->
- It may be obvious but &nbsp; `u8`, &nbsp;&nbsp; `&u8`, &nbsp;&nbsp; `&mut u8`, are entirely different from each other
- Any `t: T` only accepts values from exactly `T`, e.g.,
    - `f(0_u8)` can't be called with `f(&0_u8)`,
    - `f(&mut my_u8)` can't be called with `f(&my_u8)`,
    - `f(0_u8)` can't be called with `f(0_i8)`.

>  Yes, `0 != 0` (in a mathematical sense) when it comes to types! In a language sense, the operation  <code>==(0<sub>u8</sub>, 0<sub>u16</sub>)</code> just isn't defined to prevent happy little accidents.

<mini-table>

| Type | Values |
| --- | --- |
| `u8`  | <code>{ 0<sub>u8</sub>, 1<sub>u8</sub>, ..., 255<sub>u8</sub> }</code> |
| `u16`  | <code>{ 0<sub>u16</sub>, 1<sub>u16</sub>, ..., 65_535<sub>u16</sub> }</code> |
| `&u8`  | <code>{ 0xffaa<sub>&u8</sub>, 0xffbb<sub>&u8</sub>, ... }</code> |
| `&mut u8`  | <code>{ 0xffaa<sub>&mut u8</sub>, 0xffbb<sub>&mut u8</sub>, ... }</code> |

<subtitle>How values differ between types.</subtitle>

</mini-table>



- However, Rust might sometimes help to **convert between types**<sup>1</sup>
    - **casts** manually convert values of types, `0_i8 as u8`
    - **coercions**  {{ above(target="#language-sugar") }} automatically convert types if safe<sup>2</sup>, `let x: &u8 = &mut 0_u8;`




<footnotes>

<sup>1</sup> Casts and coercions convert values from one set (e.g., `u8`) to another (e.g., `u16`), possibly adding CPU instructions to do so; and in such differ from **subtyping**, which would imply type and subtype are part of the same set (e.g., `u8` being subtype of `u16` and `0_u8` being the same as `0_u16`) where such a conversion would be purely a compile time check. Rust does not use subtyping for regular types (and `0_u8` _does_ differ from `0_u16`) but sort-of for lifetimes. {{ link(url = "https://featherweightmusings.blogspot.com/2014/03/subtyping-and-coercion-in-rust.html") }}

<sup>2</sup> Safety here is not just physical concept (e.g., <code>&u8</code> can't be coerced to <code>&u128</code>), but also whether 'history has shown that such a conversion would lead to programming errors'.

</footnotes>

</description>
</generics-section>



<!-- Section -->
<generics-section id="ttg-impl-s">
<header>Implementations &mdash; <code>impl S { }</code></header>
<description>

<mini-zoo class="zoo">
    <entry>
        <type class="primitive"><code>u8</code></type>
        <impl><code>impl { ... }</code></impl>
    </entry>
    <entry>
        <type class="composed"><code>String</code></type>
        <impl><code>impl { ... }</code></impl>
    </entry>
    <entry>
        <type class="composed"><code>Port</code></type>
        <impl><code>impl { ... }</code></impl>
    </entry>
</mini-zoo>

```
impl Port {
    fn f() { ... }
}
```

- Types usually come with implementation, e.g., `impl Port {}`, behavior _related_ to type:
    - **associated functions** `Port::new(80)`
    - **methods** `port.close()`

> What's considered _related_ is more philosophical than technical, nothing (except good taste) would prevent a `u8::play_sound()` from happening.


</description>
</generics-section>


<!-- Section -->
<generics-section id="ttg-traits">
<header>Traits &mdash; <code>trait T { }</code></header>
<description>

<mini-zoo class="zoo">
    <entry>
        <trait-impl>⌾ <code>Copy</code></trait-impl>
    </entry>
    <entry>
        <trait-impl>⌾ <code>Clone</code></trait-impl>
    </entry>
    <entry>
        <trait-impl>⌾ <code>Sized</code></trait-impl>
    </entry>
    <entry>
        <trait-impl>⌾ <code>ShowHex</code></trait-impl>
    </entry>
</mini-zoo>

- **Traits** ...
    - are way to "abstract" behavior,
    - trait author declares semantically _this trait means X_,
    - other can implement ("subscribe to") that behavior for their type.
- Think about trait as "membership list" for types:


<mini-table>

<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th>Copy Trait</th></tr>
        <tr class="subheader"><th><code>Self</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>u8</code></td></tr>
        <tr><td><code>u16</code></td></tr>
        <tr><td><code>...</code></td></tr>
    </tbody>
</table>

</mini-table>

<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th>Clone Trait</th></tr>
        <tr class="subheader"><th><code>Self</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>u8</code></td></tr>
        <tr><td><code>String</code></td></tr>
        <tr><td><code>...</code></td></tr>
    </tbody>
</table>

</mini-table>

<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th>Sized Trait</th></tr>
        <tr class="subheader"><th><code>Self</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>char</code></td></tr>
        <tr><td><code>Port</code></td></tr>
        <tr><td><code>...</code></td></tr>
    </tbody>
</table>

</mini-table>

<subtitle>Traits as membership tables, <code>Self</code> refers to the type included.</subtitle>

</mini-table>


- **Whoever is part of that membership list will adhere to behavior of list.**
- Traits can also include associated methods, functions, ...

```
trait ShowHex {
    // Must be implemented according to documentation.
    fn as_hex() -> String;

    // Provided by trait author.
    fn print_hex() {}
}
```

<mini-zoo class="zoo">
    <entry>
        <trait-impl>⌾ <code>Copy</code></trait-impl>
    </entry>
</mini-zoo>

```
trait Copy { }
```

- Traits without methods often called **marker traits**.
- `Copy` is example marker trait, meaning _memory may be copied bitwise_.

<mini-zoo class="zoo">
    <entry>
        <trait-impl>⌾ <code>Sized</code></trait-impl>
    </entry>
</mini-zoo>


- Some traits entirely outside explicit control
- `Sized` provided by compiler for types with _known size_; either this is, or isn't


</description>
</generics-section>


<!-- Section -->
<generics-section id="xxx">
<header>Implementing Traits for Types &mdash; <code>impl T for S { }</code></header>
<description>


```
impl ShowHex for Port { ... }
```
- Traits are implemented for types 'at some point'.
- Implementation `impl A for B` add type `B` to the trait membership list:

<mini-table>

<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th>ShowHex Trait</th></tr>
        <tr class="subheader"><th><code>Self</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>Port</code></td></tr>
    </tbody>
</table>

</mini-table>
</mini-table>

- Visually, you can think of the type getting a "badge" for its membership:

<mini-zoo class="zoo">
    <entry>
        <type class="primitive"><code>u8</code></type>
        <impl><code>impl { ... }</code></impl>
        <trait-impl>⌾ <code>Sized</code></trait-impl>
        <trait-impl>⌾ <code>Clone</code></trait-impl>
        <trait-impl>⌾ <code>Copy</code></trait-impl>
    </entry>
    <entry>
        <type class="composed"><code>Device</code></type>
        <impl><code>impl { ... }</code></impl>
        <trait-impl>⌾ <code>Transport</code></trait-impl>
    </entry>
    <entry>
        <type class="composed"><code>Port</code></type>
        <impl><code>impl { ... }</code></impl>
        <trait-impl>⌾ <code>Sized</code></trait-impl>
        <trait-impl>⌾ <code>Clone</code></trait-impl>
        <trait-impl>⌾ <code>ShowHex</code></trait-impl>
    </entry>
</mini-zoo>

</description>
</generics-section>




<!-- Section -->
<generics-section id="xxx">
<header>Traits vs. Interfaces</header>
<description>


<mini-zoo class="zoo">
    <person>👩‍🦰</person>
    <entry>
        <trait-impl>⌾ <code>Eat</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>🧔</person>
    <entry>
        <type class="composed"><code>Venison</code></type>
        <trait-impl>⌾ <code>Eat</code></trait-impl>
    </entry>
</mini-zoo>


<mini-zoo class="zoo" style="margin-left: 10px; width: 130px;">
    <person></person>
    <entry>
        <code style="text-align:center; width: 100%;"></code>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>🎅</person>
    <entry>
        <code>venison.eat()</code>
    </entry>
</mini-zoo>

{{ tablesep() }}

**Interfaces**

- In **Java**, Alice creates interface `Eat`.
- When Bob authors `Venison`, he must decide if `Venison` implements `Eat` or not.
- In other words, all membership must be exhaustively declared during type definition.
- When using `Venison`, Santa can make use of behavior provided by `Eat`:

```
// Santa imports `Venison` to create it, can `eat()` if he wants.
import food.Venison;

new Venison("rudolph").eat();
```


{{ tablesep() }}
{{ tablesep() }}


<mini-zoo class="zoo">
    <person>👩‍🦰</person>
    <entry>
        <trait-impl>⌾ <code>Eat</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>🧔</person>
    <entry>
        <type class="composed"><code>Venison</code></type>
    </entry>
</mini-zoo>


<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>👩‍🦰</person> / <person>🧔</person>
    <entry>
        <type class="composed"><code>Venison</code></type>
        <code style="text-align:center; width: 100%;">+</code>
        <trait-impl>⌾ <code>Eat</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>🎅</person>
    <entry>
        <code>venison.eat()</code>
    </entry>
</mini-zoo>

{{ tablesep() }}

**Traits**

- In **Rust**, Alice creates trait `Eat`.
- Bob creates type `Venison` and decides not to implement `Eat` (he might not even know about `Eat`).
- Someone<sup>*</sup> later decides adding `Eat` to `Venison` would be a really good idea.
- When using `Venison` Santa must import `Eat` separately:

```
// Santa needs to import `Venison` to create it, and import `Eat` for trait method.
use food::Venison;
use tasks::Eat;

// Ho ho ho
Venison::new("rudolph").eat();
```

<footnotes>

<sup>*</sup> To prevent two persons from implementing `Eat` differently Rust limits that choice to either Alice or Bob; that is, an `impl Eat for Venison` may only happen in the crate of `Venison` or in the crate of `Eat`. For details see coherence. {{todo()}}

</footnotes>


</description>
</generics-section>


</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-types-2" name="tab-group-types">
<label for="tab-types-2"><b>Generics</b></label>
<panel><div>


<!-- Section -->
<generics-section id="xxx">
<header>Type Constructors &mdash; <code>Vec&lt;&gt;</code></header>
<description>

<mini-zoo class="zoo">
    <entry>
        <type class="composed"><code>Vec&lt;u8&gt;</code></type>
    </entry>
    <entry>
        <type class="composed"><code>Vec&lt;char&gt;</code></type>
    </entry>
</mini-zoo>

- `Vec<u8>` is type "vector of bytes"; `Vec<char>` is type "vector of chars", but what is `Vec<>`?

<mini-table>

| Construct |   Values |
| --- | --- |
| `Vec<u8>`  |  `{ [], [1], [1, 2, 3], ... }` |
| `Vec<char>`  |  `{ [], ['a'], ['x', 'y', 'z'], ... }` |
| `Vec<>`  |  - |

<subtitle>Types vs type constructors.</subtitle>

</mini-table>



<mini-zoo class="zoo">
    <entry>
        <type class="generic dotted"><code>Vec&lt;&gt;</code></type>
    </entry>
</mini-zoo>

- `Vec<>` is no type, does not occupy memory, can't even be translated to code.
- `Vec<>` is **type constructor**, a "template" or "recipe to create types"
    - allows 3<sup>rd</sup> party to construct concrete type via parameter,
    - only then would this `Vec<UserType>` become real type itself.

</description>
</generics-section>


<!-- Section -->
<generics-section id="xxx">
<header>Generic Parameters &mdash; <code>&lt;T&gt;</code></header>
<description>

<mini-zoo class="zoo">
    <entry>
        <type class="generic dotted"><code>Vec&lt;T&gt;</code></type>
    </entry>
    <entry>
        <type class="generic dotted"><code>[T; 128]</code></type>
    </entry>
    <entry>
        <type class="generic dotted"><code>&T</code></type>
    </entry>
    <entry>
        <type class="generic dotted"><code>&mut T</code></type>
    </entry>
    <entry>
        <type class="generic dotted"><code>S&lt;T&gt;</code></type>
    </entry>
</mini-zoo>

- Parameter for `Vec<>` often named `T` therefore `Vec<T>`.
- `T` "variable name for type" for user to plug in something specfic, `Vec<f32>`, `S<u8>`, &hellip;


<mini-table>

| Type Constructor |  Produces Family |
| --- | --- |
| `struct Vec<T> {}`  |  `Vec<u8>`, `Vec<f32>`, `Vec<Vec<u8>>`, ... |
| `[T; 128]`  |  `[u8; 128]`, `[char; 128]`, `[Port; 128]` ... |
| `&T`  |  `&u8`, `&u16`, `&str`,  ... |

<subtitle>Type vs type constructors.</subtitle>

</mini-table>


```
// S<> is type constructor with parameter T; user can supply any concrete type for T.
struct S<T> {
    x: T
}

// Within 'concrete' code an existing type must be given for T.
fn f() {
    let x: S<f32> = S::new(0_f32);
}

```

</description>
</generics-section>


<!-- Section -->
<generics-section id="xxx">
<header>Const Generics &mdash; <code>[T; N]</code> and <code>S&lt;const N: usize&gt;</code></header>
<description>

<mini-zoo class="zoo">
    <entry>
        <type class="generic dotted"><code>[T; n]</code></type>
    </entry>
    <entry>
        <type class="generic dotted"><code>S&lt;const N&gt;</code></type>
    </entry>
</mini-zoo>

- Some type constructors not only accept specific type, but also **specific constant**.
- `[T; n]` constructs array type holding `T` type `n` times.
- For custom types declared as `MyArray<T, const N: usize>`.

<mini-table>

| Type Constructor |  Produces Family |
| --- | --- |
| `[u8; N]`  |  `[u8; 0]`, `[u8; 1]`, `[u8; 2]`, ... |
| `struct S<const N: usize> {}`  |  `S<1>`, `S<6>`, `S<123>`,  ... |

<subtitle>Type constructors based on constant.</subtitle>

</mini-table>


```
let x: [u8; 4]; // "array of 4 bytes"
let y: [f32; 16]; // "array of 16 floats"

// `MyArray` is type constructor requiring concrete type `T` and
// concrete usize `N` to construct specific type.
struct MyArray<T, const N: usize> {
    data: [T; N],
}
```

</description>
</generics-section>


<!-- Section -->
<!-- <generics-section id="xxx">
<header>Generics in Types</header>
<description>

</description>
</generics-section> -->




<!-- Section -->
<generics-section id="xxx">
<header>Bounds (Simple) &mdash; <code>where T: X</code></header>
<description>

<mini-zoo class="zoo">
    <person>🧔</person>
    <entry>
        <type class="generic dotted"><code>Num&lt;T&gt;</code></type>
    </entry>
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
    <person>🎅</person>
    <entry>
        <type class="composed"><code>Num&lt;u8&gt;</code></type>
    </entry>
    <entry>
        <type class="composed"><code>Num&lt;f32&gt;</code></type>
    </entry>
    <entry>
        <type class="composed"><code>Num&lt;Cmplx&gt;</code></type>
    </entry>
    <narrow-entry>
        <code style="text-align:center; width: 50px;">&nbsp;</code>
    </narrow-entry>
    <entry class="">
        <type class="primitive"><code>u8</code></type>
        <trait-impl>⌾ <code>Absolute</code></trait-impl>
        <trait-impl>⌾ <code>Dim</code></trait-impl>
        <trait-impl>⌾ <code>Mul</code></trait-impl>
    </entry>
    <entry class="grayed">
        <type class="composed"><code>Port</code></type>
        <trait-impl>⌾ <code>Clone</code></trait-impl>
        <trait-impl>⌾ <code>ShowHex</code></trait-impl>
    </entry>
</mini-zoo>

- If `T` can be any type, how can we _reason_ about (write code) for such a `Num<T>`?
- Parameter **bounds**:
    - limit what types (**trait bound**) or values (**const bound** {{ todo() }}) allowed,
    - we now can make use of these limits!
- Trait bounds act as "membership check":

<mini-table>

<div style="display: inline-block;">

```
// Type can only be constructed for some `T` if that
// T is part of `Absolute` membership list.
struct Num<T> where T: Absolute {
    ...
}

```

</div>


<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th>Absolute Trait</th></tr>
        <tr class="subheader"><th><code>Self</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>u8</code></td></tr>
        <tr><td><code>u16</code></td></tr>
        <tr><td><code>...</code></td></tr>
    </tbody>
</table>

</mini-table>
</mini-table>


<!--
// Constant `N` must be `usize`
struct Arrayf32<const N: usize> {
    data: [f32; N],
} -->

<footnotes>

We add bounds to the struct here. In practice it's nicer add bounds to the respective impl blocks instead, see later this section.

</footnotes>

<!-- > Note to self, is `const N: usize` a "const bound"? It seemingly acts as one, limiting the choice of values for N (albeit to specific types only). -->

</description>
</generics-section>


<!-- Section -->
<generics-section id="xxx">
<header>Bounds (Compound) &mdash; <code>where T: X + Y</code></header>
<description>

<mini-zoo class="zoo">
    <entry class="grayed">
        <type class="primitive"><code>u8</code></type>
        <trait-impl>⌾ <code>Absolute</code></trait-impl>
        <trait-impl>⌾ <code>Dim</code></trait-impl>
        <trait-impl>⌾ <code>Mul</code></trait-impl>
    </entry>
    <entry class="grayed">
        <type class="primitive"><code>f32</code></type>
        <trait-impl>⌾ <code>Absolute</code></trait-impl>
        <trait-impl>⌾ <code>Mul</code></trait-impl>
    </entry>
    <entry class="grayed">
        <type class="primitive"><code>char</code></type>
    </entry>
    <entry>
        <type class="composed"><code>Cmplx</code></type>
        <trait-impl>⌾ <code>Absolute</code></trait-impl>
        <trait-impl>⌾ <code>Dim</code></trait-impl>
        <trait-impl>⌾ <code>Mul</code></trait-impl>
        <trait-impl>⌾ <code>DirName</code></trait-impl>
        <trait-impl>⌾ <code>TwoD</code></trait-impl>
    </entry>
    <entry class="grayed">
        <type class="composed"><code>Car</code></type>
        <trait-impl>⌾ <code>DirName</code></trait-impl>
    </entry>
</mini-zoo>



```
struct S<T>
where
    T: Absolute + Dim + Mul + DirName + TwoD
{ ... }
```

- Long trait bounds can look intimidating.
- In practice, each `+ X` addition to a bound merely cuts down space of eligible types.

</description>
</generics-section>



<!-- Section -->
<generics-section id="xxx">
<header>Implementing Families &mdash; <code>impl&lt;&gt;</code></header>
<description>

{{ tablesep() }}

When we write:
```
impl<T> S<T> where T: Absolute + Dim + Mul {
    fn f(&self, x: T) { ... };
}
```
It can be read as:
- here is an implementation recipe for any type `T` (the `impl <T>` part),
- where<!--sup>*</sup--> that type must be member of the `Absolute + Dim + Mul` traits,
- you may add an implementation block to `S<T>`,
- containing the methods ...

You can think of such `impl<T> ... {} ` code as **abstractly implementing a family of behaviors**. Most notably, they allow 3<sup>rd</sup> parties to transparently materialize implementations similarly to how type constructors materialize types:

```
// If compiler encounters this, it will
// - check `0` and `x` fulfill the membership requirements of `T`
// - create two new version of `f`, one for `char`, another one for `u32`.
// - based on "family implementation" provided
s.f(0_u32);
s.f('x');
```


</description>
</generics-section>


<!-- Section -->
<generics-section id="xxx">
<header>Blanket Implementations &mdash; <code>impl&lt;T&gt X for T { ... }</code></header>
<description>

{{ tablesep() }}

Can also write "family implementations" so they apply trait to many types:

```
// Also implements Serialize for any type if that type already implements ToHex
impl<T> Serialize for T where T: ToHex { ... }
```

These are called **blanket implementations**.

<mini-table>

<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th>ToHex</th></tr>
        <tr class="subheader"><th><code>Self</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>Port</code></td></tr>
        <tr><td><code>Device</code></td></tr>
        <tr><td><code>...</code></td></tr>
    </tbody>
</table>

</mini-table>

<div style="display: inline-block; width: 100px;">

→  Whatever was in left table, may be added to right table, based on the following recipe (`impl`) →

</div>

<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th>Serialize Trait</th></tr>
        <tr class="subheader"><th><code>Self</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>u8</code></td></tr>
        <tr><td><code>Port</code></td></tr>
        <tr><td><code>...</code></td></tr>
    </tbody>
</table>

</mini-table>

</mini-table>


They can be neat way to give foreign types functionality in a modular way if they just implement another interface.

</description>
</generics-section>


</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-types-3" name="tab-group-types">
<label for="tab-types-3"><b>Advanced Concepts</b>{{ esoteric() }}</label>
<panel><div>


<!-- Section -->
<!-- <generics-section id="xxx">
<header>Pseudo-Specialization</header>
<description>

</description>
</generics-section> -->




<!-- Section -->
<generics-section id="xxx">
<header>Trait Parameters &mdash; <code>Trait&lt;In&gt; { type Out; } </code></header>
<description>

{{ tablesep() }}

Notice how some traits can be "attached" multiple times, but others just once?

<mini-zoo class="zoo">
    <entry style="left:300px; top: 25px;">
        <type class="composed"><code>Port</code></type>
        <trait-impl class="">⌾ <code>From&lt;u8&gt;</code></trait-impl>
        <trait-impl class="">⌾ <code>From&lt;u16&gt;</code></trait-impl>
    </entry>
    <entry style="left:400px; top: 25px;">
        <type class="composed"><code>Port</code></type>
        <trait-impl class="">⌾ <code>Deref</code></trait-impl>
        <associated-type class="grayed"><code>type u8;</code></associated-type>
    </entry>
</mini-zoo>

<!--
<mini-zoo class="zoo">
    <entry>
        <trait-impl class="">⌾ <code>A&lt;T&gt;</code></trait-impl>
    </entry>
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
    <entry>
        <trait-impl class="">⌾ <code>A&lt;u8&gt;</code></trait-impl>
    </entry>
    <entry>
        <trait-impl class="">⌾ <code>A&lt;f32&gt;</code></trait-impl>
    </entry>
    <entry>
        <trait-impl class="">⌾ <code>A&lt;str&gt;</code></trait-impl>
    </entry>
</mini-zoo>

<br>

<mini-zoo class="zoo">
    <entry>
        <trait-impl class="">⌾ <code>B</code></trait-impl>
        <associated-type class=""><code>type T;</code></associated-type>
    </entry>
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
    <entry>
        <trait-impl class="">⌾ <code>B</code></trait-impl>
        <associated-type class=""><code>T = u8;</code></associated-type>
    </entry>
</mini-zoo> -->

<br>

{{ tablesep() }}

Why is that?

- Traits themselves can be generic over two **kinds of parameters**:
    - `trait From<I> {}`
    - `trait Deref { type O; }`
- Remember we said traits are "membership lists" for types and called the list `Self`?
- Turns out, parameters `I` (for **input**) and `O` (for **output**) are just more _columns_ to that trait's list:

```
impl From<u8> for u16 {}
impl From<u16> for u32 {}
impl Deref for Port { type O = u8; }
impl Deref for String { type O = str; }
```


<mini-table>

<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th colspan="2">From</th></tr>
        <tr class="subheader"><th><code>Self</code></th><th><code>I</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>u16</code></td><td><code>u8</code></td></tr>
        <tr><td><code>u32</code></td><td><code>u16</code></td></tr>
        <tr><td colspan="2"><code>...</code></td></tr>
    </tbody>
</table>

</mini-table>


<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th colspan="2">Deref</th></tr>
        <tr class="subheader"><th><code>Self</code></th><th><code>O</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>Port</code></td><td><code>u8</code></td></tr>
        <tr><td><code>String</code></td><td><code>str</code></td></tr>
        <tr><td colspan="2"><code>...</code></td></tr>
    </tbody>
</table>

</mini-table>

<subtitle>Input and output parameters.</subtitle>

</mini-table>


Now here's the twist,
- **any output `O` parameters must be uniquely determined by input parameters `I`**,
- (in the same way as a relation `X Y` would represent a function),
- `Self` counts as an input.

A more complex example:

```
trait Complex<I1, I2> {
    type O1;
    type O2;
}
```

- this creates a relation relation of types named `Complex`,
- with 3 inputs (`Self` is always one) and 2 outputs, and it holds `(Self, I1, I2) => (O1, O2)`

<mini-table>

<table>
    <thead>
        <tr style=""><th colspan="5">Complex</th></tr>
        <tr class="subheader"><th><code>Self [I]</code></th><th><code>I1</code></th><th><code>I2</code></th><th><code>O1</code></th><th><code>O2</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>Player</code></td><td><code>u8</code></td><td><code>char</code></td><td><code>f32</code></td><td><code>f32</code></td></tr>
        <tr><td><code>EvilMonster</code></td><td><code>u16</code></td><td><code>str</code></td><td><code>u8</code></td><td><code>u8</code></td></tr>
        <tr><td><code>EvilMonster</code></td><td><code>u16</code></td><td><code>String</code></td><td><code>u8</code></td><td><code>u8</code></td></tr>
        <tr><td><code>NiceMonster</code></td><td><code>u16</code></td><td><code>String</code></td><td><code>u8</code></td><td><code>u8</code></td></tr>
        <tr><td><code>NiceMonster</code><sup>{{ bad() }}</sup></td><td><code>u16</code></td><td><code>String</code></td><td><code>u8</code></td><td><code>u16</code></td></tr>
    </tbody>
</table>

<subtitle>Various trait implementations. The last one is not valid as `(NiceMonster, u16, String)` has <br> already uniquely determined the outputs.</subtitle>

</mini-table>

</description>
</generics-section>



<!-- Section -->
<generics-section id="xxx">
<header>Trait Authoring Considerations (Abstract)</header>
<description>

<mini-zoo class="zoo">
    <person>👩‍🦰</person>
    <entry>
        <trait-impl class="dotted">⌾ <code>A&lt;I&gt;</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>🧔</person>
    <entry>
        <type class="composed"><code>Car</code></type>
    </entry>
</mini-zoo>


<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>👩‍🦰</person> / <person>🧔</person>
    <entry>
        <type class="composed"><code>Car</code></type>
        <trait-impl class="dotted">⌾ <code>A&lt;I&gt;</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>🎅</person>
    <entry>
        <code>car.a(0_u8)</code>
        <code>car.a(0_f32)</code>
    </entry>
</mini-zoo>

<br>

<mini-zoo class="zoo">
    <person>👩‍🦰</person>
    <entry>
        <trait-impl class="">⌾ <code>B</code></trait-impl>
        <associated-type class=""><code>type O;</code></associated-type>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>🧔</person>
    <entry>
        <type class="composed"><code>Car</code></type>
    </entry>
</mini-zoo>


<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>👩‍🦰</person> / <person>🧔</person>
    <entry>
        <type class="composed"><code>Car</code></type>
        <trait-impl class="">⌾ <code>B</code></trait-impl>
        <associated-type class=""><code>T = u8;</code></associated-type>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>🎅</person>
    <entry>
        <code>car.b(0_u8)</code>
        <code style="text-decoration: line-through;">car.b(0_f32)</code>
    </entry>
</mini-zoo>

- Parameter choice (input vs. output) also determines who may be allowed to add members:
    - `I` parameters allow "familes of implementations" be forwarded to user (Santa),
    - `O` parameters must be determined by trait implementor (Alice or Bob).

```
trait A<I> { }
trait B { type O; }

// Implementor adds (X, u32) to A.
impl A<u32> for X { }

// Implementor adds family impl. (X, ...) to A, user can materialze.
impl<T> A<T> for Y { }

// Implementor must decide specific entry (X, O) added to B.
impl B for X { type O = u32; }
```



<mini-table>

<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th colspan="2">A</th></tr>
        <tr class="subheader"><th><code>Self</code></th><th><code>I</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>X</code></td><td><code>u32</code></td></tr>
        <tr><td><code>Y</code></td><td><code>...</code></td></tr>
    </tbody>
</table>

<subtitle>Santa may add more members by providing his own type for <code>T</code>.</subtitle>

</mini-table>


<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th colspan="2">B</th></tr>
        <tr class="subheader"><th><code>Self</code></th><th><code>O</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>Player</code></td><td><code>String</code></td></tr>
        <tr><td><code>X</code></td><td><code>u32</code></td></tr>
    </tbody>
</table>

<subtitle>For given set of inputs (here <code>Self</code>), implementor must pre-select <code>O</code>.</subtitle>

</mini-table>

</mini-table>


</description>
</generics-section>


<!-- Section -->
<generics-section id="trait-authoring-examples">
<header>Trait Authoring Considerations (Example)</header>
<description>

<mini-zoo class="zoo">
    <entry>
        <trait-impl class="">⌾ <code>Query</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <narrow-entry>
        <code style="text-align:center; width: 100%;">vs.</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo">
    <entry>
        <trait-impl class="dotted">⌾ <code>Query&lt;I&gt;</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <narrow-entry>
        <code style="text-align:center; width: 100%;">vs.</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo">
    <entry>
        <trait-impl class="">⌾ <code>Query</code></trait-impl>
        <associated-type class=""><code>type O;</code></associated-type>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <narrow-entry>
        <code style="text-align:center; width: 100%;">vs.</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo">
    <entry>
        <trait-impl class="dotted">⌾ <code>Query&lt;I&gt;</code></trait-impl>
        <associated-type class=""><code>type O;</code></associated-type>
    </entry>
</mini-zoo>



{{ tablesep() }}

Choice of parameters goes along with purpose trait has to fill.

<hr>


**No Additional Parameters**

```
trait Query {
    fn search(&self, needle: &str);
}

impl Query for PostgreSQL { ... }
impl Query for Sled { ... }

postgres.search("SELECT ...");
```

<mini-zoo class="zoo">
    <person>👩‍🦰</person>
    <entry>
        <trait-impl class="">⌾ <code>Query</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo">
    <person>🧔</person>
    <entry>
        <type class="composed"><code>PostgreSQL</code></type>
        <trait-impl class="">⌾ <code>Query</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <entry>
        <type class="composed"><code>Sled</code></type>
        <trait-impl class="">⌾ <code>Query</code></trait-impl>
    </entry>
</mini-zoo>

{{ tablesep() }}

Trait author assumes:
- neither implementor nor user need to customize API.

{{ tablesep() }}

<hr>

**Input Parameters**

```
trait Query<I> {
    fn search(&self, needle: I);
}

impl Query<&str> for PostgreSQL { ... }
impl Query<String> for PostgreSQL { ... }
impl<T> Query<T> for Sled where T: ToU8Slice { ... }

postgres.search("SELECT ...");
postgres.search(input.to_string());
sled.search(file);
```

<mini-zoo class="zoo">
    <person>👩‍🦰</person>
    <entry>
        <trait-impl class="dotted">⌾ <code>Query&lt;I&gt;</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo">
    <person>🧔</person>
    <entry>
        <type class="composed"><code>PostgreSQL</code></type>
        <trait-impl class="">⌾ <code>Query&lt;&str&gt;</code></trait-impl>
        <trait-impl class="">⌾ <code>Query&lt;String&gt;</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <entry>
        <type class="composed"><code>Sled</code></type>
        <trait-impl class="dotted">⌾ <code>Query&lt;T&gt;</code></trait-impl>
        <note><span style="margin-left: 10px; display: inline-block; transform: rotate(90deg); font-size: 100%">↲</span> where <code>T</code> is <code>ToU8Slice</code>.</note>
    </entry>
</mini-zoo>


{{ tablesep() }}

Trait author assumes:
- implementor would customize API in multiple ways for same `Self` type,
- users may want ability to decide for which `I`-types behavior should be possible.

{{ tablesep() }}


<hr>


**Output Parameters**

```
trait Query {
    type O;
    fn search(&self, needle: Self::O);
}

impl Query for PostgreSQL { type O = String; ...}
impl Query for Sled { type O = Vec<u8>; ... }

postgres.search("SELECT ...".to_string());
sled.search(vec![0, 1, 2, 4]);
```

<mini-zoo class="zoo">
    <person>👩‍🦰</person>
    <entry>
        <trait-impl class="">⌾ <code>Query</code></trait-impl>
        <associated-type class=""><code>type O;</code></associated-type>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo">
    <person>🧔</person>
    <entry>
        <type class="composed"><code>PostgreSQL</code></type>
        <trait-impl class="">⌾ <code>Query</code></trait-impl>
        <associated-type class=""><code>O = String;</code></associated-type>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <entry>
        <type class="composed"><code>Sled</code></type>
        <trait-impl class="">⌾ <code>Query</code></trait-impl>
        <associated-type class=""><code>O = Vec&lt;u8&gt;;</code></associated-type>
    </entry>
</mini-zoo>


{{ tablesep() }}

Trait author assumes:
- implementor would customize API for `Self` type (but in only one way),
- users do not need, or should not have, ability to influence customization for specific `Self`.

> As you can see here, the term **input** or **output** does **not** (necessarily) have anything to do with whether `I` or `O` are inputs or outputs to an actual function!

{{ tablesep() }}

<hr>

**Multiple In- and Output Parameters**

```
trait Query<I> {
    type O;
    fn search(&self, needle: I) -> Self::O;
}

impl Query<&str> for PostgreSQL { type O = String; ... }
impl Query<CString> for PostgreSQL { type O = CString; ... }
impl<T> Query<T> for Sled where T: ToU8Slice { type O = Vec<u8>; ... }

postgres.search("SELECT ...").to_uppercase();
sled.search(&[1, 2, 3, 4]).pop();
```

<mini-zoo class="zoo">
    <person>👩‍🦰</person>
    <entry>
        <trait-impl class="dotted">⌾ <code>Query&lt;I&gt;</code></trait-impl>
        <associated-type class=""><code>type O;</code></associated-type>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo">
    <person>🧔</person>
    <entry>
        <type class="composed"><code>PostgreSQL</code></type>
        <trait-impl class="">⌾ <code>Query&lt;&str&gt;</code></trait-impl>
        <associated-type class=""><code>O = String;</code></associated-type>
        <trait-impl class="">⌾ <code>Query&lt;CString&gt;</code></trait-impl>
        <associated-type class=""><code>O = CString;</code></associated-type>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <entry>
        <type class="composed"><code>Sled</code></type>
        <trait-impl class="dotted">⌾ <code>Query&lt;T&gt;</code></trait-impl>
        <associated-type class=""><code>O = Vec&lt;u8&gt;;</code></associated-type>
        <note><span style="margin-left: 10px; display: inline-block; transform: rotate(90deg); font-size: 100%">↲</span> where <code>T</code> is <code>ToU8Slice</code>.</note>
    </entry>
</mini-zoo>


{{ tablesep() }}

Like examples above, in particular trait author assumes:
- users may want ability to decide for which `I`-types ability should be possible,
- for given inputs, implementor should determine resulting output type.


</description>
</generics-section>



<!-- Section -->
<generics-section id="xxx">
<header>Dynamic / Zero Sized Types</header>
<description>

<mini-zoo class="zoo" style="">
    <entry>
        <type class="composed"><code>MostTypes</code></type>
        <trait-impl>⌾ <code>Sized</code></trait-impl>
        <note>Normal types.</note>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <narrow-entry style="width: 60px;">
        <code style="text-align:center; width: 100%;">vs.</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo" style="">
    <entry>
        <type class="zero"><code>Z</code></type>
        <trait-impl>⌾ <code>Sized</code></trait-impl>
        <note>Zero sized.</note>
    </entry>
</mini-zoo>


<mini-zoo class="zoo">
    <narrow-entry style="width: 60px;">
        <code style="text-align:center; width: 100%;">vs.</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo" style="">
    <entry>
        <type class="primitive"><code>str</code></type>
        <trait-impl class="grayed">⌾ <code style="text-decoration: line-through">Sized</code></trait-impl>
        <note>Dynamically sized.</note>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="">
    <entry>
        <type class="primitive"><code>[u8]</code></type>
        <trait-impl class="grayed">⌾ <code style="text-decoration: line-through">Sized</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="">
    <entry>
        <type class="primitive"><code>dyn Trait</code></type>
        <trait-impl class="grayed">⌾ <code style="text-decoration: line-through">Sized</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="">
    <entry>
        <type class="primitive"><code>...</code></type>
        <trait-impl class="grayed">⌾ <code style="text-decoration: line-through">Sized</code></trait-impl>
    </entry>
</mini-zoo>


- A type `T` is **`Sized`** {{ std(page="std/marker/trait.Sized.html") }} if at compile time it is known how many bytes it occupies, `u8` and `&[u8]` are, `[u8]` isn't.
- Being `Sized` means `impl Sized for T {}` holds. Happens automatically and cannot be user impl'ed.
- Types not `Sized` are called **dynamically sized types** {{ book(page="ch19-04-advanced-types.html#dynamically-sized-types-and-the-sized-trait") }} {{ nom(page="exotic-sizes.html#dynamically-sized-types-dsts") }}  {{ ref(page="dynamically-sized-types.html#dynamically-sized-types") }} (DSTs), sometimes **unsized**.
- Types without data are called **zero sized types** {{ nom(page="exotic-sizes.html#zero-sized-types-zsts") }} (ZSTs), do not occupy space.

<div class="color-header sized cheats">

| 示例 | 说明 |
|---------|-------------|
| `struct A { x: u8 }` | Type `A` is sized, i.e., `impl Sized for A` holds, this is a 'regular' type. |
| `struct B { x: [u8] }` | Since `[u8]` is a DST, `B` in turn becomes DST, i.e., does not `impl Sized`. |
| `struct C<T> { x: T }` | Type params **have** implicit `T: Sized` bound, e.g., `C<A>` is valid, `C<B>` is not. |
| `struct D<T: ?Sized> { x: T }` | Using **`?Sized`** {{ ref(page="trait-bounds.html#sized") }} allows opt-out of that bound, i.e., `D<B>` is also valid. |
| `struct E;` | Type `E` is zero-sized (and also sized) and will not consume memory. |
| `trait F { fn f(&self); }` | Traits **do not have** an implicit `Sized` bound, i.e., `impl F for B {}` is valid.  |
| {{ tab() }} `trait F: Sized {}` | Traits can however opt into `Sized` via supertraits.{{ above(target="#functions-behavior") }} |
| `trait G { fn g(self); }` | For `Self`-like params DST `impl` may still fail as params can't go on stack.  |

</div>


</description>
</generics-section>


<!-- Section -->
<generics-section id="xxx">
<header><code>?Sized</code></header>
<description>


<mini-zoo class="zoo">
    <entry>
        <type class="generic dotted"><code>S&lt;T&gt;</code></type>
    </entry>
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
    <entry>
        <type class="composed"><code>S&lt;u8&gt;</code></type>
    </entry>
    <entry>
        <type class="composed"><code>S&lt;char&gt;</code></type>
    </entry>
    <entry>
        <type class="composed grayed"><code>S&lt;str&gt;</code></type>
    </entry>
</mini-zoo>

```
struct S<T> { ... }
```

- `T` can be any concrete type.
- However, there exists invisible default bound `T: Sized`, so `S<str>` is not possible out of box.
- Instead we have to add `T : ?Sized` to opt-out of that bound:

<mini-zoo class="zoo">
    <entry>
        <type class="generic dotted"><code>S&lt;T&gt;</code></type>
    </entry>
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
    <entry>
        <type class="composed"><code>S&lt;u8&gt;</code></type>
    </entry>
    <entry>
        <type class="composed"><code>S&lt;char&gt;</code></type>
    </entry>
    <entry>
        <type class="composed"><code>S&lt;str&gt;</code></type>
    </entry>
</mini-zoo>

```
struct S<T> where T: ?Sized { ... }
```



</description>
</generics-section>


<!-- Section -->
<generics-section id="xxx">
<header>Generics and Lifetimes &mdash; <code>&lt;'a&gt;</code></header>
<description>

<mini-zoo class="zoo">
    <entry>
        <type class="generic dotted"><code>S&lt;'a&gt;</code></type>
    </entry>
    <entry>
        <type class="generic dotted"><code>&'a f32</code></type>
    </entry>
    <entry>
        <type class="generic dotted"><code>&'a mut u8</code></type>
    </entry>
</mini-zoo>

- Lifetimes act<sup>*</sup> like type parameters:
    - user must provide specific `'a` to instantiate type (compiler will help within methods),
    - as `Vec<f32>` and `Vec<u8>` are different types, so are `S<'p>` and `S<'q>`,
    - meaning you can't just assign value of type `S<'a>` to variable expecting `S<'b>` (exception: "subtype" relationship for lifetimes, e.g. `'a` outliving `'b`).


<mini-zoo class="zoo">
    <entry>
        <type class="generic dotted"><code>S&lt;'a&gt;</code></type>
    </entry>
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
    <entry>
        <type class="composed"><code>S&lt;'auto&gt;</code></type>
    </entry>
    <entry>
        <type class="composed"><code>S&lt;'static&gt;</code></type>
    </entry>
</mini-zoo>


- `'static` is only nameable instance of the _typespace_ lifetimes.

```
// `'a is free parameter here (user can pass any specific lifetime)
struct S<'a> {
    x: &'a u32
}

// In non-generic code, 'static is the only nameable lifetime we can explicitly put in here.
let a: S<'static>;

// Alternatively, in non-generic code we can (often must) omit 'a and have Rust determine
// the right value for 'a automatically.
let b: S;
```

<footnotes>

<sup>*</sup> There are subtle differences, for example you can create an explicit instance `0` of a type `u32`, but with the exception of `'static` you can't really create a lifetime, e.g., "lines 80 - 100", the compiler will do that for you. {{ link(url="https://medium.com/nearprotocol/understanding-rust-lifetimes-e813bcd405fa" )}}

</footnotes>


> Note to self and TODO: that analogy seems somewhat flawed, as if `S<'a>` is to `S<'static>` like `S<T>` is to `S<u32>`, then `'static` would be a _type_; but then what's the value of that type?

</description>
</generics-section>


<!-- Section -->
<!-- <generics-section id="xxx">
<header>Another <code>?X</code></header>
<description>

- `Sized` is trait, automatically implemented **and** automatically used as default bound
- Could there (ever) be another trait `T` so that:
    - `S<T>` means `S<T> where T: Sized + X` by default and
    - you'd have to opt out with `S<T> where T: ?X` ?
- Issue:
    - Any `S<T>` written today does not know `X`, so can't opt into supporting it
    - If `X` were introduced and not implemented for any existing type, `S<T>` would stop working on that type

</description>
</generics-section> -->


<!-- Section -->
<!-- <generics-section id="xxx">
<header>GAT {{ experimental() }}</header>
<description>


</description>
</generics-section> -->



<!-- Section -->
<!-- <generics-section id="xxx">
<header>(Co-/Contra-) Variance </header>
<description>


</description>
</generics-section>
 -->

<!-- Section -->
<!-- <generics-section id="zoo_todo">
<header>Todo</header>
<description>


</description>
</generics-section>
 -->


</div></panel></tab>

</tabs>

<footnotes>

Examples expand by clicking.

</footnotes>




## Type Zoo {#type-zoo}

A visual overview of types and traits in crates.

<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 750px;">


<zoo class="zoo">

<!-- REGION -->
<region style="height: 310px;">
<!-- Primitives -->
<group style="left:6%; width: 200px;">
    <entry style="left:100px; top: 10%;">
        <type class="primitive"><code>u8</code></type>
    </entry>
    <entry style="left:20px; top: 32%;">
        <type class="primitive"><code>u16</code></type>
    </entry>
    <entry style="left:30px; top: 20%;">
        <type class="primitive"><code>f32</code></type>
    </entry>
    <entry style="left:0px; top: 7%;">
        <type class="primitive"><code>bool</code></type>
    </entry>
    <entry style="left:120px; top: 32%;">
        <type class="primitive"><code>char</code></type>
    </entry>
    <label style="left:8px; top: 43%;">Primitive Types</label>
</group>
<!-- Composed -->
<group style="left:50%; width: 350px;">
    <entry style="left:110px; top: 60px;">
        <type class="composed"><code>File</code></type>
    </entry>
    <entry style="left:180px; top: 34%;">
        <type class="composed"><code>String</code></type>
    </entry>
    <entry style="left:230px; top: 13%;">
        <type class="composed"><code>Builder</code></type>
    </entry>
    <label style="left:150px; top: 43%;">Composite Types</label>
</group>
<!-- Type constructors -->
<group style="left: 30px; top:53%; width: 200px;">
    <!-- Group -->
    <entry style="left:50px; top: 8%;">
        <type class="composed"><code>Vec&lt;T&gt;</code></type>
    </entry>
    <entry style="left:45px; top: 9%;">
        <type class="composed"><code>Vec&lt;T&gt;</code></type>
    </entry>
    <entry style="left:40px; top: 10%;">
        <type class="generic dotted"><code>Vec&lt;T&gt;</code></type>
    </entry>
    <!-- Group -->
    <entry style="left:170px; top: 2%;">
        <type class="primitive"><code>&'a T</code></type>
    </entry>
    <entry style="left:165px; top: 3%;">
        <type class="primitive"><code>&'a T</code></type>
    </entry>
    <entry style="left:160px; top: 4%;">
        <type class="generic dotted"><code>&'a T</code></type>
    </entry>
    <!-- Group -->
    <entry style="left:140px; top: 18%;">
        <type class="primitive"><code>&mut 'a T</code></type>
    </entry>
    <entry style="left:135px; top: 19%;">
        <type class="primitive"><code>&mut 'a T</code></type>
    </entry>
    <entry style="left:130px; top: 20%;">
        <type class="generic dotted"><code>&mut 'a T</code></type>
    </entry>
    <!-- Group -->
    <entry style="left:40px; top: 28%;">
        <type class="primitive"><code>[T; n]</code></type>
    </entry>
    <entry style="left:35px; top: 29%;">
        <type class="primitive"><code>[T; n]</code></type>
    </entry>
    <entry style="left:30px; top: 30%;">
        <type class="generic dotted"><code>[T; n]</code></type>
    </entry>
    <label style="left:80px; top: 40%;">Type Constructors</label>
</group>
<!-- Functrions -->
<group style="left: 50%; top:53%; width: 200px;">
    <!-- Group -->
    <entry style="left:10px; top: 8%;">
        <function class=""><code>Vec&lt;T&gt;</code></function>
    </entry>
    <entry style="left:5px; top: 9%;">
        <function class=""><code>Vec&lt;T&gt;</code></function>
    </entry>
    <entry style="left:0px; top: 10%;">
        <function class="dotted"><code>f&lt;T&gt;() {}</code></function>
    </entry>
    <!-- Group -->
    <entry style="left:20px; top: 24%;">
        <function><code>drop() {}</code></function>
    </entry>
    <label style="left:10px; top: 40%;">Functions</label>
</group>
<!-- Unsized -->
<!-- <group style="left: 50%; top:53%;">
    <entry style="left:30%; top: 10%;">
        <type class="unsized"><code>str</code></type>
    </entry>
    <entry style="left:35%; top: 20%;">
        <type class="unsized"><code>[u8]</code></type>
    </entry>
    <entry style="left:28%; top: 30%;">
        <type class="unsized"><code>dyn Trait</code></type>
    </entry>
    <label style="left:30%; top: 40%;">Unsized Types</label>
</group> -->
<!-- Macros -->
<group class="grayed" style="left: 80%; top:53%; width: 140px;">
    <entry style="left:5px; top: 15%;">
        <macro><code>PI</code></macro>
    </entry>
    <entry style="left:0px; top: 28%;">
        <macro><code>dbg!</code></macro>
    </entry>
    <label style="left:20px; top: 40%;">Other</label>
</group>
<!-- Traits -->
<group style="left:36%; width: 30px;">
    <entry style="left:20px; top: 20px;">
        <trait-impl>⌾ <code>Copy</code></trait-impl>
    </entry>
    <entry style="left:60px; top: 90px;">
        <trait-impl class="">⌾ <code>Deref</code></trait-impl>
        <associated-type class=""><code>type Tgt;</code></associated-type>
    </entry>
    <entry style="left:90px; top: 50px;">
        <trait-impl class="">⌾ <code>From&lt;T&gt;</code></trait-impl>
    </entry>
    <entry style="left:85px; top: 55px;">
        <trait-impl class="">⌾ <code>From&lt;T&gt;</code></trait-impl>
    </entry>
    <entry style="left:80px; top: 60px;">
        <trait-impl class="dotted">⌾ <code>From&lt;T&gt;</code></trait-impl>
    </entry>
    <label style="left:60px; top: 43%;">Traits</label>
</group>
</region>
<region-label>Items defined in upstream crates.</region-label>

<!-- REGION -->
<region class="your-crate" style="height: 190px;">
<!-- traits -->
<group style="left:5px; width: 200px;">
    <entry style="left:10px; top: 25px;">
        <trait-impl class="">⌾ <code>Serialize</code></trait-impl>
    </entry>
    <entry style="left:30px; top: 65px;">
        <trait-impl class="">⌾ <code>Transport</code></trait-impl>
    </entry>
    <entry style="left:15px; top: 105px;">
        <trait-impl class="">⌾ <code>ShowHex</code></trait-impl>
    </entry>
    <!-- <label style="left:60px; top: 165px">Traits</label> -->
</group>
<!-- types -->
<group style="left:150px; width: 200px;">
    <entry style="left:0px; top: 25px;">
        <type class="composed"><code>Device</code></type>
        <trait-impl class="grayed">⌾ <code>From&lt;u8&gt;</code></trait-impl>
        <!-- <trait-impl class="grayed">⌾ <code>Deref</code></trait-impl>
        <associated-type class="grayed"><code>type Thing;</code></associated-type> -->
        <note>Foreign trait impl. for local type.</note>
    </entry>
    <entry style="left:100px; top: 25px;">
        <type class="grayed composed"><code>String</code></type>
        <trait-impl class="">⌾ <code>Serialize</code></trait-impl>
        <note>Local trait impl. for foreign type.</note>
    </entry>
    <entry style="left:200px; top: 25px;">
        <type class="composed grayed"><code>String</code></type>
        <trait-impl class="grayed">⌾ <code>From&lt;u8&gt;</code></trait-impl>
        <note>{{ bad() }} Illegal, foreign trait for f. type.</note>
    </entry>
    <entry style="left:200px; top: 110px;">
        <type class="composed grayed"><code>String</code></type>
        <trait-impl class="grayed">⌾ <code>From&lt;Port&gt;</code></trait-impl>
        <note>Exception: Legal if used type local.</note>
    </entry>
    <entry style="left:300px; top: 25px;">
        <type class="composed"><code>Port</code></type>
        <trait-impl class="">⌾ <code>From&lt;u8&gt;</code></trait-impl>
        <trait-impl class="">⌾ <code>From&lt;u16&gt;</code></trait-impl>
        <note>Mult. impl. of trait with differing <b>IN</b> params.</note>
    </entry>
    <entry style="left:400px; top: 25px;">
        <type class="composed"><code>Container</code></type>
        <trait-impl class="">⌾ <code>Deref</code></trait-impl>
        <associated-type class="grayed"><code>Tgt = u8;</code></associated-type>
        <trait-impl class="">⌾ <code>Deref</code></trait-impl>
        <associated-type class="grayed"><code>Tgt = f32;</code></associated-type>
        <note>{{ bad() }} Illegal impl. of trait with differing <b>OUT</b> params.</note>
    </entry>
    <entry style="left:510px; top: 15px;">
        <type class="composed"><code>T</code></type>
    </entry>
    <entry style="left:505px; top: 20px;">
        <type class="composed"><code>T</code></type>
    </entry>
    <entry style="left:500px; top: 25px;">
        <type class="generic dotted"><code>T</code></type>
        <trait-impl class="">⌾ <code>ShowHex</code></trait-impl>
        <note>Blanket impl. of trait for any type.</note>
    </entry>
</group>
</region>
<region-label>Your crate.</region-label>

<!-- REGION -->
<!-- <region style="height: 90px;">
<group style="left:324px; width: 200px;">
    <entry style="left:20px; top: 30px;">
        <code>ccc.f();</code>
    </entry>
</group>
</region>
<region-label>Downstream crates.</region-label> -->

</zoo>

<footnotes>

A walk through the jungle of types, traits, and implementations that (might possibly) exist in your application.

</footnotes>



<!-- End scrollable overflow-->
</div>
</div>




## Type Conversions

How to get `B` when you have `A`?

<div class="color-header variance">

<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-variance-1" name="tab-variance" checked>
<label for="tab-variance-1"><b>Intro</b></label>
<panel><div>

```
fn f(x: A) -> B {
    // How can you obtain B from A?
}
```

| Method | Explanation |
|--------| -----------|
| **Identity** | Trivial case, `B` **is exactly** `A`. |
| **Computation** | Create and manipulate instance of `B` by **writing code** transforming data. |
| **Casts** | **On-demand** conversion between types where caution is advised. |
| **Coercions** | **Automatic** conversion within _'weakening ruleset'_.<sup>1</sup> |
| **Subtyping** | **Automatic** conversion within _'same-layout-different-lifetimes ruleset'_.<sup>1</sup> |

{{ tablesep() }}

<footnotes>

<sup>1</sup> While both convert `A` to `B`, **coercions** generally link to an _unrelated_ `B` (a type "one could reasonably expect to have different methods"),
while **subtyping** links to a `B` differing only in lifetimes.

</footnotes>

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-variance-2" name="tab-variance">
<label for="tab-variance-2"><b>Computation (Traits)</b></label>
<panel><div>

```
fn f(x: A) -> B {
    x.into()
}
```

_Bread and butter_ way to get `B` from `A`. Some traits provide canonical, user-computable type relations:

| Trait | Example | Trait implies ... |
|--------| -----------|-----------|
| `impl From<A> for B {}` | `a.into()` | _Obvious_, always-valid relation. |
| `impl TryFrom<A> for B {}` | `a.try_into()?` | _Obvious_, sometimes-valid relation. |
| `impl Deref for A {}` | `*a` | `A` is smart pointer carrying `B`; also enables coercions.  |
| `impl AsRef<B> for A {}` | `a.as_ref()` | `A` can be _viewed_ as `B`. |
| `impl AsMut<B> for A {}` | `a.as_mut()` | `A` can be mutably viewed as `B`. |
| `impl Borrow<B> for A {}` | `a.borrow()` | `A` has borrowed _analog_ `B` (behaving same under `Eq`, ...). |
| `impl ToOwned for A { ... }` | `a.to_owned()` | `A` has owned analog `B`. |


<!--
<footnotes>

<sup>1</sup> Pretty much any function, like `is_signed(x)`, puts values of two types in a _specific_ relationship, especially if their _meaning_ is highly _overloaded_ (e.g., `true` in the `is_signed` relation is proxy for a different concept than `true` in an `is_odd` one). In contrast, the traits above (and type conversions in general) are mainly about unambiguous conversions across any possible meaning.

</footnotes>
 -->

</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-variance-3" name="tab-variance">
<label for="tab-variance-3"><b>Casts</b></label>
<panel><div>

```
fn f(x: A) -> B {
    x as B
}
```

Convert types **with keyword `as`** if conversion _relatively obvious_ but **might cause issues**. {{ nom(page="casts.html") }}


|  A | B | Example | Explanation |
|----|----| ----| -----------|
| `Ptr` | `Ptr` | `device_ptr as *const u8` | If `*A`, `*B` are `Sized`. |
| `Ptr` | `Integer` | `device_ptr as usize` |  |
| `Integer` | `Ptr` | `my_usize as *const Device` |  |
| `Number` | `Number` | `my_u8 as u16` | Often surprising behavior. {{ above(target="#numeric-types-ref") }} |
| `enum` w/o fields | `Integer` | `E::A as u8` |  |
| `bool` | `Integer` | `true as u8` |  |
| `char` | `Integer` | `'A' as u8` |  |
| `&[T; N]` | `*const T` | `my_ref as *const u8` |  |
| `fn(...)` | `Ptr` | `f as *const u8` | If `Ptr` is `Sized`.  |
| `fn(...)` | `Integer` | `f as usize` |  |

{{ tablesep() }}

<footnote>

Where `Ptr`, `Integer`, `Number` are just used for brevity and actually mean:
- `Ptr` any `*const T` or `*mut T`;
- `Integer` any countable `u8` ... `i128`;
- `Number` any `Integer`, `f32`, `f64`.

</footnote>

> **Opinion** {{ opinionated() }} &mdash; Casts, esp. `Number` - `Number`, can easily go wrong.
> If you are concerned with correctness, consider more explicit methods instead.

</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-variance-4" name="tab-variance">
<label for="tab-variance-4"><b>Coercions</b></label>
<panel><div>

```
fn f(x: A) -> B {
    x
}
```

Automatically **weaken** type `A` to `B`; types can be _substantially_<sup>1</sup> different. {{ nom(page="coercions.html") }}


|  A | B |  Explanation |
|----|----| -----------|
| `&mut T` | `&T` | **Pointer weakening**. |
| `&mut T` | `*mut T` | - |
| `&T` | `*const T` | - |
| `*mut T` | `*const T` | - |
| `&T` | `&U` | **Deref**, if `impl Deref<Target=U> for T`. |
| `T` | `U` | **Unsizing**, if `impl CoerceUnsized<U> for T`.<sup>2</sup> {{ experimental() }} |
| `T` | `V` | **Transitivity**, if `T` coerces to `U` and `U` to `V`. |
| <code>&vert;x&vert; x + x</code> | `fn(u8) -> u8` | **Non-capturing closure**, to equivalent `fn` pointer. |

{{ tablesep() }}

<footnote>

<sup>1</sup> _Substantially_ meaning one can regularly expect a coercion result `B` to be _an entirely different type_ (i.e., have entirely different methods) than the original type `A`.

<sup>2</sup> Does not quite work in example above as unsized can't be on stack; imagine `f(x: &A) -> &B` instead. Unsizing works by default for:
- `[T; n]` to `[T]`
- `T` to `dyn Trait` if `impl Trait for T {}`.
- `Foo<..., T, ...>` to `Foo<..., U, ...>` under arcane {{ link(url="https://doc.rust-lang.org/nomicon/coercions.html") }} circumstances.

</footnote>


</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-variance-5" name="tab-variance">
<label for="tab-variance-5"><b>Subtyping</b></label>
<panel><div>

```
fn f(x: A) -> B {
    x
}
```

Automatically converts `A` to `B` for types **only differing in lifetimes** {{ nom(page="subtyping.html") }} - subtyping **examples**:


| A<sup>(subtype)</sup>  | B<sup>(supertype)</sup> | Explanation |
|--------| -----------| -----------|
| `&'static u8` | `&'a u8` | Valid, <i>forever-</i>pointer is also <i>transient-</i>pointer. |
| `&'a u8` | `&'static u8` | {{ bad() }} Invalid, transient should not be forever. |
| `&'a &'b u8` | `&'a &'b u8` | Valid, same thing. **But now things get interesting. Read on.** |
| `&'a &'static u8` | `&'a &'b u8` | Valid, `&'static u8` is also `&'b u8`; **covariant** inside `&`.  |
| `&'a mut &'static u8` | `&'a mut &'b u8` | {{ bad() }} Invalid and surprising; **invariant** inside `&mut`. |
| `Box<&'a static>` | `Box<&'a u8>` | Valid, box with forever is also box with transient; covariant. |
| `Box<&'a u8>` | `Box<&'static u8>` | {{ bad() }} Invalid, box with transient may not be with forever. |
| `Box<&'a mut u8>` | `Box<&'a u8>` | {{ bad() }} <sup>⚡</sup> Invalid, see table below, `&mut u8` never _was a_ `&u8`. |
| `Cell<&'a static>` | `Cell<&'a u8>` | {{ bad() }} Invalid, cells are **never** something else; invariant. |
| `fn(&'static u8)` | `fn(&'u8 u8)` | {{ bad() }} If `fn` needs forever it may choke on transients; **contravar.**|
| `fn(&'a u8)` | `fn(&'static u8)` |  But sth. that eats transients **can be**(!) sth. that eats forevers. |
| `for<'r> fn(&'r u8)` | `fn(&'a u8)` | Higher-ranked type `for<'r> fn(&'r u8)` is also `fn(&'a u8).` |


{{ tablesep() }}

In contrast, these are **not**{{ bad() }} examples of subtyping:

|  A | B |  Explanation |
|----|----| -----------|
| `u16` | `u8` | {{ bad() }} **Obviously invalid**; `u16` should never automatically be `u8`. |
| `u8` | `u16` | {{ bad() }} Invalid **by design**; types w. different data still never subtype even if they _could_. |
| `&'a mut u8` | `&'a u8` | {{ bad() }} Trojan horse, not subtyping; but coercion (still works, just not subtyping). |

{{ tablesep() }}

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-variance-8" name="tab-variance">
<label for="tab-variance-8"><b>Variance</b></label>
<panel><div>

```
fn f(x: A) -> B {
    x
}
```

Automatically converts `A` to `B` for types **only differing in lifetimes** {{ nom(page="subtyping.html") }} -  subtyping **variance rules**:

- A longer lifetime `'a` that outlives a shorter `'b` is a subtype of `'b`.
- Implies `'static` is subtype of all other lifetimes `'a`.
- Whether types with parameters (e.g., `&'a T`) are subtypes of each other the following variance table is used:

| Construct<sup>1</sup> | `'a` | `T` | `U` |
|--------| -----------| -------| -------|
| `&'a T` | covariant | covariant |  |
| `&'a mut T` | covariant | invariant |  |
| `Box<T>` |  | covariant |  |
| `Cell<T>` |  | invariant |  |
| `fn(T) -> U` |  | **contra**variant | covariant |
| `*const T` |  | covariant |  |
| `*mut T` |  | invariant |  |

<footnotes>

**Covariant** means if `A` is subtype of `B`, then `T[A]` is subtype of `T[B]`. <br>
**Contravariant** means if `A` is subtype of `B`, then **`T[B]`** is subtype of `T[A]`. <br>
**Invariant** means even if `A` is subtype of `B`, neither `T[A]` nor `T[B]` will be subtype of the other.<br>
<!-- <br> -->

<sup>1</sup> Compounds like `struct S<T> {}` obtain variance through their used fields, usually becoming invariant if multiple variances are mixed.<br>

</footnotes>

> 💡 **In other words**, 'regular' types are never subtypes of each other (e.g., `u8` is not subtype of `u16`),
> and a `Box<u32>` would never be sub- or supertype of anything.
> However, generally a `Box<A>`, _can_ be subtype of `Box<B>` (via covariance) if `A` is a subtype
> of `B`, which can only happen if `A` and `B` are 'sort of the same type that only differed in lifetimes', e.g., `A` being `&'static u32` and `B` being `&'a u32`.

</div></panel></tab>

</tabs>

</div>


{{ tablesep() }}




---

# 编码指南


## Rust 惯用法 {#idiomatic-rust}

Java 或 C 的使用者需要转换下思维：

<div class="color-header blue">

| 习语 | 代码 |
|--------| ---- |
| **用表达式思考** | `x = if x { a } else { b };` |
|  | `x = loop { break 5 };`  |
|  | `fn f() -> u32 { 0 }`  |
| **用迭代器思考** | `(1..10).map(f).collect()` |
|  | <code>names.iter().filter(&vert;x&vert; x.starts_with("A"))</code> |
| **用 `?` 捕获异常** | `x = try_something()?;` |
|  | `get_option()?.run()?` |
| **使用强类型** | `enum E { Invalid, Valid { ... } }` 之于 `ERROR_INVALID = -1` |
|  | `enum E { Visible, Hidden }` 之于 `visible: bool` |
|  | `struct Charge(f32)` 之于 `f32` |
| **提供生成器** | `Car::new("Model T").hp(20).run();` |
| **分离实现** | 泛型 `S<T>` 可以对每个 `T` 都有不同的实现。 |
|   | Rust 没有面向对象，但通过 `impl` 可以实现特化。 |
| **Unsafe** | 尽量避免 `unsafe {}`，因为总是会有更快更安全的解决方案的。除了 FFI。 |
| **实现 Trait** | `#[derive(Debug, Copy, ...)]`。根据需要实现 `impl`。|
| **工具链** | 利用 [**clippy**](https://github.com/rust-lang/rust-clippy) 可以提升代码质量。 |
|  | 用 [**rustfmt**](https://github.com/rust-lang/rustfmt) 格式化可以帮助别人看懂你的代码。 |
|  | 添加**单元测试** {{ book(page="ch11-01-writing-tests.html") }}（`#[test]`），确保代码正常运行。 |
|  | 添加**文档测试** {{ book(page="ch14-02-publishing-to-crates-io.html") }}（` ``` my_api::f() ``` `），确保文档匹配代码。 |
| **文档** | 以文档注解的 API 可显示在 [**docs.rs**](https://docs.rs) 上。 |
|  | 不要忘记在开始加上**总结句**和**例程**。 |
|  | 如果有这些也加上：**Panics**、**Errors**、**Safety**、**Abort** 和**未定义行为**。 |


</div>



{{ tablesep() }}

> 🔥 **强烈**建议对所有共享项目都遵循
> [**API 指南**](https://rust-lang.github.io/api-guidelines/)（[**检查列表**](https://rust-lang.github.io/api-guidelines/checklist.html)）
> ！ 🔥


{{ tablesep() }}



## Async-Await 101

类似于 C# 或 TypeScript 的 async / await，但又有所不同：


<tabs class="color-header orange">

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-async-1" name="tab-async" checked>
<label for="tab-async-1"><b>Basics</b></label>
<panel><div>



| 语法 | 说明 |
|---------|-------------|
| `async`  | Anything declared `async` always returns an `impl Future<Output=_>`. {{ std(page="std/future/trait.Future.html") }} |
| {{ tab() }} `async fn f() {}`  | Function `f` returns an `impl Future<Output=()>`. |
| {{ tab() }} `async fn f() -> S {}`  | Function `f` returns an `impl Future<Output=S>`. |
| {{ tab() }} `async { x }`  | Transforms `{ x }` into an `impl Future<Output=X>`. |
| `let sm = f();   ` | Calling `f()` that is `async` will **not** execute `f`, but produce state machine `sm`. {{ note(note="1") }} {{ note(note="2") }} |
| {{ tab() }} `sm = async { g() };`  | Likewise, does **not** execute the `{ g() }` block; produces state machine. |
| `runtime.block_on(sm);`  | Outside an `async {}`, schedules `sm` to actually run. Would execute `g()`. {{ note(note="3") }} {{ note(note="4") }}|
| `sm.await` | Inside an `async {}`, run `sm` until complete. Yield to runtime if `sm` not ready. |



<footnotes>

<sup>1</sup> Technically `async` transforms following code into anonymous, compiler-generated state machine type; `f()` instantiates that machine. <br>
<sup>2</sup> The state machine always `impl Future`, possibly `Send` & co, depending on types used inside `async`. <br>
<sup>3</sup> State machine driven by worker thread invoking `Future::poll()` via runtime directly, or parent `.await` indirectly. <br>
<sup>4</sup> Rust doesn't come with runtime, need external crate instead, e.g., [async-std](https://github.com/async-rs/async-std) or [tokio 0.2+](https://crates.io/crates/tokio). Also, more helpers in [futures crate](https://github.com/rust-lang-nursery/futures-rs).

</footnotes>



</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-async-2" name="tab-async">
<label for="tab-async-2"><b>Execution Flow</b></label>
<panel><div>


对每个 `x.await`，状态机将会通过控制转移到状态机 `x`。有时，由 `.await` 调用的低级状态机并未就绪，此时，工作线程直接返回到运行时，以使得它可以驱动另一个 Future。一段时间后，运行时：
- **可能**恢复执行。常见于此，除非 `sm` / `Future` 已析构。
- **可能**由前一个**或另一个**工作线程恢复执行（取决于运行时）。

`async` 代码块内部代码的简易流程图如下：


<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```
       consecutive_code();           consecutive_code();           consecutive_code();
START --------------------> x.await --------------------> y.await --------------------> READY
// ^                          ^     ^                               Future<Output=X> 就绪 -^
// 由运行时调用                 |     |
// 或由外部 .await 调用         |     会由另一个线程恢复（下一个最佳可用的），
//                            |     或者当 Future 已析构时根本不会执行。
//                            |
//                            执行 `x`。若已就绪，则继续执行。
//                            若未就绪，返回当前线程到运行时。
```

</div>
</div>

</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-async-3" name="tab-async">
<label for="tab-async-3"><b>Caveats</b></label>
<panel><div>


With the execution flow in mind, some considerations when writing code inside an `async` construct:

<div class="color-header orange">


| 语法 {{ note(note="1") }} | 说明 |
|---------|-------------|
| `sleep_or_block();` | 显然不对{{ bad() }}，当前线程永不终止，阻碍执行器。 |
| `set_TL(a); x.await; TL();` | 显然不对{{ bad() }}，`await` 会由其他线程返回，[thread local](https://doc.rust-lang.org/std/macro.thread_local.html) 无效。 |
| `s.no(); x.await; s.go();` | 可能不对{{ bad() }}，如果等待时 `Future` 被析构，则 `await` [不会返回](http://www.randomhacks.net/2019/03/09/in-nightly-rust-await-may-never-return/)。{{ note(note="2") }} |
| `Rc::new(); x.await; rc();` | 非 `Send` 类型拒绝实现 `impl Future`。兼容性差。 |

</div>

<footnotes>

<sup>1</sup> Here we assume `s` is any non-local that could temporarily be put into an invalid state;
`TL` is any thread local storage, and that the `async {}` containing the code is written
without assuming executor specifics. <br/>
<sup>2</sup> Since [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html) is run in any case when `Future` is dropped, consider using drop guard that cleans up / fixes application state if it has to be left in bad condition across `.await` points.

</footnotes>

</div></panel></tab>

<!-- end tabs -->
</tabs>


{{ tablesep() }}


## 闭包 API {#closures-in-apis}

There is a subtrait relationship `Fn` : `FnMut` : `FnOnce`. That means a closure that
implements `Fn` {{ std(page="std/ops/trait.Fn.html") }} also implements `FnMut` and `FnOnce`. Likewise a closure
that implements `FnMut` {{ std(page="std/ops/trait.FnMut.html") }} also implements `FnOnce`. {{ std(page="std/ops/trait.FnOnce.html") }}

从调用者的角度来看这意味着：

<div class="color-header green">

| Signature | Function `g` can call &hellip; |  Function `g` accepts &hellip; |
|--------| -----------| -----------|
| `g<F: FnOnce()>(f: F)`  | &hellip; `f()` once. |  `Fn`, `FnMut`, `FnOnce`  |
| `g<F: FnMut()>(mut f: F)`  | &hellip; `f()` multiple times. | `Fn`, `FnMut` |
| `g<F: Fn()>(f: F)`  | &hellip; `f()` multiple times.  | `Fn` |

</div>

<footnotes>

注意，对调用者来说，如何**确定** `Fn` 闭包，是最为严格的。但是一个**包含** `Fn` 的闭包，对调用者来説，是对任意函数都最兼容的。

</footnotes>



{{ tablesep() }}

站在定义闭包的角度来看：

<div class="color-header green">

| 闭包 | 实现<sup>*</sup> | 说明 |
|--------| -----------| --- |
| <code> &vert;&vert; { moved_s; } </code> | `FnOnce` | 调用者必须放弃 `moved_s` 的所有权。 |
| <code> &vert;&vert; { &mut s; } </code> | `FnOnce`, `FnMut` | 允许 `g()` 改变调用者的局部状态 `s`。 |
| <code> &vert;&vert; { &s; } </code> | `FnOnce`, `FnMut`, `Fn` | 可能不会导致状态改变，但可能会共享和重用 `s`。 |

</div>

<div class="footnotes">

<sup>*</sup> Rust [偏向于以索引捕获](https://doc.rust-lang.org/stable/reference/expressions/closure-expr.html)（在调用者视角上最“兼容” `Fn` 的闭包），但也可以用 `move || {}` 语法通过复制或者移动捕获相关环境变量。。

</div>

{{ tablesep() }}

这会带来如下优势和劣势：

<div class="color-header green">

| 要求 | 优势 | 劣势 |
|--------| -----------| -----------|
| `F: FnOnce`  | <span class="good">容易满足调用者。</span> | <span class="bad">仅用一次，`g()` 仅会调用 `f()` 一次。</span> |
| `F: FnMut`  | <span class="good">允许 `g()` 改变调用者状态。</span> | <span class="bad">调用者不能在 `g()` 期间重用捕获。</span> |
| `F: Fn`  | <span class="good">可同时存在多个。</span> | <span class="bad">最难由调用者生成。</span> |

</div>


{{ tablesep() }}



<!-- ## Macro Hygiene -->
<!-- {{ tablesep() }} -->





## Unsafe, Unsound, Undefined

Unsafe 导致 unsound，unsound 导致 undefined，undefined 是一切原力的阴暗面。



<tabs>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-unsafe-1" name="tab-unsafe" checked>
<label for="tab-unsafe-1"><b>Unsafe Code</b></label>
<panel><div>


**Unsafe 代码**

- 标记为 `unsafe` 的代码有特权。比如，解引用裸指针，或调用其他 `unsafe` 函数。
- 这是一份特殊的**作者必须给编译器的承诺**，编译器**会**相信你。
- `unsafe` 代码自身并非有害，但危险的是 FFI 使用方或者异常的数据结构。

<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```rust
// `x` must always point to race-free, valid, aligned, initialized u8 memory.
unsafe fn unsafe_f(x: *mut u8) {
    my_native_lib(x);
}
```
</div></div></div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-unsafe-2" name="tab-unsafe" >
<label for="tab-unsafe-2"><b>Undefined Behavior</b></label>
<panel><div>


**未定义行为 (UB)**
- 如前所述，`unsafe` 代码意味着对编译器的[特殊承诺](https://doc.rust-lang.org/stable/reference/behavior-considered-undefined.html)（否则它就不需要是 `unsafe` 的了）。
- 不遵守承诺会使编译器产生错误的代码，执行错误的代码会导致未定义行为。
- 在触发未定义行为之后，**任何**事情都可能发生。这种不知不觉的影响可能1)难以捉摸，2)明显远离事发现场，或3)只有在某些条件下才会被发现。
- 一个表面上**可以运行**的程序（包括任意数量的单元测试），并不能证明含有未定义行为的代码不会因为一些偶然原因而失败。
- 含有未定义行为的代码在客观上是危险的、无效的，根本不应该存在。

<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">


```rust
if should_be_true() {
   let r: &u8 = unsafe { &*ptr::null() };    // 一旦运行，整个程序都会处于未定义状态。
} else {                                     // 尽管这一行看似什么都没干，程序可能两条路径
    println!("the spanish inquisition");     // 都运行了，然后破坏掉数据，或者发生别的。
}
```
</div></div></div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-unsafe-3" name="tab-unsafe" >
<label for="tab-unsafe-3"><b>Unsound Code</b></label>
<panel><div>


**Unsound 代码**
- 任何会由于用户输入而导致 _safe_ Rust 产生未定义行为的都是 **unsound**（不健全）的（尽管仅仅可能是理论上的）。
- 比如 `unsafe` 代码可能违反上述承诺而产生未定义行为。
- Unsound 代码对稳定性和安全性造成风险，且违背了大部分 Rust 用户的基本假设。

<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```rust
fn unsound_ref<T>(x: &T) -> &u128 {      // Signature looks safe to users. Happens to be
    unsafe { mem::transmute(x) }         // ok if invoked with an &u128, UB for practically
}                                        // everything else.
```

</div></div></div></panel></tab>

</tabs>

{{ tablesep() }}

>
> **负责任地使用 unsafe** {{ opinionated() }}
>
> - 除非非用不可，不要使用 `unsafe`。
> - Follow the [Nomicon](https://doc.rust-lang.org/nightly/nomicon/), [Unsafe Guidelines](https://rust-lang.github.io/unsafe-code-guidelines/), **always** uphold **all** safety invariants, and **never** invoke [UB](https://doc.rust-lang.org/stable/reference/behavior-considered-undefined.html).
> - 最小化 `unsafe` 用例，封装成易于评审的小的、优雅的模块。
> - Never create unsound abstractions; if you can't encapsulate `unsafe` properly, don't do it.
> - 每个 `unsafe` 用例应当同时提供关于其安全性的纯文本理由提要。


{{ tablesep() }}



## API 稳定性 {#api-stability}

When updating an API, these changes can break client code.{{ rfc(page="1105-api-evolution.html") }} Major changes (🔴) are **definitely breaking**, while minor changes (🟡) **might be breaking**:

<div class="color-header api-stability">


{{ tablesep() }}

| Crate |
|---------|
| 🔴 编写一个 _stable_ 的 crate 但却依赖了 _nightly_。 |
| 🟡 修改了 Cargo 的功能（比如添加或移除功能） |

{{ tablesep() }}


| 模块 |
|---------|
| 🔴 重命名、移动、移除任何公开项。 |
| 🟡 添加新的公开项，因为 `use your_crate::*` 可能会破坏现有代码。 |

{{ tablesep() }}

| 结构体 |
|---------|
| 🔴 当所有字段都为公开时添加私有字段。 |
| 🔴 当没有私有字段时添加公开字段。 |
| 🟡 当至少有一个字段时添加或移除私有字段（在更改前或更改后）。 |
| 🟡 将有私有字段（至少有一个字段）的元组结构转换到普通结构，或反之。 |

{{ tablesep() }}

| 枚举 |
|---------|
| 🔴 Adding new variants; can be mitigated with early `#[non_exhaustive]` {{ ref(page="attributes/type_system.html#the-non_exhaustive-attribute") }} |
| 🔴 Adding new fields to a variant. |


{{ tablesep() }}

| Trait |
|---------|
| 🔴 添加非默认项，将会破坏已有的 `impl T for S {}`。 |
| 🔴 任何不必要的项签名修改，都会影响到使用者或者实现方。 |
| 🟡 添加一个默认项，可能会和另一个 trait 产生歧义。 |
| 🟡 添加默认类型参数。 |

{{ tablesep() }}

| Trait |
|---------|
| 🔴 实现任何“基本”trait。**不去**实现一个基本 trait 是一种最基本的承诺。 |
| 🟡 实现任何非基本的 trait，可能会导致歧义。 |

{{ tablesep() }}

| 固有实现 |
|---------|
| 🟡 添加内部项，可能会导致客户端倾向于调用这个 trait 的 fn 而导致编译错误。 |

{{ tablesep() }}

| 类型定义签名 |
|---------|
| 🔴 强约束（如 `<T>` 到 `<T: Clone>`）。 |
| 🟡 弱约束。 |
| 🟡 添加默认类型参数。 |
| 🟡 泛型归纳。 |

| 函数签名 |
|---------|
| 🔴 添加或移除参数。 |
| 🟡 引入新的类型参数。 |
| 🟡 泛型归纳。 |


{{ tablesep() }}

| 行为更改 |
|---------|
| 🔴 / 🟡 **改变语义可能不会导致编译器错误，但可能会使用户产生错误的逻辑。** |


</div>


{{ tablesep() }}


<!-- ## Authoring Quality Crates

> **Note** <sup>💬</sup> &mdash; This chapter is mildly **subjective**. That said, it tries to be observational with respect to successful Rust crates (i.e., crates with most downloads should check most of these boxes).


<div class="color-header quality_crate">

#### Code Patterns

| What | Why |
|--------| ---- |
| ☐ Write idiomatic code, follow API guides. |  |
| ☐ Regularly use `clippy`, `fmt` |   |
| ☐ Err on the side of `#[deny]`, not `#[allow]` | asdasd |


#### Infrastructure

| What | Why |
|--------| ---- |
| ☐ Minimize dependencies. | asds |
| ☐ Add optional deps. to essential `trait` crates |  asds |
| ☐ Have unit & integration tests |  asds |
| ☐ Have benchmarks |  asds |


#### Site

| What | Why |
|--------| ---- |
| ☐ Feature **prominent** API example, screenshot ... | asds |
| ☐ Have permissive license for libs. | asds |

</div>

<footnotes>


</footnotes> -->


<!-- Don't render this section for printing, won't be helpful -->
<noprint>

---

# 附录


## 外链和服务 {#links-services}

这里列出了其他的优秀指南和图表。

<div class="color-header lavender">


<!-- This is for major other "cheat sheet" like material on the web. Main question when adding: does it add something
    significant not found elsewhere? -->
| 备忘清单 | 说明 |
|--------| -----------|
| [Rust Learning⭐](https://github.com/ctjhoa/rust-learning) | 可能是学习 Rust 最好的链接合集。 |
| [Functional Jargon in Rust](https://github.com/JasonShin/functional-programming-jargon.rs) | Rust 的函数编程术语解释合集。 |
| [Periodic Table of Types](http://cosmic.mearie.org/2014/01/periodic-table-of-rust-types) | 解释各种类型和引用是如何联系在一起的。 |
| [Futures](https://rufflewind.com/img/rust-futures-cheatsheet.html) | 如何使用 Future。 |
| [Rust Iterator Cheat Sheet](https://danielkeep.github.io/itercheat_baked.html) | `std::iter` 和 `itertools` 的迭代器相关方法总结 |
| [Type-Based Rust Cheat Sheet](https://upsuper.github.io/rust-cheatsheet/) | 常见类型和转换方法。 |

</div>


{{ tablesep() }}


多数 Rust 资料都由社区开发。


<div class="color-header lavender">

<!-- Official Rust online "books" about Rust itself or major components (e.g., WebAssembly, Embedded, ...). Good test
    for inclusion can be official community involvement, +1k Github stars, ... -->
| Books&nbsp;️📚  | Description |
|--------| -----------|
| [The Rust Programming Language](https://doc.rust-lang.org/stable/book/) | Standard introduction to Rust, **start here if you are new**. |
| {{ tab() }} [API Guidelines](https://rust-lang.github.io/api-guidelines/) | How to write idiomatic and re-usable Rust. |
| {{ tab() }} [Asynchronous Programming](https://rust-lang.github.io/async-book/)  {{ experimental() }} | Explains `async` code, `Futures`, ... |
| {{ tab() }} [Design Patterns](https://rust-unofficial.github.io/patterns//) | Idioms, Patterns, Anti-Patterns. |
| {{ tab() }} [Edition Guide](https://doc.rust-lang.org/nightly/edition-guide/) | Working with Rust 2015, Rust 2018, and beyond.  |
| {{ tab() }} [Guide to Rustc Development](https://rustc-dev-guide.rust-lang.org/index.html) | Explains how the compiler works internally. |
| {{ tab() }} [Little Book of Rust Macros](https://veykril.github.io/tlborm/introduction.html) | Community's collective knowledge of Rust macros. |
| {{ tab() }} [Reference](https://doc.rust-lang.org/stable/reference/) {{ experimental() }}  | Reference of the Rust language.  |
| {{ tab() }} [RFC Book](https://rust-lang.github.io/rfcs/) | Look up accepted RFCs and how they change the language. |
| {{ tab() }} [Performance Book](https://nnethercote.github.io/perf-book/) | Techniques to improve the speed and memory usage. |
| {{ tab() }} [Rust Cookbook](https://rust-lang-nursery.github.io/rust-cookbook/) | Collection of simple examples that demonstrate good practices. |
| {{ tab() }} [Rust in Easy English](https://dhghomon.github.io/easy_rust/Chapter_3.html) | Explains concepts in simplified English, **good alternative start**. |
| {{ tab() }} [Rust for the Polyglot Programmer](https://www.chiark.greenend.org.uk/~ianmdlvl/rust-polyglot/index.html) | A guide for the experienced programmer. |
| {{ tab() }} [Rustdoc Book](https://doc.rust-lang.org/stable/rustdoc/) | Tips how to customize `cargo doc` and `rustdoc`. |
| {{ tab() }} [Rustonomicon](https://doc.rust-lang.org/nomicon/) | Dark Arts of Advanced and Unsafe Rust Programming. |
| {{ tab() }} [Unsafe Code Guidelines](https://rust-lang.github.io/unsafe-code-guidelines/)  {{ experimental() }} | Concise information about writing `unsafe` code. |
| {{ tab() }} [Unstable Book](https://doc.rust-lang.org/unstable-book/index.html) | Information about unstable items, e.g, `#![feature(...)]`.  |
| [The Cargo Book](https://doc.rust-lang.org/cargo/) | How to use `cargo` and write `Cargo.toml`. |
| [The CLI Book](https://rust-lang-nursery.github.io/cli-wg/) | Information about creating CLI tools. |
| [The Embedded Book](https://docs.rust-embedded.org/book/intro/index.html) | Working with embedded and `#![no_std]` devices. |
| {{ tab() }} [The Embedonomicon](https://docs.rust-embedded.org/embedonomicon/) | First `#![no_std]` from scratch on a Cortex-M. |
| [The WebAssembly Book](https://rustwasm.github.io/docs/book/) | Working with the web and producing `.wasm` files. |
| {{ tab() }} [The `wasm-bindgen` Guide](https://rustwasm.github.io/docs/wasm-bindgen/) | How to bind Rust and JavaScript APIs in particular. |

</div>

<footnotes>

For more inofficial books see [Little Book of Rust Books](https://lborb.github.io/book/title-page.html).

</footnotes>

<!-- Disabled for now as looks abandoned w/o content -->
<!-- | {{ tab() }} [SIMD Performance Guide](https://rust-lang.github.io/packed_simd/perf-guide/) {{ experimental() }} | Work with `u8x32` or `f32x8` to speed up your computations.  | -->


{{ tablesep() }}

通用组件的综合查找表。

<div class="color-header lavender">

<!-- Table-like sites, often auto-generated. -->
| Tables&nbsp;📋| Description |
|--------| -----------|
| [Rust Changelog](https://github.com/rust-lang/rust/blob/master/RELEASES.md) | See all the things that changed in a particular version. |
| [Rust Forge](https://forge.rust-lang.org/) | Lists release train and links for people working on the compiler. |
| {{ tab() }} [Rust Platform Support](https://doc.rust-lang.org/rustc/platform-support.html) | All supported platforms and their Tier. |
| {{ tab() }} [Rust Component History](https://rust-lang.github.io/rustup-components-history/) | Check **nightly** status of various Rust tools for a platform. |
| [ALL the Clippy Lints](https://rust-lang.github.io/rust-clippy/master/) | All the [**clippy**](https://github.com/rust-lang/rust-clippy) lints you might be interested in. |
| [Configuring Rustfmt](https://rust-lang.github.io/rustfmt/) | All [**rustfmt**](https://github.com/rust-lang/rustfmt) options you can use in `.rustfmt.toml`. |
| [Compiler Error Index](https://doc.rust-lang.org/error-index.html) | Ever wondered what `E0404` means? |
</div>

{{ tablesep() }}


提供信息或工具的在线服务。

<div class="color-header lavender">

<!-- Other online web services related to Rust. As a heuristic, things here should
    be essential (or at least address a major concern as "best of class") and be
    a self-contained, user-facing web site. -->
| Services&nbsp;⚙️ | Description |
|--------| -----------|
| [crates.io](https://crates.io/) | All 3<sup>rd</sup> party libraries for Rust. |
| [std.rs](https://std.rs/) | Shortcut to `std` documentation. |
| [docs.rs](https://docs.rs/) | Documentation for 3<sup>rd</sup> party libraries, automatically generated from source. |
| [lib.rs](https://lib.rs/) | Unofficial overview of quality Rust libraries and applications. |
| [caniuse.rs](https://caniuse.rs/) | Check which Rust version introduced or stabilized a feature. |
| [Rust Playground](https://play.rust-lang.org/) | Try and share snippets of Rust code. |
| [Rust Search Extension](https://rust.extension.sh/) | Browser extension to search docs, crates, attributes, books, &hellip;|

</div>

{{ tablesep() }}


## 打印 PDF {#printing-pdf}


> Want this Rust cheat sheet as a PDF? Download the <a href="https://s3.eu-central-1.amazonaws.com/cheats.rs/rust_cheat_sheet.pdf"><b>latest PDF here</b></a>. Alternatively, generate it yourself via <i>File > Print</i> and then "Save as PDF" (works great in Chrome, has some issues in Firefox).

</noprint>

<footer>

[Ralf Biedert](https://xr.io), {{ year() }} – [cheats.rs](https://cheats.rs)
<br/>
中文翻译 [Kingfree](https://github.com/kingfree)
<br/>
<noprint>

[许可证](legal)

</noprint>

</footer>
