+++
title = "Ruby Process.spawn 缓冲区阻塞"
author = ["likui"]
date = 2021-05-13T21:00:00+08:00
lastmod = 2021-05-13T21:26:28+08:00
tags = ["ruby"]
draft = false
+++

## Ruby Process.spawn 阻塞 {#ruby-process-dot-spawn-阻塞}

Ruby 中使用 `Process.spawn` 和 `pipe` 时，缓冲区为 64KB，如果不及时读取数据，将会发生阻塞。

```ruby
#!/usr/bin/env ruby

# cmd = "bash -c 'for i in {1..6500}; do echo '123456789'; done'"
cmd = "bash -c 'for i in {1..6600}; do echo '123456789'; done'"

pipe_cmd_in, pipe_cmd_out = IO.pipe
cmd_pid = Process.spawn(cmd, :out => pipe_cmd_out, :err => pipe_cmd_out)

Process.wait(cmd_pid)
exitstatus = $?.exitstatus

pipe_cmd_out.close
out = pipe_cmd_in.read
puts "child: cmd out length = #{out.length}; Exit status: #{exitstatus}"
```


### 参考 {#参考}

-   <https://stackoverflow.com/questions/13829830/ruby-process-spawn-stdout-pipe-buffer-size-limit>
