# 目錄

- [物件導向程式設計 (OOP) 深入探討](#物件導向程式設計-oop-深入探討)
  - [繼承 (Inheritance)](#繼承-inheritance)
  - [介面 (Interfaces)](#介面-interfaces)
  - [抽象類別 (Abstract Classes)](#抽象類別-abstract-classes)
  - [Traits](#traits)
  - [靜態方法與屬性 (Static Methods & Properties)](#靜態方法與屬性-static-methods--properties)
  - [存取修飾子 (Access Modifiers)](#存取修飾子-access-modifiers)
  - [魔術方法 (Magic Methods)](#魔術方法-magic-methods)
  - [Final 類別與方法](#final-類別與方法)
  - [Late Static Binding (`static::`)](#late-static-binding-static)
  - [例外處理 (Exception Handling)](#例外處理-exception-handling)
- [常用函式速查表](#常用函式速查表)
  - [陣列 (Array) 相關函式](#陣列-array-相關函式)
  - [陣列排序函式](#陣列排序函式)
  - [字串 (String) 相關函式](#字串-string-相關函式)
  - [數學函式](#數學函式)
  - [類別與物件 (Class & Object) 相關函式](#類別與物件-class--object-相關函式)
  - [魔術常數 (Magic Constants)](#魔術常數-magic-constants)
- [Generator（生成器）](#generator生成器)
- [Closure（閉包）進階](#closure閉包進階)
- [日期與時間 (DateTime)](#日期與時間-datetime)
- [命名空間 (Namespaces)](#命名空間-namespaces)
- [PHP 版本新功能](#php-版本新功能)
  - [PHP 7.0](#php-70)
  - [PHP 7.1](#php-71)
  - [PHP 7.2](#php-72)
  - [PHP 7.3](#php-73)
  - [PHP 7.4](#php-74)
  - [PHP 8.0](#php-80)
  - [PHP 8.1](#php-81)
  - [PHP 8.2](#php-82)
  - [PHP 8.3](#php-83)
  - [PHP 8.4](#php-84)
  - [PHP 8.5](#php-85)

---

---

# 物件導向程式設計 (OOP) 深入探討

物件導向（Object-Oriented Programming, OOP）是一種程式設計範式，將程式中的資料與操作資料的行為封裝在「物件（Object）」中。OOP 模擬現實世界中事物的特性，使程式更容易設計、維護與擴充。

## OOP 核心思想 (三大原則)

### 1. 封裝 (Encapsulation)
封裝是將資料 (物件的屬性) 和操作該資料的方法 (物件的方法) 捆綁在一起的機制，並對外部隱藏物件的內部狀態。外部程式碼只能透過物件提供的公開方法來與之互動，而不能直接存取其內部資料。這有助於保護資料的完整性，並降低系統的複雜度。

### 2. 繼承 (Inheritance)
繼承是一種「is-a」的關係，它允許一個新的類別 (子類別) 獲取另一個類別 (父類別) 的屬性和方法。子類別可以重用父類別的程式碼，也可以覆寫 (override) 父類別的方法或添加自己的新功能，從而實現程式碼的重用和擴展。

### 3. 多型 (Polymorphism)
多型 (字面意思是 "many forms") 指的是不同的物件可以對相同的訊息做出不同的回應。在實務上，這通常是透過介面 (Interface) 或抽象類別 (Abstract Class) 實現的。當多個類別實現同一個介面時，我們可以像對待同一個類型一樣對待它們的物件，但每個物件在執行相同的方法時，會表現出各自獨特的行為。這讓程式碼更具彈性和可擴展性。

## 繼承 (Inheritance)
繼承允許一個類別 (子類別) 繼承另一個類別 (父類別) 的屬性和方法，實現程式碼重用。

```php
class Animal {
    public function eat() {
        echo "This animal eats food.";
    }
}

// Dog 繼承自 Animal
class Dog extends Animal {
    public function bark() {
        echo "Woof!";
    }
}

$dog = new Dog();
$dog->eat();  // 繼承自 Animal 的方法
$dog->bark(); // 自己的方法
```

## 介面 (Interfaces)
介面定義了一個「契約」，它只定義方法名稱和參數，但不包含具體實現。任何實現該介面的類別都必須提供這些方法的具體程式碼。

```php
interface Loggable {
    public function log(string $message);
}

class FileLogger implements Loggable {
    public function log(string $message) {
        file_put_contents('app.log', $message, FILE_APPEND);
    }
}

class DatabaseLogger implements Loggable {
    public function log(string $message) {
        // 將訊息寫入資料庫的邏輯
    }
}
```

## 抽象類別 (Abstract Classes)
抽象類別是介於介面和具體類別之間的產物。它不能被實例化，但可以包含已經實現的方法和未實現的抽象方法。子類別必須實現父類別中所有的抽象方法。

```php
abstract class Shape {
    // 這是一個已實現的方法
    public function getColor(): string {
        return 'red';
    }

    // 這是一個抽象方法，子類別必須實現它
    abstract public function getArea(): float;
}

class Square extends Shape {
    private float $side;

    public function __construct(float $side) {
        $this->side = $side;
    }

    // 實現父類別的抽象方法
    public function getArea(): float {
        return $this->side * $this->side;
    }
}
```

## Traits
Traits 是一種在單一繼承的語言 (如 PHP) 中實現程式碼水平重用的機制。一個類別可以使用 `use` 關鍵字來引入一個或多個 Trait 的方法。

```php
trait Sharable {
    public function share(string $item) {
        echo "Sharing " . $item;
    }
}

class Post {
    use Sharable;
    public string $title;
}

class Photo {
    use Sharable;
    public string $url;
}

$post = new Post();
$post->share('My new blog post');
```

## 靜態方法與屬性 (Static Methods & Properties)
靜態成員屬於類別本身，而不是類別的某個實例。可以直接透過類別名稱和 `::` 來存取，而不需要建立物件。

```php
class MathHelper {
    public static float $pi = 3.14;

    public static function add(int $a, int $b): int {
        return $a + $b;
    }
}

// 直接存取靜態屬性
echo MathHelper::$pi; // 3.14

// 直接呼叫靜態方法
echo MathHelper::add(5, 10); // 15
```

## 存取修飾子 (Access Modifiers)

- **`public`**: 公開的。可以在任何地方被存取。
- **`protected`**: 受保護的。只能在該類別自身、其父類別、以及其子類別中存取。
- **`private`**: 私有的。只能在宣告它的那個類別中存取。

```php
class MyClass {
    public $public = 'Public';
    protected $protected = 'Protected';
    private $private = 'Private';

    public function printHello() {
        echo $this->public;    // OK
        echo $this->protected; // OK
        echo $this->private;   // OK
    }
}

class MySubClass extends MyClass {
    public function printHello2() {
        echo $this->public;    // OK
        echo $this->protected; // OK
        // echo $this->private;   // Error
    }
}

$obj = new MyClass();
echo $obj->public; // OK
// echo $obj->protected; // Error
// echo $obj->private;   // Error
```

## 魔術方法 (Magic Methods)
魔術方法是 PHP 保留的特殊方法，以雙底線開頭，在特定事件觸發時自動被呼叫。

| 方法 | 觸發時機 |
|------|---------|
| `__construct()` | 物件被建立時 |
| `__destruct()` | 物件被銷毀時 |
| `__toString()` | 物件被當作字串使用時 |
| `__get($name)` | 存取不存在或不可存取的屬性時 |
| `__set($name, $value)` | 寫入不存在或不可存取的屬性時 |
| `__isset($name)` | 對不存在屬性呼叫 `isset()` 時 |
| `__unset($name)` | 對不存在屬性呼叫 `unset()` 時 |
| `__call($name, $args)` | 呼叫不存在或不可存取的方法時 |
| `__callStatic($name, $args)` | 靜態呼叫不存在的方法時 |
| `__invoke(...$args)` | 物件被當作函式呼叫時 |
| `__clone()` | 物件被 `clone` 複製時 |

```php
class MagicClass {
    private array $data = [];

    // 攔截屬性讀取
    public function __get(string $name): mixed {
        return $this->data[$name] ?? null;
    }

    // 攔截屬性寫入
    public function __set(string $name, mixed $value): void {
        $this->data[$name] = $value;
    }

    // 物件轉字串
    public function __toString(): string {
        return json_encode($this->data);
    }

    // 物件當函式呼叫
    public function __invoke(int $x): int {
        return $x * 2;
    }
}

$obj = new MagicClass();
$obj->name = 'Alice';   // 觸發 __set
echo $obj->name;        // 觸發 __get → 'Alice'
echo $obj;              // 觸發 __toString → '{"name":"Alice"}'
echo $obj(5);           // 觸發 __invoke → 10
```

## Final 類別與方法
`final` 關鍵字可防止類別被繼承、或方法被覆寫。

```php
final class Singleton {
    private static ?self $instance = null;

    private function __construct() {}

    public static function getInstance(): static {
        return self::$instance ??= new static();
    }
}

// class ExtendedSingleton extends Singleton {} // Error：無法繼承 final 類別

class Base {
    final public function doSomething(): void {
        echo 'cannot be overridden';
    }
}

class Child extends Base {
    // public function doSomething(): void {} // Error：無法覆寫 final 方法
}
```

## Late Static Binding (`static::`)
`self::` 永遠指向定義該方法的類別；`static::` 則指向實際被呼叫的類別（執行期解析）。

```php
class ParentClass {
    public static function create(): static {
        return new static(); // 依呼叫者決定實例化哪個類別
    }

    public static function selfName(): string {
        return self::class; // 永遠是 'ParentClass'
    }

    public static function staticName(): string {
        return static::class; // 依呼叫者而定
    }
}

class ChildClass extends ParentClass {}

$obj = ChildClass::create();          // ChildClass 的實例
echo ChildClass::selfName();          // 'ParentClass'
echo ChildClass::staticName();        // 'ChildClass'
```

## 例外處理 (Exception Handling)

```php
// 自訂例外
class DatabaseException extends RuntimeException {
    public function __construct(
        string $message,
        private readonly string $query = '',
        int $code = 0,
        ?\Throwable $previous = null,
    ) {
        parent::__construct($message, $code, $previous);
    }

    public function getQuery(): string {
        return $this->query;
    }
}

// try / catch / finally
try {
    throw new DatabaseException('Connection failed', 'SELECT * FROM users', 500);
} catch (DatabaseException $e) {
    echo $e->getMessage(); // 'Connection failed'
    echo $e->getQuery();   // 'SELECT * FROM users'
} catch (\Throwable $e) {
    // 捕捉所有錯誤與例外（含 Error）
    echo $e->getMessage();
} finally {
    // 無論是否拋出例外都會執行
    echo 'cleanup done';
}
```

---

# 常用函式速查表

## 陣列 (Array) 相關函式

#### `array_chunk()`
將一個陣列分割成多個較小的區塊。
```php
$input = ['a', 'b', 'c', 'd', 'e'];
$chunks = array_chunk($input, 2);
// $chunks is [['a', 'b'], ['c', 'd'], ['e']]
```

#### `array_column()`
回傳陣列中指定單一欄位的值。
```php
$records = [
    ['id' => 2135, 'first_name' => 'John'],
    ['id' => 3245, 'first_name' => 'Sally'],
];
$first_names = array_column($records, 'first_name');
// $first_names is ['John', 'Sally']
```

#### `array_diff()`
計算陣列的差集 (回傳在第一個陣列中，但不在其他陣列中的值)。
```php
$array1 = ["a", "b", "c"];
$array2 = ["b", "c", "d"];
$diff = array_diff($array1, $array2);
// $diff is ["a"]
```

#### `array_filter()`
使用回呼函式過濾陣列中的元素。
```php
$numbers = [1, 2, 3, 4, 5, 6];
$even = array_filter($numbers, fn($n) => $n % 2 == 0);
// $even is [2, 4, 6]
```

#### `array_flip()`
交換陣列中的鍵 (key) 與值 (value)。
```php
$input = ['a' => 1, 'b' => 2, 'c' => 3];
$flipped = array_flip($input);
// $flipped is [1 => 'a', 2 => 'b', 3 => 'c']
```

#### `array_intersect()`
計算陣列的交集。
```php
$array1 = ["a", "b", "c"];
$array2 = ["b", "c", "d"];
$intersect = array_intersect($array1, $array2);
// $intersect is ["b", "c"]
```

#### `array_keys()` / `array_values()`
回傳陣列所有的鍵或所有的值。
```php
$array = ['color' => 'blue', 'size' => 'medium'];
$keys = array_keys($array); // ['color', 'size']
$values = array_values($array); // ['blue', 'medium']
```

#### `array_map()`
將回呼函式作用到每個陣列元素上。
```php
$numbers = [1, 2, 3];
$squares = array_map(fn($n) => $n * $n, $numbers);
// $squares is [1, 4, 9]
```

#### `array_merge()`
合併一個或多個陣列。
```php
$array1 = ['a', 'b'];
$array2 = ['c', 'd'];
$merged = array_merge($array1, $array2);
// $merged is ['a', 'b', 'c', 'd']
```

#### `array_shift()` / `array_unshift()`
從陣列開頭移出 (shift) 或加入 (unshift) 元素。
```php
$stack = ['a', 'b', 'c'];
$first = array_shift($stack); // $first is 'a', $stack is ['b', 'c']
array_unshift($stack, 'z'); // $stack is ['z', 'b', 'c']
```

#### `array_pop()` / `array_push()`
從陣列結尾移出 (pop) 或加入 (push) 元素。
```php
$stack = ['a', 'b', 'c'];
$last = array_pop($stack); // $last is 'c', $stack is ['a', 'b']
array_push($stack, 'z'); // $stack is ['a', 'b', 'z']
```

#### `array_sum()`
計算陣列中所有值的總和。
```php
$numbers = [10, 20, 30];
$sum = array_sum($numbers); // $sum is 60
```

#### `in_array()`
檢查值是否存在於陣列中。
```php
$haystack = ['apple', 'banana'];
if (in_array('apple', $haystack)) {
    echo "Found apple!";
}
```

#### `count()`
計算陣列中的元素數量。
```php
$items = [1, 2, 3];
echo count($items); // 3
```

#### `array_reverse()`
回傳一個元素順序相反的陣列。
```php
$input = ['a', 'b', 'c', 1, 2, 3];
$reversed = array_reverse($input);
// $reversed is [3, 2, 1, 'c', 'b', 'a']
```

#### `array_unique()`
移除陣列中重複的值，並回傳過濾後的新陣列。
```php
$input = ['a', 'b', 'a', 'c', 'b'];
$unique = array_unique($input);
// $unique is [0 => 'a', 1 => 'b', 3 => 'c'] (keys are preserved)
```

#### `array_reduce()`
使用回呼函式將陣列逐步累積為單一值。
```php
$numbers = [1, 2, 3, 4, 5];

$sum = array_reduce($numbers, fn($carry, $item) => $carry + $item, 0);
// 15

$product = array_reduce($numbers, fn($carry, $item) => $carry * $item, 1);
// 120

// 將陣列轉成關聯陣列
$users = [['id' => 1, 'name' => 'Alice'], ['id' => 2, 'name' => 'Bob']];
$byId = array_reduce($users, function ($carry, $user) {
    $carry[$user['id']] = $user['name'];
    return $carry;
}, []);
// [1 => 'Alice', 2 => 'Bob']
```

#### `array_walk()`
對陣列每個元素套用回呼函式，**直接修改原陣列**（與 `array_map` 不同，不回傳新陣列）。
```php
$prices = ['apple' => 1.5, 'banana' => 0.8, 'cherry' => 3.0];

// $key 是選填參數
array_walk($prices, function (&$price, $key) {
    $price = '$' . number_format($price, 2);
});
// $prices = ['apple' => '$1.50', 'banana' => '$0.80', 'cherry' => '$3.00']

// 傳入額外參數
array_walk($prices, fn(&$v, $k, $prefix) => $v = $prefix . $v, 'Price: ');
```

#### `array_splice()`
從陣列中移除一段元素，並可選擇性地插入新元素。
```php
$arr = ['a', 'b', 'c', 'd', 'e'];

// 從 index 1 移除 2 個元素
$removed = array_splice($arr, 1, 2);
// $arr = ['a', 'd', 'e'], $removed = ['b', 'c']

// 移除並插入
$arr = ['a', 'b', 'c', 'd'];
array_splice($arr, 1, 2, ['x', 'y', 'z']);
// $arr = ['a', 'x', 'y', 'z', 'd']
```

## 陣列排序函式

#### `sort()` / `rsort()`
升冪 / 降冪排序，**重新索引**鍵值。
```php
$a = [3, 1, 4, 1, 5];
sort($a);  // [1, 1, 3, 4, 5]
rsort($a); // [5, 4, 3, 1, 1]
```

#### `asort()` / `arsort()`
升冪 / 降冪排序，**保留**原有鍵值對應。
```php
$a = ['b' => 3, 'a' => 1, 'c' => 2];
asort($a);  // ['a'=>1, 'c'=>2, 'b'=>3]
arsort($a); // ['b'=>3, 'c'=>2, 'a'=>1]
```

#### `ksort()` / `krsort()`
依**鍵**升冪 / 降冪排序。
```php
$a = ['c' => 3, 'a' => 1, 'b' => 2];
ksort($a);  // ['a'=>1, 'b'=>2, 'c'=>3]
```

#### `usort()`
以自訂回呼函式排序（重新索引）。
```php
$users = [
    ['name' => 'Charlie', 'age' => 30],
    ['name' => 'Alice',   'age' => 25],
    ['name' => 'Bob',     'age' => 28],
];

usort($users, fn($a, $b) => $a['age'] <=> $b['age']);
// 依 age 升冪：Alice, Bob, Charlie
```

#### `uasort()` / `uksort()`
自訂排序並**保留鍵**（`uasort`）、依**鍵**自訂排序（`uksort`）。

#### `array_multisort()`
同時對多個陣列或多欄位排序。
```php
$names = ['Charlie', 'Alice', 'Bob'];
$ages  = [30, 25, 28];

array_multisort($ages, SORT_ASC, $names);
// $ages:  [25, 28, 30]
// $names: ['Alice', 'Bob', 'Charlie']
```

## 數學函式

#### 常用數學函式
```php
abs(-5);          // 5（絕對值）
ceil(4.1);        // 5（無條件進位）
floor(4.9);       // 4（無條件捨去）
round(4.5);       // 5（四捨五入）
round(4.567, 2);  // 4.57（保留兩位小數）

max(1, 2, 3);     // 3
min(1, 2, 3);     // 1
max([1, 2, 3]);   // 3（也接受陣列）

pow(2, 10);       // 1024（次方）
sqrt(16);         // 4.0（平方根）
log(M_E);         // 1.0（自然對數）
log(100, 10);     // 2.0（log₁₀(100)）

fmod(10, 3);      // 1.0（浮點數取餘）
intdiv(10, 3);    // 3（整數除法，PHP 7+）
```

#### 隨機數
```php
rand(1, 100);          // 1~100 隨機整數（不適合加密用途）
mt_rand(1, 100);       // 使用 Mersenne Twister，比 rand() 快且更均勻
random_int(1, 100);    // 密碼學安全的隨機整數（PHP 7+）
random_bytes(16);      // 16 bytes 密碼學安全隨機二進位字串
```

#### 進位轉換
```php
base_convert('ff', 16, 10); // '255'（十六進位轉十進位）
decbin(255);   // '11111111'（十進位轉二進位字串）
decoct(8);     // '10'
dechex(255);   // 'ff'
bindec('1010'); // 10（二進位字串轉十進位）
```

#### 數學常數
```php
M_PI;    // 3.14159265...
M_E;     // 2.71828182...
M_SQRT2; // 1.41421356...
INF;     // 無限大
NAN;     // 非數值

is_infinite(INF); // true
is_nan(NAN);      // true
is_finite(1.0);   // true
```

## 類別與物件 (Class & Object) 相關函式

#### `method_exists()`
檢查物件或類別中是否存在指定的方法。
```php
class MyClass { public function myMethod() {} }
$obj = new MyClass();
if (method_exists($obj, 'myMethod')) {
    echo "Method exists.";
}
```

#### `property_exists()`
檢查物件或類別中是否存在指定的屬性。
```php
class MyClass { public $myProp; } 
$obj = new MyClass();
if (property_exists($obj, 'myProp')) {
    echo "Property exists.";
}
```

#### `get_class()`
回傳物件的類別名稱。
```php
$obj = new MyClass();
echo get_class($obj); // "MyClass"
```

#### `get_object_vars()`
回傳由物件屬性組成的關聯陣列。
```php
$obj = new MyClass();
$obj->myProp = 'value';
$vars = get_object_vars($obj);
// $vars is ['myProp' => 'value']
```

## 字串 (String) 相關函式

#### `strlen()`
回傳字串的長度（位元組數，非字元數）。
```php
strlen('Hello'); // 5
strlen('你好');   // 6（UTF-8 每個中文字 3 bytes）
```

#### `mb_strlen()`
以字元為單位計算字串長度，正確處理多位元組字元。
```php
mb_strlen('你好', 'UTF-8'); // 2
```

#### `strpos()` / `strrpos()`
尋找子字串第一次（或最後一次）出現的位置，找不到回傳 `false`。
```php
strpos('Hello World', 'World');  // 6
strrpos('Hello World Hello', 'Hello'); // 12
```

#### `str_contains()` / `str_starts_with()` / `str_ends_with()`
PHP 8.0+，語意更清晰的字串搜尋函式。
```php
str_contains('Hello World', 'World');    // true
str_starts_with('Hello World', 'Hello'); // true
str_ends_with('Hello World', 'World');   // true
```

#### `substr()`
回傳字串的一部分。
```php
substr('Hello World', 6);     // 'World'
substr('Hello World', 6, 3);  // 'Wor'
substr('Hello World', -5);    // 'World'
```

#### `str_replace()`
搜尋並取代字串中的內容。
```php
str_replace('World', 'PHP', 'Hello World'); // 'Hello PHP'

// 也支援陣列
str_replace(['a', 'e', 'i'], '*', 'Hello Alice'); // 'H*llo *l*c*'
```

#### `str_pad()`
將字串填充到指定長度。
```php
str_pad('5', 3, '0', STR_PAD_LEFT);  // '005'
str_pad('Hi', 10, '-', STR_PAD_BOTH); // '----Hi----'
```

#### `trim()` / `ltrim()` / `rtrim()`
移除字串兩端（或單端）的空白或指定字元。
```php
trim('  Hello  ');      // 'Hello'
ltrim('  Hello  ');     // 'Hello  '
rtrim('  Hello  ');     // '  Hello'
trim('--Hello--', '-'); // 'Hello'
```

#### `strtolower()` / `strtoupper()`
轉換為全小寫或全大寫。
```php
strtolower('Hello World'); // 'hello world'
strtoupper('Hello World'); // 'HELLO WORLD'
```

#### `ucfirst()` / `ucwords()`
首字母大寫；每個單字的首字母大寫。
```php
ucfirst('hello world'); // 'Hello world'
ucwords('hello world'); // 'Hello World'
```

#### `explode()` / `implode()`
以分隔符號分割字串為陣列、或將陣列合併為字串。
```php
$parts = explode(',', 'a,b,c'); // ['a', 'b', 'c']
$str   = implode('-', $parts);  // 'a-b-c'
```

#### `sprintf()`
將格式化的字串輸出（不直接 echo）。
```php
$msg = sprintf('Hello, %s! You are %d years old.', 'Alice', 30);
// 'Hello, Alice! You are 30 years old.'

$price = sprintf('%.2f', 3.14159); // '3.14'
```

#### `preg_match()` / `preg_replace()`
正規表達式比對與取代。
```php
preg_match('/\d+/', 'Order 42', $matches);
echo $matches[0]; // '42'

preg_replace('/\s+/', '-', 'Hello World Test'); // 'Hello-World-Test'
```

#### `number_format()`
格式化數字（加千位分隔符）。
```php
number_format(1234567.891, 2, '.', ','); // '1,234,567.89'
```

## 魔術常數 (Magic Constants)

它們的值會隨著它們被使用的位置而改變。

- `__LINE__`: 檔案中的目前行號。
- `__FILE__`: 檔案的完整路徑和檔名。
- `__DIR__`: 檔案所在的目錄。
- `__FUNCTION__`: 函式名稱。
- `__CLASS__`: 類別名稱。
- `__METHOD__`: 類別的方法名稱。
- `__NAMESPACE__`: 目前的命名空間名稱。

---

# Generator（生成器）
`yield` 讓函式變成 Generator，每次呼叫 `current()` / `next()` 時才執行至下一個 `yield`，不會一次載入全部資料。

## 基本用法
```php
function fibonacci(): Generator {
    [$a, $b] = [0, 1];
    while (true) {
        yield $a;
        [$a, $b] = [$b, $a + $b];
    }
}

$gen = fibonacci();
for ($i = 0; $i < 8; $i++) {
    echo $gen->current() . ' '; // 0 1 1 2 3 5 8 13
    $gen->next();
}
```

## yield 鍵值對
```php
function indexedItems(): Generator {
    yield 'first'  => 'apple';
    yield 'second' => 'banana';
}

foreach (indexedItems() as $key => $value) {
    echo "$key: $value\n";
}
```

## 向 Generator 傳值（`send()`）
```php
function logger(): Generator {
    while (true) {
        $msg = yield;
        echo '[LOG] ' . $msg . "\n";
    }
}

$log = logger();
$log->current();        // 啟動 Generator
$log->send('App started');  // [LOG] App started
$log->send('User login');   // [LOG] User login
```

## `yield from`（委派）
```php
function inner(): Generator {
    yield 1;
    yield 2;
    return 'inner done'; // Generator 的回傳值
}

function outer(): Generator {
    $result = yield from inner(); // 取得 inner 的 return 值
    echo $result; // 'inner done'
    yield 3;
}

foreach (outer() as $v) {
    echo $v . ' '; // 1 2 3
}
```

---

# Closure（閉包）進階

## 捕捉外部變數（`use`）
```php
$multiplier = 3;

$fn = function (int $n) use ($multiplier): int {
    return $n * $multiplier;
};

echo $fn(5); // 15

// 以傳參考方式捕捉，閉包內修改會影響外部
$count = 0;
$increment = function () use (&$count): void {
    $count++;
};
$increment();
echo $count; // 1
```

## 箭頭函式自動捕捉（PHP 7.4+）
箭頭函式（`fn`）自動以**傳值**方式捕捉外部變數，無需 `use`。
```php
$factor = 10;
$fn = fn($n) => $n * $factor; // 自動捕捉 $factor
echo $fn(3); // 30
```

## `Closure::bind()` / `bindTo()`
將閉包綁定到指定物件，使其可存取該物件的 `private`/`protected` 成員。
```php
class Counter {
    private int $count = 0;
}

$increment = Closure::bind(
    function (int $by) { $this->count += $by; },
    new Counter(),
    Counter::class
);
$increment(5);

// bindTo() 是實例方法版本
$getCount = function () { return $this->count; };
$bound = $getCount->bindTo(new Counter(), Counter::class);
echo $bound(); // 0
```

## `Closure::call()` （PHP 7.0+）
一步完成綁定並呼叫，比 `bind()` 更簡潔。
```php
class Foo {
    private string $name = 'Foo';
}

$getName = function () { return $this->name; };
echo $getName->call(new Foo()); // 'Foo'
```

## 靜態閉包（`static function`）
靜態閉包無法綁定 `$this`，可避免意外持有物件引用。
```php
$fn = static function (int $n): int {
    return $n * 2;
};
```

---

# 日期與時間 (DateTime)

## 建立
```php
$now  = new DateTimeImmutable();               // 現在
$dt   = new DateTimeImmutable('2025-01-15 10:30:00');
$dt   = new DateTimeImmutable('now', new DateTimeZone('Asia/Taipei'));

// 從格式字串解析
$dt   = DateTimeImmutable::createFromFormat('Y/m/d', '2025/01/15');
```

## 格式化（`format()`）
```php
$dt = new DateTimeImmutable('2025-01-15 10:30:00');

$dt->format('Y-m-d');            // '2025-01-15'
$dt->format('Y-m-d H:i:s');     // '2025-01-15 10:30:00'
$dt->format('D, d M Y');        // 'Wed, 15 Jan 2025'
$dt->format('U');                // Unix timestamp
```

常用格式字元：

| 字元 | 意義 | 範例 |
|------|------|------|
| `Y` | 四位年 | 2025 |
| `m` | 兩位月 | 01–12 |
| `d` | 兩位日 | 01–31 |
| `H` | 24h 時 | 00–23 |
| `i` | 分 | 00–59 |
| `s` | 秒 | 00–59 |
| `N` | 星期（1=週一） | 1–7 |
| `U` | Unix timestamp | 1736936400 |

## 加減時間（`modify()` / `add()` / `sub()`）
`DateTimeImmutable` 回傳新物件，`DateTime` 修改自身。
```php
$dt = new DateTimeImmutable('2025-01-15');

$dt->modify('+7 days');           // 2025-01-22
$dt->modify('next Monday');       // 下個星期一
$dt->add(new DateInterval('P1Y2M3D')); // +1年2月3天
$dt->sub(new DateInterval('PT2H'));    // -2小時
```

## 比較
```php
$a = new DateTimeImmutable('2025-01-01');
$b = new DateTimeImmutable('2025-06-01');

$a < $b;  // true
$a == $b; // false

$diff = $a->diff($b);
echo $diff->days;   // 151
echo $diff->months; // 5
```

## Unix Timestamp 互轉
```php
$ts = time();                          // 目前 Unix timestamp
$dt = new DateTimeImmutable('@' . $ts); // 從 timestamp 建立
$ts = $dt->getTimestamp();             // 取回 timestamp
```

---

# 命名空間 (Namespaces)
命名空間用來組織程式碼，避免不同套件之間的類別、函式、常數名稱衝突，類似於資料夾的概念。

## 宣告命名空間
```php
<?php
// 必須是檔案的第一個有效陳述式
namespace App\Models;

class User {
    // ...
}
```

## 使用命名空間（`use`）
```php
<?php
namespace App\Controllers;

use App\Models\User;           // 引入類別
use App\Services\UserService as Service; // 引入並重新命名（別名）

class UserController {
    public function index(): void {
        $user = new User();
        $service = new Service();
    }
}
```

## 群組引入
```php
use App\Models\{User, Post, Comment};
use function App\Helpers\{formatDate, formatPrice};
use const App\Config\{VERSION, DEBUG};
```

## 全域命名空間
在命名空間內存取全域（PHP 內建）的類別或函式，需加上 `\` 前綴。
```php
namespace App;

// 呼叫全域函式
$len = \strlen('hello');

// 實例化全域類別
$dt = new \DateTime();

// 捕捉全域例外
try {
    // ...
} catch (\Exception $e) {}
```

## `__NAMESPACE__` 與 `namespace` 關鍵字
```php
namespace App\Models;

echo __NAMESPACE__; // 'App\Models'

// 動態建立完整類別名稱
$class = namespace\User::class; // 'App\Models\User'
```

---

# PHP 版本新功能

# PHP 7.0
## Scalar Type Declarations
```php
function addNumbers(int $a, int $b): int {
    return $a + $b;
}
```

## Return Type Declarations
```php
function getName(): string {
    return 'John Doe';
}
```

## Null Coalesce Operator (`??`)
```php
$name = $_GET['name'] ?? 'Guest';
```

## Spaceship Operator (`<=>`)
```php
$result = 1 <=> 2; // 返回 -1
$result = 2 <=> 2; // 返回 0
$result = 3 <=> 2; // 返回 1
```

## Anonymous Classes
```php
$logger = new class implements Logger {
    public function log(string $msg) {
        echo $msg;
    }
};
```

## Strict Types
```php
declare(strict_types=1);

function addNumbers(int $a, int $b): int {
    return $a + $b;
}
addNumbers(1, '2'); // TypeError：strict 模式下不允許型別強制轉換
```

## Group `use` Declarations
```php
// 之前
use App\Controllers\HomeController;
use App\Controllers\UserController;

// 之後
use App\Controllers\{HomeController, UserController};
```

## `Closure::call()`
將閉包綁定到物件並立即呼叫，比 `bindTo()` 更簡潔。
```php
class Foo {
    private $value = 42;
}

$fn = function() { return $this->value; };

echo $fn->call(new Foo()); // 42
```

## Generator Delegation (`yield from`)
允許 Generator 委派給另一個 Generator、陣列或 `Traversable`。
```php
function innerGenerator() {
    yield 1;
    yield 2;
}

function outerGenerator() {
    yield 0;
    yield from innerGenerator();
    yield 3;
}

foreach (outerGenerator() as $v) {
    echo $v; // 0, 1, 2, 3
}
```

# PHP 7.1
## Nullable Types
```php
function setAge(?int $age): void {
    // $age 可以是 int 或 null
}
```

## Void Return Type
```php
function sayHello(): void {
    echo "Hello";
}
```

## Class Constant Visibility
```php
class MyClass {
    private const PRIVATE_CONST = 'private';
    public const PUBLIC_CONST = 'public';
}
```

## Multi-catch Exception Handling
```php
try {
    // ...
} catch (FirstException | SecondException $e) {
    // ...
}
```

## Symmetric Array Destructuring
```php
// 使用 [] 取代 list()
$data = [[1, 'Tom'], [2, 'Alice']];

[[$id1, $name1], [$id2, $name2]] = $data;

// 搭配 foreach
foreach ($data as [$id, $name]) {
    echo "$id: $name";
}
```

## `iterable` Pseudo-Type
陣列或實現 `Traversable` 的物件都可作為 `iterable`。
```php
function processItems(iterable $items): void {
    foreach ($items as $item) {
        // ...
    }
}

processItems([1, 2, 3]);                  // 陣列
processItems(new ArrayIterator([1, 2])); // 物件
```

# PHP 7.2
## Object Type Hinting
```php
function process(object $obj): void {
    // ...
}
```

## Abstract Method Override
子類別覆寫 Trait 中的抽象方法時，簽名規則放寬，允許更改參數名稱與型別（相容性擴展）。

# PHP 7.3
## `JSON_THROW_ON_ERROR`
`json_decode` 和 `json_encode` 在出錯時可以拋出 `JsonException`。
```php
try {
    json_decode("{}", false, 512, JSON_THROW_ON_ERROR);
} catch (\JsonException $e) {
    echo $e->getMessage(); // "Syntax error"
}
```

## Trailing Comma in Function Calls
```php
foo(1, 2, 3,); // 允許尾隨逗號
```

## `array_key_first()` / `array_key_last()`
取得陣列第一個或最後一個鍵，不影響陣列內部指標。
```php
$arr = ['a' => 1, 'b' => 2, 'c' => 3];

array_key_first($arr); // 'a'
array_key_last($arr);  // 'c'
```

## Flexible Heredoc / Nowdoc Syntax
結束標記可縮排，縮排量會從每行內容中移除。
```php
$sql = <<<SQL
    SELECT *
    FROM users
    WHERE id = 1
    SQL; // 結束標記可縮排，不需對齊左邊界
```

## `is_countable()`
檢查變數是否可傳入 `count()`（陣列或實現 `Countable` 的物件）。
```php
$items = [1, 2, 3];

if (is_countable($items)) {
    echo count($items); // 3
}
```

# PHP 7.4
## Typed Properties
```php
class User {
    public int $id;
    public string $name;
}
```

## Arrow Functions
```php
$numbers = [1, 2, 3];
$squares = array_map(fn($n) => $n ** 2, $numbers);
```

## Null Coalescing Assignment Operator (`??=`)
```php
$data['key'] ??= 'default';
```

## Spread Operator in Array Expression
```php
$array1 = [1, 2];
$combined = [...$array1, 3, 4];
```

## Preloading
在 `php.ini` 中設定 `opcache.preload`，可於伺服器啟動時預先載入常用類別到記憶體，減少每次請求的解析開銷。
```ini
opcache.preload=/var/www/preload.php
opcache.preload_user=www-data
```

## `WeakReference`
對物件持有弱引用，不阻止垃圾回收，適用於快取場景。
```php
$obj = new stdClass();
$ref = WeakReference::create($obj);

$ref->get(); // stdClass 物件
unset($obj);
$ref->get(); // null（物件已被 GC 回收）
```

## Covariant / Contravariant Types
**Covariant**（共變）：子類別覆寫方法時，回傳型別可以更具體。  
**Contravariant**（逆變）：子類別覆寫方法時，參數型別可以更寬泛。
```php
class Animal {}
class Dog extends Animal {}

interface Creator {
    public function create(): Animal;
}

// Covariant return type：回傳更具體的子型別
class DogCreator implements Creator {
    public function create(): Dog { // OK
        return new Dog();
    }
}

interface Consumer {
    public function consume(Dog $dog): void;
}

// Contravariant parameter：接受更寬泛的父型別
class AnimalConsumer implements Consumer {
    public function consume(Animal $animal): void {} // OK
}
```

# PHP 8.0
## JIT (Just-In-Time) Compiler
JIT 編譯器被引入以提升 PHP 在 CPU 密集型工作負載下的效能，但對於典型的 Web 應用，效能提升可能不明顯。

## Union Types
```php
function process(int|string $value): void {
    // ...
}
```

## Named Arguments
```php
htmlspecialchars($string, double_encode: false);
```

## Constructor Property Promotion
```php
class Point {
    public function __construct(
        public float $x = 0.0,
        public float $y = 0.0,
    ) {}
}
```

## `match` Expression
```php
$message = match ($statusCode) {
    200, 300 => 'OK',
    404 => 'Not Found',
    default => 'Unknown status',
};
```

## Nullsafe Operator (`?->`)
```php
$country = $session?->user?->getAddress()?->country;
```

## Attributes
提供原生的元資料（metadata）機制，取代 PHPDoc 註解。
```php
#[Attribute]
class Route {
    public function __construct(public string $path) {}
}

#[Route('/home')]
class HomeController {}

// 透過反射讀取
$ref = new ReflectionClass(HomeController::class);
$attrs = $ref->getAttributes(Route::class);
echo $attrs[0]->newInstance()->path; // '/home'
```

## New String Functions
```php
str_contains('Hello World', 'World');  // true
str_starts_with('Hello World', 'Hello'); // true
str_ends_with('Hello World', 'World');   // true
```

## `throw` as Expression
`throw` 可用於箭頭函式、三元運算子等表達式中。
```php
$value = $input ?? throw new InvalidArgumentException('Input required');

$name = fn() => throw new Exception('Not implemented');
```

## `mixed` Type
```php
function debug(mixed $value): void {
    var_dump($value); // 接受任意型別
}
```

## `$object::class`
可在物件實例上直接使用 `::class` 取得實際類別名稱，等同於 `get_class($obj)`。
```php
$user = new User();
echo $user::class; // "App\Models\User"

// 亦支援 nullsafe 使用情境
echo $obj?->getUser()::class;
```

## `Stringable` Interface
任何實作 `__toString()` 的類別會自動隱含實現 `Stringable` 介面，可用於型別宣告。
```php
function render(string|Stringable $content): string {
    return (string) $content;
}

class HtmlElement {
    public function __toString(): string {
        return '<div>Hello</div>';
    }
}

render(new HtmlElement()); // OK，自動視為 Stringable
```

## `WeakMap`
類似 `WeakReference`，但以物件為鍵的 Map。物件被 GC 回收後，對應的條目自動移除，適合快取附加在物件上的計算結果。
```php
$map = new WeakMap();
$obj = new stdClass();

$map[$obj] = 'some cached value';
echo count($map); // 1

unset($obj);
echo count($map); // 0（物件回收後自動清除）
```

# PHP 8.1
## Enumerations (Enums)
```php
enum Status {
    case Pending;
    case Approved;
}
```

## Backed Enums
Enum 的每個 case 可以附帶一個 `int` 或 `string` 值，支援從值還原（`from()` / `tryFrom()`）。
```php
enum Color: string {
    case Red   = 'red';
    case Green = 'green';
    case Blue  = 'blue';
}

$color = Color::from('red');    // Color::Red
$color = Color::tryFrom('xxx'); // null（不拋出例外）

echo Color::Red->value; // 'red'
```

## Enum Methods & Interfaces
Enum 可以實現介面並定義方法。
```php
interface HasLabel {
    public function label(): string;
}

enum Status: int implements HasLabel {
    case Active   = 1;
    case Inactive = 0;

    public function label(): string {
        return match($this) {
            Status::Active   => '啟用',
            Status::Inactive => '停用',
        };
    }
}

echo Status::Active->label(); // '啟用'
```

## `Enum::cases()`
回傳所有 case 的陣列，常用於生成下拉選單或連同 `array_column` 一起使用。
```php
enum Status: string {
    case Active   = 'active';
    case Inactive = 'inactive';
    case Pending  = 'pending';
}

// 取得所有 case
Status::cases();
// [Status::Active, Status::Inactive, Status::Pending]

// 建立選項陣列（用於表單下拉選單）
$options = array_column(
    array_map(fn($c) => ['value' => $c->value, 'label' => $c->name], Status::cases()),
    null
);
// [['value'=>'active','label'=>'Active'], ...]
```

## Readonly Properties
```php
class User {
    public readonly string $name;
    public function __construct(string $name) {
        $this->name = $name;
    }
}
```

## First-Class Callable Syntax
```php
$callback = $this->myMethod(...);
```

## Fibers
為 PHP 帶來了輕量級的併發能力 (協程)。

## Intersection Types
```php
function process(Printable&Cacheable $obj): void {
    // $obj 必須同時實現 Printable 和 Cacheable 介面
}
```

## `never` Return Type
宣告函式永遠不會正常回傳（必定拋出例外或終止程式）。
```php
function redirect(string $url): never {
    header("Location: $url");
    exit();
}
```

## `new` in Initializers
可在參數預設值、屬性預設值等初始化位置直接使用 `new`。
```php
class UserService {
    public function __construct(
        private Logger $logger = new NullLogger(),
    ) {}
}

#[Route(new Path('/home'))]
class HomeController {}
```

## `array_is_list()`
檢查陣列是否為索引從 0 開始、連續且無間隙的純列表。
```php
array_is_list([1, 2, 3]);          // true
array_is_list(['a' => 1, 'b' => 2]); // false
array_is_list([0 => 'a', 1 => 'b']); // true
array_is_list([1 => 'a', 0 => 'b']); // false（順序錯誤）
```

# PHP 8.2
## Read-Only Classes
```php
readonly class UserData {
    public string $name;
    public int $age;
}
```

## `null`, `true`, `false` as Standalone Types
```php
function alwaysFalse(): false {
    return false;
}
```

## Disjunctive Normal Form (DNF) Types
```php
function process((CanRead&CanWrite)|null $file): void {
    // ...
}
```

## Dynamic Properties Deprecated
直接為物件設定未宣告的屬性已被棄用，以減少錯誤。若要允許動態屬性，可以在類別前加上 `#[AllowDynamicProperties]` 屬性。

## `\Random\Randomizer`
全新的 `\Random` 擴展，提供物件導向的隨機數 API，支援可替換的隨機引擎（Engine），更易於測試與複現。
```php
$randomizer = new \Random\Randomizer();

$randomizer->getInt(1, 100);       // 1~100 隨機整數
$randomizer->shuffleArray([1, 2, 3, 4]); // 隨機排列陣列
$randomizer->getBytes(16);         // 16 bytes 隨機二進位字串

// 使用固定種子引擎（可重現結果，適合測試）
$seeded = new \Random\Randomizer(
    new \Random\Engine\Mt19937(seed: 42)
);
$seeded->getInt(1, 100); // 每次相同結果
```

## Constants in Traits
Trait 現在支援定義常數。
```php
trait HasVersion {
    public const VERSION = '1.0';
}

class App {
    use HasVersion;
}

echo App::VERSION; // 1.0
```

## `#[SensitiveParameter]`
標記敏感參數，使其在例外的 stack trace 中以 `<redacted>` 顯示，避免密碼等敏感資訊外洩。
```php
function login(
    string $user,
    #[\SensitiveParameter] string $password
): void {
    throw new Exception('Auth failed');
}
// stack trace 中 $password 會顯示 SensitiveParameterValue，不會洩漏明文
```

# PHP 8.3
## Typed Class Constants
```php
class MyClass {
    public const string VERSION = '1.0';
}
```

## `json_validate()`
提供一個比 `json_decode` 更高效的方式來驗證一個字串是否為有效的 JSON。
```php
if (json_validate($jsonString)) {
    // ...
}
```

## Dynamic class constant and Enum member fetch
```php
class MyClass {
    public const MY_CONST = 42;
}

$constName = 'MY_CONST';
echo MyClass::{$constName}; // 42
```

## `#[Override]`
標記方法意圖覆寫父類別方法，若父類別中沒有對應方法則在靜態分析時報錯，避免因拼字錯誤導致覆寫失效。
```php
class ParentClass {
    public function doSomething(): void {}
}

class ChildClass extends ParentClass {
    #[Override]
    public function doSomething(): void {} // OK

    #[Override]
    public function doSomethig(): void {} // 靜態分析錯誤：父類別無此方法
}
```

## `mb_str_pad()`
多位元組字串版本的 `str_pad()`，正確處理中文等多位元組字元的填充。
```php
mb_str_pad('你好', 6, ' ');  // '你好    '（以字元數計算，非位元組數）
str_pad('你好', 6, ' ');     // 可能因編碼問題結果不正確
```

## Granular `DateTime` Exceptions
日期時間相關函式現在會拋出具體的例外型別，而非通用的 `Exception` 或返回 `false`。
```php
try {
    new DateTimeImmutable('invalid date');
} catch (DateMalformedStringException $e) {
    echo $e->getMessage();
}
```

# PHP 8.4
## Property Hooks
允許在屬性上直接定義 `get` / `set` 存取邏輯，取代繁瑣的 getter/setter 方法。
```php
class User {
    public string $name {
        get => strtoupper($this->name);
        set => trim($value);
    }
}
```

## Asymmetric Visibility
支援對屬性的讀取與寫入設定不同的存取權限。
```php
class Post {
    public private(set) int $views = 0;

    public function incrementViews(): void {
        $this->views++; // 類別內部可寫入
    }
}

$post = new Post();
echo $post->views; // 外部可讀取
// $post->views = 10; // 錯誤：外部無法寫入
```

## `#[\Deprecated]` Attribute
可在原生 PHP 程式碼中標記函式、方法或常數為已棄用，觸發與內建棄用相同的警告。
```php
#[\Deprecated('Use newMethod() instead', since: '2.0')]
function oldMethod(): void {}
```

## New Array Functions
新增四個陣列搜尋函式，無需自行撰寫迴圈。
```php
$nums = [1, 2, 3, 4, 5];

array_find($nums, fn($n) => $n > 3);        // 4 (第一個符合的值)
array_find_key($nums, fn($n) => $n > 3);    // 3 (第一個符合的鍵)
array_any($nums, fn($n) => $n > 4);         // true
array_all($nums, fn($n) => $n > 0);         // true
```

## `new` Without Parentheses in Expressions
在運算式中使用 `new` 實例化物件時，不再需要額外加括號即可鏈式呼叫。
```php
// PHP 8.4 之前需要寫成 (new Request())->getPath()
$path = new Request()->getPath();
```

## Lazy Objects
透過 `ReflectionClass` 建立惰性物件，僅在首次存取屬性或方法時才初始化，適合用於 DI 容器。
```php
$reflector = new ReflectionClass(MyService::class);
$lazyObject = $reflector->newLazyGhost(
    function (MyService $obj): void {
        $obj->__construct(/* 昂貴的初始化 */);
    }
);
```

## BCMath Object API (`\BcMath\Number`)
提供以物件導向方式操作任意精度數值，支援運算子多載。
```php
$a = new \BcMath\Number('10.5');
$b = new \BcMath\Number('3.2');
$result = $a + $b; // \BcMath\Number('13.7')
echo $result;      // 13.7
```

# PHP 8.5
## Pipe Operator (`|>`)
管線運算子讓函式的鏈式呼叫更具可讀性，將左側的值作為右側 callable 的第一個引數傳入。
```php
$result = 'hello world'
    |> strtoupper(...)
    |> trim(...)
    |> fn($s) => $s . '!';
// 'HELLO WORLD!'
```

## `array_first()` / `array_last()`
取得陣列第一個或最後一個元素，比 `reset()` / `end()` 更語意明確且不影響陣列內部指標。
```php
$items = [3, 1, 4, 1, 5];

array_first($items); // 3
array_last($items);  // 5
```

## `#[NoDiscard]` Attribute
標記函式或方法的回傳值不應被忽略，若呼叫端未使用回傳值則發出警告。
```php
#[\NoDiscard('Return value contains the processed result')]
function processData(array $data): array {
    return array_map(fn($x) => $x * 2, $data);
}

processData([1, 2, 3]); // 警告：回傳值被丟棄
```

## `ReflectionConstant`
新增 `ReflectionConstant` 類別，讓全域常數也能透過反射 API 進行內省。
```php
define('APP_VERSION', '1.0.0');

$ref = new ReflectionConstant('APP_VERSION');
echo $ref->getName();  // APP_VERSION
echo $ref->getValue(); // 1.0.0
```

## `bcdivmod()`
一次回傳 BCMath 整數除法的商與餘數，避免重複計算。
```php
[$quotient, $remainder] = bcdivmod('17', '5'); // ['3', '2']
```
