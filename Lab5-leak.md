### Diagnosing a Memory Leak

In this lab, you will use PerfView to diagnose a memory leak in a .NET application.

#### Task 1

Run the **MemoryLeak\Binaries\MemoryLeak.exe** application. It prints out some statistics about processed requests and its memory usage. As you can see, the memory usage is going up.

Run **PerfView.exe** and click **Memory** > **Take Heap Snapshot**. Locate the **MemoryLeak.exe** process and click **Dump GC Heap**. A minute later, take another snapshot. At this point, you can close the **MemoryLeak.exe** process.

#### Task 2

In PerfView, double-click the **MemoryLeak.gcdump** file on the left pane. You should get a report of the largest types on the heap. These should be `Request`, `Response`, and `DbConnection`. The **Exc Ct** column indicates the number of objects from that type, and the **Exc** column indicates the number of bytes occupied by these objects.

Double-click the **MemoryLeak.1.gcdump** file on the left pane. To compare this snapshot to the baseline, use **Diff** > **With Baseline**. It looks like we have a steady memory leak.

Double-click the largest type (which should be `Request`). PerfView will show you what’s keeping objects of that type in memory. At this point, you should be equipped to go back to the application’s code (under **MemoryLeak\Sources**) and determine how to fix the problem.

#### Task 3 (Optional)

Remove the offending code and run the application again. Use PerfView again to verify that there are no memory leaks anymore.
