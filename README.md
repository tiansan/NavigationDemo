# NavigationDemo

在创建导航图之前，必须为项目设置导航架构组件。要在Android Studio中设置项目，请执行以下操作。
   
1、单击文件>设置（Mac上的Android Studio>首选项），在左窗格中选择Experimental，选中Enable Navigation Editor，然后重新启动Android Studio。

2、将以下导航架构组件添加到您的应用程序或模块的 build.gradle文件中。有关添加体系结构组件的更多信息 build.gradle，请参阅向项目添加组件。

注意：如果要在Android Studio中使用导航架构组件，则必须使用Android Studio 3.2 Canary 14或更高版本。
   
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
      implementation "android.arch.navigation:navigation-fragment:$rootProject.navigationVersion"
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

在MainAcitivty中使用：
```kotlin

   class MainActivity : AppCompatActivity() {

       private lateinit var appBarConfiguration: AppBarConfiguration
       private lateinit var navController: NavController

       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_main)
           navController = Navigation.findNavController(this, R.id.garden_nav_fragment)
           appBarConfiguration = AppBarConfiguration(navController.graph, drawer_layout)

           setSupportActionBar(toolbar)
           setupActionBarWithNavController(navController, drawer_layout)

           navigation_view.setupWithNavController(navController)
       }

       override fun onSupportNavigateUp(): Boolean {
           return navController.navigateUp(appBarConfiguration) || super.onSupportNavigateUp()
       }

       override fun onBackPressed() {
           if (drawer_layout.isDrawerOpen(Gravity.START)) {
               drawer_layout.closeDrawer(Gravity.START)
           } else {
               super.onBackPressed()
           }
       }
   }

```
