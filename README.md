## Table of Contents

[JavaScript Concept](#javascript-concept)

[JavaScript Core](#javascript-core)

  1. [Lexical Structure](#lexical-structure)
  2. [Types, Values, and Variables](#types-values-and-variables)
  3. [Expressions and Operators](#expressions-and-operators)
  4. [Statements](#statements)
  5. [Objects](#objects)
  6. [Arrays](#arrays)
  7. [Functions](#functions)

[Reference Information](#reference-information)

<br />

## JavaScript Concept

* JavaScript 於 1995 年由任職 Netscape 的 [Brendan Eich](https://twitter.com/BrendanEich) 所創 

* ECMAScript 為 JavaScript 的標準化名稱

<br />

## JavaScript Core

<a name="lexical-structure"></a>
Lexical Structure

  * JavaScript 的程式，需使用 Unicode 字元集撰寫 (ES5 要求實作支援 Unicode 3 later)

  * JavaScript 會區分大小寫，因此「關鍵字、變數、函式名稱、識別字」必須要大小寫一致

  * **字面值 (_literal_)** : 直接出現在程式中的資料值

    ex :
    ```javascript
    12                  // 數字 12
    1.2                 // 數字 1.2
    "hello world"       // 一列字串
    {x:1, y:2}          // 物件初值設定式
    [1, 2, 3, 4, 5]     // 陣列初值設定式
    ```

  * **識別字 (_identifier_)** : 就是個名稱，用來為「變數、函式名稱、迴圈中的標籤」命名，必須是「字母、底線、錢幣符號」開頭，接續字元可以是「字母、數字、底線、錢幣符號」

  * **保留字** : 不能用做識別字的語彙

    ex :

    ```javascript
    break、class、var 或 int
    ```

**[⬆ back to top](#table-of-contents)**

<br />
<br />

<a name="types-values-and-variables"></a>
Types, Values, and Variables

  * JavaScript 型別分成兩類：基本型別 (_primitive types_) 與 物件型別 (_object types_)

  * **基本型別 (_primitive types_)**：數字、字串、布林值、null、undefined

  * **物件型別 (_object types_)**：任何不是基本型別者，皆是物件型別

  * JavaScript 變數不具型別 (_untyped_)、採用語彙範疇 (_lexical scoping_)、變數用 `var` 宣告 (_declare_)

  * JavaScript 中的數字都以浮點數值 (_floating-point values_) 表示，不是整數值 (_integer values_)，**切記運算時可能會有誤差**

  * 數值運算的結果大於最大可表示的數字時，結果會是無限值 `Infinity` (_infinity value_)

  * 零除以零會是非數值 `NaN` (_not-a-number value_)

  * **字串字面值**：只要把字串的字元包在成對的單、雙引號 (_single or double quotes_) 中即可

    ex :

    ```javascript
    ""            // 空字串
    'testing'
    "3.14"
    ```

  * **字串字面值中的轉義序列 (_escape sequence_)**：用於表示字串中本來無法表示的字元，用 `\` 來操作

    ex :

    ```javascript
    'You\'re right, it can\'t be a quote'
    ```

  * **字串串接 (_concatenate strings_)**：`+` 運算子，可將兩字串連接起來

    ex :

    ```javascript
    msg = 'Hello, ' + 'World';     // => 'Hello, World'
    ```

  * **null**：這個值代表沒有值存在 (_the absence of a value_)

  * **undefined**：包含在以下幾種情況中「尚未初始化的變數、調用不存在的物件特性或陣列元素、沒有回傳值的函式、沒有提供對應引數 (_argument_) 的函式參數 (_parameter_)」

  * **全域物件 (_global object_)**：當 JavaScript 直譯器啟動 或 瀏覽器載入新頁面，它會創建一個全域物件，並給它下列初始特性：

    * undefined、Infinity、NaN

    * isNaN()、parseInt()、eval()

    * Date()、RegExp()、String()、Object() 這類建構函式

    * Math 與 JSON 這類全域物件

  * **this 關鍵字**：不是一個常數，它的估算值會隨著在程式中的位置而改變

    > 不同於變數，this 關鍵字沒有範疇 (_scope_)

    - 在 **頂層 (_top-level_)** 中：this 參考至全域物件

      > top-level：即不包含在任何函式定義內的程式碼

    - 函式調用：this 參考至全域物件，strict 模式中 為 `undefined`

    - 方法調用：this 參考至方法所屬的物件

    ex :

    ```javascript
    var obj = {

      m: function() {

        var self = this;

        console.log(this === obj);       // => true

        func();

        function func() {

          console.log(this === obj);     // => false，this 為全域物件 或 undefined
          console.log(self === obj);     // => true，self 是外層的 this 值
        }
      }
    };

    obj.m();
    ```

  * **外覆物件 (_wrapper object_)**：每當參考「字串、數字、布林值」的特性，JavaScript 就會將它們轉為一個暫時物件，這個物件繼承了對應型別的原型特性，一旦特性被參考完畢，這個暫時物件就被丟棄，**null 與 undefined**並無此種物件，**此物件的特性是唯讀且不得定義新特性**

  * **基本型別 (_primitive types_)**：是用值 (_by value_) 相比，值是不可變的 (_immutable_)，兩者具有相同的值時，兩值相等

    ex：

    ```javascript
    var s = 'hello';     // 創建一些小寫文字
    s.toUpperCase();     // 回傳 'HELLO'，但沒有更動 s
    s                    // => 'hello'：原字串並未改變
    ```

  * **物件型別 (_object types_)**：是參考 (_by references_) 相比，值是可變的 (_mutable_)，兩者即便擁有相同的特性，也不相等; 除非指涉至 (_refer to_) 同一個物件時，才相等

    ex：

    ```javascript
    var a = [];          // 變數 a 指涉一個空陣列
    var b = a;           // 現在 b 也指涉至同一個陣列
    b[0] = 1;            // 使 b 指涉的陣列變異
    a[0]                 // => 1：透過變數 a 也可以看見這個改變
    a === b              // => true：a 與 b 指涉至同一個物件，所以它們相等
    ```

  * **明確的 (_explicit_) 型別轉換**：可透過轉換函式轉換型別

    ex :

    ```javascript
    Number('3')       // => 3
    String(false)     // => 'false'
    Boolean([])       // => true
    Object(3)         // => new Number(3)
    ```

  * **變數宣告 (_variable declare_)**：使用 `var`，可用同一個關鍵字宣告多個變數，也可直接初始化 (_initialization_)，只宣告並未初始化的變數，它的值會是 `undefined`

    ex :

    ```javascript
    var i, sum;

    var x = 0, y = 1, z = 2;
    ```

    > automatically global：If you assign a value to a variable that has not been declared, it will automatically become a global variable. Even if the value is assigned inside a function.

    > global variables are not created automatically in "Strict Mode".

  * **變數範疇 (_variable scope_)**：在頂層 (_top-level_) 宣告的變數為全域變數 (_global variable_)，在函式主體中定義的變數為區域變數 (_local variable_)，函式參數 (_parameters_) 也算區域變數

  * **變數優先序 (_precedence_)**：區域變數的優先序，比同樣名稱的全域變數還高

    ex :

    ```javascript
    var scope = 'global';        // 宣告全域變數

    function checkScope() {

        var scope = 'local';     // 宣告同名的區域變數

        return scope;            // 回傳區域變數的值
    }

    checkScope();                // => 'local'
    ```

  * **函式範疇 (_function scope_)**：只有在定義變數的函式及其內的任何巢狀函式中，才看得到這些變數

    > Each function creates a new scope.

  * **全域變數 (_global variables_)**

    - A variable declared outside a function, becomes global.

    - A global variable has global scope：All scripts and functions on a web page can access it.

    > 當你宣告一個全域變數，實際上你是定義全域物件中的一個特性

    > In HTML, the global scope is the window object. All global variables belong to the window object.

  * **區域變數 (_local variables_)**

    - Variables declared within a JavaScript function, become local to the function.

    - Local variables have local scope：They can only be accessed within the function.

  * The Lifetime of JavaScript Variables

    - The lifetime of a JavaScript variable starts when it is declared.

    - Local variables are deleted when the function is completed.

    - In a web browser, global variables are deleted when you close the browser window (or tab).

  * **拉升 (_Hoisting_)**：`var` 宣告的變數 和 `function` 宣告的函式，都會被 "拉升" 至範疇的頂端

    - Variable declarations are processed before any code is executed.

    - JavaScript only hoists declarations, not initializations.

    - 對於函式宣告述句，函式名稱與函式主體兩者都會被 "拉升"

    ex :

    ```javascript
    // 函式宣告拉升

    foo();
    function foo() {     // 此函式被拉升了

    }

    // 實際執行時，會將上述程式碼以下列方式執行

    function foo() {

    }

    foo();

    // 變數宣告拉升

    foo();
    var foo = function () {

    };

    // 實際執行時，會將上述程式碼以下列方式執行

    var foo;
    foo();     // TypeError：undefined is not a function
    foo = function () {

    };
    ```

**[⬆ back to top](#table-of-contents)**

<br />
<br />

<a name="expressions-and-operators"></a>
Expressions and Operators

  * **運算式 (_expression_)**：直譯器可以估算 (_evaluate_) 它，進而產生一個結果值

  * **運算子 (_operators_)**：運算子大多用標點符號 (_punctuation_) 來表示，擁有優先序 (_precedence_)、結合律 (_associativity_)

  * **運算元 (_operands_)**：被運算子所估算 (_evaluate_) 的元素

    ex :

    ```javascript
    1 + 2;          // => 3; + 為運算子，1 和 2 為運算元
    11 < 3;         // => true
    delete o.x;     // 刪除物件 o 的特性 x
    ```

**[⬆ back to top](#table-of-contents)**

<br />
<br />

<a name="statements"></a>
Statements

  * **條件述句 (_conditional statements_)**：`if`、`else if`、`switch`

    ex :

    ```javascript
    // if statement

    if (username === null) {

        username = 'Justin Ho';

    } else {

        console.log(username);

    }

    // else if statement

    if (x === 1) {

        // 執行程式區塊 1

    } else if (x === 2) {

        // 執行程式區塊 2

    } else if (x === 3) {

        // 執行程式區塊 3

    } else {

        // 所有的條件都不滿足，就執行程式碼區塊 4
    }

    // switch statement

    /* case 匹配與否是由 === 同一性 (identity) 運算子所判定
     *
     * ECMAScript 標準允許每個 case 後面跟的可以是任意運算式
     *
     * 如果沒有匹配的 case 且不存在 default: 標籤，則跳過整個 switch 主體
     */

    switch (x) {

        case 'number':     // 如果 x 等於 'number'，則執行此處
          // 執行程式區塊 1
          break;

        case 'string':
          // 執行程式碼區塊 2
          break;

        default:           // 如果都沒有找到相同的值，則執行此處
          //執行程式碼區塊 3
          break;           // 在這裡停止執行
    }
    ```

  * **迴圈述句 (_looping statements_)**：`while`、`do/while`、`for`、`for/in`

    ex :

    ```javascript

    // while statement

    var count = 0;

    while (count < 10) {

        console.log(count);
        count++;
    }

    // do/while statement

    var array = [1, 2, 3];
    var len = array.length, i = 0

    do {

        console.log(array[i]);

    } while (++i < len);

    // for statement

    for (var count = 0; count < 10; count++) {

        console.log(count);
    }

    // for/in statement

    /* 直譯器僅會列出物件中可列舉的 (enumerable) 特性
     */

    for (var p in o) {         // 指定 o 的特性名稱給變數 p

        console.log(o[p]);     // 印出每個特性值
    }
    ```

  * **被加上標籤的述句 (_labeled statement_)**：為述句加上一個標籤，可在程式其他地方參考此述句，標籤名稱可以是任何合法的識別字，但不能是保留字，標籤的名稱與變數、函式名稱的命名空間不同

    ex :

    ```javascript
    mainloop: while (token != null) {

        // 省略程式碼...

        continue mainloop;     // 跳至具名 (named) 迴圈的下一次迭代

        // 省略更多程式碼...
    }
    ```

  * **跳躍述句 (_jump statements_)**：`break`、`continue`、`return`、`try/catch/finally`

    ex :

    ```javascript
    // break statement

    for (var i = 0; i < a.length; i++) {

        if (a[i] == target) {

            break;     // 可使最內層的外圍迴圈，立即終止並跳離
        }
    }

    // continue statement

    for (i = 0; i < data.length; i++) {

        if (!data[i]) {

            continue;     // 重新開始下一次迭代
        }

        total += data[i];
    }

    // return statement

    function square(x) {

        return x*x;     // 回傳該運算式的值給呼叫者 (caller)
    }

    // try/catch/finally statement

    /* 當有例外 (exception) 被拋出，直譯器會立刻停止正常的程式執行流程
     *
     * 並跳至最近的例外處理器 (exception handler)，也就是 catch block
     *
     * try：用來界定需要例外處理的程式碼範圍
     *
     * catch：try 區塊只要有例外拋出，catch 區塊即刻被調用
     *
     * finally：不管 try 有無拋出例外，該區塊都會被執行
     *
     * catch、finally 區塊都是非必需的，但至少要有一個伴隨 try 區塊
     */

    try {

        // 欲執行的程式碼放這裡

    } catch (exception) {     // exception 具有區塊範疇 (block scope)，只在 catch 區塊被定義

        // 在此處理捕獲的例外，可透過 exception 來參考拋出的 物件 或 值

    } finally {

        // try 區塊以下列任一種方式終止時，它們就會被執行：

        // 1) 抵達區塊結尾後正常結束
        // 2) 因為 break、continue 或 return 述句
        // 3) 有例外發生，並被上方的 catch 子句所處理
        // 4) 有個未被捕獲的例外，仍在傳遞
    }
    ```
  * 'use strict'：指出接在其後的程式碼屬於**strict 程式碼**，如果函式主體是定義在 strict 程式碼之中，該函式也屬於 strict 程式碼

**[⬆ back to top](#table-of-contents)**

<br />
<br />

<a name="objects"></a>
Objects

  * 物件是特性的集合

  * 每個特性均有其相關連的特性屬性 (_property attributes_)

    * 可寫 (_writable_)：指明該特性的值能否被更動

    * 可列舉 (_enumerable_)：指明該特性名稱是否可被 for/in 迴圈回傳

    * 可配置 (_configurable_)：指明該特性是否可被刪除，以及它的屬性能否被更動

  * 每個物件均有其相關連的物件屬性 (_object attributes_)

    * (_prototype_)：指明該物件繼承至哪個物件

    * (_class_)：是個字串，用以區分該物件的種類

    * (_extensible_)：指明是否可在該物件加入新特性

  * 創建物件可透過 3 種方式「物件字面值 (_object literal_)、new 關鍵字、Object.create()」

    - new 關鍵字後面必須接著函式調用，透過這種方式調用的函式稱為**建構式 (_constructor_)**

      > 除了內建的建構式 (Object、Date、RegExp...etc) 之外，也可以定義自己的建構式來初始化並創建物件

    ex :

    ```javascript
    // 物件字面值

    var empty = {};
    var point = {x:0, y:0};
    var point2 = {x: point.x, y:point.y+1};
    var book = {
        "main title": "JavaScript",
        'sub-title': "The Definitive Guide",
        "for": "all audiences",
        author: {
            firstname: "David",
            surname: "Flanagan",
        }
    };

    // new 關鍵字

    var o = new Object();         // 創建空物件，等同於 {}
    var a = new Array();          // 創建空陣列，等同於 []
    var d = new Date();           // 創建代表目前時間的 Date 物件
    var r = new RegExp("js");     // 創建用來範式比對的 RegExp 物件

    // Object.create()

    var o1 = Object.create({x: 1, y: 2});     // o1 繼承了特性 x 與 y
    var o2 = Object.create(null);             // o2 不會繼承任何特性或方法
    ```

  * 每個物件都有第二個物件與之關聯，而這第二個物件就稱為原型，第一個物件就從這個原型繼承特性

  * **原型鏈 (_prototype chain_)**：物件與原型之間繼承的關係就稱為原型鏈

  * 所有用物件字面值建立的物件，都有同一個原型物件，我們用 Object.prototype 來參考這個原型物件

  * 透過 new 關鍵字與建構式調用所產生的物件，其原型為**建構函式 (_constructor function_)** 的 prototype 特性值

    > 由 new Object() 創建的物件繼承自 Object.prototype 與 {} 創建的物件相同

    > 由 new Date() 創建的物件，其原型為 Date.prototype

  * Object.create() 建立的物件，可指定原型或不繼承任何原型物件

  * 要獲取或設定特性的值可透過「`.`、`[]`」運算子

    ex :

    ```javascript
    // 獲取

    var author = book.author;
    var name = author.surname;
    var title = book['main title']

    // 設定

    book.edition = 6;
    book['main title'] = 'ECMAScript';
    book['Hello' + 'World'] = 'helloworld';
    ```

  * 如果已存在繼承特性 (_inherited property_) x，再新增一個同名的自有特性 x，則此自有特性會覆寫 (_override_) 繼承特性 x

  * 特性的指定會檢視原型鏈 (_prototype chain_)，判斷這個指定是否可行，如果該指定被允許，它只會在原本的物件上新建或設定特性，永遠不會修改到原型鏈中的物件

  * 繼承只在查用特性時發生，而不在設定特性時發生，意思是無法透過繼承去修改原型物件的特性

  * 刪除指定特性可透過「`delete`」運算子，但只能刪除自有特性，且不會刪除 configurable 屬性為 false 的特性

    ex :

    ```javascript
    delete bookauthor;
    delete book['main title'];
    ```

  * 查看物件的指定特性屬性可透過 `Object.getOwnPropertyDescriptor()`

    ex :

    ```javascript
    var o = {x:1, y:2, z:3};

    console.log(Object.getOwnPropertyDescriptor(o, 'y'));

    // 回傳值如下

    /* [object Object] {
     *   configurable: true,
     *   enumerable: true,
     *   value: 2,
     *   writable: true
     * }
     */
    ```

  * 設定物件特性的屬性可透過 `Object.defineProperty()`

    ex :

    ```javascript
    var o = {};

    Object.defineProperty(o, 'x', {

        value: 1,
        writable: true,
        enumerable: false,
        configurable: true

    });

    // 查看特性是否存在

    o.x;     // => 1
    ```

  * 設定多筆物件特性與其屬性可透過 `Object.defineProperties()`

  * 遍歷物件中的特性可透過下列方式

    - 自有特性 (_own properties_)：Object.getOwnPropertyNames(object)，包含不可列舉的特性

    - 繼承特性 (_inherited properties_)：for-in 迴圈，列出自有、繼承的可列舉的特性

  * 讀取、設定物件屬性 (_object attributes_)

    - 原型 (_prototype_)

      - 讀取：Object.getPrototypeOf(object)

      - 設定：Object.setPrototypeOf(object, prototype)

    - 類別 (_class_)

      - 讀取：Object.prototype.toString.call(object).slice(8, -1)，僅有此間接方式可取得

      - 設定：無

    - 擴充性 (_extensible_)

      > 所有內建與使用者自定義的物件，預設都是可擴充的

      - 讀取：Object.isExtensible(object)，判斷物件是否為可擴充

      - 設定：Object.preventExtensions(object)，將物件設為不可擴充(_nonextensible_)

  * **物件序列化 (_serialization_)**：將物件轉成字串，並讓它可由字串復原成物件

    ex :

    ```javascript
    var o = {x:1, y:{z:[false, null, '']}};     // 定義一個物件

    var s = JSON.stringify(o);                  // 序列化 物件o，將 物件o 轉成字串

    var p = JSON.parse(s);                      // 復原被序列化的 物件 o

    // 調用被復原的 物件o 特性

    console.log(p.y.z[0]);                      // => false
    ```

**[⬆ back to top](#table-of-contents)**

<br />
<br />

<a name="arrays"></a>
Arrays

  * 陣列的元素可以是任何的型別，同一陣列中的不同元素可能具有不同型別

  * 建立陣列元素可透過 `[]`、`new Array()`，**陣列字面值允許在結尾加上逗號**

    ex :

    ```javascript
    var empty = [];                    // 空陣列
    var primes = [2, 3, 5, 7, 11];     // 五個數值元素的陣列
    var misc = [1.1, true, 'a',];      // 三個不同型別的元素，加上尾隨的逗號

    var base = 1024;
    var table = [base, base + 1, base + 2, base + 3];

    var count = [1,,3];     // count[1] => undefined
    var undefs = [,,];      // 稀疏陣列

    var a = new Array();                          // 等同於 []
    var a = new Array(10);                        // 指定陣列長度
    var a = new Array(5, 4, 3, 2, 1, 'test');     // 含有六個元素的陣列
    ```

  * 讀取或寫入陣列的值可透過 `[]`

    ex :

    ```javascript
    var a = ['world'];          // 建立具有單一元素的陣列
    var value = a[0];           // 讀取元素 0
    var a[1] = 3.14;            // 寫入元素 1

    var i = 2;
    var a[i + 1] = 'hello';     // 寫入元素 3
    ```

  * forEach()：可迭代所有元素，第一個參數為函式，forEach() 會用三個引數呼叫你指定的函式，而缺點是無法使用 `break` 關鍵字中斷

    - 第一個引數：陣列元素值

    - 第二個引數：陣列元素的索引

    - 第三個引數：陣列本身

    ex :

    ```javascript
    var data = [1, 2, 3, 4, 5];

    data.forEach(function(value, index, array) {

      array[index] = value + 1;
    });

    console.log(data);     // => [2, 3, 4, 5, 6]
    ```

**[⬆ back to top](#table-of-contents)**

<br />
<br />

<a name="functions"></a>
Functions

  * **函式 (_function_)**：是 JavaScript 的程式碼區塊，僅定義一次，可以被多次調用 (_invoked_)

  * 如果一個函式被指定給物件的特性，則稱為方法 (_method_)

  * 函式宣告可透過 `function`

    ex :

    ```javascript
    function distance(x1, y1, x2, y2) {          // distance 為函式名稱，後面 () 包覆的內容為參數 (parameters)

        var dx = x2 - x1;
        var dy = y2 - y1;

        return Math.sqrt(dx * dx + dy * dy);     // 透過 return 回傳此函數的回傳值
    }
    ```

  * 函式宣告實際上是宣告一個變數，然後把函式物件指定給它，而函式運算式則沒有宣告變數

  * 函式運算式的函式名稱是**非必要的**

    ex :

    ```javascript
    var x = 10;
    var square = function(x) {return x * x;}
    console.log(square(x));                                 // => 100

    data.sort(function(a, b) {return a-b;});                // 函式運算式也可以當作其他函式的引數

    var tensquared = (function(x) {return x * x} (10));     // 函式運算式也可以在宣告後立即調用
    ```

  * 調用函式可透過四種方式「`函式調用`、`方法調用`、`建構式調用`、`間接調用`」

    - 調用情境

      - 函式調用：ES3 及 非strict的ES5中，調用情境為全域物件，在strict模式中，則為 `undefined`

      - 方法調用：調用方法的物件即是調用情境，可用關鍵字 `this` 參考該物件

      - 建構式調用：建構式調用會產生一個新物件，此物件即是調用情境，可用關鍵字 `this` 參考該物件

      - 間接調用：call() 與 apply() 方法的第一個參數即可指定調用情境

    ex :

    ```javascript
    // 函式調用

    printprops(10, 5);

    // 方法調用

    o.printprops(10, 5);

    // 建構式調用

    var o = new Object();
    var o = new Object;

    // 間接調用

    f.call(o);           // 把函式 f() 當成物件 o 的方法來調用
    f.apply(o);
    f.call(o, 1, 2);     // 第一個引數指出要在哪個物件上調用函式，之後的引數為要傳入函式的引數
    ```

  * 函式調用不會對傳入的引數做任何型別檢查，也不會檢查引數個數

  * 函式調用的引數比宣告的參數少時，額外的參數會被設為 undefined

  * 函式調用的引數比宣告的參數多時，可透過 `arguments` 參考

  * arguments 是一種類陣列物件 (_array-like object_)

    ex :

    ```javascript
    function f(x, y, z) {

        console.log(arguments[0]);         // arguments[0] 等於，引數 x
        console.log(arguments[1]);         // arguments[1] 等於，引數 y
        console.log(arguments[2]);         // arguments[2] 等於，引數 z

        // 三個引數被調用

        console.log(arguments.length);     // => 3
    }
    ```

  * 函式不只是語法，它也是「值」(_value_)

    ex :

    ```javascript
    function square(x) {return x * x;}             // 定義一個函式

    var s = square;                                // 現在 s 與 square 參考至相同的函式
    square(4);                                     // => 16
    s(4);                                          // => 16

    var a = [function(x) {return x * x;}, 20];     // 一個陣列字面值
    a[0](a[1]);                                    // => 400
    ```

  * 函式是一種特化的物件，所以它也有特性

    ex :

    ```javascript
    uniqueInteger.counter = 0;            // 初始化這個函式物件的 counter 特性

    function uniqueInteger () {
      return uniqueInteger.counter++;     // 回傳並遞增 counter 特性
    }
    ```

  * 參數傳遞方式：為 Call by sharing，複製參考到新的參照上，修改會改變原有參照，賦予新值則會產生新的參考

    ex :

    ```javascript
    var arr1 = [1,2,3];
    var arr2 = arr1;       // arr1 和 arr2，指向相同的參考上

    arr2 = [4,5,6];        // 新建立一個 Array，並將它指向 arr2

    console.log(arr1);     // => [1, 2, 3]
    ```

  * 每個函式都有一個 prototype 特性，用來參考 prototype 物件，透過 new 關鍵字實例化物件，則會用此 prototype 物件繼承其他物件

  * call()、apply()：用於間接呼叫函式，可操作原本物件上沒有的方法，並指定運行環境

    - call(thisArg, arg1, arg2)：第一個參數為調用情境，第二個開始的參數為欲代入函式的引數

    - apply(thisArg, [argsArray])：第一個參數為調用情境，第二個參數是一個陣列，其內容為欲代入函式的引數

    ex :

    ```javascript
    var obj1 = {

      getName: function () {

        return this.name;
      }
    };

    var obj2 = {                              // obj2 沒有 getName()

      name: 'Justin'
    }

    console.log(obj1.getName.call(obj2));     // => 'Justin'，透過 call() 讓 obj2 間接呼叫 obj1 的函式
    ```

  * bind()：用於將一個函式繫結至 (bind to) 一個物件

    ex：

    ```javascript
    // 當你在函式 f 上調用 bind() 方法，並傳入物件 o，這個方法會回傳一個新的函式
    // 調用這個新函式，會把原本的函式 f 當作 o 的方法來調用
    // 任何傳給新函式的引數都會傳入原本的函式

    function f(y) { return this.x + y; }     // 這個函式需要繫結
    var o = { x: 1 };                        // 我們會繫結至物件 o
    var g = f.bind(o);                       // 呼叫 g(x) 會調用 o.f(x)
    g(2);                                    // => 3
    ```

  * **回呼 (_callback_)**：是一個函式，將其當作引數放進另一個函式等待被操作，前者就是後者的回呼

    ex :

    ```javascript
    var func = function() {

      console.log('Hello World');
    };

    window.addEventListener('load', func, false);     // => 'Hello World'，觸發 load 事件時，呼叫 func()
    ```

  * **閉包 (_closure_)**：closure is a function having access to the parent scope, even after the parent function has closed.

    - It makes it possible for a function to have "**private**" variables.

    - closure 會捕捉它們外層函式 (即它們被定義之處) 的區域變數 (以及參數) 之繫結

    ex :

    ```javascript
    // JavaScript 函式執行時使用的範疇鏈 (scope chain)，是在它們定義時生效的範疇鏈
    // 巢狀函式 func() 定義時的範疇鏈，其中的變數 scope 是繫結至 (bound to) 值 "local scope"
    // 這個繫結 (binding) 在 func 執行時仍然有效，不管它是在何處被執行

    var scope = 'global scope';

    function checkScope() {

      var scope = 'local scope';

      function func() {

        return console.log(scope);
      }

      return func;
    }

    checkScope()();    // => 'local scope'，func() 為 closure
    ```

**[⬆ back to top](#table-of-contents)**

<br />
<br />

## Reference Information

JavaScript : The Definitive Guide,  6E Traditional Chinese (Author：David Flanagan)

Speaking JavaScript, Traditional Chinese (Author：Dr. Axel Rauschmayer)

JavaScript — call-by-sharing (Author：Avinash Kondeti)

  - https://medium.com/wwstay-engineering/javascript-call-by-sharing-2d3ca42c4d02#.ms38pikzt

簡單介紹JavaScript參數傳遞 (Author：Tommy Lin)

  - http://www.slideshare.net/YiTaiLin/java-script-63031051

<br />
