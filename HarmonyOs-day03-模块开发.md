- <img width="980" height="655" alt="image" src="https://github.com/user-attachments/assets/a7dc9584-620c-49f5-ba73-cb5c68ef3848" />
#### Ability
- 可以创建entry或者feature，产物是HAP或者APP
#### Native C++
- 可以创建entry或者feature，产物是HAP或者APP
- 带CMake等Native开发相关的代码
#### Shared Library
- 动态共享包，产物是HSP
- 适用于应用内多个模块（如 Entry、Feature）都需要使用的公共业务逻辑（如网络请求、数据加密、公共组件），以优化包体积。
#### Static Library
- 静态共享包，产物是HAR
- 适用于需要跨应用共享的通用工具库或UI组件库。
#### 结构
- 主模块：entry（应用模块）
- 功能模块：feature_a（从应用模块拆分出的子模块，比如商品详情模块，购物车模块，个人中心模块）
- 库模块：Shared Library 或者 Static Library，lib_a（只有逻辑，没有ui）
##### entry 模块
- 可以依赖其他feature模块或者hsp、har模块，但是不能依赖其他entry模块
- src/main/module.json5中："type": "entry"
##### feature 模块
- 可以依赖其他feature模块或者hsp、har模块，但是不能依赖其他entry模块
- src/main/module.json5中："type": "feature"
##### Shared Library 模块（hsp）
- 可以依赖其他hsp、har模块，但是不能依赖feature、entry模块
- src/main/module.json5中："type": "shared"
##### Static Library 模块（har）
- 可以依赖其他har模块，但是不能依赖feature、entry、hsp模块
- src/main/module.json5中："type": "har"
#### 模块化开发
- 创建工具类：在hsp模块下的utils包中，创建CountdownUtil.ets文件，里面创建CountdownImpl类
- 导出工具类：
  - 要导出的类必须用export修饰，其他类和模块才能使用，export class CountdownImpl implements Countdown { ... }
  - 二次导出：与src平级创建Index.ets文件，并导出CountdownImpl，可以用as起别名，二次导出的好处是，方便管理（约定大于强制，此处没有控制可见性的作用），方便使用方引入：
  - <img width="741" height="130" alt="image" src="https://github.com/user-attachments/assets/90754d97-a624-4046-b8fd-29e963442f38" />
- 使用方添加hsp模块的依赖：
  - 确认hsp模块的oh-package.json5中，名称是lib_b_shared_3568
  - <img width="516" height="246" alt="image" src="https://github.com/user-attachments/assets/41eea116-ea63-4cd8-a42e-c8a4e3847f87" />
  - 在entry模块的oh-package.json5中，导入依赖
  - <img width="527" height="281" alt="image" src="https://github.com/user-attachments/assets/44655b63-159e-4215-bd4b-449f7df71c8e" />

