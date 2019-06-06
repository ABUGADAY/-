# JS代码规范

## 前言

此文档用以基卫内部开发约束

## 一、结构规范

**[强制]** 使用 4 个空格做为一个缩进层级，不允许使用 2 个空格 或 tab 字符。



## 二、书写规范

### 2.1空格

**[强制]**二元运算符两侧必须有一个空格，一元运算符与操作对象之间不允许有空格。

**[强制]** 用作代码块起始的左花括号 { 前必须有一个空格。

eg.

```javascript
// good
if (condition) {
}

while (condition) {
}

function funcName() {
}

// bad
if (condition){
}

while (condition){
}

function funcName(){
}
```

**[强制]** if / else / for / while / function / switch / do / try / catch / finally 关键字后，必须有一个空格。

eg.

```javascript
// good
if (condition) {
}

while (condition) {
}

(function () {
})();

// bad
if(condition) {
}

while(condition) {
}

(function() {
})();
```

### 2.2换行

**[强制]** 每个独立语句结束后必须换行。

**[强制]** 每行不得超过 120 个字符。

**[强制]** 超长的不可分割的代码允许例外，比如复杂的正则表达式。长字符串不在例外之列。

eg.

```javascript
    // good
    if (user.isAuthenticated()
        && user.isInRole('admin')
        && user.hasAuthority('add-admin')
        || user.hasAuthority('delete-admin')
    ) {
        // Code
    }
    
    var result = number1 + number2 + number3
        + number4 + number5;
    
    
    // bad
    if (user.isAuthenticated() &&
        user.isInRole('admin') &&
        user.hasAuthority('add-admin') ||
        user.hasAuthority('delete-admin')) {
        // Code
    }
    
    var result = number1 + number2 + number3 +
        number4 + number5;
```

**[强制]** 在函数声明、函数表达式、函数调用、对象创建、数组创建、for语句等场景中，不允许在 , 或 ; 前换行。

```javascript
    // good
    var obj = {
        a: 1,
        b: 2,
        c: 3
    };
    
    foo(
        aVeryVeryLongArgument,
        anotherVeryLongArgument,
        callback
    );
    
    // bad
    var obj = {
        a: 1
        , b: 2
        , c: 3
    };
    
    foo(
        aVeryVeryLongArgument
        , anotherVeryLongArgument
        , callback
    );
```

**[建议]** 不同行为或逻辑的语句集，使用空行隔开，更易阅读。

eg.

```javascript
// 仅为按逻辑换行的示例，不代表setStyle的最优实现
function setStyle(element, property, value) {
    if (element == null) {
        return;
    }

    element.style[property] = value;
}
```

**[建议]** 对于 if...else...、try...catch...finally 等语句，推荐使用在 } 号后添加一个换行 的风格，使代码层次结构更清晰，阅读性更好。

eg.

```javascript
if (condition) {
    // some statements;
}
else {
    // some statements;
}

try {
    // some statements;
}
catch (ex) {
    // some statements;
}
```

### 2.3其他

**[强制]** 不得省略语句结束的分号。

**[强制]** 在 if / else / for / do / while 语句中，即使只有一行，也不得省略块 {...}。

eg.

```javascript
// good
if (condition) {
    callFunc();
}

// bad
if (condition) callFunc();
if (condition)
    callFunc();
```

**[强制]**及时删除废弃的注释代码，减轻运维负担



## 三、 命名规范

ECMAScript 规范中标识符采用驼峰大小写格式，驼峰命名法由小(大)写字母开始，后续每个单词首字母都大写。根据首字母是否大写，分为两种方式：

1. Pascal Case 大驼峰式命名法：首字母大写。eg：StudentInfo、UserInfo、ProductInfo
2. Camel Case 小驼峰式命名法：首字母小写。eg：studentInfo、userInfo、productInfo

标识符，则包括变量、函数名、类名、属性名和函数或类的参数，每个命名方法又略有不同，下面详细解释一下：

### 3.1 变量

**命名方法**：小驼峰式命名法。

**命名规范**：前缀应当是名词。(函数的名字前缀为动词，以此区分变量和函数)

**命名建议**：尽量在变量名字中体现所属类型，如:length、count等表示数字类型；而包含name、title表示为字符串类型。

**eg**:

```
// 好的命名方式
let maxCount = 10;
let tableTitle = 'LoginTable';
// 不好的命名方式
let setCount = 10;
let getTitle = 'LoginTable';
```

### 3.2 常量

**命名方法**：名称全部大写。

**命名规范**：使用大写字母和下划线来组合命名，下划线用以分割单词。

**eg**:

```
const MAX_COUNT = 10;
const URL = 'http://www.foreverz.com';
```

### 3.3 函数

**命名方法**：小驼峰式命名法。

**命名规范**：前缀应当为动词。

**命名建议**：可使用常见动词约定

| 动词 | 含义                         | 返回值                                                |
| ---- | ---------------------------- | ----------------------------------------------------- |
| can  | 判断是否可执行某个动作(权限) | 函数返回一个布尔值。true：可执行；false：不可执行     |
| has  | 判断是否含有某个值           | 函数返回一个布尔值。true：含有此值；false：不含有此值 |
| is   | 判断是否为某个值             | 函数返回一个布尔值。true：为某个值；false：不为某个值 |
| get  | 获取某个值                   | 函数返回一个非布尔值                                  |
| set  | 设置某个值                   | 无返回值、返回是否设置成功或者返回链式对象            |
| load | 加载某些数据                 | 无返回值或者返回是否加载完成的结果                    |

**eg**:

```
// 是否可阅读
function canRead(): boolean {
  return true;
}
// 获取名称
function getName(): string {
  return this.name;
}
```

### 3.4 类 & 构造函数

**命名方法**：大驼峰式命名法，首字母大写。

**命名规范**：前缀为名称。

**eg**:

```
class Person {
  public name: string;
  constructor(name) {
    this.name = name;
  }
}
const person = new Person('mevyn');
```

### 3.5 类的成员

类的成员包含：

1. 公共属性和方法：跟变量和函数的命名一样。
2. 私有属性和方法：前缀为_(下划线)，后面跟公共属性和方法一样的命名方式。

**eg**:

```
class Person {
  private _name: string;
  constructor() { }
  // 公共方法
  getName() {
    return this._name;
  }
  // 公共方法
  setName(name) {
    this._name = name;
  }
}
const person = new Person();
person.setName('mervyn');
person.getName(); // ->mervyn
```



## 四、注释规范

### 4.1 行内注释

**说明**：行内注释以两个斜线开始，以行尾结束。

**语法**：code // 这是行内注释

**使用方式**：//(双斜线)与代码之间保留一个空格，并且//(双斜线)与注释文字之间保留一个空格。

**命名建议**：

```
// 用来显示一个解释的评论
// -> 用来显示表达式的结果，
// >用来显示 console 的输出结果，
```

**eg**:

```
function test() { // 测试函数
  console.log('Hello World!'); // >Hello World!
  return 3 + 2; // ->5
}
```

### 4.2 单行注释

**说明**：单行注释以两个斜线开始，以行尾结束。

**语法**：// 这是单行注释

**使用方式**：单独一行：//(双斜线)与注释文字之间保留一个空格。

**eg**：

```
// 调用了一个函数；1)单独在一行
setTitle();
```

### 4.3 多行注释

**说明**：以 `/*` 开头， `*/` 结尾

**语法**：`/* 注释说明 */`

**使用方法**：若开始`/*`和结束`*/`都在一行，推荐采用单行注释。若至少三行注释时，第一行为`/*`，最后行为`*/`，其他行以`*`开始，并且注释文字与`*`保留一个空格。

**eg**:

```
/*
* 代码执行到这里后会调用setTitle()函数
* setTitle()：设置title的值
*/
setTitle();
```

### 4.4 函数(方法)注释

**说明**：函数(方法)注释也是多行注释的一种，但是包含了特殊的注释要求，参照[JSDoc](https://link.juejin.im/?target=http%3A%2F%2Fwww.css88.com%2Fdoc%2Fjsdoc%2F)

**语法**：

```
/** 
* 函数说明 
* @关键字 
*/
```

**常用注释关键字**：(只列出一部分，并不是全部)

| 注释名   | 语法                                      | 含义                 | 示例                                         |
| -------- | ----------------------------------------- | -------------------- | -------------------------------------------- |
| @param   | @param 参数名 {参数类型} 描述信息         | 描述参数的信息       | @param name {String} 传入名称                |
| @return  | @return {返回类型} 描述信息               | 描述返回值的信息     | @return {Boolean} true:可执行;false:不可执行 |
| @author  | @author 作者信息 [附属信息：如邮箱、日期] | 描述此函数作者的信息 | @author 张三 2015/07/21                      |
| @version | @version XX.XX.XX                         | 描述此函数的版本号   | @version 1.0.3                               |
| @example | @example 示例代码                         | 演示函数的使用       | @example setTitle(‘测试’)                    |



```javascript
/**
* 合并Grid的行
* @param grid {Ext.Grid.Panel} 需要合并的Grid
* @param cols {Array} 需要合并列的Index(序号)数组；从0开始计数，序号也包含。
* @param isAllSome {Boolean} ：是否2个tr的cols必须完成一样才能进行合并。true：完成一样；false(默认)：不完全一样
* @return void
* @author polk6 2015/07/21 
* @example
* _________________                             _________________
* |  年龄 |  姓名 |                             |  年龄 |  姓名 |
* -----------------      mergeCells(grid,[0])   -----------------
* |  18   |  张三 |              =>             |       |  张三 |
* -----------------                             -  18   ---------
* |  18   |  王五 |                             |       |  王五 |
* -----------------                             -----------------
*/
function mergeCells(grid: Ext.Grid.Panel, cols: Number[], isAllSome: boolean = false) {
  // Do Something
}
```



## 五、包的规范

**[强制]**包命名采用全小写
**[强制]**复制代码时如果遇到包文件夹下只有单个文件夹的情况 

需要先在资源管理器中新建相应的文件夹，而不是整个包复制粘贴

> 在idea中，若文件夹下只有一个文件夹，原有的文件夹结构会被破坏
>
> 例如 对以下包 ag.script直接复制
>
> +-chis
> |
> +--application
> |
> +----ag
> |
> +------script
>
> 得到的结果是
>
> +-chis
> |
> +--application
> |
> +----ag.script
>
> 框架无法解析会引发报错



## 六、类的规范

**[强制]**文件名采用大驼峰命名方式 CamelCase
**[强制]**常量名全大写，用**_**分割,例如 MAX_VALUE
**[建议]**不得自行更改基础类的实现，在chis中体现为BizXXX.js ， 在phis中体现为SimpleXXX.js

如果需要自行实现，在自行实现的代码中重写函数

**[强制]**继承哪个展示类就以该类名为后缀

eg.

> 继承了BizSimpleListView.js 命名为 HypertensionRecordListView.js

**[建议]**采用统一前缀

eg.

> 高血压 全称Hypertension 简称 HY

**[建议]**将cfg定义写在同个文件中，避免一部分定义在***.app**一部分定义在***.js**中

eg.

bad

```xml
<module id="D01-hr" name="高血压档案列表"
			script="chis.application.hy.script.record.HypertensionRecordListView" type="1">
			<properties>
				<p name="entryName">
					chis.application.hy.schemas.MDC_HypertensionRecord
				</p>
				<p name="serviceId">chis.hypertensionService</p>
				<p name="listServiceId">chis.hypertensionListService</p>
				<p name="visitRefId">D0-1-3</p>
			</properties>
			<action id="createDoc" name="新建" iconCls="create" group="create" />
			<action id="modify" name="查看" iconCls="update" group="update" />
			<action id="writeOff" name="注销" iconCls="common_writeOff"
				group="update" />
			<action id="revert" name="恢复" iconCls="healthDoc_revert" />	
			<action id="visit" name="随访" iconCls="visit"
				group="update" />
			<action id="print" name="打印" />
		</module>
```

```javascript
  this.confirmWriteOffServiceAction = "checkLogoutHypertensionRecord";
  this.activateId = "MDC_HypertensionRecord";
  this.checkServiceAction = "ifHypertensionRecordExist";
```

good

```xml
<module id="D01-hr" name="高血压档案列表"
			script="chis.application.hy.script.record.HypertensionRecordListView" type="1">
			<properties>
				<p name="entryName">
                    chis.application.hy.schemas.MDC_HypertensionRecord
                </p>
				<p name="serviceId">chis.hypertensionService</p>
				<p name="listServiceId">chis.hypertensionListService</p>
                <p name="confirmWriteOffServiceAction">checkLogoutHypertensionRecord</p>
                <p name="activateId">MDC_HypertensionRecord</p>
                <p name="checkServiceAction">ifHypertensionRecordExist</p>
				<p name="visitRefId">D0-1-3</p>
			</properties>
			<action id="createDoc" name="新建" iconCls="create" group="create" />
			<action id="modify" name="查看" iconCls="update" group="update" />
			<action id="writeOff" name="注销" iconCls="common_writeOff"
				group="update" />
			<action id="revert" name="恢复" iconCls="healthDoc_revert" />	
			<action id="visit" name="随访" iconCls="visit"
				group="update" />
			<action id="print" name="打印" />
		</module>
```


## 七、函数规范

**[强制]**函数、变量采用小驼峰命名方式 camelCase 

**[强制]**流程代码不得与函数代码混写，代码块中只允许流程的定义或者函数的定义

**[强制]**复杂函数必须有相关的说明注释，表明输入与输出，对关键代码行进行解释



## 八、组件规范

**[强制]**系统中的提示统一使用MyMessageTip

eg.

```javascript
return MyMessageTip.msg("提示", "请选择建档结束日期！", true);
```