# Swift Tour

https://docs.swift.org/swift-book/GuidedTour/GuidedTour.html

## バージョン

swift 5.1 - Xcode 11に対応

## 宿題範囲

### 必須

```
for / where
Closure
enum構文 / switch-case 文 / where 句
Optinal Binding / guard-let 文 / nil
```

### 余裕があれば

```
Tuple
extension (protocol)
computed property
```

## 本編

### 標準出力

```swift
print("Hello, world!")
// Prints "Hello, world!"
```

### 変数・定数

`let`で定数を、`var`で変数となる。一度宣言すればこれらのキーワードを再度使用する必要はない。

```swift
var myVariable = 42
myVariable = 50
let myConstant = 42
```

初期値が宣言されない、十分な値を持たない場合はコロンの後に型を宣言する。

```swift
let implicitInteger = 70
let implicitDouble = 70.0
let explicitDouble: Double = 70
```

型を変換する場合は明示的に宣言する。

```swift
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```

Pythonで言うフォーマット文

```swift
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit."
```

複数行

```swift
let quotation = """
I said "I have \(apples) apples."
And then I said "I have \(apples + oranges) pieces of fruit."
"""
```

配列・辞書型: 辞書型の末尾には`,`の入力が許されている

```swift
var shoppingList = ["catfish", "water", "tulips"]
shoppingList[1] = "bottle of water"

var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
]
occupations["Jayne"] = "Public Relations"
```

配列の追加・初期化

```swift
shoppingList.append("blue paint")
print(shoppingList)

let emptyArray = [String]()
let emptyDictionary = [String: Float]()
```

### 制御フロー

`if`文の条件はBoolean式にする。

```swift
let individualScores = [75, 43, 103, 87, 12]
var teamScore = 0
for score in individualScores {
    if score > 50 {
        teamScore += 3
    } else {
        teamScore += 1
    }
}
print(teamScore)
// Prints "11"
```

値があるか不明な変数に対して`if let`を使うことができる。optional値には何らかの値または`nil`を指定できる。型宣言の末尾に`?`を付与することによって、optional値とすることができる。

`if let`では、optional値が`nil`の場合、ブロック内の処理はスキップされる。

```swift
var optionalString: String? = "Hello"
print(optionalString == nil)
// Prints "false"

var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)"
}
```

`??`を使用してoptional値を制御する。下の場合、`nickName`に値が無い場合は`fullName`が適用される。

```swift
let nickName: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickName ?? fullName)"
```

switch文。`case`に複数条件を指定することができる。`let`と`where`の使い方も確認する。Javaのように各`case`に`break`を明示する必要はない。

```swift
let vegetable = "red pepper"
switch vegetable {
case "celery":
    print("Add some raisins and make ants on a log.")
case "cucumber", "watercress":
    print("That would make a good tea sandwich.")
case let x where x.hasSuffix("pepper"):
    print("Is it a spicy \(x)?")
default:
    print("Everything tastes good in soup.")
}
// Prints "Is it a spicy red pepper?"
```

`for - in`によるイテレーション処理。辞書型のKVに対しても利用可能。

```swift
let interestingNumbers = [
    "Prime": [2, 3, 5, 7, 11, 13],
    "Fibonacci": [1, 1, 2, 3, 5, 8],
    "Square": [1, 4, 9, 16, 25],
]
var largest = 0
for (kind, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
        }
    }
}
print(largest)
// Prints "25"
```

`while`はその書き方によって少なくとも1回は実行させることができる。

```swift
var n = 2
while n < 100 {
    n *= 2
}
print(n)
// Prints "128"

var m = 2
repeat {
    m *= 2
} while m < 100
print(m)
// Prints "128"
```

Pythonで言う`range(4)`と同様。ここで`<`を省略した場合は`4`を含むことになる。

```swift
var total = 0
for i in 0..<4 {
    total += i
}
print(total)
// Prints "6"
```

### 関数とクロージャ

引数には型を明示する。`->`の右にはreturnする型を宣言する。使用する場合もパラメータ名を書く。

```swift
func greet(person: String, day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet(person: "Bob", day: "Tuesday")
```

パラメータ名の左にラベル（エイリアスのようなもの）を指定すると、呼び出し時にはラベルを記載することになる。`_`をラベルにすると省略できる。

```swift
func greet(_ person: String, on day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet("John", on: "Wednesday")
```

タプルによって関数から複数の値を返すことができる。タプルの参照はパラメータ名でもインデックス順でも可能。

```swift
func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
    var min = scores[0]
    var max = scores[0]
    var sum = 0

    for score in scores {
        if score > max {
            max = score
        } else if score < min {
            min = score
        }
        sum += score
    }

    return (min, max, sum)
}
let statistics = calculateStatistics(scores: [5, 3, 100, 3, 9])
print(statistics.sum)
// Prints "120"
print(statistics.2)
// Prints "120"
```

関数は入れ子にすることができる。

```swift
func returnFifteen() -> Int {
    var y = 10
    func add() {
        y += 5
    }
    add()
    return y
}
returnFifteen()
```

関数は型としても扱うことができる。

```swift
func makeIncrementer() -> ((Int) -> Int) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer() // 関数を変数に格納する
increment(7) // 関数の実行
```

関数を引数として別の関数に渡すことができる。

```swift
func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
    for item in list {
        if condition(item) {
            return true
        }
    }
    return false
}
func lessThanTen(number: Int) -> Bool {
    return number < 10
}
var numbers = [20, 19, 7, 12]
hasAnyMatches(list: numbers, condition: lessThanTen)
```

クロージャ。あ意味わからん

```swift
numbers.map({ (number: Int) -> Int in
    let result = 3 * number
    return result
})
```

### オブジェクトとクラス

クラス宣言。変数や関数などは今までと同様に書ける

```swift
class Shape {
    var numberOfSides = 0
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```

クラスのインスタンス化。

```swift
var shape = Shape()
shape.numberOfSides = 7
var shapeDescription = shape.simpleDescription()
```

イニシャライザ。コンストラクタのようなもの

```swift
class NamedShape {
    var numberOfSides: Int = 0
    var name: String

    init(name: String) {
        self.name = name
    }

    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```

サブクラスの宣言。コロンの後にスーパークラスを指定する。メソッドの実装は`override`で表現する。

```swift
class Square: NamedShape {
    var sideLength: Double

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 4
    }

    func area() -> Double {
        return sideLength * sideLength
    }

    override func simpleDescription() -> String {
        return "A square with sides of length \(sideLength)."
    }
}
let test = Square(sideLength: 5.2, name: "my test square")
test.area()
test.simpleDescription()
```

getter/setterの実装。setterの中では暗黙的な名称`newValue`を持つ。

```swift
class EquilateralTriangle: NamedShape {
    var sideLength: Double = 0.0

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 3
    }

    var perimeter: Double {
        get {
            return 3.0 * sideLength
        }
        set {
            sideLength = newValue / 3.0
        }
    }

    override func simpleDescription() -> String {
        return "An equilateral triangle with sides of length \(sideLength)."
    }
}
var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
print(triangle.perimeter)
// Prints "9.3"
triangle.perimeter = 9.9
print(triangle.sideLength)
// Prints "3.3000000000000003"
```

### 列挙と構造

`enum`で列挙を作成する。クラスや型のように扱え、メソッドを所持することもできる。

```swift
enum Rank: Int {
    case ace = 1
    case two, three, four, five, six, seven, eight, nine, ten
    case jack, queen, king

    func simpleDescription() -> String {
        switch self {
        case .ace:
            return "ace"
        case .jack:
            return "jack"
        case .queen:
            return "queen"
        case .king:
            return "king"
        default:
            return String(self.rawValue)
        }
    }
}
let ace = Rank.ace
let aceRawValue = ace.rawValue
```

通常、Swiftは0からはじまり1ずつ増加する値を割り当てるが、開発者自身によってその振る舞いを変更することができる。上の例では`1`が`Ace`に割り当てられている。数値だけでなく文字列も使用できる。
