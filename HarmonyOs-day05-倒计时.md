#### 实现一个倒计时功能，看看学到了哪些知识
- **模块化开发**：倒计时功能（逻辑+ui）要抽取出一个倒计时工具类（逻辑），这个工具类不应该放在主模块里，要放在har或者hsp类型的library模块里
  - 模块间依赖：被依赖模块的oh-package.json5文件中的name字段，就是依赖模块的oh-package.json5文件中的dependencies字段里的key
  - 类的导出：工具类要导出，才能被其他模块使用。导出的管理，Index.ets文件。export修饰类。export { CountdownImpl as Countdown, CountdownCallback } from './src/main/ets/utils/public/CountdownUtil'
  - 类的导入：import { Countdown, CountdownCallback } from 'lib_b_shared_3568';
- **逻辑：接口/实现/回调**：
  - 定义一个接口：包含开始，暂停，恢复，重置，递减，结束
  - 工具类实现这个接口，并实现倒计时的完整逻辑，使用 setTimeOut & clearTimeOut 或者 setInterval & clearInterval 实现倒计时
  - 定义一个回调接口，接口里至少有一个方法，就是onTick(current: number): void，用于将每次递减后的值回调给使用方
- **ui：文本/输入框/按钮/容器**：
  - Text：文本（宽，高，字体大小，字体颜色，对齐，边框，内边距，外边距，圆角，背景色）
  - TextInput：输入框（输入拦截，变化回调）
  - Button：按钮（自定义按钮边框跟随按下状态改变颜色，点击事件，触摸事件）
  - Row：行容器
  - Column：列容器（设置宽高和主轴（列的主轴是Y轴）对齐方式：Column() { ... }.width('100%').height('100%').justifyContent(FlexAlign.Center)）
- **工具方法**
- 主线程运行、弹出吐司：
- <img width="558" height="299" alt="image" src="https://github.com/user-attachments/assets/ec52ce76-ad65-4797-9b70-bdf1de12d3ec" />
- **组件复用**
- <img width="435" height="331" alt="image" src="https://github.com/user-attachments/assets/62654d79-ebb4-4f7b-9b23-d5579c5284b9" />
- <img width="348" height="654" alt="image" src="https://github.com/user-attachments/assets/9caa665e-b383-4bb8-bab8-150c0f4ca4d4" />
- **注解的使用**
- @State：组件内私有，用它标记的成员变量，将会和ui联动，它的数值变化，会引起ui更新
- @Watch('onTick')：监听某个变量的变化，当值发生变化时会触发调用onTick方法，如果值和上次相同，则不会触发调用onTick方法
- <img width="611" height="261" alt="image" src="https://github.com/user-attachments/assets/b0948d27-0bb9-4671-b69c-cf51055ae1b1" />





  
