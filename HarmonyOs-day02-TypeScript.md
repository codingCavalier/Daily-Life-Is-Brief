- let定义变量，const定义常量
- 基本类型：
  - number：数字
  - string：字符串
  - boolean：布尔
  - any：类似Kotlin的Any或者Java的Object，**但是ArkTS不让用any类型**
  - union类型：使用竖线分隔，let p: string|number = '';表示p可以是字符串或者数字中的一种类型
  - 对象类型：比如用interface定义的People类，let p: People = {name:'Andy', age: 20}，取值p.name，**ArkTS中必须写明类型People，而TypeScript中可以不写，默认Object类型**
- 容器类型：
  - 数组：`let arr: string[] = ['abc','def']`或者`let arr: Array<string> = ['aaa','bbb']`，取值`arr[0]`，如果所取角标越界则返回undefined
- 逻辑控制：
  - if - else：
    - 允许多分支即if - else-if - else-if - else
    - 使用===判断，即要类型相同，又要数值相同
    - 使用==判断，默认自动类型转换后对比值是否相同，建议使用===，因为==有类型转换性能开销以及不确定后果
    - **空字符串''、数字0、null、undefined：这几个值都表示false，其他值都表示true**
  - switch：
    - 也是用case关键字：case 'abc': { let x = 0; break; }
    - 大括号可写可不写，写了大括号，则形成此case自己的作用域，内部定义的变量不与其他分支冲突
    - **也是必须写break**
    - 也有default缺省分支
- 遍历：
  - for：
    - **TypeScript支持for...in遍历（拿到角标），但是ArkTS不支持**
    - ArkTS支持for...of遍历（拿到值）。TypeScript也支持。**记住const关键字接收遍历的值**
  - while
```ArkTS
// 普通for循环
for (let i = 0; i < 10; i++) {
  console.log(`${i}`);
}
// 普通while循环
let i = 0;
while (i < 10) {
  console.log(`i=${i}`);
  i++;
}
// TypeScript支持for...in遍历（拿到角标），但是ArkTS不支持
let arr: string[] = ['a', 'b', 'c']
for (const i in arr) {
  console.log(arr[i]);
}
// ArkTS支持for...of遍历（拿到值）
let arr: string[] = ['a', 'b', 'c']
for (const str of arr) {
  console.log(str);
}
```
- 定义函数：箭头函数
  - 箭头函数表达式（写方法中）：let func1 = (name: string): number => { console.log(`Hello ${name}`); return 30; }
  - 成员函数（写类中）：func1 = (name: string): number => { console.log(`Hello ${name}`); return 30; }
  - 可选参数（参数名加问号?）：func1 = (name?: string): number => { console.log(`Hello ${name}`); return 30; }
  - 默认参数（有默认值）：func1 = (name: string = '路人甲'): number => { console.log(`Hello ${name}`); return 30; }
- 枚举类型：
  - 不赋值，默认打印的是角标（从0开始）
  - 赋值，打印的是所赋的值
  - **不支持混合类型，即有的赋值number，有的赋值string，这样不允许**
- 接口：interface People
- 类：class，实现接口 class A implements People
- 创建对象：let a: A = new A()
- 
