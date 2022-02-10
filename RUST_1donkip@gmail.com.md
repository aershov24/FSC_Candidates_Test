# Topic: RUST

**Author**: Allan Kiprop

**QAs Total**: 3

## Q: Why to use `lock` statement in C#?

**Difficulty:** `Junior`

**Source:**

https://stackoverflow.com/questions/6029804/how-does-lock-work-exactly

**Details**:

Provide some code example.

**Answer:**

The `lock` keyword ensures that one thread _does not enter a critical section of code_ while another thread is in the critical section. If another thread tries to enter a locked code, it will wait, block, until the object is released.

The `lock` keyword calls [`Enter`](http://msdn.microsoft.com/en-us/library/system.threading.monitor.enter.aspx) at the start of the block and [`Exit`](http://msdn.microsoft.com/en-us/library/system.threading.monitor.exit.aspx) at the end of the block. `lock` keyword actually handles [`Monitor`](http://msdn.microsoft.com/en-us/library/System.Threading.Monitor%28v=vs.110%29.aspx) class at back end.

For example:

```cs
private static readonly Object obj = new Object();

lock (obj)
{
  // critical section
}
```

---

## Q: What is the difference between `INNER JOIN` and `OUTER JOIN`?

**Difficulty**: `Junior`

**Source:**

https://github.com/chetansomani/SQL-Interview-Questions

**Answer:**

Assuming you're joining on columns with no duplicates, which is a very common case:

* An `INNER JOIN` of A and B gives the result of A intersect B, i.e. the inner part of a **Venn diagram** intersection.
* An `OUTER JOIN` of A and B gives the results of A union B, i.e. the outer parts of a **Venn diagram** union.
* A `LEFT OUTER JOIN` will give all rows in A, plus any common rows in B.
* A `RIGHT OUTER JOIN` will give all rows in B, plus any common rows in A.
* A `FULL OUTER JOIN` will give you the `union` of A and B, i.e. all the rows in A and all the rows in B. If something in A doesn't have a corresponding datum in B, then the B portion is null, and vice versa.

Consider:

![](https://i.stack.imgur.com/1UKp7.png)
