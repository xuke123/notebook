#主线程循环

* 每秒一次

   1. 日志缓存刷新到磁盘,即使这个事务没有提交(总是)
   1. 合并插入缓存(可能)
   1. 至多刷新100个InnoDB缓冲池中脏页到磁盘(可能)
   1. 如果当前没有用户活动,切换到background loop(可能)

* 十秒一次
    1. 刷新100个脏页到磁盘(可能)
    1. 合并至多5个插入缓存(总是)
    1. 将日志缓冲刷新到磁盘(总是)
    1. 删除无用undo页(总是)
    1. 刷新100个或者10个脏页到磁盘(总是)

* 后台循环

    1. 删除无用undo页(总是)
    2. 合并20个插入缓存(总是)
    3. 跳回主循环(总是)
    4. 不断刷新100个页直到符合条件(可能,跳转到flushloop完成)
 
* 刷新循环

* 暂停循环
  
(无事可做时,挂起,等待时间)