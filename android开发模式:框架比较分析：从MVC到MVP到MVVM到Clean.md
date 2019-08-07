## 开发模式对比分析

|MVC|MVP|MVVM|MVPVM|Clean
|---|---|---|---|---|---|---|---|
|修改|3|4|5|5|5
|新增|3|5|4|5|5
|复用|3|4|4|4|5
|单元测试|3|4|5|5|4
|UI测试|4|4|4|4|4
|学习成本|3|4|5|5|5
|代码复杂度|3|4|5|5|5
|实现复杂度|1|3|2|4|5|
|代码量|1|3|2|4|5|
|可读性|2|4|1|4|4|
|可维护性|1|3|2|4|5|
|优点|开发简单|模型视图分离，逻辑清晰|双向绑定，简洁清晰|逻辑清晰，耦合度低|耦合度极低
|缺点|业务增加后，不易维护|抽象接口较多|可读性较差，出现问题不易定位|实现业务复杂度高|业务实现复杂读极高
|适用场景|极小型项目|中大型项目|中大型项目|大型项目|超大型项目

## 模式详解
### MVC
![MVC](https://img-blog.csdnimg.cn/20190513133917201.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIzMDgxNzc5,size_16,color_FFFFFF,t_70)
1. 介绍
     MVC=Model+View+Controller
* Model：数据模型层，主要负责数据的获取
* View：视图层，页面的显示，即xml
* Controller：控制器，业务逻辑的核心控制，即activity/fragment
2. 详细实现
* 略
3. 详解参考
* Android开发模式之MVC：https://www.jianshu.com/p/f98bd6650014
* 
### MVP
![MVP](https://img-blog.csdnimg.cn/20190513134023937.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIzMDgxNzc5,size_16,color_FFFFFF,t_70)
1. 介绍
    MVP=Model+View+Presenter
* Model：数据模型层，主要负责数据的获取
* View：视图层，页面的显示，即xml+activity/fragment
* Presenter：控制器，业务逻辑的核心控制
2. 详细实现
  代码地址：https://github.com/googlesamples/android-architecture/tree/todo-mvp-dagger/ ，我们拿该项目中的taskDetail来举例分析说明
* TaskDetailContract：view和presenter的抽象接口层，两个接口合在一起写，方便实现和管理，是解决mvp中接口过多的一种方式
* TaskDetailFragment：view的实现层，实现了TaskDetailContract中view的抽象接口
* TaskDetailPresenter：presenter的实现层，实现了TaskDetailContract中presenter的抽象接口
* TaskDetailModule：依赖关系定义层，定义了依赖注入中的依赖关系
3. 扩展封装
	[MvpDaggerArch架构使用文档](https://blog.csdn.net/qq_23081779/article/details/96143754)
5. 详解参考
* 深入浅出Dagger2 : 从入门到爱不释手: https://www.jianshu.com/p/626b2087e2b1
* Google官方MVP+Dagger2架构详解: https://www.jianshu.com/p/01d3c014b0b1
### MVVM
![MVVM](https://img-blog.csdnimg.cn/2019051313404167.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIzMDgxNzc5,size_16,color_FFFFFF,t_70)
1. 介绍
    MVVM=Model+View+ViewModel
* Model：数据模型层，主要负责数据的获取
* View：视图层，页面的显示，即xml+activity/fragment
* ViewModel：控制器，业务逻辑的核心控制
2. 详细实现
   代码地址：https://github.com/googlesamples/android-architecture/tree/todo-mvvm-databinding/ ，我们仍然拿TaskDetail来举例分析
  * taskdetail_frag.xml: View层
   * TaskDetailViewModel: ViewModel层
   * TaskDetailFragment: 对View和ViewModel进行初始化
 
### MVPVM
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190513134610502.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIzMDgxNzc5,size_16,color_FFFFFF,t_70)
1. 介绍
MVPVM=Model+View+Presenter+ViewModel
在没有使用类似MVP架构的时候，逻辑一般都直接写在了Activity或者Fragment里，导致View层很臃肿，业务逻辑、UI操作和数据耦合到了一起，结构混乱。现在，View层要处理的逻辑全部委托给Presenter处理，View层专注实现UI，Presenter专注实现业务逻辑，它们之间通过View Interface和Presenter Interface交互。在google推出databinding后，View Interface的部分功能可以转移到ViewModel中去，进一步降低View层的臃肿。
* View层：实现View Interface，对外提供showDialog、showToast之类的方法
* ViewModel层：以databinding为基础，对外提供控制xml界面的方法
* Presenter层：实现Presenter Interface，处理业务逻辑
* Model层：服务器数据对应数据模型类
2. 详细实现
* 略


### Clean
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190513134203235.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIzMDgxNzc5,size_16,color_FFFFFF,t_70)
1. 介绍
    Clean 一般是指，代码以洋葱的形状依据一定的依赖规则被划分为多层：内层对于外层一无所知。这就意味着依赖只能由外向内。
2. 详细实现
  代码地址：https://github.com/android10/Android-CleanArchitecture ，该项目主要分为以下几个模块
* domain：抽象业务层
* data：数据层
* presentation：展示层
3. 详解参考
* The Clean Architecture-Uncle Bob ：https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html