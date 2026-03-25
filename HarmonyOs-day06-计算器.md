#### 实现一个计算器功能，看看学到了哪些知识
- **UI**：计算器就是很多个按钮，最简单的是4x5=20个按钮
  - 每个按钮想做出点击效果，按下去是橘黄色，于是自定义一个Button
    - <img width="602" height="534" alt="image" src="https://github.com/user-attachments/assets/63c9ced5-fee4-4af5-b40b-c1e71f489d08" />
    - @State 注解依然是负责**内部**状态数据和ui的联动
    - @Prop 注解负责接收**外部**传参和内部ui的联动，比如清空按钮的显示，会根据输入框是否有内容，切换"C"和"AC"的文字显示
  - 布局是5行4列，如果摊开了写，会显得很繁琐，于是自定义一个可动态添加任意个子组件的**行**布局
    - <img width="660" height="540" alt="image" src="https://github.com/user-attachments/assets/1553d1ec-6172-4318-91e3-5f8d006c4959" />
    - 这里的子组件直接添加的按钮，也可以定义一个block，由外界传入，用于添加其他类型的子组件。这么做的好处是，使用方便，且可以复用
    - <img width="670" height="534" alt="image" src="https://github.com/user-attachments/assets/12096cc9-fab5-4772-835f-0509812d81da" />
  - 按钮之间添加分割线
    - 横向：Divider().vertical(false).color(Color.Orange).strokeWidth(1).width(240)
    - 竖向：Divider().vertical(true)
  - 显示输入内容的组件，不需要使用TextInput，使用Text即可。
  - 删除按钮使用图片显示
    - Image($r('app.media.delete'))，这样写，是引用的项目内media下的图片。
    - <img width="311" height="199" alt="image" src="https://github.com/user-attachments/assets/2d52c52c-2611-43f0-bf95-3417e57c2fb3" />
    - interpolation(ImageInterpolation.High)，控制图片显示质量。colorFilter，可以实现对图片的颜色混合渲染，这里是显示成白色图片
    - <img width="559" height="455" alt="image" src="https://github.com/user-attachments/assets/16ed1ee9-39d2-4567-ac0f-50e02c33107b" />
    - Image($rawfile('minions.png'))，这样写，是引用的项目内的rawfile下的图片。
    - <img width="297" height="139" alt="image" src="https://github.com/user-attachments/assets/01abf66a-d02f-4bd9-bf95-67bee39ce9b7" />
    - Image('http://xxxx.png')，这样写，是网络图片，需要添加网络权限，位置在main/module.json5中
    - <img width="491" height="250" alt="image" src="https://github.com/user-attachments/assets/6e0de934-07f6-426a-a116-a2abfa14d6fc" />





