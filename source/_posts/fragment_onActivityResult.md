---
title: fragment_onActivityResult
date: 2018-05-30 23:07:59
categories:
- android
tags: 
- lifecycle
---
```java
class AuthHandlerFragment : Fragment() {
        private val requestCode = 100
        var callBack: ((requestCode: Int, resultCode: Int, data: Intent?) -> Unit)? = null
        val intent :Intent = Intent("action")
        init {
            intent.putExtra("token", "token")
        }
        override fun onAttach(context: Context?) {
            super.onAttach(context)
            startActivityForResult(intent,requestCode)
        }
        override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
            if (requestCode == this.requestCode) {
                callBack?.invoke(requestCode, resultCode, data)
            } else
                super.onActivityResult(requestCode, resultCode, data)
        }
    }
```


# 