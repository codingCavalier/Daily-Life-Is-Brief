1. 如果接口里的方法是可选的，即允许不实现此方法，那么用`?`修饰
- <img width="542" height="372" alt="image" src="https://github.com/user-attachments/assets/1e882f96-4f70-4c02-9e71-93300379ee4b" />

2. 如果要传入的是接口，即入参是接口的实例：
- **且接口里只有一个方法，且没有具体的方法名**，则可以采用箭头函数的方式传参
- <img width="765" height="117" alt="image" src="https://github.com/user-attachments/assets/4fae8ce4-cc83-43fd-afe8-2be9dfc4b3c3" />
- <img width="516" height="145" alt="image" src="https://github.com/user-attachments/assets/e5df03f9-9f4a-455c-8fed-9408fd9c78b5" />
- **且接口里的方法都有具体方法名，包括接口有多个方法的情况**，则采用“对象字面量”方式传参
- <img width="312" height="78" alt="image" src="https://github.com/user-attachments/assets/0242a60a-def7-4cee-a937-d102d512198c" />
- <img width="446" height="273" alt="image" src="https://github.com/user-attachments/assets/26471dff-484d-44d8-96b3-9adf7577b195" />
- **特别重要：**，使用“对象字面量”方式传参如果编辑器代码检查报错（Object literal must correspond to some explicitly declared class or interface (arkts-no-untyped-obj-literals) <ArkTSChec>）
  - 解决办法：将接口放到ts文件中，而非ets文件中！

3. 如果箭头函数里只有一个参数，可以省略括号，写成这样：onChange(value => { })，否则就要写括号：onChange((value) => { })
