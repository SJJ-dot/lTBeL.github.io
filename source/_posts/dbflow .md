---
title: dbflow
date: 2018-05-30 22:59:59
categories:
- android
tags: 
- database
---
>类型转换
```kotlin
@com.raizlabs.android.dbflow.annotation.TypeConverter
class PointListTypeConverter : TypeConverter<String, List<Point>>() {
    private val type = object : TypeToken<List<Point>>() {}.type
    override fun getDBValue(model: List<Point>?): String = gson.toJson(model)

    override fun getModelValue(data: String?): List<Point> = gson.fromJson(data, type)

}
```


# 