# NavigationDemo

在项目里的build.gradle添加
```java

    buildscript {
        ext {
            navigationVersion = '1.0.0-alpha09'
        }
        repositories {
            google()
        }
        dependencies {
            classpath "android.arch.navigation:navigation-safe-args-gradle-plugin:$navigationVersion"
        }
    }

```

在应用里的build.gradle添加
> java
```java

   apply plugin: 'androidx.navigation.safeargs'
   
   dependencies {
      implementation "android.arch.navigation:navigation-fragment:$rootProject.navigationVersion" // use -ktx for Kotlin
      implementation "android.arch.navigation:navigation-ui:$rootProject.navigationVersion"
   }

```
>kotlin
```kotlin

   apply plugin: 'androidx.navigation.safeargs'
   
   dependencies {
      implementation "android.arch.navigation:navigation-fragment-ktx:$rootProject.navigationVersion"
      implementation "android.arch.navigation:navigation-ui-ktx:$rootProject.navigationVersion"
   }

```
