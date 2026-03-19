---
title: celery使用
tags: 
  - python
categories: 
  - 技术
date: 2026-03-19
---


消费者.py

```python
import celery
import time

from celery.schedules import crontab

backend = 'redis://127.0.0.1:6379/0'
broker = 'redis://127.0.0.1:6379/1'
cel = celery.Celery('test', backend=backend,broker=broker,include=['task01','task02'])
cel.conf.broker_connection_retry_on_startup = True
#celery -A celery_task worker -l info -P eventlet
# 设置Celery Beat的定时任务

cel.conf.beat_schedule = {
    'add-every-30-seconds': {
        'task': 'celery_task.send_msg',
        'schedule': 10.0,
        'args': ('admn',)
    },
}
cel.conf.timezone = 'UTC'

@cel.task
def send_msg(name):
    print("向%s发送邮件..." % name)
    time.sleep(5)
    print("向%s发送邮件完成" % name)
    return "ok"
```

使用
```python
from celery_task import send_msg
from task01 import eat
from task02 import drink
result = send_msg.delay("wa")
eat.delay()
drink.delay()

```

