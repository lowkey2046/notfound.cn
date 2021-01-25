---
title: "Ruby GC"
date: 2021-01-25T20:02:10+08:00
tags: ["ruby"]
draft: true
---

```ruby
# GC.stat
{
 :count=>24,                                # GC 次数 count = major_gc_count + minor_gc_count
 :heap_allocated_pages=>118,                # 当前已分配的堆空间
 :heap_sorted_length=>118,                  # 内存中堆的实际大小
 :heap_allocatable_pages=>0,                # 堆页面中所有槽数量
 :heap_available_slots=>48094,
 :heap_live_slots=>47939,                   # 活跃对象数
 :heap_free_slots=>155,
 :heap_final_slots=>0,
 :heap_marked_slots=>37509,
 :heap_eden_pages=>118,
 :heap_tomb_pages=>0,
 :total_allocated_pages=>118,
 :total_freed_pages=>0,
 :total_allocated_objects=>199455,
 :total_freed_objects=>151516,
 :malloc_increase_bytes=>44912,
 :malloc_increase_bytes_limit=>16777216,
 :minor_gc_count=>20,                       # minor GC 次数
 :major_gc_count=>4,                        # major GC 次数
 :compact_count=>0,
 :remembered_wb_unprotected_objects=>449,
 :remembered_wb_unprotected_objects_limit=>672,
 :old_objects=>36480,
 :old_objects_limit=>56796,
 :oldmalloc_increase_bytes=>1216872,
 :oldmalloc_increase_bytes_limit=>16777216
 }
```

- 对象内存占用计算
- 内存泄漏判断

## 参考

- [Understanding Ruby GC through GC.stat](https://ruby-china.org/topics/37982)
