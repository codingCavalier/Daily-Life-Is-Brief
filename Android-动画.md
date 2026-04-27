1. ViewPropertyAnimator
- 简介 
  - 它不是`Animator`的子类，而是一个独立的类
  - **它在view内部，是单例的，所有属性动画，共享一个`ViewPropertyAnimator`**
  - **view的属性变化，靠的是native层修改，靠的是view内部的RenderNode对象**，不仅仅是动画，平时我们修改view的属性，也是通过native层修改
  - <img width="654" height="274" alt="image" src="https://github.com/user-attachments/assets/0d6e9b6b-888d-42d1-a656-e770356052a8" />
- 动画的驱动
  - 它的启动靠的是内部新建的一个`ValueAnimator`，给`ViewPropertyAnimator`添加监听后，`ValueAnimator`的启动会触发`ViewPropertyAnimator`的启动
  - 当调用`view.animate()`时，会获得一个`ViewPropertyAnimator`对象，此对象持有view的引用，然后调用`.translationX(xx)`时，内部会记录下此时此刻view的`translationX`的值，作为起始值。**因此，修改view的初始值，必须在调用位移透明度旋转等相关操作，前设置，在`onAnimationStart`回调时设置初始值，为时已晚**
  - `ViewPropertyAnimator`动画的执行，靠的是`ValueAnimator`的`onAnimationUpdate`的回调，`ViewPropertyAnimator`里面针对每次startAnimation都会存储一份`PropertyBundle`，用于记录这次动画所有修改的属性相关的数据，包括：属性在native层的指针，起始值，结束和起始的差值（这个差值乘以百分比的进度，就是属性值每次需要变化的增量）

2. ValueAnimator
- 简介
  - `Animator`的直接子类。`Animator`的另一个直接子类是`AnimatorSet`，一共就这两个直接子类。
  - `ValueAnimator`的两个直接子类是`ObjectAnimator`和`TimeAnimator`
  - 有`setIntValues`、`setFloatValues`、`setObjectValues`等方法用于设置起始值和结束值
- 动画的驱动
  - 靠的是`AnimationHandler`，其内部维护与`Choreographer`的交互，靠`Choreographer`的回调，触发每一帧动画的计算和属性赋值
