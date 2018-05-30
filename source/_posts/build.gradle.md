---
title: build.gradle
date: 2018-05-30 23:00:59
categories:
- android
tags: 
- gradle
---
```groovy
apply plugin: 'com.android.application'
apply plugin: 'kotlin-android'
apply plugin: 'kotlin-android-extensions'
apply plugin: 'kotlin-kapt'

def shortHash = 'git log -1 --pretty=%h'.execute([], project.rootDir).text.trim().toUpperCase()
def currentBranch = 'git symbolic-ref --short -q HEAD'.execute([], project.rootDir).text.trim()
def commitCont = 'git rev-list HEAD --count'.execute([], project.rootDir).text.trim().toInteger()
android {
    compileSdkVersion 27

    defaultConfig {
        applicationId "com.skylin.uav.v02.dev"
        minSdkVersion 16
        targetSdkVersion 27
        versionCode commitCont

        buildConfigField "Integer", "Inte_V", "VALUE"
        buildConfigField "String", "AAAA", "\"$AAA\""

    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
    android.applicationVariants.all { variant ->
        variant.outputs.all {
            outputFileName = "DMZ-${currentBranch}-${variant.buildType.name}(${variant.versionCode})-${variant.versionName}.apk"
        }
    }
    productFlavors{
        flavorDimensions "base", "custom"

        beta {
            dimension "base"
            versionName "2.5.3" + "($shortHash)"

            buildConfigField "boolean", "LOG", "false"
            buildConfigField "String", "API_V2", "\"$domain_release$api_v2\""
            buildConfigField "String", "API_V3", "\"$domain_release$api_v3\""

        }
        develop {
            dimension "base"
            versionName "3.0.1.0" + "($shortHash)"

            buildConfigField "boolean", "LOG", "true"
            buildConfigField "String", "API_V2", "\"$domain_devel$api_v2\""
            buildConfigField "String", "API_V3", "\"$domain_devel$api_v3\""

        }
        common {
            dimension "custom"

        }
        custom {
            dimension "custom"
        }
    }
}

dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])

    implementation "org.jetbrains.kotlin:kotlin-stdlib-jre7:$kotlin_version"
    implementation "org.jetbrains.anko:anko:0.10.5"

    implementation 'com.android.support:appcompat-v7:27.1.1'
    implementation 'com.android.support.constraint:constraint-layout:1.1.0'

    implementation 'com.squareup.retrofit2:retrofit:2.4.0'
    implementation 'com.squareup.retrofit2:adapter-rxjava2:2.4.0'
    implementation 'com.squareup.retrofit2:converter-gson:2.4.0'
    implementation "com.squareup.retrofit2:converter-scalars:2.4.0"
    implementation 'com.squareup.okhttp3:logging-interceptor:3.9.0'

    implementation 'io.reactivex.rxjava2:rxjava:2.1.14'
    implementation 'io.reactivex.rxjava2:rxandroid:2.0.2'
    implementation 'io.reactivex.rxjava2:rxkotlin:2.2.0'

    implementation 'com.sjianjun:aLog:1.1.3'

    implementation 'org.osmdroid:osmdroid-android:6.0.1'
    //digi
    implementation 'org.slf4j:slf4j-api:1.7.25'
    implementation 'org.slf4j:slf4j-android:1.7.25'
    implementation 'com.digi:android-sdk-addon:3'

    kapt "com.github.Raizlabs.DBFlow:dbflow-processor:${dbflow_version}"
    implementation "com.github.Raizlabs.DBFlow:dbflow-kotlinextensions:${dbflow_version}"

    implementation 'com.blankj:utilcode:1.6.4'
    implementation 'com.sjianjun:permissionUtil:1.0.0'

}

```


# 