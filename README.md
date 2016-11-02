# JavaScript Notes

| This is menu area |
| ------------- |

> 以下所述均以 ECMA Script 5 為主

## JavaScript Concept

* JavaScript 於 1995 年由任職 Netscape 的 [Brendan Eich](https://twitter.com/BrendanEich) 所創 

* ECMA Script 為 JavaScript 的標準化名稱

<br />

## JavaScript Core

語彙結構

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

<br />


型別、值與變數

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

  * **全域物件 (_global object_)**：當 JavaScript 直譯器啟動 或 瀏覽器載入新頁面，它會創建一個全域物件，並給它初始特性

    * undefined、Infinity、NaN

    * isNaN()、parseInt()、eval()

    * Date()、RegExp()、String()、Object() 這類建構函式

    * Math 與 JSON 這類全域物件

  * **this**：在頂層 (_top-level_) 程式碼，可使用 `this` 參考全域物件

    ex :

    ```javascript
    var global = this;     // 定義一個全域變數參考全域物件
    ```

  * **外覆物件 (_wrapper object_)**：每當參考「字串、數字、布林值」的特性，JavaScript 就會將它們轉為一個暫時物件，這個物件繼承了對應型別的原型特性，一旦特性被參考完畢，這個暫時物件就被丟棄，**null 與 undefined**並無此種物件，**此物件的特性是唯讀且不得定義新特性**

  * **基本型別 (_primitive types_)**：是用值 (_by value_) 相比，值是不可變的 (_immutable_)，兩者具有相同的值時，兩值相等

  * **物件型別 (_object types_)**：是參考 (_by references_) 相比，值是可變的 (_mutable_)，兩者即便擁有相同的特性，也不相等; 除非指涉至 (_refer to_) 同一個物件時，才相等

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

<br />

運算式與運算子

  * **運算式 (_expression_)**：直譯器可以估算 (_evaluate_) 它，進而產生一個結果值



<br />


## Client-Side JavaScript


<br />

## Server-Side JavaScript


<br />

## Reference Information

JavaScript : The Definitive Guide,  6E Traditional Chinese (Author：David Flanagan)

<br />