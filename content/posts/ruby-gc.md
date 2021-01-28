---
title: "Ruby GC"
date: 2021-01-20T10:27:23+08:00
tags: ["ruby"]
draft: true
---


```ruby
# ruby 2.7.2

{
  :count=>24,          # GC 次数
  :minor_gc_count=>20, # 尝试回收生存时间小于等于 3 个 GC 周期的对象
  :major_gc_count=>4,  # 尝试回收所有对象
  :compact_count=>0,   # 压缩移动对象次数，可减少内存碎片

  :heap_sorted_length=>119,

  :heap_available_slots=>48505,  # 所有 slots 数量
  :heap_live_slots=>48330,       # 存活 slots 数量
  :heap_free_slots=>175,         # 空想 slots 数量
  :heap_final_slots=>0,          #
  :heap_marked_slots=>36741,     # 旧对象 slots 数量

  :heap_allocated_pages=>119,    # 已分配堆 page 数量
  :heap_allocatable_pages=>0,    # 可分配堆 page 数量

  :heap_eden_pages=>119,
  :heap_tomb_pages=>0,
  :total_allocated_pages=>119,
  :total_freed_pages=>0,

  :total_allocated_objects=>200406,
  :total_freed_objects=>152076,

  :remembered_wb_unprotected_objects=>434,
  :remembered_wb_unprotected_objects_limit=>644,

  :old_objects=>35848,           # 老对象数量
  :old_objects_limit=>56878,

  :malloc_increase_bytes=>81712,             # 堆外对象分配的空间
  :malloc_increase_bytes_limit=>16777216,
  :oldmalloc_increase_bytes=>1243928,        # old 堆外对象分配空间
  :oldmalloc_increase_bytes_limit=>16777216
}
```

heap 中的每个 RValue 结构体大小为 40bytes，并不能存放 long_str 那么大的字符串，当超出这个范围的时，Ruby 将其存放到了系统的 heap 去了，已经不由 RValue 结构来存储了。从

## 参考

- [关于 Ruby 内存使用的一些优化和探索](https://ruby-china.org/topics/27057)
- [Ruby GC 自述](https://ruby-china.org/topics/37118)
- [Understanding Ruby GC through GC.stat](https://ruby-china.org/topics/37982)
- [Ruby 内存分配](https://www.jianshu.com/p/e4f184e92375)
- [How Ruby Uses Memory](https://ruby-china.org/topics/25790)
