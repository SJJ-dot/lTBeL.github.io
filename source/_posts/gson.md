---
title: gson
date: 2018-05-30 23:06:59
categories:
- android
tags: 
- json
---
>序列化带Expose注解的字段 
```kotlin
@Expose
var key = "";

val gson = GsonBuilder().excludeFieldsWithoutExposeAnnotation().create()
```

>序列化跳过带Expose注解的字段 （这里不想自己再去写注解声明就用了原来的）
```kotlin
val gson = GsonBuilder().addSerializationExclusionStrategy(object : ExclusionStrategy {
    override fun shouldSkipClass(clazz: Class<*>?): Boolean = false

    override fun shouldSkipField(f: FieldAttributes): Boolean {
        val expose = f.getAnnotation(Expose::class.java)
        return expose != null && !expose.serialize
    }
}).create()

@Expose(serialize = false,)
var key = 0;

```

>序列化别名
```kotlin
@SerializedName("authed") //json 中名字为authed
Authedaaaaa

@SerializedName(value = "ret", alternate = [ "code"])
var ret: Int = 0

```
>反序列化
```kotlin

inline fun <reified T> Gson.fromJson(json: String): T {
    return fromJson(json, object: TypeToken<T>() {}.type)
}

```
>json 数字类型返回空字符串异常处理
```kotlin

val gson = GsonBuilder()
        .also { gb ->
            ScalarsJsonDeserializer.types.forEach { gb.registerTypeAdapter(it, ScalarsJsonDeserializer) }
        }.create()

private object ScalarsJsonDeserializer : JsonDeserializer<Any> {
    val types = arrayOf<Type>(String::class.java,
            Boolean::class.java,
            Byte::class.java,
            Char::class.java,
            Double::class.java,
            Float::class.java,
            Int::class.java,
            Long::class.java,
            Short::class.java
    )

    override fun deserialize(json: JsonElement?, typeOfT: Type?, context: JsonDeserializationContext?): Any? {
        return try {
            when (typeOfT) {
                String::class.java -> json?.asString
                Boolean::class.java -> json?.asBoolean
                Byte::class.java -> json?.asByte
                Char::class.java -> json?.asCharacter
                Double::class.java -> json?.asDouble
                Float::class.java -> json?.asFloat
                Int::class.java -> json?.asInt
                Long::class.java -> json?.asLong
                Short::class.java -> json?.asShort
                else -> null
            }
        } catch (e: Exception) {
            null
        }
    }

}
```


# 