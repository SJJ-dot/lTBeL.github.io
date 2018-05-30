---
title: android 备份数据库文件
date: 2018-05-30 22:55:59
categories:
- android
tags: 
- database
---
```java
File filesDir = null;
try {
    filesDir = new File(getFilesDir().getParentFile(), "databases");
    for (File file : filesDir.listFiles()) {
        Log.e(file);
        FileInputStream fileInputStream = new FileInputStream(file);
        byte[] buffer = new byte[4096];
        int len;
        ByteArrayOutputStream byteArrayOutputStream = new ByteArrayOutputStream();
        Base64OutputStream base64OutputStream = new Base64OutputStream(byteArrayOutputStream, Base64.DEFAULT);
        while ((len = fileInputStream.read(buffer)) != -1) {
            base64OutputStream.write(buffer, 0, len);
        }
        fileInputStream.close();

        ByteArrayInputStream byteArrayInputStream = new ByteArrayInputStream(byteArrayOutputStream.toString().getBytes());
        Base64InputStream base64InputStream = new Base64InputStream(byteArrayInputStream, Base64.DEFAULT);
        File dbfile = new File(Environment.getExternalStorageDirectory(), "dbfile/"+file.getName());
        if (!dbfile.exists()) {
            dbfile.getParentFile().mkdirs();
            dbfile.createNewFile();
        }
        FileOutputStream fileOutputStream = new FileOutputStream(dbfile);
        while ((len = base64InputStream.read(buffer)) != -1) {
            fileOutputStream.write(buffer,0,len);
        }
        fileOutputStream.flush();
        fileOutputStream.close();

    }
} catch (Exception e) {
    Log.e("aa", e);
}

Log.e(filesDir);
```