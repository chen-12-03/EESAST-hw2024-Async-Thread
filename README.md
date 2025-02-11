
作业共两道题，**任选一道题作答即可**. 在提交的 PR 里需要注明作答了哪道题或者全部作答.

提交的 PR 中只需要看第二个部分 “No unresolved conversations”(绿色打勾) / “Unresolved conversations”(红色打叉)；**如果显示为后者，请按照 review comment 修改代码**.

## 第 1 题

**作业要求:**

- 设计一系列异步计算结点，并进一步组织为一颗计算树；当数据结点发生变化的时候，与之关联的所有上级结点都将更新它们的输出.
- 打开 `HW-Async&Thread-1/` 下的 C# 项目，根据已有的代码编写完整程序. 可以根据自己的想法适当修改已有结构，也可以完全不遵循已有结构，使用如多线程等其他方案实现.
- 对计算的要求: 必须在数据变化之后立即开始 (即异步计算)，而不能在读取输出值时才开始 (即同步计算).
  - 一个例子: `Val` 属性中不得存在计算过程 (如 `val = ExprA.val + ExprB.val;`)，可以将计算过程放在 `Update` 里面.
- 输出应当准确无误；或者，你也可以提供一个 `bool` 属性，指示输出值是否可以读取.

**拓展要求:**

在各结点的计算前加上延时，比如

```CS
val = ExprA.val + ExprB.val;
```

改成

```CS
Thread.Sleep(100);
// 或Task.Delay(100).Wait();
val = ExprA.val + ExprB.val;
```

思考我们应当如何使用这些计算结点.

## 第 2 题

**作业要求:**

- 设计一个随时间在一定范围内变化的变量；可以改变变化的方向 (增减) 以及变化的速度，也可以在某一时刻强制设置为一个特定值；应当能够安全地读取变量的值.
  - 一个实例: 初始值为 $0$、初始速度为 $1$，并且在第 $200$ 毫秒变速为 $2$，那么在第 $300$ 毫秒的理论值应当为 $1 \times 200 + 2 \times 100 = 400$.
- 打开 `HW-Async&Thread-2/` 下的 C# 项目，根据已有的代码编写完整程序. 这道题最好采用多线程的方式解决，应当维护变量的线程安全性 (即解决多线程的读写互斥问题).
- 所谓的“随时间变化”，并不一定需要 `val` 实时发生变化，只要在某些特定的时间点改变即可.
- 用 `Environment.TickCount` 获取当前时间的毫秒数.