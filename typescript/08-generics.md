# #8: Generics

**Generics** cho phép chúng ta định nghĩa các loại dữ liệu linh hoạt, tạo ra các hàm, lớp, và giao diện có thể làm việc với nhiều **types** khác nhau mà không cần viết lại code nhiều lần.

## Working with Generic Type Variables

Để sử dụng **Generics** trong **TS**, chúng ta sử dụng **syntax:** `<> (<T, U, .....>)` sau tên của một **function**, **class** hoặc **interface**

### Sử dụng Generic trong Functions

Các **generics function** cho phép bạn tạo ra các **function** có thể làm việc với nhiều kiểu dữ liệu khác nhau. Bạn có thể xác định **generic type** trong cặp dấu ngoặc nhọn (`<T>`) và sử dụng nó trong các khai báo **function.**

```tsx
function reverse<T>(array: T[]): T[] {
  return array.reverse();
}

let numbers: number[] = [1, 2, 3, 4, 5];
let reversedNumbers = reverse(numbers); // [5, 4, 3, 2, 1]

let strings: string[] = ["apple", "banana", "cherry"];
let reversedStrings = reverse(strings); // ["cherry", "banana", "apple"]
```

### Generic Classes

**Generics** cũng có thể được sử dụng trong khai báo **class** để tạo ra các **classes** có thể làm việc với nhiều **types** khác nhau. Bạn có thể xác định **generic type** khi khai báo **class** và sử dụng nó trong các thành phần của **class**.

```tsx
class Stack<T> {
  private items: T[] = [];

  push(item: T): void {
    this.items.push(item);
  }

  pop(): T | undefined {
    return this.items.pop();
  }
}

let numberStack = new Stack<number>();
numberStack.push(1);
numberStack.push(2);
numberStack.push(3);

console.log(numberStack.pop()); // 3

let stringStack = new Stack<string>();
stringStack.push("Hello");
stringStack.push("World");

console.log(stringStack.pop()); // "World"
```

Trong ví dụ này, chúng ta khai báo **generic** **class** `Stack` với **generic type** `T`. **Generic** **class** này cho phép lưu trữ và truy xuất các phần tử có kiểu dữ liệu tùy ý. Bằng cách tạo một đối tượng dựa trên **generic** **class** `Stack` với một kiểu dữ liệu cụ thể, chúng ta có thể thực hiện các tác vụ dựa trên các thành phần của nó.

### Generics interface

**Generics** cũng có thể được sử dụng trong **interface.**

```tsx
interface Comparable<T> {
  compareTo(other: T): number;
}

class Person implements Comparable<Person> {
  constructor(private name: string, private age: number) {}

  compareTo(other: Person): number {
    if (this.age < other.age) {
      return -1;
    } else if (this.age > other.age) {
      return 1;
    } else {
      return 0;
    }
  }
}

const john = new Person("John", 25);
const jane = new Person("Jane", 30);

console.log(john.compareTo(jane)); // -1
```

## Generic Constraints

**Generic Constraints** trong **TS** là một cách để áp đặt các ràng buộc và giới hạn kiểu dữ liệu cho các tham số generic trong các hàm, lớp, và interfaces. 
Nó cho phép bạn chỉ định kiểu dữ liệu mà một tham số generic có thể nhận, đảm bảo rằng các phép toán và truy cập dữ liệu chỉ áp dụng cho các kiểu dữ liệu phù hợp.

Khi bạn sử dụng Generic Constraints, bạn sẽ sử dụng từ khóa **`extends`** sau tên tham số generic, sau đó chỉ định kiểu hoặc union kiểu mà tham số generic phải kế thừa hoặc thỏa mãn.

### Ràng buộc với Interface

```tsx
 interface Vehicle {
  brand: string;
  year: number;
}

function getLatestVehicle<T extends Vehicle>(vehicles: T[]): T | undefined {
  if (vehicles.length === 0) {
    return undefined;
  }

  let latestVehicle = vehicles[0];
  for (let i = 1; i < vehicles.length; i++) {
    if (vehicles[i].year > latestVehicle.year) {
      latestVehicle = vehicles[i];
    }
  }

  return latestVehicle;
}

const cars: Vehicle[] = [
  { brand: "Toyota", year: 2018 },
  { brand: "Honda", year: 2020 },
  { brand: "Ford", year: 2019 },
];

const latestCar = getLatestVehicle(cars);
console.log(latestCar); // Output: { brand: 'Honda', year: 2020 }

const motorcycles: Vehicle[] = [];
const latestMotorcycle = getLatestVehicle(motorcycles);
console.log(latestMotorcycle); // Output: undefined
```

Trong ví dụ này, chúng ta định nghĩa một **interface** `Printable` với một phương thức `print()`. Hàm `printItem` sử dụng **Generic Constraints** để chỉ chấp nhận các đối tượng có kiểu dữ liệu implement interface `Printable`. Nhờ đó, chúng ta có thể gọi phương thức `print()` trên đối tượng được truyền vào.

### Ràng buộc với class

```tsx
class Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  sound(): void {
    console.log("Making sound...");
  }
}

class Dog extends Animal {
  sound(): void {
    console.log("Woof!");
  }
}

function makeSound<T extends Animal>(animal: T): void {
  animal.sound();
}

const dog = new Dog("Buddy");
makeSound(dog); // In ra "Woof!"
```

Trong ví dụ này, chúng ta sử dụng Generic Constraints để chỉ chấp nhận các đối tượng có kiểu dữ liệu là lớp con của lớp `Animal`. Hàm `makeSound` chỉ gọi phương thức `sound()` trên đối tượng được truyền vào.

## Generic Parameter Defaults

**Generic Parameter Defaults** cho phép chúng ta đặt giá trị mặc định cho các **Generic type** trong trường hợp không xác định kiểu dữ liệu cụ thể cho chúng.

Khi định nghĩa một **Generic type** chúng ta có thể chỉ định một giá trị mặc địnó nh cho bằng cách sử dụng `=` . Khi không có kiểu dữ liệu cụ thể được cung cấp cho **Generic type**, **TS** sẽ sử dụng giá trị mặc định này.

```tsx
function getValueOrDefault<T = string>(value: T): T {
  return value || "default";
}

const result1 = getValueOrDefault("Hello"); // "Hello"
const result2 = getValueOrDefault<number>(null); // "default"
const result3 = getValueOrDefault(); // result3  "default"
```

Một số ví dụ phức tạp hơn về cách sử dụng **Generic Parameter Defaults**:

```tsx
interface Entity {
  id: string;
}

class Repository<T extends Entity = Entity> {
  private items: T[];

  constructor() {
    this.items = [];
  }

  getAll(): T[] {
    return this.items;
  }

  getById(id: string): T | undefined {
    return this.items.find(item => item.id === id);
  }

  add(item: T): void {
    this.items.push(item);
  }

  update(item: T): void {
    const index = this.items.findIndex(existingItem => existingItem.id === item.id);
    if (index !== -1) {
      this.items[index] = item;
    }
  }

  delete(id: string): void {
    this.items = this.items.filter(item => item.id !== id);
  }
}

interface User extends Entity {
  name: string;
  age: number;
}

const userRepository = new Repository<User>();
userRepository.add({ id: "1", name: "John", age: 30 });
userRepository.add({ id: "2", name: "Alice", age: 25 });

const users = userRepository.getAll();
console.log(users); 
// [{ id: "1", name: "John", age: 30 }, { id: "2", name: "Alice", age: 25 }]

const user = userRepository.getById("1");
console.log(user); // { id: "1", name: "John", age: 30 }

userRepository.update({ id: "1", name: "John Doe", age: 35 });

userRepository.delete("2");
```

Trong ví dụ này, chúng ta định nghĩa một **class** `Repository` với một **Generic type** `T` được `extends` là **interface** `Entity`. Giá trị mặc định cho `T` là `Entity` nếu không có type cụ thể được cung cấp.

**********Class********** `Repository` có các ************methods************ `getAll`, `getById`, `add`, `update` và `delete` để xử lý các logic. Chúng ta có thể sử dụng lớp `Repository` với kiểu dữ liệu cụ thể như `User` và thực hiện các thao tác CRUD trên đối tượng `User`.`

- Vd là việc với Api

```tsx
interface ApiResponse<T> {
  data: T;
  error: boolean;
  message: string;
}

class ApiClient {
  async get<T = any>(url: string): Promise<ApiResponse<T>> {
    const response = await fetch(url);
    const data = await response.json();
    return {
      data,
      error: false,
      message: "Success",
    };
  }

  async post<T = any>(url: string, body: any): Promise<ApiResponse<T>> {
    const response = await fetch(url, {
      method: "POST",
      body: JSON.stringify(body),
    });
    const data = await response.json();
    return {
      data,
      error: false,
      message: "Success",
    };
  }
}

interface User {
  id: number;
  name: string;
  email: string;
}

async function fetchUserData(): Promise<User> {
  const apiClient = new ApiClient();
  const response = await apiClient.get<User>("/users/1");
  if (!response.error) {
    return response.data;
  } else {
    throw new Error(response.message);
  }
}

async function updateUser(user: Partial<User>): Promise<User> {
  const apiClient = new ApiClient();
  const response = await apiClient.post<User>("/users/1", user);
  if (!response.error) {
    return response.data;
  } else {
    throw new Error(response.message);
  }
}

(async () => {
  try {
    const userData = await fetchUserData();
    console.log(userData);

    const updatedUser = await updateUser({ name: "John Doe" });
    console.log(updatedUser);
  } catch (error) {
    console.error(error);
  }
})();
```

Trong ví dụ trên, chúng ta định nghĩa một `ApiClient` để tương tác với một API bên ngoài. Các phương thức `get` và `post` trong `ApiClient` có sử dụng **Generic Parameter Defaults** với **type** mặc định là `any`. Điều này cho phép chúng ta sử dụng phương thức này mà không cần cung cấp kiểu dữ liệu cụ thể.

Sau đó, chúng ta định nghĩa một `User` **interface** và sử dụng `ApiClient` để lấy thông tin người dùng và cập nhật thông tin người dùng. Chúng ta sử dụng **Generic Parameter** để xác định kiểu dữ liệu mà chúng ta mong đợi từ API.

Trong cuối cùng, chúng ta gọi hai hàm `fetchUserData` và `updateUser` để lấy và cập nhật thông tin người dùng. Chúng ta cũng xử lý các trường hợp lỗi và log kết quả ra console.

Với sử dụng **Generic Parameter Defaults**, chúng ta có thể linh hoạt sử dụng `ApiClient` và xác định kiểu dữ liệu cụ thể mà chúng ta mong đợi từ API mà không cần lặp lại việc chỉ định kiểu dữ liệu trong mỗi lần sử dụng.

# [lesson 9: Utility types](09-utility-types.md)