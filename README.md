�����JavaScript����ǳ������ڴ���Ĳ��ԡ��Ķ�������Ҳ���Ŷ�Э����������İ�������ô��־�ڳ�Ϊ�����ǰ�˿�������ʦ���㣬�ǳ��б�Ҫ�˽Ⲣ���ڿ�����������Щԭ��������������Github�����������һ��JavaScript��������ı���淶��������ĩ����Сʱ������һ�¡�������Ӣ�ĺܺã�����ֱ���Ķ�Ӣ�ģ���ַ[������](https://github.com/front-thinking/clean-code-javascript/ "������")������ˮƽ���ޣ���׾��Ӣ�����Ĳ��ã���Ҷ��������
## Ŀ¼
  1. ����
  2. ����
  3. ����
  4. �������ݽṹ
  5. ��
  6. ����
  7. ����
  8. ��ʽ
  9. ע��

## ����
![ڶг���������������ͼƬ���������Ķ������ʱ����ں�������������](https://camo.githubusercontent.com/2050cd696ecddcabad1380b1964c48a60597323e/687474703a2f2f7777772e6f736e6577732e636f6d2f696d616765732f636f6d6963732f7774666d2e6a7067)

Դ��Robert C. Martin's����[��*Clean Code*��](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)�������ܽ���ͬ��������JavaScript���������ԭ���ⲻ��һ������ָ�ϣ�����һ������������д���߿ɶ��ԡ������Ժ��ع��Ե�JavaScript��������ָ��ԭ��

�����������ᵽ��ÿһ��ԭ�򶼱���ñ��ϸ�����أ����ڿ����б����ڹ㷺ִ�еľ͸����ˡ���Ȼ��Щ������Щ����ָ�����飬����Щ���鶼�Ǳ������*Clean Code*���ģ����������ھ���ḻ�������Ƕ��꿪����������

���Ǵ����������̽�����ȥ�˰�����ͣ�����������Ȼ������·�ϲ���ǰ����������ܹ���ܹ�����һ���õ�ʱ��Ҳ���ʱ���ǽ���ѭ���ϸ�Ĺ�����ǰ��������Щָ��ԭ����Ϊ�����������Ŷӱ�д��JavaScript������Խ�ʯ�ɡ�

���Ҫ����һ�µ��ǣ��˽���Щԭ�򲢲����������̱��һ������ĳ���Ա�����Ҽ�ʹ������ѭ��Щԭ��Ҳ������ζ���㲻�᷸��ÿһ�д��붼�����һ����ԭò��̳����յ���ʽ�����գ����ǽ���Щ����ͬ���������Ǵ���ʱָ����覴����������Ϊ���������Ҫ��������ɥ����Ҫ�ɵ�������Щ���ɵĴ��룡


## **����**
### ʹ��������ġ����ÿɶ��Եı�����

**Bad:**
```javascript
var yyyymmdstr = moment().format('YYYY/MM/DD');
```

**Good:**
```javascript
var yearMonthDay = moment().format('YYYY/MM/DD');
```


### �̶�ֵ������ʹ��ES6����

�ڲ��Ƽ��������У��������Ըı䡣
��������һ���������ó���Ӧ�����������б��ֲ��䡣


**Bad:**
```javascript
var FIRST_US_PRESIDENT = "George Washington";
```

**Good**:
```javascript
const FIRST_US_PRESIDENT = "George Washington";
```



### ��������ĺ���Ӧʹ����ͬ�Ĵʻ�

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


### ʹ�ÿɼ���������

�����Ķ�����Զ������д�Ĵ����Ķࡣ���ʹ��Щ���Ǳ�д�Ĵ���ӵ�����õĿɶ��Ժͼ����Ա��ʮ����Ҫ����Ϊ��������������ϡ��Źֻ��߻�ɬ�Ѷ�ʵ�����ǶԴ����Ķ��߾޴���˺�����ˣ��ѱ���������Ϊ�����׼���Щ��

**Bad:**
```javascript
// ��ȥ��525600��������?
for (var i = 0; i < 525600; i++) {
  runCronJob();
}
```

**Good**:
```javascript
// ������ͨ��`var`����Ϊ�ɼ����ı�����.
var MINUTES_IN_A_YEAR = 525600;
for (var i = 0; i < MINUTES_IN_A_YEAR; i++) {
  runCronJob();
}
```


### ʹ���Խ��͵ı���
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


### ������ʽӳ��
��ʾ��ӳ�����ʽӳ��õöࡣ

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


### �����Ӳ���Ҫ������
������Щ��/�������Ѿ���������Ϣ���ͱ��ٱ��������ظ���Щ�ˡ�

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


### ʹ�ø��Ӽ��Ķ�·д��

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


## **����**
### �������� (�������Ҫ����2��)

�������Ĳ������������޵ķ�Χ�Ǽ�Ϊ��Ҫ�ģ��⽫ʹ����Ժ�����ʱ���ø��Ӽ򵥡�ӵ�г���3�����ϵĲ�����������ϻ��ң��������㲻�ò�Ϊÿһ�������Ĳ�����������case��

û�в�������������������1��2��������ok�ģ�����3�������������Ҫ�������⡣�κγ���3������������Ƿǳ����ġ�ͨ������£������Ĳ���������������ô��ĺ���ְ�𽫱��ӷ�ס��Է������������ĺ�����ȷ��Ҫ����Ĳ�������һ�����߲�εĶ����������������Ǹ����ǵġ�

����JavaScript�������ǳ����ף������������κ�����Ҫʹ�ô��������������ֱ��ʹ�ö��������档

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



### ����Ӧ����ѭ��һְ��ԭ��

��������������������Ҫ�Ĺ����ˡ��������������鳬��һ����ʱ��ͬʱҲ��ζ�����ǽ����������ϡ����Ժ͸㶮�������ú�����ԭ���������ֻ���һ���£����ǽ���ø��������ع������Ҵ���Ҳ���ø��������Ķ��ͼ�ࡣ��ʵ���������Ǵӱ�ƪ�������ᵽ�ĸ���ԭ���������������һ�������Ѿ��Ⱥܶ����Ա����ţ�Ƴ�ǰ�ˡ�

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


### ��������Ӧ���ܹ�������ְ��

**Bad:**
```javascript
function dateAdd(date, month) {
  // ...
}

let date = new Date();

// ��ȥ����TM�ĵ�����Ҫ����ɶ��
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


### ����Ӧ�ý���һ�����

����ĺ���ͬʱ�������ʱ����ͬʱҲ��ζ����ĺ�������е�ӷ�ײ����ˡ��������ĳ�����Ϊ���㣬�⽫����������������ĸ����ԺͿɲ����ԡ�

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


### �ɵ��ظ��Ĵ���

���κ�����£�Ҳ��Զ����Զ������ظ��Ĵ��롣���Ǹ���û�д��ڵ����ɣ�������Щ�ظ��Ĵ������������Ϊһ��רҵ����Ա�ύ�������Ĵ����ˡ��ظ��Ĵ���ͨ����ζ���ڴ������в�ֹһ���ط����Ըı���ͬ���߼���JavaScript�������͵ģ���˱�дͨ�ú����ǳ����㡣�㾡�ɺú�����JavaScript������ԡ�


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


### ʹ��Ĭ�ϵĲ������������ڸ�ֵʱʹ�ö�·��ֵ
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


### ʹ��Object.assignʱ����Ĭ�ϵĶ���

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



### ��ʹ�ñ�־λ��flag����Ϊ�����Ĳ���

��־λflag�����ڸ����Ķ������������������һ���¡���ǰ���ᵽ��������Ӧ���ǵ�һְ��ġ������ĺ������ݲ�ͬ�ı�־λ����ͬ���£���ô����������ϸ�ְɡ�

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


### ���⸱����

���һ���������˽��ղ��������ش������⻹���������£���ô���Ǿ�˵��������и����á������ÿ�����д��һ���ļ����޸�ȫ�ֱ��������߲�С�İ����Ǯ������İ���ˡ�

Ҳ����ĳЩ��������ȷ��Ҫ�ڳ��������Ӹ����á�����ǰ���ᵽ�ģ�����ܾ�����Ҫдһ���ļ�����ô���������������Խ�����·�װ���������ڶ�����������и����дͬһ���ļ��Ĺ��ܣ���һ����װ�õ�service��������¡�һ���������ǽ���һ����

������Ҫ��Ŀ���Ǳ���һЩ�����Ŀӣ������ڶ������乲��״̬��ʹ�ÿɱ��������ݶ�û�н������и����õĵط������������������������һ������ô��϶�����Щ��������һ��ĳ���Ա��ɭ��

**Bad:**
```javascript
// ������ĺ������õ�ȫ�ֱ�����
// ��������������ĺ���Ҳ����������֣���ô�����ᱻ�ƻ���
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


### ����Ⱦȫ�ֺ���

��Ⱦȫ����JavaScript����ʵ�������������ˡ�����������о��ƻ��������Ŀ����Щʹ����ЩAPI���û���ֱ�������ڲ�Ʒ�з�����bug��֪��������ˡ���������һ�����ӣ��������Ҫ��JavaScript���õ�Array��չdiff����һ�����������ڷ�������������첿�֡���ֱ�ӽ�������Array.prototype�£�����������ƻ�������Ҳͬ��������һ���µĿ⡣�������Ŀ����Ҳ��ʹ��diff����һ��������������ɲ�ͬ���£����緵�����������е�һ�������һ������Ԫ�ء���Ҳ����Ϊʲôʹ��ES6�����̳�Array�Եø������ˡ�

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


### ӵ������ʽ���

���Haskell����IPA����ôJavaScript����O'Douls�������˵��JavaScript����Haskellһ���Ǻ���ʽ���ԣ�������ӵ�к���ʽ�ĵ�ζ������ʽ���Ը��Ӽ������ڲ��ԡ�����ʹ�����ַ�ʽ����̡�

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


### ��װ�����ж�

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


### ������ж�

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


### ���������ж�

����ܿ��������������ܡ�էһ�������ƾ��󲿷��˶���˵�����Ӳ���if�Ļ���TM����ɶ�£��������ھ��󲿷������������ö�̬�����ͬ����������ô�������ķ�Ӧͨ���ǡ��ðɣ���ô��ô����ʲô�ô�������ΪʲôҪ��ô���������𰸾���ǰ������ѧ���ļ�����ԭ�򣺺�����һְ��ԭ�򡣵���ĺ���������������if����ʱ���Ǿ���ζ����ĺ�����Υ����һְ��ԭ��

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


### ���������ж� (��1����)

JavaScript�������͵����ԣ�����ζ�ź������Դ����κ����͵Ĳ�������ʱ���������ɶ�Ҳ�����һ���鷳�����磬�������жϡ������кܶ��ַ������Ա�����ô��������Ҫ���ǵ����ṩ������APIs��

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


### ���������ж�(��2����)

�����ʹ�õ������ַ��������ͺ����������Ļ������ͣ�������ʹ�ö�̬�����㵫�ֵ�ȷ��Ҫʹ�������жϵ�ʱ����Ӧ�ÿ���ʹ��TypeScript��TypeScript��JavaScript���һ������ѡ����JavaScript���﷨֮�����ṩ��̬���͵��﷨�ǡ���JavaScript�����������������ͼ�������ܶ����⣬������������˴�����������룬�⽫���󽵵ʹ���Ŀɶ��ԡ������ʱ�̱���JavaScript�������࣬��д���õĲ������������õĴ��������Բ�����Ϳ��ܷ�����ˣ�����Щ�����жϵ��½���TypeScript�ɡ�

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


### ��������Ż�

��ʵ���������������ʱ�Ѿ����˺ܶ���ʽ���Ż����󲿷�ʱ���������Ż������˷�ʱ�䡣 [�ʹ�����](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)������Բ��Ҷ�����Щ�Ż���ͬʱ���ֹ�ע��ֱ����Щ��Ҫ�Ż��ĵ㱻�޸���

**Bad:**
```javascript

// �ɵ��������len����ÿ��ѭ��ʱ�����¸�ֵ
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


### �ɵ�û�õĴ���

û�õĴ�����ظ��Ĵ���һ����⡣����û��ʲô������������������Ĵ�����ɵ���Щ�������õĴ��롣�󲿷ֵ����鶼�����ð汾���ƹ�����ɡ�

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


## **�������ݽṹ**
### ʹ��getters��setters

JavaScriptû�нӿڻ������ͣ���˱�������ģʽ�Ƚ����ѣ���Ϊ����û��public��private��Щ�ؼ��֡���ˣ�ʹ��getters��setters�����ʶ�������ݱ�ֱ�Ӷ�ȡ���������Ҫ�úܶࡣ��Ϊ�����������Ϊ�ʣ���ô������һ��������б����ش����Ϊ����

1. ������Ҫ���ıȽ�����ȡ��������Ը����ʱ���㲻��ȥ���Ҳ��޸Ĵ����е�ÿһ��accessor��
2. ʹ��set����У���ø��ӷ��㣻
3. ��װ�ڲ����֣�
4. ��getting��setting��ʱ������log����error������ӷ��㣻
5. �̳�����࣬����Ը���Ĭ�ϵĹ��ܣ�
6. �����ӳټ��ض�������ԣ�����ӷ������˻�ȡ��


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



### ʹ����ӵ��˽������
ES5���µİ汾�п���ͨ���հ������.

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



## **��**
### ��һְ��ԭ�� (SRP)

���ڡ�Clean Code�����ᵽ�ģ�����Ӧ���г���һ��ԭ��������һ���ࡱ������������Դ�һ��������Ǽ�һ�����Ѻܶ�Ĺ��ܶ�����һ�����￴�����ǳ����ˡ��������⽫���������ǳ����ι̶��Ҹ��˺ܶ��������ԭ�򡣽��͸�����Ŀ�����������Ҫ����һְ��ԭ�������Ҫ����Ϊ����������ӵ�������˸��ָ����Ĺ��ܣ���ô�����һ�㶼ʹ��ǳ���������⽫���������Ĵ����������Ӱ�졣

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


### ����-�պ�ԭ�� (OCP)

����Bertrand Meyer˵���ģ������ʵ�壨�ࡢģ�顢�����ȣ�Ӧ�ö�����չ�ǿ��ŵģ����Ƕ����޸��Ǳպϵġ���So����ɶ��˼�أ����ԭ��ǿ��������Ӧ����������û����̳���չ���ģ�飬�����Ǵ����js�ļ����޸�����

**Bad:**
```javascript
class AjaxRequester {
  constructor() {
    // ���������Ҫ������HTTP�����Ļ�������DELETE����ô�죿������Ҫ������ļ��ֶ���������
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



### Liskov �滻ԭ�� (LSP)

���ڼ򵥵ĸ�����������һ�����µ��������Ķ����ǡ����A��T�����࣬��ôT���͵Ķ�����Ա�S���͵Ķ������滻���Ӷ�Ҳ����ı��κγ������еĹ���(��ȷ�ԡ�����ִ�е�)�����ⶨ�忴���������¡�

��õĽ������������һ����������࣬��ô����͸�������໥�滻����Ӱ����ȷ�Ľ�����������Ȼ����о�������������ǿ�һ�¾���ķ���-�����ε����ӡ�����ѧ����������Ҳ�ǳ����Σ���������㽫�̳б��Ϊʹ�á�is-a���Ĺ�ϵ������ܺܿ������鷳��

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


###�ӿڸ���ԭ�� (ISP)

����JavaScript��û�нӿ���˱���ԭ�򲢲�������������һ�����ϸ����ء�Ȼ������ʹJavaScriptȱ�����ͻ��ƣ�����ԭ��һ���Ƿǳ���Ҫ�ͺ���ġ�

�ӿڸ���ԭ����ζ�š��ͻ��˲�Ӧ�ñ�ǿ������������ʹ�õĽӿڡ�������Ѽ�����ͣ��ӿ���JavaScript���ǱȽ���ʽ�Ĺ���

һ���ܺõ���ʾ��������İ����ǣ�������Ҫ�������ö����������ӡ����ÿͻ��������ô�����ѡ��������ģ���Ϊ�󲿷ֵ�ʱ�����ǲ�����Ҫ��Щ���á�����Щ���õĶ����ÿ�ѡ�ģ��Ӷ���ֹ�����һ���ֽӿڡ�

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
  animationModule: function() {} // �����������ǲ�����Ҫ����
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


### ��������ԭ��(DIP)

����ԭ����������ؼ������ݣ�
1. �߽�ģ�鲻Ӧ�������ͽ�ģ�顣���Ƕ�Ӧ����������
2. ����Ӧ������ϸ�ڡ�ϸ��Ӧ����������


էһ������ܱȽ�������⣬���������ʹ�ù�AngularJS�Ļ����Ѿ��������ԭ���ʵ���ˣ�������ע�롣����������ǲ�һ���ĸ����������ԭ���ʾ�߽�ģ��Ӧ�ñ���֪���ͽ�ģ���ϸ�ڡ������ͨ������ע����ʵ�֡�����������ĵ��洦���ǽ�����ģ�����϶ȡ��������������к�����ģʽ֮һ�����ǵĴ����ع���÷ǳ����ѡ�

����֮ǰ�ᵽ�ģ�JavaScriptû�нӿڵĸ����������ĳ�������ʽ�ġ������˵�������������Ƕ�����౩¶��������������Եġ�������������У�����ӿھ����κ�Requestģ����InventoryTracker��������һ��requestItems�ķ�����

**Bad:**
```javascript
class InventoryTracker {
  constructor(items) {
    this.items = items;

    // BAD: ���Ǵ����˶�ĳһ������requestʵ�ֵ�����
    // ����Ӧ�ý�����requestItems����һ��request����
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


### ����ʹ��ES6���������ES5����ͨ����

���ڵ��͵�ES5������˵����ÿɶ������õļ̳С����캯���ͷ�������ǳ����ѡ��������Ҫ�̳У���ôѡ����ɡ�Ȼ���������㷢������Ҫ�ܴ��Ҹ��ӵĶ�����ô����ѡ��С�ĺ����������ࡣ

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



### ʹ����ʽ��������

�롶Clean Code���Ľ�����㣵��ǣ�����������ӵ�в�ͬ�ĵط���������ʽ����һ��������ı���Ϊ�ǲ�����Ĳ���Υ��[Demeter����](https://en.wikipedia.org/wiki/Law_of_Demeter)�ġ��������ȷ�ǶԵģ���������ģʽ��JavaScript�зǳ����ã�������ںܶ�⺯���ж�������������jQuery��Lodash����ʹ��Ĵ���ǳ����б���Ժ͸��ٵ������ԡ���ˣ���˵��ʹ����ʽ�������ò��ҿ�һ����Ĵ����ô�����ࡣ������ຯ���У��򵥵ķ���this��ÿһ��������ĩβ����Ϳ���ʹ����ʽ�����ˡ�

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


### ������ڼ̳�
������ע���� [*���ģʽ*](https://en.wikipedia.org/wiki/Design_Patterns) ���ᵽ��,��Ӧ��ʹ���������ʹ�ü̳С�������һ���ʹ����Ϻͼ̳еĺô��������и�����Ҫ�ĸ��Ծ�������㱾�ܵ�ѡ��̳У���ͼȥ��������Ƿ���Ը��õĽ��������⡣

��������롰����ɶʱ��ʹ�ü̳��أ��������Ҫ��������Ҫ�������ɶ�����ˣ���������ֱ�ӵ��б�����������̳б���ϸ����ʵ�ʱ��

1. ��ļ̳б����ǡ�is-a���Ĺ�ϵ�������ǡ�has-a���Ĺ�ϵ��
2. ������ظ�ʹ����Ļ������룻
3. ����Ҫͨ���̳л�������չ���ࡣ

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


## **����**

���Ա���ɹ��ܸ���Ҫ�������û�в����������߲����Ĳ��ԣ���ôÿ�����޸����д����ʱ���㶼����ȷ����û���ƻ�ʲô����ô�����㹻�Ĳ�������ȡ��������Ŷӣ�����ӵ�аٷ�֮�ٵĸ������������ﵽ�����ŵķ����������˵����ʹ��һ���õĲ��Կ���⣬����ܻ���Ҫʹ��һ���õ�[�����ʹ���](http://gotwarlost.github.io/istanbul/)��

��Ϊ�㲻л���Զ��ҽ���ˡ�������һ������õ�[���Կ��](http://jstherightway.org/#testing-tools)��������һ������Ŷ�ϲ���ġ������ҵ�һ�������ŶӵĿ�ܺ���һ����Ŀ����Ƕ�ÿһ��ģ���ÿһ�����Զ�д���������������ϲ������������������ô�ܰ��������������ҪĿ��������㷢���κ�������֮ǰ��Ҫ�ﵽ��ĸ�����Ŀ�ꡣ


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


## **����**
### ʹ��Promises�������ǻص�
�ص���������������ģ�������ᵼ�¹����Ƕ�ס�ʹ��ES6��Promise���������õ�ȫ�����͡���ʹ�ðɡ�

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


### Async/Await��Promises������

Promises������ڻص���˵�ǳ���������������ES7������async��await�Ӷ��ṩ�˸�����ķ���������Ҫ���ľ����ں���ǰ����asyn�ؼ��֣�Ȼ����Ϳ���д����߼���������һ��then�����ˡ��������Գ������ES7�����ԣ���ôʹ������ɡ�

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



## **��ʽ**

��ʽ�ͷǳ������ˡ�������ĺܶԹ�������û�б������ع̶��ĺͿ�Ĺ�����Ҫ�Ĺ۵���Ǳ�Ϊ�˸�ʽ���������������д�����[��ʽ������](http://standardjs.com/rules.html)������Զ���ʽ����ʹ��һ�����ɡ��ڸ�ʽ�������������˷ѹ���ʦ��ʱ���������


### ʹ�������ԵĴ�д

JavaScript�������͵ģ���˴�д�������ܶ������ı����������ȡ���Щ���������۵ģ��������Ŷ���һ������ϲ���ļ��ɡ������ǣ���������ѡ������ĸ�������������һ�¡�

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



### �����ĵ����ߺͱ�������Ӧ�ñ��ֽ�Щ

���һ����������������һ����������Щ����Ӧ���ڴ���λ���ϱ��ֽ�һЩ����������£�������Ӧ�������ڱ����������档�������������϶��¶����룬�����Ķ���ֽһ������ˣ�Ҳͬ�������֯��Ĵ��롣

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



## **ע��**
### ����ע����Щӵ�и����߼��ĵط�
ע����һ����ǿ�Ľ��ͣ������Ǳ���ġ����õĴ���󲿷ֶ������ҽ��͵ġ�

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


### ���ע�͵��Ĵ������ڴ�����

�汾���ƹ����������ڵ�ԭ�򡣽���ʷ����������ʷ�汾�м��ɡ�

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


### ��д��־�Ƶ�ע��

��ס��ʹ�ð汾���ơ���������Ҫ������Щ���ġ�ע�ʹ��룬��������־�Ƶ�ע�͡�ʹ��git logȥ��ȡ��ʷ��־��

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


### ����ʹ��λ�ñ��

��ͨ�����ǰѴ����ø��ҡ��ú����ͱ�����ͨ�����ʵ������͸�ʽ��������������õ��Ӿ��ṹ��

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


### ������Դ�������������ע��

�����������ļ��øɵ��¡�

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
