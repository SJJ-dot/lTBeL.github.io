---
title: 重启APP
date: 2018-05-30 23:04:59
categories:
- android
tags: 
- crash
---
```kotlin
val restartIntent = PendingIntent.getActivity(app, 0, Intent(app,MainActivity::class.java),PendingIntent.FLAG_ONE_SHOT);
val mgr = app.getSystemService(Context.ALARM_SERVICE) as AlarmManager
mgr.set(AlarmManager.RTC, System.currentTimeMillis() + 1000, restartIntent)

System.exit(0)
```


# 