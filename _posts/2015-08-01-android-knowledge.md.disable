---
layout: post
title: 《第一行代码》读书笔记
category: blog-cn
tags: Android 面试
keywords: 
description:
---


### 说明

最近在准备校招的面试，为了准备的系统一点，又看了一遍郭霖大神的《第一行代码》，看的过程做了一些笔记，誊抄到这里，方便自己复习。


### 一. Android系统架构
>1. Linux内核层（Linux Kernel）——为硬件提供驱动
>2. 系统运行库（Android runtime & Libraries）——Android特性支持+核心库+虚拟机
>3. 应用框架层（Application Framework）——提供构建应用程序时，可能用到的API
>4. 应用层（Application）应用程序

### 二. 四大组件
>1. 活动（Activity）：程序界面
>2. 服务（Service）：不需要与用户交互，在后台运行的组件
>3. 广播接收器（Broadcast Receiver）：允许应用程序接收到各种广播，比如短信，电话...
>4. 内容提供者（Content Provider）：为应用程序的数据共享提供了可能

### 三.Activity

#### 1. 如何标识应用的首界面？ 
>1. 设置ACTION为MAIN: <action android:name="android.intent.ACTION.MAIN"/>
>2. 设置Category为LAUNCHER:<category android:name="android.intent.category. LAUNCHER"/>

#### 2. 如何向下一个Activity传递数据？
>利用Intent，putExtra（）函数

#### 3. 如何向上一个Activity传递数据？
>在上一个Activity利用startActivityForResult()，并且重写onActivityResult（）方法，在下一个Activity中用setResult（）方法传递数据

#### 4. Activity的生命周期？
>1. onCreate():新建Activity，不可见
>2. onStart():开始Activity，可见，但不可交互
>3. onResume():进入运行状态，可见，也可交互
>4. onPause():进入暂停状态，部分可见，不可交互
>5. onStop():进入停止状态，完全不可见
>6. onDestroy():进入销毁状态

#### 5. Activity的管理？
>Task（返回栈）

#### 6. Activity被迫被系统回收时，如何保存临时数据？
>重写onSaveInstanceState()方法，将数据保存在Bundle参数中，在onCreate()方法中，判断bundle参数是否为null，若不为null，则从中取出保存的参数

#### 7. Activity的四种启动方式
>1. standard:默认启动方式，每次启动都会创建该活动的一个新的实例
>2. singleTop:若启动时，返回栈的栈顶为该Activity的实例，则直接使用该实例，不新建
>3. singleTask：若启动时，返回栈内已有该Activity的实例，则该Activity实例以上的Activity全部出栈，直接使用该实例
>4. singleInstance：启动时新建一个新的返回栈来管理这个Activity

#### 8. 如何打印出某个界面对应的Activity名称（如何知道当前界面在哪一个活动）？
>在Activity的onCreate()方法中，getClass().getSimpleName();

#### 9. 如何随时随地的退出程序？
>实现一个Activity管理类，用一个List保存所有的Activity实例，打开新的实例的时候，调用addActivity()方法，关闭Activity时调用removeActivity方法，退出程序时调用finishAll()方法。

### 四.布局&控件

#### 1. 四大布局都有啥？
>RelativeLayout, LinearLayout, FrameLayout, TableLayout

#### 2. LinearLayout布局中，layout_gravity和gravity属性有啥不同？
>layout_gravity指的是控件相对于父布局的位置，gravity指的是空间中的文字相对于控件的位置

#### 3. 如何优化ListView的性能？
>1. 在getView方法中，利用convertView进行Item布局的重用（省去了inflate方法）
>2. 利用内部类ViewHolder进行控件的重用（省去了findViewById()）

#### 4. Android中的常见单位？
>1. px:像素
>2. pt:磅，1pt=1/72英寸
>3. dp/dip:密度无关像素（设备独立像素），在160dpi屏幕上，1dp=1px；在320dpi屏幕上，1dp=2px
>4. dpi：像素密度，屏幕每英寸所包含的像素数
>5. sp：scaled pixels，主要用于描述字体大小，1sp=（dpi/72）pt

### 五.广播

#### 1. 广播分为哪几种，有什么区别？
>1. 标准广播：一种异步执行的广播，广播发出后，所有的广播接收器几乎同一时间接收到广播，它们之间没有先后关系，该广播也是无法截断的
>2. 有序广播：一种同步执行的广播，广播发出后，同一时刻只有一个广播接收器能够接收到该广播，当该广播接收器处理完后，广播继续传播。优先级高的广播接收器先接收到广播消息，还可以截断正在传递的广播。

#### 2. 注册广播的方式分为几种？

>两种
>
>1. 静态注册：在AndroidManifest.xml文件中注册
>2. 动态注册：在代码中注册

#### 3. 何为本地广播？

>本地广播，只能在本应用内发送和接收，用LocalBroadcastManager进行管理

### 六.数据持久化

#### 1. 数据的持久化存储方式有哪几种，分别适用于存储哪些数据？
>1. 文件存储，适用于存储一些简单的文本或二进制文件
>2. SharedPreferences，适用于存储一些键值对，比如账号，密码等（为.xml格式文件）
>3. 数据库存储（SQLite），适用于存储负载的关系型数据（为.db格式文件）

#### 2. 文件存储的保存和读取功能依赖的两个核心方法为？
>openFileInput()和openFileOutput()

#### 3. 文件存储的保存路径为？
>/data/data/<package name>/files/目录下

#### 4. SharedPreferences文件的保存路径为？
>/data/data/<package name>/shared_prefs/目录下

#### 5. 利用SQLiteOpenHelper创建的数据库存放的路径为？
>/data/data/<package name>/databases/目录下

#### 6. 获取SharedPreferences对象的三种方法？
>1. Context类的getSharedPreference()方法，两个参数：一个文件名和一个操作模式
>2. Activity类的getPreference()方法，一个参数，即操作模式
>3. PreferenceManager类的静态方法getDefaultSharedPreference()

#### 7. Android中如何创建或升级数据库？
>1. 先编写一个类继承SQLiteOpenHelper，实现onCreate()和onUpdate()方法
>2. 在Activity代码文件中，初始化一个自定义的数据库辅助类的对象，调用getReadableDatabase()或getWritableDatabase()方法，返回一个可读/可写的SQLiteDatabase数据库对象

### 七. 内容提供者

#### 1. Content Resolver和Content Provider分别有何作用？
>1. 用Content Resolver类可以去访问其他应用的共享数据（用getContentResolver获取实例）
>2. 用Content Provider类可以共享自己应用的数据

#### 2. 如何实现自己的Content Provider？
>集成Content Provider类，实现自己的Content Provider子类，重写父类的onCreate(),query(),insert(),update(),delete(),getType()方法

### 八. 媒体类

#### 1. 如何获取通知管理器和通知的实例？
>1. 通知管理器：NotificationManager manager=（NotificationManager）getSystemService（Context.NOTIFICATION_SERVICE）;
>2. 通知：Notification notification=new Notification(R.drawable.icon, "This is ticker text", System.currentTimeMillis());

#### 2. PendingIntent与Intent有何不同？
>1. 相同：它们都可以去指明某一个“意图”，都可以用于启动活动，启动服务以及发送广播
>2. 不同：Intent更加倾向于去立即执行某个动作，而PendingIntent更加倾向于在某个合适的时机去执行某个动作。所以，可以把PendingIntent简单的理解为延迟执行的Intent

#### 3. 如何拦截短信？
>在自己的应用里，注册广播接收器，接收短信到来的广播，并设置广播接收器的优先级高于系统短信应用，在onReceive()函数里abortBroadcast（）

#### 4. 播放音频的类为？它都有哪些函数？
>1. MediaPlayer
>2. setDataSource(); prepare(); start(); pause(); reset(); seekTo(); stop(); release(); isPlaying(); getDuration();

#### 5. 播放视频用到的类为？常用的控制函数为？
>1. VideoView
>2. setVideoPath(); start(); pause(); resume(); seekTo(); isPlaying(); getDuration(); suspend();

### 九.服务

#### 1. 服务（Service）适合执行哪些任务？
>适用于去执行那些不需要和用户交互，而且需要长期运行的任务

#### 2. Android的UI是线程不安全的，如何理解？
>也就是说，如果想要更新应用里的线程元素，则必须在主线程中进行，否则就会出现异常。

#### 3. 如何判断当前所在的线程是否是主线程？
> 判断 Looper.myLooper==Lopper.getMainLopper() 是否为true

#### 4. Android中异步消息处理主要包括哪几个部分？
>1. Message: Message就是在线程之间传递的消息，它可以在内部携带少量的信息，用于不同线程之间交换数据
>2. Handler：也就是消息处理者，主要用于发送和处理消息，发送消息一般使用sendMessage(),发出的消息经过一系列辗转处理后，最终会传递到Handler的HandleMessage()中
>3. MessageQueue:消息队列，每个线程都只会有一个MessageQueue对象，它主要用于存放所有通过Handler发送的消息，这部分消息会一直存在于消息队列中，等待被处理。
>4. Looper：Looper是每个线程中的MessageQueue管家，每个线程中只会有一个Looper对象，调用Looper的Loop()方法后，就会进入到一个无限循环中，然后每当发现MessageQueue中存在一条消息，就会将它取出，并传递到Handler的handleMessage()方法中

#### 5. Android异步消息处理的流程？
>首先，在主线程中创建一个Handler对象，并重写handleMessage()方法，当子线程需要进行UI操作时，就创建一个Message对象，并通过主线程的Handler对象将这条消息发出去，之后这条消息被添加到主线程的MessageQueue中等待被处理，而Looper则会一直尝试从MessageQueue中取出待处理消息，最后分发回Handler中的handleMessage()方法中。因为Handler是在主线程中创建的，将所以此时的handleMessage()方法中的代码也是在主线程运行的，因此可以放心的进行UI操作了

#### 6. AsyncTask的概念及基本点
>1. AsyncTask的实现原理也是基于异步消息处理机制的，只是Android帮我们做了很好的封装而已
>2. AsyncTask是一个抽象类，所以如果我们想使用它，就必须要创建一个子类去继承它
>3. 经常要重写的四个方法：onPreExecute(), doInBackground(Params...)(若需要更新元素，调用publishProgress(Progress)方法)，onProgressUpdate(Progress), onPostExecute(Result)

#### 7. 服务的生命周期？
>1. 用startService()开启服务后会执行onCreate(),onStart()方法，若已经在运行，则只会执行onStart()方法
>2. 用bindService()开启服务后会执行onCreate(),onBind()方法，若已经在运行，则只会执行onBind()方法，调用unBindService()会结束服务，执行onDestroy()
>3. 若同时用了startService和bindService开启服务，则必须同时调用了stopService()和UNBindService()才会执行onDestroy()方法
>4. 无论调用了多少次startService()或bindService()，service都只有一个实例，调用一次stopService()或UNBindService()即可结束

#### 8. IntentService的概念及要点
>1. service是默认运行在主线程的，若直接在服务里去处理一些耗时的逻辑，就很容易出现ANR（Application Not Responding）,因此，我们应该在服务的方法里开启一个子线程，在里面处理那些耗时的逻辑
>2. service开启后是一直运行的，所以，完成任务后，应调用stopSelf()停止自身
>3. 为了可以简单的创建一个异步的，会自动停止的任务，Android专门提供了一个IntentService类，在子类中实现onHandleIntent()这个抽象方法，在这个方法里处理一些具体的逻辑

### 十. 网络

#### 1. 常用的发送Http请求的两种方式？
>HttpURLConnnection和HttpClient

#### 2. 解析xml的两种方法？
>pull和SAX

#### 3. 解析Json的两种方法？
>JsonObject和Gson

#### 4. Fragment的生命周期及相应的回调方法？
>添加一个碎片——onAttach()——onCrate()——onCreateView()——onActivityCreated()——onStart()——onResume()——碎片激活——onPause()——onStop()——onDestroyView()——onDestroy——onDetach()——碎片销毁