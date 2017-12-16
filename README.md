# FragmentRigger
![R](/images/R.png)
![i](/images/i.png)
![g](/images/g.png)
![g](/images/g.png)
![e](/images/e.png)
![r](/images/r.png)

:boom:A powerful library to manage Fragments.    
一个强大的Fragment管理框架。（[中文版README](README-CN.md)）

![Platform](https://img.shields.io/badge/platform-Androd-green.svg)
![Release](https://img.shields.io/badge/release-1.0.0-brightgreen.svg)
![Download](https://api.bintray.com/packages/jkb/maven/fragment-rigger/images/download.svg)
![SDK](https://img.shields.io/badge/SDK-12%2B-green.svg)
![Build](https://img.shields.io/badge/build-passing-brightgreen.svg)
![Build](https://img.shields.io/badge/Powered%20by-AsPectJ-blue.svg)
[![AsPectJ](https://img.shields.io/badge/license-MIT-yellowgreen.svg)](https://github.com/HujiangTechnology/gradle_plugin_android_aspectjx)
[![JingYeoh](https://img.shields.io/badge/author-JustKiddingBaby-red.svg)](http://blog.justkiddingbaby.com/)

>This might is the library to manage fragments at the least cost of use. Do not need to extend any class!!!Do not need to extend any class!!!the most thing must be said for three times!!!
you just only cost one line annotation code when you are using `FragmentRigger`.
Principle of library is define the pointcuts for Fragment/Activity lifecycle methods and bind to the proxy class to execute.

### Feature
- [x] **Powerful api**
- [x] **Enough English notes**
- [x] **Strictest exceptions**
- [x] **Resolve usual exceptions and bugs in fragments**
- [x] **Never lost any fragment transaction commit**
- [x] **Extend the android native fragment methods,add some usual methods such as `onBackPressed()`**
- [x] **Print tree for the fragment stack**
- [x] **Fragment lazy load**
- [x] **Fragment transition animations**
- [ ] **Fragment shared elements transition animations**

### Problem solved
* ~~Fragment view overlapping~~
* ~~Fragment Multi-level showing~~
* ~~Fragment stack manager~~
* ~~Fragment transaction commit failed~~
* ~~Commit the transaction when the host activity is not resumed~~
* ~~Multiple commits are interconnected but the fragment transaction commit does not happen immediately~~
* ~~A series of exceptions when memory restarting~~
* ~~Data saved and restored when the screen is flipped~~
* ~~Can not perform this action after onSaveInstanceState~~
* ~~Lazy loading in ViewPager and other scenarios~~
* ~~The animation does not perform in different scenarios~~

### Using example
>**The library at the least cost of use** is this library's target，Provides powerful api.
this library is differ from the existed fragment library.do not need to extend any class，you just only need add one line annotation code.
you can manage fragments by proxy class，This library uses a plug-in approach to reduce the cost of use.

**1、Make your class support the library**
>Add `@Puppet` annotation for your `Activity/Fragment` that need to use this library.

```java
//MainActivity.java
@Puppet(containerViewId = R.id.atyContent)//containerViewId is the fragment to be placed in.
public class MainActivity extends AppCompatActivity
```
```java
//TestFragment.java
@Puppet
public class TestFragment extends Fragment
```

**2、Using this library to manage `Fragment`**
>Do not need extend any class，add `@Puppet` annotation，use the proxy class `Rigger` to manage fragments.

```java
@Puppet(containerViewId = R.id.atyContent)
public class MainActivity extends AppCompatActivity{
  ...
  //add and show a fragment and add it to the stack，this fragment is placed in the container view.
   Rigger.getRigger(this).startFragment(TestFragment.newInstance());
}
```

### Demo
>本项目支持常见场景下的`Fragment`操纵方式，如有不支持的场景，欢迎提交[Issues](https://github.com/JustKiddingBaby/FragmentRigger/issues)或者[Email me ](mailto:yangjing9611@foxmail.com)

|栈管理|同级替换|
|:---:|:-----:|
|<img src="/images/start.gif" width = "200px"/>|<img src="/images/replace.gif" width = "200px"/>
|支持Fragment同级\多层嵌套，并提供返回自动显示栈顶成员等一系列场景支持|在一个`container`中只显示一个Fragment，对比原生的使用，提供强大并简易的Api支持|
|[StartFragment.java](/app/src/main/java/com/yj/app/test/start/StartFragment.java)|[ReplaceFragment.java](/app/src/main/java/com/yj/app/test/replace/ReplaceFragment.java)|

|同级显示|懒加载|
|:---:|:-----:|
|<img src="/images/show.gif" width = "200px"/>|<img src="/images/lazyload.gif" width = "200px"/>|
通过`show`方法显示`Fragment`，支持预加载，懒加载等场景|支持`ViewPager`等场景下的懒加载机制，使用简单，一行注解就可以支持|
|[ShowFragment.java](/app/src/main/java/com/yj/app/test/show/ShowFragment.java)|[LazyLoadFragment.java](/app/src/main/java/com/yj/app/test/lazyload/LazyLoadFragment.java)

|栈内成员树状图|
|:----------:|
|<img src="/images/tree.png" width = "300px"/>|
|可在Log中实时查看自己栈内的成员并以树状图打印出栈内`Fragment tag`|
|[StartFragment.java](/app/src/main/java/com/yj/app/test/start/StartFragment.java)|

>上面的demo只是展示了部分常用的场景，主要是为了突出本框架强大的Api支持，一些针对`Fragment`的其他功能在上面几个demo中也有体现，
如：`转场动画`、`原生方法的扩展`等，详细使用请看Wiki。

### How to config
>本项目`AOP`的实现是通过`AsPectJ`来实现的，所以在配置本项目的同时需要加入`AsPectJ`的支持。

**1、Add in the root project `build.gradle`**
```gradle
buildscript {
    dependencies {
        ...
        classpath 'com.hujiang.aspectjx:gradle-android-plugin-aspectjx:1.0.10'
    }
}
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}
```
**2、Add in the `application` `build.gradle`**
```gralde
apply plugin: 'android-aspectjx'
android{
  ...
}
```
**3、Add in the `library` `build.gradle`**
```gradle
compile 'com.justkiddingbaby:fragment-rigger:1.0.0'
```

### Release log
##### V1.0.0[2017/12/15]  
1、完成基础功能

### License
![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f8/License_icon-mit-88x31-2.svg/128px-License_icon-mit-88x31-2.svg.png)

本项目遵循MIT开源协议. 浏览[LICENSE](https://opensource.org/licenses/MIT)查看更多信息.