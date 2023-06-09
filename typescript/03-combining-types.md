# #3: Combining Types 

**Combining Types** là tính năng kết hợp giữa các **types** lại với nhau để tạo ra các **********types********** phức tạp mới, nó sẽ có tính chất kế thừa hoặc chứa `propertites` và `methods` từ kiểu dữ liệu gốc.

## Type Alias

**Type Alias** trong TypeScript cho phép ta đặt tên mới cho một kiểu dữ liệu đã tồn tại hoặc kết hợp nhiều kiểu dữ liệu thành một kiểu dữ liệu mới. Điều này giúp ta tạo ra các tên gọi ngắn gọn và dễ hiểu hơn cho các kiểu dữ liệu phức tạp.

Để định nghĩa một Type Alias, ta sử dụng từ khóa **type**. Dưới đây là cú pháp định nghĩa **Type Alias** cơ bản:

```tsx
type Name = string;
type Age = number;
type User = { name: Name; age: Age };

const user: User = { name: 'John', age: 30 };
```

## Keyof Operator 

Operator **keyof** là Phép toán **`keyof`** cho phép bạn trích xuất tập hợp các khóa (keys) của một kiểu dữ liệu đối tượng. Nó trả về một liên hợp các chuỗi **keys** trong đối tượng.

Toán tử **keyof** thường được sử dụng để truy cập và xử lý các thuộc tính của một đối tượng.

```tsx
type Person = {
  name: string;
  age: number;
  address: string;
};

type PersonKeys= keyof Person; //PersonKeys will have the value "name" | "age" | "address"
```

Ví dụ trên chúng ta có một **type alias**  `Person` , và dùng **keyof** để tạo ra một **union** chứa các **properties name - keys** của `Person` :

```tsx
const person: Person = {
  name: "John",
  age: 25,
  address: "123 Street",
};

function getProperty(obj: Person, key: keyof Person) {
  return obj[key];
}

const name = getProperty(person, "name"); // "John"
const age = getProperty(person, "age"); // 25
```

[What Is "keyof typeof" Used For in TypeScript? - Designcise](https://www.designcise.com/web/tutorial/what-is-keyof-typeof-used-for-in-typescript)
### 1. Union Types

**Union Types** cho phép bạn chỉ định nhiều **types** có thể cho một **variable** hoặc một **parameter**, sử dụng **union type** bằng kí hiểu: **`|`**

```tsx
type UnionType = Type1 | Type2 | Type3;
```

- **union type** với **variable**
    
    ```tsx
    let myVariable: number | string ;
    
    myVariable = "Hello";
    myVariable = 10;
    ```
    
- **union type** với **function**
    
    ```tsx
      function combine(input1: string | number, input2: string | number) {
      	return input1 + input2;
      }
    ```
    

### Intersection Types

**Intersection Types**, **types** sẽ bao gồm tất cả các thuộc tính và phương thức từ các kiểu đã được kết hợp:

```tsx
type typeAB = typeA & typeB;

```

1. Kết hợp các `interfaces`:
    
    ```tsx
    interface Car {
      brand: string;
      color: string;
    }
    
    interface Electric {
      batteryCapacity: number;
    }
    
    type ElectricCar = Car & Electric;
    
    const tesla: ElectricCar = {
      brand: "Tesla",
      color: "Black",
      batteryCapacity: 75
    };
    ```
    
2. Kết hợp các `functions`:
    
    ```tsx
     type MathOperation = (a: number, b: number) => number;
     type Loggable = (message: string) => void;
    
     type Calculator = MathOperation & Loggable;
    
     const calculator: Calculator = (a, b) => {
       const result = a + b;
       console.log("Result: " + result);
       return result;
     };
    
     calculator(5, 3);  // Result: 8
    ```
    

### ****Sự khác nhau giữa Union Types và Intersection Types****

**Xung đột** **Intersection types:** Khi sử dụng **Intersection Types**, cần lưu ý rằng nếu có `properties` hoặc `methods` có đặt cùng `key` và sử dụng `&`. Điều này có thể dẫn đến xung đột và khó khăn trong việc xử lý và sử dụng các `properties` hoặc `methods` .

```tsx
interface Person {
    name: string;
    age: number;
}

interface Student {
    studentCode: number;
    age: string;
}

let student: Student & Person = {
    studentCode: 10022022,
    name: "Vu",
    age: 22 // Error: Type 'number' is not assignable to type 'never'
}
```

Trong ví dụ trên, lỗi xảy ra vì có một xung đột trong thuộc tính `age` giữa `Person` và `Student`. Kiểu `Person` định nghĩa `age` là `number`, trong khi kiểu `Student` định nghĩa `age` là `string`. Khi bạn kết hợp hai kiểu này thành kiểu lại, **TS** không thể xác định được kiểu chính xác cho `age`.

Để giải quyết vấn đề này, bạn có thể sử dụng **Union Types (`|`)** thay vì **Intersection Types (`&`)** nếu muốn có một thuộc tính có thể có giá trị của nhiều kiểu khác nhau. Dưới đây là ví dụ sử dụng **Union Types**: