整洁的JavaScript代码非常有利于代码的测试、阅读和评审，也给团队协作带来极大的帮助。那么，志在成为优秀的前端开发工程师的你，非常有必要了解并且在开发中遵守这些原则。这里是来自于Github上他人整理的一份JavaScript代码整洁的编码规范，利用周末几个小时翻译了一下。如果你的英文很好，建议直接阅读英文，地址[戳这里](https://github.com/front-thinking/clean-code-javascript/ "戳这里")。由于水平有限，笨拙的英语，翻译的不好，大家多提意见。
## 目录
  1. 介绍
  2. 变量
  3. 函数
  4. 对象及数据结构
  5. 类
  6. 测试
  7. 并发
  8. 格式
  9. 注释

## 介绍
![诙谐的软件质量评估的图片，即当你阅读代码的时候随口吼出的咒骂的数量](https://camo.githubusercontent.com/2050cd696ecddcabad1380b1964c48a60597323e/687474703a2f2f7777772e6f736e6577732e636f6d2f696d616765732f636f6d6963732f7774666d2e6a7067)

源自Robert C. Martin's的书[《*Clean Code*》](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)，本文总结了同样适用于JavaScript的软件工程原则。这不是一个代码指南，而是一个帮你提升编写更高可读性、复用性和重构性的JavaScript软件代码的指导原则。

并不是这里提到的每一个原则都必须得被严格的遵守，而在开发中被大众广泛执行的就更少了。虽然这些仅仅是些代码指导建议，但这些建议都是编纂进《*Clean Code*》的，它们来自于经验丰富的作者们多年开发的提炼。

我们创造出软件工程仅仅过去了半个世纪，而且我们仍然在这条路上不断前进。当软件架构像架构本身一样久的时候，也许彼时我们将遵循更严格的规则。眼前，就让这些指导原则作为评估你和你的团队编写的JavaScript代码的试金石吧。

最后要提醒一下的是：了解这些原则并不会让你立刻变成一个优秀的程序员，而且即使多年遵循这些原则也并不意味着你不会犯错。每一行代码都像黏土一样从原貌雕刻成最终的形式。最终，我们将那些我们同伴评审我们代码时指出的瑕疵凿掉。别因为初稿代码需要提升而沮丧，需要干掉的是那些糟粕的代码！


## **变量**
### 使用有意义的、良好可读性的变量名

**Bad:**
```javascript
var yyyymmdstr = moment().format('YYYY/MM/DD');
```

**Good:**
```javascript
var yearMonthDay = moment().format('YYYY/MM/DD');
```


### 固定值定义请使用ES6常量

在不推荐的例子中，变量可以改变。
当你声明一个常量，该常量应在整个程序中保持不变。


**Bad:**
```javascript
var FIRST_US_PRESIDENT = "George Washington";
```

**Good**:
```javascript
const FIRST_US_PRESIDENT = "George Washington";
```



### 功能相近的函数应使用相同的词汇

**Bad:**
```javascript
getUserInfo();
getClientData();
getCustomerRecord();
```

**Good**:
```javascript
getUser();
```


### 使用可检索的名称

我们阅读代码远比我们写的代码多的多。因此使那些我们编写的代码拥有良好的可读性和检索性变得十分重要。因为将变量名命名的稀奇古怪或者晦涩难懂实在是是对代码阅读者巨大的伤害。因此，把变量名命名为更容易检索些。

**Bad:**
```javascript
// 我去，525600哪里来的?
for (var i = 0; i < 525600; i++) {
  runCronJob();
}
```

**Good**:
```javascript
// 将它们通过`var`声明为可检索的变量名.
var MINUTES_IN_A_YEAR = 525600;
for (var i = 0; i < MINUTES_IN_A_YEAR; i++) {
  runCronJob();
}
```


### 使用自解释的变量
**Bad:**
```javascript
const cityStateRegex = /^(.+)[,\\s]+(.+?)\s*(\d{5})?$/;
saveCityState(cityStateRegex.match(cityStateRegex)[1], cityStateRegex.match(cityStateRegex)[2]);
```

**Good**:
```javascript
const cityStateRegex = /^(.+)[,\\s]+(.+?)\s*(\d{5})?$/;
const match = cityStateRegex.match(cityStateRegex)
const city = match[1];
const state = match[2];
saveCityState(city, state);
```


### 避免隐式映射
显示的映射比隐式映射好得多。

**Bad:**
```javascript
var locations = ['Austin', 'New York', 'San Francisco'];
locations.forEach((l) => {
  doStuff();
  doSomeOtherStuff();
  ...
  ...
  ...
  // Wait, what is `l` for again?
  dispatch(l);
});
```

**Good**:
```javascript
var locations = ['Austin', 'New York', 'San Francisco'];
locations.forEach((location) => {
  doStuff();
  doSomeOtherStuff();
  ...
  ...
  ...
  dispatch(location);
});
```


### 别增加不必要的描述
对于那些类/对象名已经包含的信息，就别再变量名中重复这些了。

**Bad:**
```javascript
var Car = {
  carMake: 'Honda',
  carModel: 'Accord',
  carColor: 'Blue'
};

function paintCar(car) {
  car.carColor = 'Red';
}
```

**Good**:
```javascript
var Car = {
  make: 'Honda',
  model: 'Accord',
  color: 'Blue'
};

function paintCar(car) {
  car.color = 'Red';
}
```


### 使用更加简洁的短路写法

**Bad:**
```javascript
function createMicrobrewery(name) {
  var breweryName;
  if (name) {
    breweryName = name;
  } else {
    breweryName = 'Hipster Brew Co.';
  }
}
```

**Good**:
```javascript
function createMicrobrewery(name) {
  var breweryName = name || 'Hipster Brew Co.'
}
```


## **函数**
### 函数参数 (理想情况要少于2个)

将函数的参数限制在有限的范围是极为重要的，这将使你测试函数的时候变得更加简单。拥有超过3个以上的参数将导致组合混乱，在这里你不得不为每一个独立的参数测试数个case。

没有参数才是最理想的情况。1到2个参数是ok的，但是3个参数的情况需要极力避免。任何超过3个参数的情况是非常糟糕的。通常情况下，如果你的参数超过两个，那么你的函数职责将变得臃肿。以防极少情况下你的函数的确需要更多的参数，用一个更高层次的对象来替代多个参数是更明智的。

由于JavaScript定义对象非常容易，因此你可以在任何你需要使用大量参数的情况下直接使用对象来代替。

**Bad:**
```javascript
function createMenu(title, body, buttonText, cancellable) {
  ...
}
```

**Good**:
```javascript
var menuConfig = {
  title: 'Foo',
  body: 'Bar',
  buttonText: 'Baz',
  cancellable: true
}

function createMenu(menuConfig) {
  ...
}

```



### 函数应该遵循单一职责原则

这可能是软件工程中最重要的规则了。当函数做的事情超过一件的时候，同时也意味着它们将变得难以组合、测试和搞懂。尽力让函数的原则隔离是它只完成一件事，它们将变得更加容易重构，而且代码也会变得更加容易阅读和简洁。老实讲，哪怕是从本篇文章中提到的各个原则中你仅带走了这一条，你已经比很多程序员更加牛逼超前了。

**Bad:**
```javascript
function emailClients(clients) {
  clients.forEach(client => {
    let clientRecord = database.lookup(client);
    if (clientRecord.isActive()) {
      email(client);
    }
  });
}
```

**Good**:
```javascript
function emailClients(clients) {
  clients.forEach(client => {
    emailClientIfNeeded(client);
  });
}

function emailClientIfNeeded(client) {
  if (isClientActive(client)) {
    email(client);
  }
}

function isClientActive(client) {
  let clientRecord = database.lookup(client);
  return clientRecord.isActive();
}
```


### 函数名就应该能够表达出其职责

**Bad:**
```javascript
function dateAdd(date, month) {
  // ...
}

let date = new Date();

// 我去，这TM的到底是要增加啥的
dateAdd(date, 1);
```

**Good**:
```javascript
function dateAddMonth(date, month) {
  // ...
}

let date = new Date();
dateAddMonth(date, 1);
```


### 函数应该仅做一层抽象

当你的函数同时抽象多层的时候，那同时也意味着你的函数变得有点臃肿不堪了。将函数的抽象层次为单层，这将会更加有利于你代码的复用性和可测试性。

**Bad:**
```javascript
function parseBetterJSAlternative(code) {
  let REGEXES = [
    // ...
  ];

  let statements = code.split(' ');
  let tokens;
  REGEXES.forEach((REGEX) => {
    statements.forEach((statement) => {
      // ...
    })
  });

  let ast;
  tokens.forEach((token) => {
    // lex...
  });

  ast.forEach((node) => {
    // parse...
  })
}
```

**Good**:
```javascript
function tokenize(code) {
  let REGEXES = [
    // ...
  ];

  let statements = code.split(' ');
  let tokens;
  REGEXES.forEach((REGEX) => {
    statements.forEach((statement) => {
      // ...
    })
  });

  return tokens;
}

function lexer(tokens) {
  let ast;
  tokens.forEach((token) => {
    // lex...
  });

  return ast;
}

function parseBetterJSAlternative(code) {
  let tokens = tokenize(code);
  let ast = lexer(tokens);
  ast.forEach((node) => {
    // parse...
  })
}
```


### 干掉重复的代码

在任何情况下，也永远、永远别包含重复的代码。它们根本没有存在的理由，而且这些重复的代码可能是你作为一个专业程序员提交的最糟糕的代码了。重复的代码通常意味着在代码里有不止一个地方可以改变相同的逻辑。JavaScript是无类型的，因此编写通用函数非常方便。你尽可好好利用JavaScript这个特性。


**Bad:**
```javascript
function showDeveloperList(developers) {
  developers.forEach(developers => {
    var expectedSalary = developer.calculateExpectedSalary();
    var experience = developer.getExperience();
    var githubLink = developer.getGithubLink();
    var data = {
      expectedSalary: expectedSalary,
      experience: experience,
      githubLink: githubLink
    };

    render(data);
  });
}

function showManagerList(managers) {
  managers.forEach(manager => {
    var expectedSalary = manager.calculateExpectedSalary();
    var experience = manager.getExperience();
    var portfolio = manager.getMBAProjects();
    var data = {
      expectedSalary: expectedSalary,
      experience: experience,
      portfolio: portfolio
    };

    render(data);
  });
}
```

**Good**:
```javascript
function showList(employees) {
  employees.forEach(employee => {
    var expectedSalary = employee.calculateExpectedSalary();
    var experience = employee.getExperience();
    var portfolio;

    if (employee.type === 'manager') {
      portfolio = employee.getMBAProjects();
    } else {
      portfolio = employee.getGithubLink();
    }

    var data = {
      expectedSalary: expectedSalary,
      experience: experience,
      portfolio: portfolio
    };

    render(data);
  });
}
```


### 使用默认的参数，而不是在赋值时使用短路赋值
**Bad:**
```javascript
function writeForumComment(subject, body) {
  subject = subject || 'No Subject';
  body = body || 'No text';
}

```

**Good**:
```javascript
function writeForumComment(subject = 'No subject', body = 'No text') {
  ...
}

```


### 使用Object.assign时设置默认的对象

**Bad:**
```javascript
var menuConfig = {
  title: null,
  body: 'Bar',
  buttonText: null,
  cancellable: true
}

function createMenu(config) {
  config.title = config.title || 'Foo'
  config.body = config.body || 'Bar'
  config.buttonText = config.buttonText || 'Baz'
  config.cancellable = config.cancellable === undefined ? config.cancellable : true;

}

createMenu(menuConfig);
```

**Good**:
```javascript
var menuConfig = {
  title: 'Order',
  // User did not include 'body' key
  buttonText: 'Send',
  cancellable: true
}

function createMenu(config) {
  config = Object.assign({
    title: 'Foo',
    body: 'Bar',
    buttonText: 'Baz',
    cancellable: true
  }, config);

  // config now equals: {title: "Order", body: "Bar", buttonText: "Send", cancellable: true}
  // ...
}

createMenu(menuConfig);
```



### 别使用标志位（flag）作为函数的参数

标志位flag就是在告诉阅读者这个函数做不仅仅一件事。而前面提到过，函数应该是单一职责的。如果你的函数根据不同的标志位做不同的事，那么将函数做个细分吧。

**Bad:**
```javascript
function createFile(name, temp) {
  if (temp) {
    fs.create('./temp/' + name);
  } else {
    fs.create(name);
  }
}
```

**Good**:
```javascript
function createTempFile(name) {
  fs.create('./temp/' + name);
}

function createFile(name) {
  fs.create(name);
}
```


### 避免副作用

如果一个函数除了接收参数并返回处理结果外还做其它的事，那么我们就说这个函数有副作用。副作用可能是写进一个文件、修改全局变量、或者不小心把你的钱都给了陌生人。

也许，在某些情况下你的确需要在程序中增加副作用。例如前面提到的，你可能就是需要写一个文件。那么，这种情况下你可以将这件事封装起来。别在多个函数和类中各完成写同一个文件的功能，用一个封装好的service来做这件事。一个，而且是仅仅一个。

这里主要的目的是避免一些常见的坑，例如在多个对象间共享状态，使用可变类型数据而没有将可能有副作用的地方集中起来。如果你能做到这一条，那么你肯定比那些做不到这一点的程序员开森。

**Bad:**
```javascript
// 被下面的函数引用的全局变量。
// 如果我们有其它的函数也在用这个名字，那么它将会被破坏。
var name = 'Ryan McDermott';

function splitIntoFirstAndLastName() {
  name = name.split(' ');
}

splitIntoFirstAndLastName();

console.log(name); // ['Ryan', 'McDermott'];
```

**Good**:
```javascript
function splitIntoFirstAndLastName(name) {
  return name.split(' ');
}

var name = 'Ryan McDermott'
var newName = splitIntoFirstAndLastName(name);

console.log(name); // 'Ryan McDermott';
console.log(newName); // ['Ryan', 'McDermott'];
```


### 别污染全局函数

污染全局是JavaScript开发实践中最糟糕的事了。你可能无意中就破坏了其它的库和那些使用这些API的用户，直到他们在产品中发现了bug才知道被你坑了。考虑这样一个例子：你可能想要给JavaScript内置的Array扩展diff这样一个方法，用于返回两个数组差异部分。你直接将其置于Array.prototype下，但是这可能破坏了其它也同样想做这一件事的库。而其它的库可能也在使用diff这样一个函数来返回完成不同的事，例如返回两个数组中第一个和最后一个差异元素。这也就是为什么使用ES6类来继承Array显得更优雅了。

**Bad:**
```javascript
Array.prototype.diff = function(comparisonArray) {
  var values = [];
  var hash = {};

  for (var i of comparisonArray) {
    hash[i] = true;
  }

  for (var i of this) {
    if (!hash[i]) {
      values.push(i);
    }
  }

  return values;
}
```

**Good:**
```javascript
class SuperArray extends Array {
  constructor(...args) {
    super(...args);
  }

  diff(comparisonArray) {
    var values = [];
    var hash = {};

    for (var i of comparisonArray) {
      hash[i] = true;
    }

    for (var i of this) {
      if (!hash[i]) {
        values.push(i);
      }
    }

    return values;
  }
}
```


### 拥抱函数式编程

如果Haskell比作IPA，那么JavaScript就是O'Douls。这就是说，JavaScript不像Haskell一样是函数式语言，但是它拥有函数式的调味。函数式语言更加简洁和易于测试。尽量使用这种方式来编程。

**Bad:**
```javascript
const programmerOutput = [
  {
    name: 'Uncle Bobby',
    linesOfCode: 500
  }, {
    name: 'Suzie Q',
    linesOfCode: 1500
  }, {
    name: 'Jimmy Gosling',
    linesOfCode: 150
  }, {
    name: 'Gracie Hopper',
    linesOfCode: 1000
  }
];

var totalOutput = 0;

for (var i = 0; i < programmerOutput.length; i++) {
  totalOutput += programmerOutput[i].linesOfCode;
}
```

**Good**:
```javascript
const programmerOutput = [
  {
    name: 'Uncle Bobby',
    linesOfCode: 500
  }, {
    name: 'Suzie Q',
    linesOfCode: 1500
  }, {
    name: 'Jimmy Gosling',
    linesOfCode: 150
  }, {
    name: 'Gracie Hopper',
    linesOfCode: 1000
  }
];

var totalOutput = programmerOutput
  .map((programmer) => programmer.linesOfCode)
  .reduce((acc, linesOfCode) => acc + linesOfCode, 0);
```


### 封装条件判断

**Bad:**
```javascript
if (fsm.state === 'fetching' && isEmpty(listNode)) {
  /// ...
}
```

**Good**:
```javascript
function shouldShowSpinner(fsm, listNode) {
  return fsm.state === 'fetching' && isEmpty(listNode);
}

if (shouldShowSpinner(fsmInstance, listNodeInstance)) {
  // ...
}
```


### 避免否定判断

**Bad:**
```javascript
function isDOMNodeNotPresent(node) {
  // ...
}

if (!isDOMNodeNotPresent(node)) {
  // ...
}
```

**Good**:
```javascript
function isDOMNodePresent(node) {
  // ...
}

if (isDOMNodePresent(node)) {
  // ...
}
```


### 避免条件判断

这可能看起来根本不可能。乍一听，估计绝大部分人都会说“老子不用if的话还TM能做啥事？”答案是在绝大部分情况下你可以用多态来完成同样的任务。那么接下来的反应通常是“好吧，那么这么做有什么好处，老子为什么要这么做？”，答案就是前面我们学到的简洁编码原则：函数单一职责原则。当你的函数或者类包含多个if语句的时候，那就意味着你的函数在违反单一职责原则。

**Bad:**
```javascript
class Airplane {
  //...
  getCruisingAltitude() {
    switch (this.type) {
      case '777':
        return getMaxAltitude() - getPassengerCount();
      case 'Air Force One':
        return getMaxAltitude();
      case 'Cesna':
        return getMaxAltitude() - getFuelExpenditure();
    }
  }
}
```

**Good**:
```javascript
class Airplane {
  //...
}

class Boeing777 extends Airplane {
  //...
  getCruisingAltitude() {
    return getMaxAltitude() - getPassengerCount();
  }
}

class AirForceOne extends Airplane {
  //...
  getCruisingAltitude() {
    return getMaxAltitude();
  }
}

class Cesna extends Airplane {
  //...
  getCruisingAltitude() {
    return getMaxAltitude() - getFuelExpenditure();
  }
}
```


### 避免类型判断 (第1部分)

JavaScript是无类型的语言，这意味着函数可以传递任何类型的参数。有时候，这种自由度也会带来一定麻烦。例如，做类型判断。这里有很多种方法可以避免这么做。首先要考虑的是提供连续性APIs。

**Bad:**
```javascript
function travelToTexas(vehicle) {
  if (vehicle instanceof Bicycle) {
    vehicle.peddle(this.currentLocation, new Location('texas'));
  } else if (vehicle instanceof Car) {
    vehicle.drive(this.currentLocation, new Location('texas'));
  }
}
```

**Good**:
```javascript
function travelToTexas(vehicle) {
  vehicle.move(this.currentLocation, new Location('texas'));
}
```


### 避免类型判断(第2部分)

如果你使用的是如字符串、整型和数组这样的基础类型，在这里使用多态不方便但又的确需要使用类型判断的时候，你应该考虑使用TypeScript。TypeScript是JavaScript外的一个绝佳选择，在JavaScript的语法之上它提供静态类型等语法糖。在JavaScript代码中做大量的类型检测会带来很多问题，如代码中增加了大量的冗余代码，这将极大降低代码的可读性。你必须时刻保持JavaScript代码整洁，编写良好的测试用例及良好的代码评审，稍不留神就可能犯错。因此，把这些类型判断的事交给TypeScript吧。

**Bad:**
```javascript
function combine(val1, val2) {
  if (typeof val1 == "number" && typeof val2 == "number" ||
      typeof val1 == "string" && typeof val2 == "string") {
    return val1 + val2;
  } else {
    throw new Error('Must be of type String or Number');
  }
}
```

**Good**:
```javascript
function combine(val1, val2) {
  return val1 + val2;
}
```


### 避免过度优化

其实当代浏览器在运行时已经做了很多隐式的优化。大部分时候，你做的优化是在浪费时间。 [猛戳这里](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)，你可以查找都有哪些优化。同时保持关注，直到那些需要优化的点被修复。

**Bad:**
```javascript

// 旧的浏览器里len会在每次循环时被重新赋值
for (var i = 0, len = list.length; i < len; i++) {
  // ...
}
```

**Good**:
```javascript
for (var i = 0; i < list.length; i++) {
  // ...
}
```


### 干掉没用的代码

没用的代码跟重复的代码一样糟糕。根本没有什么理由来保留他们在你的代码里。干掉那些毫无作用的代码。大部分的事情都可以用版本控制工具完成。

**Bad:**
```javascript
function oldRequestModule(url) {
  // ...
}

function newRequestModule(url) {
  // ...
}

var req = newRequestModule;
inventoryTracker('apples', req, 'www.inventory-awesome.io');

```

**Good**:
```javascript
function newRequestModule(url) {
  // ...
}

var req = newRequestModule;
inventoryTracker('apples', req, 'www.inventory-awesome.io');
```


## **对象及数据结构**
### 使用getters和setters

JavaScript没有接口或者类型，因此保持这种模式比较困难，因为我们没有public和private这些关键字。因此，使用getters和setters来访问对象的数据比直接读取对象的属性要好很多。“为撒？”你可能为问，那么这里又一个无序的列表来回答你的为撒：

1. 当你需要做的比仅仅获取对象的属性更多的时候，你不用去查找并修改代码中的每一个accessor；
2. 使用set后做校验变得更加方便；
3. 封装内部表现；
4. 当getting和setting的时候增加log或者error处理更加方便；
5. 继承这个类，你可以覆盖默认的功能；
6. 可以延迟加载对象的属性，例如从服务器端获取。


**Bad:**
```javascript
class BankAccount {
  constructor() {
	   this.balance = 1000;
  }
}

let bankAccount = new BankAccount();

// Buy shoes...
bankAccount.balance = bankAccount.balance - 100;
```

**Good**:
```javascript
class BankAccount {
  constructor() {
	   this.balance = 1000;
  }

  // It doesn't have to be prefixed with `get` or `set` to be a getter/setter
  withdraw(amount) {
  	if (verifyAmountCanBeDeducted(amount)) {
  	  this.balance -= amount;
  	}
  }
}

let bankAccount = new BankAccount();

// Buy shoes...
bankAccount.withdraw(100);
```



### 使对象拥有私有属性
ES5以下的版本中可以通过闭包来完成.

**Bad:**
```javascript

var Employee = function(name) {
  this.name = name;
}

Employee.prototype.getName = function() {
  return this.name;
}

var employee = new Employee('John Doe');
console.log('Employee name: ' + employee.getName()); // Employee name: John Doe
delete employee.name;
console.log('Employee name: ' + employee.getName()); // Employee name: undefined
```

**Good**:
```javascript
var Employee = (function() {
  function Employee(name) {
    this.getName = function() {
      return name;
    };
  }

  return Employee;
}());

var employee = new Employee('John Doe');
console.log('Employee name: ' + employee.getName()); // Employee name: John Doe
delete employee.name;
console.log('Employee name: ' + employee.getName()); // Employee name: John Doe
```



## **类**
### 单一职责原则 (SRP)

如在《Clean Code》中提到的，“不应该有超过一个原因来更改一个类”。就像你仅可以带一个行李箱登记一样，把很多的功能都塞进一个类里看起来非常诱人。问题是这将导致你的类非常不牢固而且给了很多更改它的原因。降低更改类的可能性至关重要。单一职责原则如此重要是因为：如果你的类拥有塞满了各种各样的功能，那么你更改一点都使你非常难以理解这将对依赖它的代码带来多大的影响。

**Bad:**
```javascript
class UserSettings {
  constructor(user) {
    this.user = user;
  }

  changeSettings(settings) {
    if (this.verifyCredentials(user)) {
      // ...
    }
  }

  verifyCredentials(user) {
    // ...
  }
}
```

**Good**:
```javascript
class UserAuth {
  constructor(user) {
    this.user = user;
  }

  verifyCredentials() {
    // ...
  }
}


class UserSettings {
  constructor(user) {
    this.user = user;
    this.auth = new UserAuth(user)
  }

  changeSettings(settings) {
    if (this.auth.verifyCredentials()) {
      // ...
    }
  }
}
```


### 开放-闭合原则 (OCP)

就像Bertrand Meyer说过的，“软件实体（类、模块、函数等）应该对于扩展是开放的，但是对于修改是闭合的”。So这是啥意思呢？这个原则强调的是你应该允许你的用户来继承扩展你的模块，而不是打开你的js文件来修改它。

**Bad:**
```javascript
class AjaxRequester {
  constructor() {
    // 如果我们需要其他的HTTP方法的话，例如DELETE，怎么办？我们需要打开这个文件手动更改它。
    this.HTTP_METHODS = ['POST', 'PUT', 'GET'];
  }

  get(url) {
    // ...
  }

}
```

**Good**:
```javascript
class AjaxRequester {
  constructor() {
    this.HTTP_METHODS = ['POST', 'PUT', 'GET'];
  }

  get(url) {
    // ...
  }

  addHTTPMethod(method) {
    this.HTTP_METHODS.push(method);
  }
}
```



### Liskov 替换原则 (LSP)

对于简单的概念来看这是一个可怕的术语。正规的定义是“如果A是T的子类，那么T类型的对象可以被S类型的对象来替换，从而也不会改变任何程序运行的规则(正确性、任务执行等)”。这定义看起来更可怕。

最好的解释是如果你有一个父类和子类，那么子类和父类可以相互替换而不影响正确的结果。这可能依然让你感觉困惑，因此让我们看一下经典的方块-长方形的例子。从数学来讲，方块也是长方形，但是如果你将继承表达为使用“is-a”的关系，你可能很快遇到麻烦。

**Bad:**
```javascript
class Rectangle {
  constructor() {
    this.width = 0;
    this.height = 0;
  }

  setColor(color) {
    // ...
  }

  render(area) {
    // ...
  }

  setWidth(width) {
    this.width = width;
  }

  setHeight(height) {
    this.height = height;
  }

  getArea() {
    return this.width * this.height;
  }
}

class Square extends Rectangle {
  constructor() {
    super();
  }

  setWidth(width) {
    this.width = width;
    this.height = width;
  }

  setHeight(height) {
    this.width = height;
    this.height = height;
  }
}

function renderLargeRectangles(rectangles) {
  rectangles.forEach((rectangle) => {
    rectangle.setWidth(4);
    rectangle.setHeight(5);
    let area = rectangle.getArea(); // BAD: Will return 25 for Square. Should be 20.
    rectangle.render(area);
  })
}

let rectangles = [new Rectangle(), new Rectangle(), new Square()];
renderLargeRectangles(rectangles);
```

**Good**:
```javascript
class Shape {
  constructor() {}

  setColor(color) {
    // ...
  }

  render(area) {
    // ...
  }
}

class Rectangle extends Shape {
  constructor() {
    super();
    this.width = 0;
    this.height = 0;
  }

  setWidth(width) {
    this.width = width;
  }

  setHeight(height) {
    this.height = height;
  }

  getArea() {
    return this.width * this.height;
  }
}

class Square extends Shape {
  constructor() {
    super();
    this.length = 0;
  }

  setLength(length) {
    this.length = length;
  }

  getArea() {
    return this.length * this.length;
  }
}

function renderLargeShapes(shapes) {
  shapes.forEach((shape) => {
    switch (shape.constructor.name) {
      case 'Square':
        shape.setLength(5);
      case 'Rectangle':
        shape.setWidth(4);
        shape.setHeight(5);
    }

    let area = shape.getArea();
    shape.render(area);
  })
}

let shapes = [new Rectangle(), new Rectangle(), new Square()];
renderLargeShapes(shapes);
```


###接口隔离原则 (ISP)

由于JavaScript中没有接口因此本条原则并不会像其它语言一样被严格遵守。然而，即使JavaScript缺少类型机制，这条原则一样是非常重要和合理的。

接口隔离原则意味着“客户端不应该被强迫依赖它并不使用的接口”。由于鸭子类型，接口在JavaScript中是比较隐式的规则。

一个很好的演示这条规则的案例是：对于需要大量设置对象的类的例子。不让客户端来设置大量的选项是有益的，因为大部分的时候它们并不需要这些设置。让这些设置的对象变得可选的，从而阻止它变成一个胖接口。

**Bad:**
```javascript
class DOMTraverser {
  constructor(settings) {
    this.settings = settings;
    this.setup();
  }

  setup() {
    this.rootNode = this.settings.rootNode;
    this.animationModule.setup();
  }

  traverse() {
    // ...
  }
}

let $ = new DOMTraverser({
  rootNode: document.getElementsByTagName('body'),
  animationModule: function() {} // 大多数情况我们并不需要动画
  // ...
});

```

**Good**:
```javascript
class DOMTraverser {
  constructor(settings) {
    this.settings = settings;
    this.options = settings.options;
    this.setup();
  }

  setup() {
    this.rootNode = this.settings.rootNode;
    this.setupOptions();
  }

  setupOptions() {
    if (this.options.animationModule) {
      // ...
    }
  }

  traverse() {
    // ...
  }
}

let $ = new DOMTraverser({
  rootNode: document.getElementsByTagName('body'),
  options: {
    animationModule: function() {}
  }
});
```


### 依赖倒置原则(DIP)

这条原则包含两个关键的内容：
1. 高阶模块不应该依赖低阶模块。它们都应该依赖抽象；
2. 抽象不应该依赖细节。细节应该依赖抽象。


乍一看这可能比较难以理解，但是如果你使用过AngularJS的话你已经见过这个原则的实现了，即依赖注入。尽管这可能是不一样的概念，依赖倒置原则表示高阶模块应该避免知道低阶模块的细节。这可以通过依赖注入来实现。这带来的最大的的益处就是降低了模块的耦合度。耦合是软件开发中很糟糕的模式之一，它是的代码重构变得非常困难。

正如之前提到的，JavaScript没有接口的概念，因此依赖的抽象是隐式的。这就是说，方法和属性是对象和类暴露给其它对象和属性的。在下面的例子中，这个接口就是任何Request模块中InventoryTracker都将包含一个requestItems的方法。

**Bad:**
```javascript
class InventoryTracker {
  constructor(items) {
    this.items = items;

    // BAD: 我们创建了对某一个具体request实现的依赖
    // 我们应该仅仅让requestItems依赖一个request方法
    this.requester = new InventoryRequester();
  }

  requestItems() {
    this.items.forEach((item) => {
      this.requester.requestItem(item);
    });
  }
}

class InventoryRequester {
  constructor() {
    this.REQ_METHODS = ['HTTP'];
  }

  requestItem(item) {
    // ...
  }
}

let inventoryTracker = new InventoryTracker(['apples', 'bananas']);
inventoryTracker.requestItems();
```

**Good**:
```javascript
class InventoryTracker {
  constructor(items, requester) {
    this.items = items;
    this.requester = requester;
  }

  requestItems() {
    this.items.forEach((item) => {
      this.requester.requestItem(item);
    });
  }
}

class InventoryRequesterV1 {
  constructor() {
    this.REQ_METHODS = ['HTTP'];
  }

  requestItem(item) {
    // ...
  }
}

class InventoryRequesterV2 {
  constructor() {
    this.REQ_METHODS = ['WS'];
  }

  requestItem(item) {
    // ...
  }
}
let inventoryTracker = new InventoryTracker(['apples', 'bananas'], new InventoryRequesterV2());
inventoryTracker.requestItems();
```


### 优先使用ES6的类而不是ES5的普通函数

对于典型的ES5的类来说，获得可读性良好的继承、构造函数和方法定义非常困难。如果你需要继承，那么选择类吧。然而，除非你发现你需要很大且复杂的对象，那么优先选择小的函数而不是类。

**Bad:**
```javascript
var Animal = function(age) {
    if (!(this instanceof Animal)) {
        throw new Error("Instantiate Animal with `new`");
    }

    this.age = age;
};

Animal.prototype.move = function() {};

var Mammal = function(age, furColor) {
    if (!(this instanceof Mammal)) {
        throw new Error("Instantiate Mammal with `new`");
    }

    Animal.call(this, age);
    this.furColor = furColor;
};

Mammal.prototype = Object.create(Animal.prototype);
Mammal.prototype.constructor = Mammal;
Mammal.prototype.liveBirth = function() {};

var Human = function(age, furColor, languageSpoken) {
    if (!(this instanceof Human)) {
        throw new Error("Instantiate Human with `new`");
    }

    Mammal.call(this, age, furColor);
    this.languageSpoken = languageSpoken;
};

Human.prototype = Object.create(Mammal.prototype);
Human.prototype.constructor = Human;
Human.prototype.speak = function() {};
```

**Good:**
```javascript
class Animal {
    constructor(age) {
        this.age = age;
    }

    move() {}
}

class Mammal extends Animal {
    constructor(age, furColor) {
        super(age);
        this.furColor = furColor;
    }

    liveBirth() {}
}

class Human extends Mammal {
    constructor(age, furColor, languageSpoken) {
        super(age, furColor);
        this.languageSpoken = languageSpoken;
    }

    speak() {}
}
```



### 使用链式方法调用

与《Clean Code》的建议相悖的是，这里是我们拥有不同的地方。方法链式调用一致有争议的被认为是不整洁的并且违背[Demeter法则](https://en.wikipedia.org/wiki/Law_of_Demeter)的。可能这的确是对的，但是这种模式在JavaScript中非常有用，你可能在很多库函数中都见到过它，如jQuery和Lodash。它使你的代码非常具有表达性和更少的冗余性。因此，我说，使用链式方法调用并且看一看你的代码多么的整洁。在你的类函数中，简单的返回this在每一个函数的末尾，你就可以使用链式调用了。

**Bad:**
```javascript
class Car {
  constructor() {
    this.make = 'Honda';
    this.model = 'Accord';
    this.color = 'white';
  }

  setMake(make) {
    this.name = name;
  }

  setModel(model) {
    this.model = model;
  }

  setColor(color) {
    this.color = color;
  }

  save() {
    console.log(this.make, this.model, this.color);
  }
}

let car = new Car();
car.setColor('pink');
car.setMake('Ford');
car.setModel('F-150')
car.save();
```

**Good**:
```javascript
class Car {
  constructor() {
    this.make = 'Honda';
    this.model = 'Accord';
    this.color = 'white';
  }

  setMake(make) {
    this.name = name;
    // NOTE: Returning this for chaining
    return this;
  }

  setModel(model) {
    this.model = model;
    // NOTE: Returning this for chaining
    return this;
  }

  setColor(color) {
    this.color = color;
    // NOTE: Returning this for chaining
    return this;
  }

  save() {
    console.log(this.make, this.model, this.color);
  }
}

let car = new Car()
  .setColor('pink')
  .setMake('Ford')
  .setModel('F-150')
  .save();
```


### 组合优于继承
正如在注明的 [*设计模式*](https://en.wikipedia.org/wiki/Design_Patterns) 中提到的,你应该使用组合优于使用继承。这里有一大堆使用组合和继承的好处。这里有个很重要的格言就是如果你本能的选择继承，试图去想想组合是否可以更好的解决你的问题。

你可能在想“那我啥时候使用继承呢？”。这就要看你手上要解决的是啥问题了，这里是最直接的列表来帮你决定继承比组合更合适的时候。

1. 你的继承表达的是“is-a”的关系，而不是“has-a”的关系；
2. 你可以重复使用类的基础代码；
3. 你想要通过继承基类来扩展子类。

**Bad:**
```javascript
class Employee {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }

  // ...
}


class EmployeeTaxData extends Employee {
  constructor(ssn, salary) {
    super();
    this.ssn = ssn;
    this.salary = salary;
  }

  // ...
}
```

**Good**:
```javascript
class Employee {
  constructor(name, email) {
    this.name = name;
    this.email = email;

  }

  setTaxData(ssn, salary) {
    this.taxData = new EmployeeTaxData(ssn, salary);
  }
  // ...
}

class EmployeeTaxData {
  constructor(ssn, salary) {
    this.ssn = ssn;
    this.salary = salary;
  }

  // ...
}
```


## **测试**

测试比完成功能更重要。如果你没有测试用例或者不够的测试，那么每次你修改运行代码的时候你都不能确定你没有破坏什么。怎么才算足够的测试用例取决于你的团队，但是拥有百分之百的覆盖率是你来达到高自信的方法。这就是说除了使用一个好的测试框架外，你可能还需要使用一个好的[覆盖率工具](http://gotwarlost.github.io/istanbul/)。

别为你不谢测试而找借口了。这里有一大堆良好的[测试框架](http://jstherightway.org/#testing-tools)，所以找一个你的团队喜欢的。当你找到一个合适团队的框架后，下一步的目标就是对每一个模块的每一个特性都写测试用例。如果你喜欢测试驱动开发，那么很棒，但是这里的主要目标就是在你发布任何新特性之前都要达到你的覆盖率目标。


### Single concept per test

**Bad:**
```javascript
const assert = require('assert');

describe('MakeMomentJSGreatAgain', function() {
  it('handles date boundaries', function() {
    let date;

    date = new MakeMomentJSGreatAgain('1/1/2015');
    date.addDays(30);
    date.shouldEqual('1/31/2015');

    date = new MakeMomentJSGreatAgain('2/1/2016');
    date.addDays(28);
    assert.equal('02/29/2016', date);

    date = new MakeMomentJSGreatAgain('2/1/2015');
    date.addDays(28);
    assert.equal('03/01/2015', date);
  });
});
```

**Good**:
```javascript
const assert = require('assert');

describe('MakeMomentJSGreatAgain', function() {
  it('handles 30-day months', function() {
    let date = new MakeMomentJSGreatAgain('1/1/2015');
    date.addDays(30);
    date.shouldEqual('1/31/2015');
  });

  it('handles leap year', function() {
    let date = new MakeMomentJSGreatAgain('2/1/2016');
    date.addDays(28);
    assert.equal('02/29/2016', date);
  });

  it('handles non-leap year', function() {
    let date = new MakeMomentJSGreatAgain('2/1/2015');
    date.addDays(28);
    assert.equal('03/01/2015', date);
  });
});
```


## **并发**
### 使用Promises，而不是回调
回调函数并不是整洁的，而且这会导致过多的嵌套。使用ES6的Promise，它是内置的全局类型。大胆使用吧。

**Bad:**
```javascript
require('request').get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin', function(err, response) {
  if (err) {
    console.error(err);
  }
  else {
    require('fs').writeFile('article.html', response.body, function(err) {
      if (err) {
        console.error(err);
      } else {
        console.log('File written');
      }
    })
  }
})

```

**Good**:
```javascript
require('request-promise').get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin')
  .then(function(response) {
    return require('fs-promise').writeFile('article.html', response);
  })
  .then(function() {
    console.log('File written');
  })
  .catch(function(err) {
    console.error(err);
  })

```


### Async/Await比Promises还整洁

Promises是相比于回调来说非常整洁的替代，但是ES7带来了async和await从而提供了更整洁的方案。你需要做的就是在函数前加上asyn关键字，然后你就可以写你的逻辑，而不用一个then函数了。如果你可以充分利用ES7的特性，那么使用这个吧。

**Bad:**
```javascript
require('request-promise').get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin')
  .then(function(response) {
    return require('fs-promise').writeFile('article.html', response);
  })
  .then(function() {
    console.log('File written');
  })
  .catch(function(err) {
    console.error(err);
  })

```

**Good**:
```javascript
async function getCleanCodeArticle() {
  try {
    var request = await require('request-promise')
    var response = await request.get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin');
    var fileHandle = await require('fs-promise');

    await fileHandle.writeFile('article.html', response);
    console.log('File written');
  } catch(err) {
      console.log(err);
    }
  }
```



## **格式**

格式就非常主观了。像这里的很对规则，这里没有必须遵守固定的和快的规则。主要的观点就是别为了格式化而争吵。这里有大量的[格式化工具](http://standardjs.com/rules.html)来完成自动格式化，使用一个即可。在格式化上争吵真是浪费工程师的时间和生命。


### 使用连续性的大写

JavaScript是无类型的，因此大写会告诉你很多关于你的变量、函数等。这些规则是主观的，因此你的团队找一个你们喜欢的即可。问题是，无论你们选择的是哪个，保持连续喝一致。

**Bad:**
```javascript
var DAYS_IN_WEEK = 7;
var daysInMonth = 30;

var songs = ['Back In Black', 'Stairway to Heaven', 'Hey Jude'];
var Artists = ['ACDC', 'Led Zeppelin', 'The Beatles'];

function eraseDatabase() {}
function restore_database() {}

class animal {}
class Alpaca {}
```

**Good**:
```javascript
var DAYS_IN_WEEK = 7;
var DAYS_IN_MONTH = 30;

var songs = ['Back In Black', 'Stairway to Heaven', 'Hey Jude'];
var artists = ['ACDC', 'Led Zeppelin', 'The Beatles'];

function eraseDatabase() {}
function restoreDatabase() {}

class Animal {}
class Alpaca {}
```



### 函数的调用者和被调用者应该保持近些

如果一个函数调用了另外一个函数，这些函数应该在代码位置上保持近一些。理想情况下，调用者应该正好在被调用者上面。我们倾向于自上而下读代码，就像阅读报纸一样。因此，也同样如此组织你的代码。

**Bad:**
```javascript
class PerformanceReview {
  constructor(employee) {
    this.employee = employee;
  }

  lookupPeers() {
    return db.lookup(this.employee, 'peers');
  }

  lookupMananger() {
    return db.lookup(this.employee, 'manager');
  }

  getPeerReviews() {
    let peers = this.lookupPeers();
    // ...
  }

  perfReview() {
      getPeerReviews();
      getManagerReview();
      getSelfReview();
  }

  getManagerReview() {
    let manager = this.lookupManager();
  }

  getSelfReview() {
    // ...
  }
}

let review = new PerformanceReview(user);
review.perfReview();
```

**Good**:
```javascript
class PerformanceReview {
  constructor(employee) {
    this.employee = employee;
  }

  perfReview() {
      getPeerReviews();
      getManagerReview();
      getSelfReview();
  }

  getPeerReviews() {
    let peers = this.lookupPeers();
    // ...
  }

  lookupPeers() {
    return db.lookup(this.employee, 'peers');
  }

  getManagerReview() {
    let manager = this.lookupManager();
  }

  lookupMananger() {
    return db.lookup(this.employee, 'manager');
  }

  getSelfReview() {
    // ...
  }
}

let review = new PerformanceReview(employee);
review.perfReview();
```



## **注释**
### 仅仅注释那些拥有复杂逻辑的地方
注释是一个勉强的解释，并不是必须的。良好的代码大部分都是自我解释的。

**Bad:**
```javascript
function hashIt(data) {
  // The hash
  var hash = 0;

  // Length of string
  var length = data.length;

  // Loop through every character in data
  for (var i = 0; i < length; i++) {
    // Get character code.
    var char = data.charCodeAt(i);
    // Make the hash
    hash = ((hash << 5) - hash) + char;
    // Convert to 32-bit integer
    hash = hash & hash;
  }
}
```

**Good**:
```javascript

function hashIt(data) {
  var hash = 0;
  var length = data.length;

  for (var i = 0; i < length; i++) {
    var char = data.charCodeAt(i);
    hash = ((hash << 5) - hash) + char;

    // Convert to 32-bit integer
    hash = hash & hash;
  }
}

```


### 别把注释掉的代码留在代码中

版本控制工具有它存在的原因。将历史代码留在历史版本中即可。

**Bad:**
```javascript
doStuff();
// doOtherStuff();
// doSomeMoreStuff();
// doSoMuchStuff();
```

**Good**:
```javascript
doStuff();
```


### 别写日志似的注释

记住，使用版本控制。根本不需要增加这些死的、注释代码，尤其是日志似的注释。使用git log去获取历史日志。

**Bad:**
```javascript
/**
 * 2016-12-20: Removed monads, didn't understand them (RM)
 * 2016-10-01: Improved using special monads (JP)
 * 2016-02-03: Removed type-checking (LI)
 * 2015-03-14: Added combine with type-checking (JR)
 */
function combine(a, b) {
  return a + b;
}
```

**Good**:
```javascript
function combine(a, b) {
  return a + b;
}
```


### 避免使用位置标记

这通常会是把代码搞得更乱。让函数和变量名通过合适的缩进和格式来给代码带来良好的视觉结构。

**Bad:**
```javascript
////////////////////////////////////////////////////////////////////////////////
// Scope Model Instantiation
////////////////////////////////////////////////////////////////////////////////
let $scope.model = {
  menu: 'foo',
  nav: 'bar'
};

////////////////////////////////////////////////////////////////////////////////
// Action setup
////////////////////////////////////////////////////////////////////////////////
let actions = function() {
  // ...
}
```

**Good**:
```javascript
let $scope.model = {
  menu: 'foo',
  nav: 'bar'
};

let actions = function() {
  // ...
}
```


### 避免在源代码中增加许可注释

这是你的许可文件该干的事。

**Bad:**
```javascript
/*
The MIT License (MIT)

Copyright (c) 2016 Ryan McDermott

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE
*/

function calculateBill() {
  // ...
}
```

**Good**:
```javascript
function calculateBill() {
  // ...
}
```
