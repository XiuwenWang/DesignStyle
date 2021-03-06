# Android Design 风格

### CoordinatorLayout 

协调AppBarLayout 和 滑动ContentView 一起动 --设置 ContentView(app:layout_behavior="@string/appbar_scrolling_view_behavior")

### AppBarLayout 

需要在子View设置 可以是：CollapsingToolbarLayout

### CollapsingToolbarLayout

<br>app:layout_scrollFlags="scroll|snap|exitUntilCollapsed|enterAlways|enterAlwaysCollapsed"
<br>scroll：必须项，没有设置不能滑动
<br>snap：就是不会停在中间 会自动滑到边界
<br>exitUntilCollapsed：exit退出 就是上滑 当你定义了一个minHeight，此布局将在滚动到达这个最小高度的时候折叠
<br>enterAlwaysCollapsed：enter进入 就是下滑 意思同上
<br>enterAlways：这个flag让任意向下的滚动都会导致该view变为可见

### Toolbar

<br>app:layout_collapseMode="pin"
<br>none：默认属性，布局将正常显示，无折叠行为。
<br>pin：CollapsingToolbarLayout折叠后，此布局将固定在顶部。
<br>parallax：CollapsingToolbarLayout折叠时，此布局也会有视差折叠效果。
<br>app:layout_collapseParallaxMultiplier="0.7"
<br>视差：说明了 就是一个快一个慢 滑动不同步


以下内如来自简书
<br>https://www.jianshu.com/p/5287d090e777

#### CoordinatorLayout 协调员布局

是用来协调其子view并以触摸影响布局的形式产生动画效果的一个super-powered FrameLayout，
其典型的子View包括：FloatingActionButton，SnackBar。注意：CoordinatorLayout是一个顶级父View。

### AppBarLayout

AppBarLayout是一个实现了很多材料设计特性的垂直的LinearLayout，它能响应滑动事件。必须在它的子view上设置app:layout_scrollFlags属性或者是在代码中调用setScrollFlags()设置这个属性。这个类的特性强烈依赖于它是否是一个CoordinatorLayout的直接子view，如果不是，那么它的很多特性不能够使用。AppBarLayout需要一个具有滑动属性的兄弟节点view，并且在这个兄弟节点View中指定behavior属性为AppBarLayout.ScrollingViewBehavior的类实例，可以使用一个内置的string表示这个默认的实例@string/appbar_scrolling_view_behavior。

AppBarLayout的子布局有5种滚动标识(上面代码CollapsingToolbarLayout中配置的app:layout_scrollFlags属性)：

scroll：所有想滚动出屏幕的view都需要设置这个flag， 没有设置这个flag的view将被固定在屏幕顶部。
enterAlways：这个flag让任意向下的滚动都会导致该view变为可见，启用快速“返回模式”。
enterAlwaysCollapsed：假设你定义了一个最小高度（minHeight）同时enterAlways也定义了，那么view将在到达这个最小高度的时候开始显示，并且从这个时候开始慢慢展开，当滚动到顶部的时候展开完。
exitUntilCollapsed：当你定义了一个minHeight，此布局将在滚动到达这个最小高度的时候折叠。
snap：当一个滚动事件结束，如果视图是部分可见的，那么它将被滚动到收缩或展开。例如，如果视图只有底部25%显示，它将折叠。相反，如果它的底部75%可见，那么它将完全展开。

### CollapsingToolbarLayout

CollapsingToolbarLayout作用是提供了一个可以折叠的Toolbar，它继承自FrameLayout，给它设置layout_scrollFlags，它可以控制包含在CollapsingToolbarLayout中的控件(如：ImageView、Toolbar)在响应layout_behavior事件时作出相应的scrollFlags滚动事件(移除屏幕或固定在屏幕顶端)。CollapsingToolbarLayout可以通过app:contentScrim设置折叠时工具栏布局的颜色，通过app:statusBarScrim设置折叠时状态栏的颜色。默认contentScrim是colorPrimary的色值，statusBarScrim是colorPrimaryDark的色值。

CollapsingToolbarLayout，音：克莱普辛。
CollapsingToolbarLayout的子布局有3种折叠模式（Toolbar中设置的app:layout_collapseMode）

off：默认属性，布局将正常显示，无折叠行为。
pin：CollapsingToolbarLayout折叠后，此布局将固定在顶部。
parallax：CollapsingToolbarLayout折叠时，此布局也会有视差折叠效果。
当CollapsingToolbarLayout的子布局设置了parallax模式时，我们还可以通过app:layout_collapseParallaxMultiplier设置视差滚动因子，值为：0~1。

### Behavior

Behavior是Android新出的Design库里新增的布局概念。Behavior只有是CoordinatorLayout的直接子View才有意义。
只要将Behavior绑定到CoordinatorLayout的直接子元素上，就能对触摸事件（touch events）、window insets、measurement、layout以及嵌套滚动
（nested scrolling）等动作进行拦截。Design Library的大多功能都是借助Behavior的大量运用来实现的。当然，
Behavior无法独立完成工作，必须与实际调用的CoordinatorLayout子视图相绑定。具体有三种方式：通过代码绑定、在XML中绑定或者通过注释实现自动绑定。
上面NestedScrollView中app:layout_behavior="@string/appbar_scrolling_view_behavior"的Behavior是系统默认的，我们也可以根据自己的需求来自定义Behavior。


