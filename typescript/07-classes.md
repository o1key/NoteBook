# #6: Classes

Classes trong TS là một phần của khái niệm hướng đối tượng(OOP), cho phép bạn mô phỏng các đối tượng trong thế giới thực và tạo ra các đối tượng dựa trên các mô hình và thuộc tính của chúng. Một lớp (class) là một bản thiết kế (template) để tạo ra các đối tượng, chứa các thuộc tính (properties) và phương thức (methods) định nghĩa cách mà đối tượng sẽ hoạt động.

## 1.Constructors
**TS** sử dụng **constructor** để khởi tạo các đối tượng. **Constructor** là các phương thức đặc biệt trong một **class**, và chúng được tự động gọi khi bạn tạo một đối tượng mới từ **class** đó bằng từ khóa `new`.

```tsx
class Person {
  name: string;

  constructor(name: string) {
    this.name = name;
    console.log("A new person has been created!");
  }
}

const person = new Person("John"); //"A new person has been created!"
console.log(person.name); // "John"
```

Mục đích chính của **constructor** là thực hiện các tác vụ khởi tạo ban đầu cho một đối tượng. Khi một đối tượng mới được tạo, **constructor** sẽ thực hiện các thao tác cần thiết để thiết lập giá trị cho các thuộc tính (**fields**) của đối tượng hoặc để thực hiện các **methods** khác trước khi đối tượng đó có thể được sử dụng.

### Parameterized Constructor

Là **constructor** có một hoặc nhiều tham số đầu vào. Chúng được sử dụng để truyền giá trị khởi tạo cho các thuộc tính của đối tượng dựa vào **constructor**.

```tsx
class Person {
  name: string;

  constructor(name: string) {
    this.name = name;
  }
}

const person = new Person("John");
console.log(person.name); // Kết quả: "John"
```

Trong ví dụ trên, chúng ta định nghĩa một **constructor** tùy chỉnh cho lớp `Person`. **Constructor** này nhận một tham số `name` và gán giá trị của tham số này vào thuộc tính `name` của đối tượng. Khi chúng ta tạo một đối tượng `person`, chúng ta phải truyền giá trị cho tham số `name` trong **constructor**.

### Constructor Overloading

Là một tính năng trong các ngôn ngữ lập trình hướng đối tượng cho phép định nghĩa nhiều phiên bản (overloads) của một **constructor** trong cùng một lớp. Mỗi phiên bản **constructor** có thể có số lượng và số **parameters** khác nhau.

Điểm mấu chốt của **constructor overloading** là khả năng tạo đối tượng từ lớp với các cách khởi tạo khác nhau dựa trên các tham số truyền vào.

```tsx
class Person {
  name: string;
  age: number;

  constructor(name: string);
  constructor(name: string, age: number);
  constructor(name: string, age?: number) {
    this.name = name;
    this.age = age || 0;
  }
}

const person1 = new Person("John");
const person2 = new Person("Jane", 25);

```

Trong ví dụ trên, chúng ta định nghĩa hai phiên bản **constructor** cho lớp `Person`. Phiên bản đầu tiên chỉ nhận một tham số `name`, trong khi phiên bản thứ hai nhận cả `name` và `age`. Chúng ta sử dụng ký hiệu `?` để đánh dấu tham số `age` trong phiên bản thứ hai là **optional**.

Khi chúng ta tạo đối tượng `person1` bằng cách gọi `new Person("John")`, phiên bản **constructor** đầu tiên sẽ được gọi và thuộc tính `name` của đối tượng sẽ được khởi tạo bằng "John", và thuộc tính `age` sẽ có giá trị mặc định là 0.

Tương tự, khi chúng ta tạo đối tượng `person2` bằng cách gọi `new Person("Jane", 25)`, phiên bản **constructor** thứ hai sẽ được gọi và thuộc tính `name` và `age` của đối tượng sẽ được khởi tạo tương ứng với giá trị truyền vào.

## 2. Methods
**Methods** (phương thức) trong **TS** là các **functions** được định nghĩa trong một **********class********** để thực hiện các hành động và tính toán trên đối tượng của lớp đó. **Method** là một phần quan trọng trong hướng đối tượng, nó cho phép đối tượng thực hiện các hành động dựa vào thông tin cung cấp và chức năng cụ thể.

Cú pháp để định nghĩa một phương thức trong **TS** là:

```tsx
class ClassName {
  methodName(parameter1: type1, parameter2: type2, ...): returnType {
	//Logic...
  }
}
```

vd: chúng ta có một **class** `Calculator` với hai **methods** `add` và `multiply`. **Method** `add` thực hiện phép cộng hai số và trả về kết quả, còn `multiply` thực hiện phép nhân hai số và trả về kết quả. Chúng ta có thể tạo một đối tượng `myCalculator` từ lớp `Calculator` và gọi các phương thức của nó để thực hiện các tính toán.

```tsx
class Calculator {
  add(a: number, b: number): number {
    return a + b;
  }

  multiply(a: number, b: number): number {
    return a * b;
  }
}

const myCalculator = new Calculator();
console.log(calculator.add(2, 3)); // Kết quả: 5
console.log(calculator.multiply(4, 5)); // Kết quả: 20

```

## Getters and Setters

là các phương thức đặc biệt được sử dụng để truy cập và cập nhật giá trị của các thuộc tính (**fields**) trong một **class**. Chúng giúp kiểm soát quyền truy cập và thực hiện các logic bổ sung khi truy cập vào các thuộc tính của một đối tượng.

### Getters

là một phương thức dùng để truy xuất giá trị của một thuộc tính. Nó được định nghĩa bằng từ khóa `get`, theo sau là tên phương thức và một khối mã thực thi. Khi truy cập vào thuộc tính thông qua getter, phương thức này sẽ được gọi và trả về giá trị tương ứng.

### Setters

là một phương thức dùng để gán giá trị cho một thuộc tính. Nó được định nghĩa bằng từ khóa `set`, theo sau là tên phương thức và một tham số để nhận giá trị mới. Khi gán giá trị cho thuộc tính thông qua setter, phương thức này sẽ được gọi và giá trị mới sẽ được sử dụng để cập nhật thuộc tính.

```tsx
class Product {
  private _price: number;
  private _discount: number;

  constructor(price: number, discount: number) {
    this._price = price;
    this._discount = discount;
  }

  get price(): number {
    return this._price;
  }

  set price(newPrice: number) {
    if (newPrice >= 0) {
      this._price = newPrice;
    } else {
      throw new Error("Invalid price");
    }
  }

  get discount(): number {
    return this._discount;
  }

  set discount(newDiscount: number) {
    if (newDiscount >= 0 && newDiscount <= 100) {
      this._discount = newDiscount;
    } else {
      throw new Error("Invalid discount");
    }
  }

  get discountedPrice(): number {
    const discountedAmount = (this._price * this._discount) / 100;
    return this._price - discountedAmount;
  }
}

const product = new Product(100, 20);
console.log(product.price);  // 100
console.log(product.discount);  // 20
console.log(product.discountedPrice);  // 80

product.price = 150;
console.log(product.price);  // 150
console.log(product.discountedPrice);  // 120

product.discount = 30;
console.log(product.discount);  // 30
console.log(product.discountedPrice);  // 105

product.price = -50;  // Throw error: Invalid price
product.discount = 150;  // Throw error: Invalid discount
```

Trong ví dụ này, chúng ta có lớp `Product` đại diện cho một sản phẩm trong cửa hàng. Lớp này có các thuộc tính `_price` và `_discount` để lưu giá và giảm giá của sản phẩm. Chúng ta sử dụng getters và setters để kiểm soát và thực hiện các quy tắc về giá trị nhập vào.

## 3. Access Modifiers
là khái niệm định nghĩa quyền truy cập vào các thành viên (thuộc tính và phương thức) của một **class**. **TS** hỗ trợ ba mức độ quyền truy cập cho thành viên trong một **class**:

### Public

cho phép truy cập vào các thành phần từ bất kỳ, bao gồm cả bên trong và bên ngoài của **class** đó.

```tsx
class Animal {
  public name: string;

  constructor(name: string) {
    this.name = name;
  }

  public makeSound() {
    console.log("The animal makes a sound");
  }
}

const cat = new Animal("Tom");
console.log(cat.name);  // Output: "Tom"
cat.makeSound();  // Output: "The animal makes a sound"
```

ví dụ trên, thuộc tính `name` và phương thức `makeSound` của **class** `Animal` được khai báo là `public`, cho phép chúng ta truy cập và sử dụng nó một cách dễ dàng. Chúng ta có thể truy cập và in ra giá trị của thuộc tính `name` và gọi phương thức `makeSound` từ đối tượng `cat`.

### Private

chỉ cho phép truy cập vào các thành phần từ bên trong cùng một **class**. Khi một thành phần được khai báo là `private`, nó chỉ có thể được truy cập và sử dụng trong phạm vi của **class** đó.

```tsx
class Animal {
  private name: string;

  constructor(name: string) {
		// No error
    this.name = name;
  }

  private makeSound() {
    console.log("The animal makes a sound");
  }
}

const cat = new Animal("Tom");
console.log(cat.name);  
// Error: Property 'name' is private and only accessible within class 'Animal'
cat.makeSound();  
// Error: Property 'makeSound' is private and only accessible within class 'Animal'
```

Thuộc tính `name` và phương thức `makeSound` của **class** `Animal` được khai báo là `private`. Do đó, chúng ta không thể truy cập trực tiếp vào thuộc tính `name` hoặc gọi phương thức `makeSound` từ bên ngoài **class**. Bất kỳ cố gắng truy cập vào các thành phần `private` sẽ gây ra lỗi. Thành phần `private` chỉ có thể được truy cập và sử dụng bên trong cùng một **class**.

Tuy nhiên, bạn có thể cung cấp các phương thức **getter** và **setter** để thay đổi giá trị của thuộc tính `private` đó.

```tsx
class Animal {
  private name: string;

  constructor(name: string) {
    this.name = name;
  }

  public getName(): string {
    return this.name;
  }

  public setName(newName: string): void {
    this.name = newName;
  }
}

const cat = new Animal("Tom");
console.log(cat.getName());  // Output: "Tom"
cat.setName("Jerry");
console.log(cat.getName());  // Output: "Jerry"

```

Thuộc tính `name` của **class** `Animal` được khai báo là `private`. Tuy nhiên, chúng ta cung cấp phương thức public `getName` để lấy giá trị của thuộc tính `name` và phương thức public `setName` để thiết lập giá trị mới cho thuộc tính `name`. Bằng cách sử dụng các phương thức này, chúng ta có thể truy cập và thay đổi giá trị của thuộc tính private `name` từ bên ngoài **class**.

### Protected

cho phép truy cập vào các thành phần từ bên trong cùng một **class** và các lớp con (subclasses) 

```tsx
class Animal {
  protected name: string;

  constructor(name: string) {
    this.name = name;
  }

  protected makeSound() {
    console.log("The animal makes a sound");
  }
}

class Cat extends Animal {
  public meow() {
    console.log(`${this.name} meows`);
    this.makeSound();
  }
}

const cat = new Cat("Tom");
console.log(cat.name);
// Error: Property 'name' is protected and only accessible within class 'Animal' and its subclasses
cat.makeSound();
// Error: Property 'makeSound' is protected and only accessible within class 'Animal' and its subclasses
cat.meow();
// Output: "Tom meows" and "The animal makes a sound"

```

Chúng ta không thể truy cập trực tiếp vào thuộc tính `name` hoặc gọi phương thức `makeSound` từ bên ngoài **class** hoặc các đối tượng của **class** `Animal`, nhưng chúng có thể được truy cập thông qua phương thức và xử lý trong phạm vi của **class** `Cat`

## 4. Class Heritage

là khái niệm cho phép một **lớp con (subclass)** kế thừa các ******properties****** và **methods** từ một **lớp cha (superclass).** **Class** con có thể sử dụng lại mã nguồn đã được triển khai trong **class** cha, mở rộng hoặc thêm các ******properties****** và **methods** mới.

Để kế thừa một **class** trong **TS**, chúng ta sử dụng từ khóa `extends` trong khai báo **class** con. Đây là cú pháp chung:

```tsx
class Animal {
  protected name: string;

  constructor(name: string) {
    this.name = name;
  }

  move(distance: number): void {
    console.log(`${this.name} moves ${distance} meters.`);
  }
}

class Dog extends Animal {
  bark(): void {
    console.log("Woof! Woof!");
  }
}

const myDog = new Dog("Buddy");
myDog.move(10);  // Kết quả: Buddy moves 10 meters.
myDog.bark();  // Kết quả: Woof! Woof!
```

Ngoài việc kế thừa từ một lớp cha, **TS** cũng hỗ trợ khái niệm **implements** để triển khai **interface**.

```tsx
interface Flyable {
  fly(): void;
}

class Bird implements Flyable {
  fly(): void {
    console.log("Bird is flying.");
  }
}

const bird = new Bird();
bird.fly();  // Kết quả: Bird is flying.
```

## 5.Overriding Methods
Là một khái niệm trong lập trình hướng đối tượng, cho phép lớp con (subclass) định nghĩa lại (override) phương thức đã được định nghĩa trong lớp cha (superclass). Khi một phương thức trong lớp con được ghi đè, phương thức đó sẽ được sử dụng thay thế phương thức trong lớp cha khi được gọi từ đối tượng của lớp con.

- Phương thức ghi đè trong lớp con phải có cùng tên, cùng kiểu trả về (hoặc kiểu con của kiểu trả về) và cùng danh sách tham số như phương thức trong lớp cha.

```tsx
abstract class Employee {
  protected name: string;
  protected salary: number;

  constructor(name: string, salary: number) {
    this.name = name;
    this.salary = salary;
  }

  abstract calculateSalary(): number;

  displayDetails() {
    console.log(`Name: ${this.name}`);
    console.log(`Salary: ${this.calculateSalary()}`);
  }
}

class ContractEmployee extends Employee {
  private contractDuration: number;

  constructor(name: string, salary: number, contractDuration: number) {
    super(name, salary);
    this.contractDuration = contractDuration;
  }

  calculateSalary() {
    return this.salary * this.contractDuration;
  }
}

class PermanentEmployee extends Employee {
  private bonus: number;

  constructor(name: string, salary: number, bonus: number) {
    super(name, salary);
    this.bonus = bonus;
  }

  calculateSalary() {
    return this.salary + this.bonus;
  }
}

const contractEmployee = new ContractEmployee('John Doe', 1000, 12);
contractEmployee.displayDetails(); // Output: "Name: John Doe", "Salary: 12000"

const permanentEmployee = new PermanentEmployee('Jane Smith', 2000, 500);
permanentEmployee.displayDetails(); // Output: "Name: Jane Smith", "Salary: 2500"
```

Trong ví dụ này, lớp `Employee` là lớp trừu tượng (abstract) chứa phương thức trừu tượng `calculateSalary()`. Lớp `ContractEmployee` và `PermanentEmployee` kế thừa từ lớp `Employee` và ghi đè (**override**) phương thức `calculateSalary()` để tính lương theo cách riêng của từng loại nhân viên.

Khi gọi phương thức `displayDetails()`, phương thức `calculateSalary()` tương ứng trong từng lớp con sẽ được gọi và trả về kết quả tính lương phù hợp. Điều này cho phép chúng ta sử dụng cùng một phương thức `displayDetails()` để hiển thị thông tin chi tiết của từng loại nhân viên, mặc dù cách tính lương khác nhau.

Với **Method Overriding**, chúng ta có thể linh hoạt triển khai các phương thức theo nhu cầu và logic của từng lớp con, đồng thời sử dụng các phương thức chung trong lớp cha để tiết kiệm code và tăng tính tái sử dụng.

## 6.Static
Trong **TS**, keyword **static** được dùng để khởi tạo các thuộc tính tĩnh (static properties) và phương thức tĩnh (static methods) của một class. Các static properties và static methods này có thể được gọi trực tiếp từ **class** sau khi đã khai báo mà không cần phải khởi tạo các đối tượng từ **class** đó. Chúng ta đi vào ví dụ cụ thể sau nhé

```tsx
class Employee {
	readonly name: string;
	age: number;
	static companyInfo = 'vn';

	constructor (name: string, age: number) {
		this.name = name;
		this.age = age;
	};

	getName (): string {
		return this.name;
	}

	static getCompanyInfo (): string {
		return this.companyInfo;
	}
}

console.log(Employee.age) // Property 'age' does not exist on type 'typeof Employee'.
console.log(Employee.getName()) // Property 'getName' does not exist on type 'typeof Employee'.
console.log(Employee.companyInfo) // vn
```

Từ ví dụ trên, chúng ta có thể thấy, chúng ta đã khai báo **static property** là `companyInfo` và **staticmethod** là `getCompanyInfo` cùng với **static** và chúng ta có thể truy cập chúng trực tiếp với **class** `Employee` mà không cần khởi tạo object cùng **new** từ chúng.

## `static` Blocks

```tsx
class MathUtils {
  static PI: number;
  static DOUBLE_PI: number;

// static blocks
  static {
    MathUtils.PI = 3.14;
    MathUtils.DOUBLE_PI = MathUtils.PI * 2;
    console.log("Static block is executed.");
  }

  static calculateArea(radius: number): number {
    return MathUtils.PI * radius * radius;
  }
}

console.log(MathUtils.PI);  // Output: 3.14
console.log(MathUtils.DOUBLE_PI);  // Output: 6.28
console.log(MathUtils.calculateArea(5));  // Output: 78.5
```

Ví dụ về việc sử dụng **static blocks** để gọi một **API** và khởi tạo dữ liệu từ kết quả **API**

```tsx
class WeatherUtils {
  static weatherData: any;

  static {
    fetch('<https://api.weatherapi.com/v1/current.json?key=YOUR_API_KEY&q=London>')
      .then(response => response.json())
      .then(data => {
        WeatherUtils.weatherData = data;
        console.log("Static block: Weather data is fetched.");
      })
      .catch(error => {
        console.error("Static block: Failed to fetch weather data.", error);
      });
  }

  static getTemperature(): number {
    if (WeatherUtils.weatherData) {
      return WeatherUtils.weatherData.current.temp_c;
    } else {
      return 0;
    }
  }
}

console.log("Temperature in London:", WeatherUtils.getTemperature());
```

**Class** `WeatherUtils` có một **static properties** `weatherData` để lưu trữ dữ liệu thời tiết. Trong **static block**, chúng ta gọi một **API** để lấy dữ liệu thời tiết từ London. Khi kết quả **API** được trả về, chúng ta gán dữ liệu vào `weatherData` và hiển thị thông báo `Static block: Weather data is fetched`. Nếu xảy ra lỗi trong quá trình gọi **API**, chúng ta hiển thị thông báo lỗi tương ứng.

Sau khi **static block**được thực thi, chúng ta có thể gọi phương thức `getTemperature` để truy cập nhiệt độ hiện tại từ dữ liệu thời tiết. Nếu dữ liệu thời tiết đã được lấy thành công, phương thức sẽ trả về nhiệt độ (temp_c). Nếu không, nó sẽ trả về giá trị 0.

## 7. Generic Classes

Bằng cách sử dụng **generic classes** bạn có thể tạo ra **Classes** mà có thể làm việc với nhiều **types** khác nhau mà không cần viết lại **code**. 

```tsx
class Stack<T> {
  private items: T[] = [];

  push(item: T): void {
    this.items.push(item);
  }

  pop(): T | undefined {
    return this.items.pop();
  }

  peek(): T | undefined {
    return this.items[this.items.length - 1];
  }

  size(): number {
    return this.items.length;
  }

  isEmpty(): boolean {
    return this.items.length === 0;
  }
}

class Employee {
  constructor(public name: string, public age: number) {}
}

const employeeStack = new Stack<Employee>();
employeeStack.push(new Employee("John Doe", 30));
employeeStack.push(new Employee("Jane Smith", 25));
employeeStack.push(new Employee("Bob Johnson", 35));

console.log(employeeStack.pop());  // Output: Employee { name: "Bob Johnson", age: 35 }
console.log(employeeStack.peek());  // Output: Employee { name: "Jane Smith", age: 25 }
console.log(employeeStack.size());  // Output: 2
console.log(employeeStack.isEmpty());  // Output: false
```

Trong ví dụ trên, chúng ta định nghĩa một **generic class** `Stack<T>`  . **********Class********** này có các phương thức như `push` (thêm phần tử vào ngăn xếp), `pop` (lấy phần tử từ đỉnh ngăn xếp và xóa nó), `peek` (xem phần tử đầu ngăn xếp mà không xóa nó), `size` (trả về số lượng phần tử trong ngăn xếp), và `isEmpty` (kiểm tra xem ngăn xếp có rỗng hay không).

Sau đó, chúng ta tạo một đối tượng `employeeStack` từ **********generic class********** `Stack<Employee>`. Đối tượng này được sử dụng để lưu trữ các đối tượng "`Employee`", mỗi đối tượng chứa thông tin về tên và tuổi của nhân viên. Sau đó sử dụng các phương thức của **********generic class********** `Stack` để thao tác và truy xuất các phần tử.

## 8. Abstract classes

là một lớp mà không thể khởi tạo trực tiếp, mà chỉ dùng để được kế thừa bởi các lớp con. Abstract class cung cấp một cấu trúc cơ bản và định nghĩa các phương thức và thuộc tính chung cho các **lớp con (subclasses)**.

```tsx
abstract class Shape {
  protected color: string;

  constructor(color: string) {
    this.color = color;
  }

  abstract getArea(): number;
  abstract getPerimeter(): number;

  getInfo(): string {
    return `Color: ${this.color}`;
  }
}

class Circle extends Shape {
  private radius: number;

  constructor(color: string, radius: number) {
    super(color);
    this.radius = radius;
  }

  getArea(): number {
    return Math.PI * this.radius ** 2;
  }

  getPerimeter(): number {
    return 2 * Math.PI * this.radius;
  }
}

class Rectangle extends Shape {
  private width: number;
  private height: number;

  constructor(color: string, width: number, height: number) {
    super(color);
    this.width = width;
    this.height = height;
  }

  getArea(): number {
    return this.width * this.height;
  }

  getPerimeter(): number {
    return 2 * (this.width + this.height);
  }
}

const circle = new Circle("Red", 5);
console.log(circle.getInfo());  // Output: "Color: Red"
console.log(circle.getArea());  // Output: 78.53981633974483
console.log(circle.getPerimeter());  // Output: 31.41592653589793

const rectangle = new Rectangle("Blue", 4, 6);
console.log(rectangle.getInfo());  // Output: "Color: Blue"
console.log(rectangle.getArea());  // Output: 24
console.log(rectangle.getPerimeter());  // Output: 20
```

Trong ví dụ trên, chúng ta có abstract class "Shape" đại diện cho các hình dạng hình học. Lớp này có thuộc tính "color" và các phương thức trừu tượng "getArea()" và "getPerimeter()" để tính diện tích và chu vi của hình dạng. Ngoài ra, lớp "Shape" còn có phương thức "getInfo()" để lấy thông tin về màu sắc của hình dạng.

Chúng ta khai báo hai lớp con là "Circle" và "Rectangle" kế thừa từ abstract class "Shape". Lớp "Circle" có thêm thuộc tính "radius" và triển khai phương thức "getArea()" và "getPerimeter()" dựa trên bán kính của hình tròn. Tương tự, lớp "Rectangle" có thuộc tính "width" và "height" và triển khai các phương thức tương ứng cho hình chữ nhật.

Khi tạo đối tượng từ các lớp con "Circle" và "Rectangle", chúng ta có thể gọi các phương thức và thuộc tính được kế thừa từ abstract class "Shape". Mỗi lớp con triển khai các phương thức trừu tượng theo cách riêng biệt, cung cấp các giá trị và logic phù hợp cho từng hình dạng.

Abstract class cho phép chúng ta xây dựng một bộ khung chung cho các lớp con và định nghĩa các phương thức trừu tượng mà các lớp con cần phải triển khai. Điều này giúp tăng tính linh hoạt, tái sử dụng code và giảm sự lặp lại trong quá trình phát triển ứng dụng.

# [lesson 8: Generics](#8-abstract-classes)