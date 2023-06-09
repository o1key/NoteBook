# #2: Typescript Types

Typescript types là một phần quan trọng trong TS, mọi khái niệm của TS đều xoay quanh về làm việc với Typescript types. Với Typescript type bạn có định nghĩa data types cho variables, parameters, objects, functions, array,… v.v. 

## Type Inference
là quá trình mà ****TS**** tự động suy luận và gán (**assign) data types** cho `variable`**,** `function`**,** `array`**,…** dựa trên mục đính sử dụng chúng. 

**Type Inference** sẽ được tự sinh ra khi bạn không sử dụng khái niệm [T**ype annotation**](https://www.notion.so/2-2-Type-annotations-2eda7ae1074e41b7aa7e90417875d88a?pvs=21) để xác định **data types** cho `variable`, `function`, `object`,….   

```tsx
let x = 5; // TS infers x as type number
let y = "hello"; // TS infers y as type string
let z = [1,2,3]; // TS infers z as type number[]

function addNumbers(a:number, b:number){
	return a + b;
}
á
let result = addNumbers(5, 10) // TS infers result as type number
```

Trong một số trường hợp phức tạp, việc sử dụng Type Inference sẽ mạng lại rui rõ vì vậy ta nên sử dụng **Type Annotation** để cung cấp một cách rõ ràng để trong việc viết ******************code******************


## Type annotation

Trong TS việc sử dụng ********************Type annotation******************** nhằm mục định khai báo rõ ràng data types cho variable, function,….. Nó cung cấp thông tin và đặc biệt nó cho biết data type trả về của function. 

```tsx
const age: number = 32 //number variable
const name: string = "Huy" // string variable
const isActive: boolean = true // boolean variable

function addNumbers(a: number, b: number): number {
	  return a + b;
	}
	
const result = addNumbers(5, 10);
console.log(result); // Output: 15
	
const invalidResult = addNumbers("5", 10); // Error: The first parameter is not of type number
console.log(invalidResult);

// Type annotation for an object
const person: { name: string; age: number; } = {
	name: "John",
	age: 30
};
		
console.log(person.name); // Output: John
console.log(person.age); // Output: 30
		
// Incorrect assignment will result in a type error
const invalidPerson: { name: string; age: number; } = {
	name: "Jane",
	age: "25" // Error: Type 'string' is not assignable to type 'number'
};
```

Ví dụ trên, mỗi `variables` , `functions` , `objects` đều sử dụng ****************type annotation**************** để cho việc làm rõ ****************data type.**************** Và bạn cũng không thể thay đổi **value** nếu **value** đó không đáp ứng được **data type** đã định nghĩa.


## Type Assertions

Để sử dụng **type assertion** chúng ta có thể sử dụng angle-bracket **<T>value** hoặc là **"as T"** syntax

```tsx
let num = 42;

// using angle-bracket syntax
let str = <string>num;

// using as syntax
let str2 = num as string;
```

## As `Const`

**as const** là một **type assertion** được dùng để khai báo một *biến* hoặc *một phần tử mảng*/*object* với kiểu dữ liệu cố định. Khi bạn đã sử dụng **as const**, **TS** sẽ hiểu rằng bạn đang khai báo giá trị chúng không được thay đổi.

Một số lưu ý khi sử dụng **as const** không chính xác:

1. Sử dụng **as const** với biến có giá trị có thể thay đổi:

```tsx
	let count = 5;
	const immutableCount = count as const;
	
	immutableCount++; // Error: Cannot assign to 'immutableCount' because it is a read-only property.
```

1. Sử dụng **as const** với mảng và thực hiện thay đổi các phần tử trong mảng:

```tsx
const numbers = [1, 2, 3] as const;

numbers[0] = 10; // Error: Index signature in type 'readonly [1, 2, 3]' only permits reading.

```

2. Sử dụng **as const** với đối tượng và thực hiện thay đổi các thuộc tính của đối tượng:

```tsx
	const person = {
	  name: "John",
	  age: 30,
	  gender: "male"
	} as const;
	
	person.age = 40; // Error: Cannot assign to 'age' because it is a read-only property.
```

## **Non-Null Assertion**

**Non-Null Assertion** Là type assertion cho phép bạn nói cho trình biên dịch biết rằng một giá trị sẽ không bao giờ là **null** hoặc **undefined**.

```tsx
let name: string | null = "John";
let length: number = name!.length;

console.log(length); //  4
```

- với thuộc tính của objects:

```tsx
interface Person {
  name: string | null;
  age: number;
}

const person: Person = {
  name: "John",
  age: 30
};

console.log(person.name!.toUpperCase()); //  "JOHN"
```

## Primitive Types

Là những kiểu dữ liệu cơ bản tích hợp sẵn trong ngôn ngữ lập trình.

1. **number**: Kiểu dữ liệu `number` đại diện cho các giá trị số. Nó có thể đại diện cho số nguyên, số thập phân hoặc số âm.
    
    ```tsx
    let age: number = 25;
    let pi: number = 3.14;
    let temperature: number = -10;
    
    ```
    
2. **string**: Kiểu dữ liệu `string` đại diện cho các chuỗi ký tự. Chuỗi có thể được đặt trong dấu nháy đơn hoặc dấu nháy kép.
    
    ```tsx
    let name: string = "John Doe";
    let message: string = 'Hello, TypeScript!'
    ```
    
3. **boolean**: Kiểu dữ liệu `boolean` đại diện cho giá trị logic và chỉ có hai giá trị: `true` hoặc `false`.
    
    ```tsx
    let isTrue: boolean = true;
    let isFalse: boolean = false;
    ```
    
4. **null** và **undefined**: `null` và `undefined` đại diện cho các giá trị không có giá trị hoặc giá trị không xác định.
    
    ```tsx
    let data: null = null;
    let value: undefined = undefined;
    ```
    
5. **void** là kiểu dữ liệu dùng để đại diện cho một `function` không return về bất kì giá trị nào. Nó được sử dụng khi bạn muốn chỉ rõ rằng function, method chỉ thực thi một tác vụ mà không có giá trị trả về .
    
    ```tsx
    function greet(): void {
      console.log("Xin chào!");
    }
    
    function calculateSum(a: number, b: number): void {
      const sum = a + b;
      console.log("Tổng =", sum);
    }
    
    greet(); // print "Xin chào!"
    calculateSum(5, 10); // print "Sum = 15"
    
    const result: void = greet(); // Error! Not assigne the value of a void function
    ```
    
    Trong ví dụ trên, hàm `greet` không trả về bất kỳ giá trị nào, chỉ đơn giản in ra một thông báo. Hàm `calculateSum` cũng không trả về giá trị, chỉ tính toán tổng của hai số và in ra kết quả.
    
    Lưu ý rằng kiểu **void** chỉ được sử dụng cho `functions` , `methods` và không thể được sử dụng cho `variables`.
    
    ```tsx
    let value: void; // Error: The 'void' type cannot be used for variables
    ```


## Object Types

Cho phép bạn định nghĩa **data types** cho **objects** có `properties`, `methods`.

1. **Object Literal**: bạn có thể sử dụng cú pháp **Object literal** để định nghĩa một **Object type** đơn giản.
    
    ```tsx
    let person: {name: string; age: number} = {
    	name:"John Doe",
    	age:23,
    }
    ```
    
2. **Typescript Interfac**
3. **Type Alias
Type Alias** trong TypeScript cho phép ta đặt tên mới cho một kiểu dữ liệu đã tồn tại hoặc kết hợp nhiều kiểu dữ liệu thành một kiểu dữ liệu mới. Điều này giúp ta tạo ra các tên gọi ngắn gọn và dễ hiểu hơn cho các kiểu dữ liệu phức tạp.
    
    ```tsx
    type Name = string;
    type Age = number;
    type User = { name: Name; age: Age };
    
    const user: User = { name: 'John', age: 30 };
    ```
    
4. **Enum:** là một tính năng cho phép bạn định nghĩa một tập hơn có giá trị cố định và assign cho chúng các tên gọi ***đại diện***, giúp việc viết mã nguồn trở nên rõ ràng và dễ đọc hơn.
    
    ```tsx
    enum Direction {
      Up = 2,
      Down,
      Left,
      Right
    }
    
    let move: Direction = Direction.Down;
    console.log(move); // Output: 3
    ```
    
    ```tsx
    enum Color {
      Red = "RED",
      Green = "GREEN",
      Blue = "BLUE"
    }
    
    let selectedColor: Color = Color.Green;
    console.log(selectedColor); // Output: "GREEN"
    ```
    
    learn more from the following links:
    
    - [Don't use Enums in Typescript, they are very dangerous 😨 - DEV Community](https://dev.to/ivanzm123/dont-use-enums-in-typescript-they-are-very-dangerous-57bh)
5. **Array**:  dùng để lưu trữ và làm việc với một tập hợp các phần từ cùng **********data types**********. Bạn có thể khải báo theo 2 cách sau:
    
    ```tsx
     let numbers: number[] = [1, 2, 3, 4, 5];
     let names: string[] = ["John", "Jane", "Mary"];
     let mixed: (number | string)[] = [1, "two", 3, "four"];
    
     =========================================================
    
     let numbers: Array<number> = [1, 2, 3, 4, 5];
     let names: Array<string> = ["John", "Jane", "Mary"];
     let mixed: Array<number | string>  = [1, "two", 3, "four"];
    
    ```
    
6. **Tuples**: một kiểu dữ liệu để lưu trữ một tập hợp các giá trị có kiểu dữ liệu khác nhau và số lượng cố định.
    - Khai báo một **tuple**
        
        ```tsx
           let person: [string, number, boolean] = ["John Doe", 25, true];
        
        ```
        
    - Truy cập phần tử trong tuple:
        
        ```tsx
         let person: [string, number, boolean] = ["John Doe", 25, true];
        
         	let name: string = person[0];
         	let age: number = person[1];
         	let isActive: boolean = person[2];
        
         	console.log(name); // Output: "John Doe"
         	console.log(age); // Output: 25
         	console.log(isActive); // Output: true
        ```
        
    - Gán giá trị tùy chỉnh cho tuple:
        
        ```tsx
         	let person: [string, number, boolean] = ["John Doe", 25, true];
         	person[1] = 30;
        ```
        
    - Sử dụng các phương thức và thuộc tính của tuple:
        
        ```tsx
          let person: [string, number, boolean] = ["John Doe", 25, true];
        
          let length: number = person.length;
          console.log(length); // Output: 3
        
          person.push("Extra");
          console.log(person); // Output: ["John Doe", 25, true, "Extra"]
        ```

## Other types

1. **any** :được dùng khi bạn muốn biến có thể chứa bất kỳ giá trị nào và không cần kiểm tra kiểu tại thời điểm biên dịch. Nó cung cấp tính linh hoạt cao và cho phép bạn làm việc với các giá trị có kiểu không xác định.
    
    Điểm quan trong khi làm việc với **any** :
    
    - Bỏ qua việc kiểm tra tại thời điểm biên dịch: Khi một biến được gán kiểu **any**, **TS** sẽ bỏ qua việc kiểm tra kiểu của biến đó. Điều này có nghĩa bạn có thể gán bất kỳ giá trị nào cho biến đó mà không gây ra lỗi biên dịch liên quan tới kiểu dữ liêu. Nhưng bên cạnh đó nó mang lại rủ, giảm tính an toàn và tính đúng đắn của mã nguồn **TS**.
        
        ```tsx
        let value: any = 10;
        
        let result = value + 5;
        console.log(result);
        
        let invalidResult = value.toUpperCase();
        console.log(invalidResult); // Runtime error: value.toUpperCase is not a function
        ```
        
        Trong ví dụ này, biến `value` có **any** **type** và có thể chứa bất kỳ giá trị nào. Mặc dù không có lỗi biên dịch khi thực hiện phép cộng với `value`, nhưng khi sử dụng phương thức `toUpperCase()`, một lỗi runtime xảy ra vì `value` không phải là một chuỗi và không có phương thức `toUpperCase(`
        
2. **"unknown"**: là một **data type** đại diện cho `values` mà chúng ta *không biết về kiểu dữ liệu chính xác của chúng* trong quá trình phát triển. Giống như **any type, unknown type** có thể assign bất kỳ value nào
    - Nếu như **any type** cho phép thực hiện bất kỳ operation nào mà không check type thì **unknown type** lại gần như không cho phép thực hiện operation nào.
        
        ```tsx
        let unknownValue: unknown;
        unknownValue.foo().bar(); // Error
        unknownValue.toString(); // Error
        unknownValue[0]; // Error
        ```
        
    - Kiểu dữ liệu an toàn: **unknown** yêu cầu bạn phải xác định kiểu dữ liệu của biến trước khi sử dụng nó. Điều này giúp đảm bảo rằng các phép toán được thực hiện trên biến sẽ hợp lệ với kiểu dữ liệu đó, giúp tránh các lỗi runtime không mong muốn.
        
        ```tsx
        function processValue(value: unknown) {
        if (typeof value === "number") {
          let result = value + 10;
          console.log(result);
        } else if (typeof value === "string") {
          let length = value.length;
          console.log(length);
        } else {
          console.log("Invalid value");
        }
        }
        
        let data: unknown = 42;
        processValue(data); // Output: 52
        
        data = "Hello, TypeScript";
        processValue(data); // Output: 16
        
        data = true;
        processValue(data); // Output: Invalid value
        
        ```
        
        hàm `processValue` nhận một `variable` có kiểu **unknown** và kiểm tra **data type** của nó trước khi thực hiện các phép toán. Bằng cách sử dụng `typeof`, chúng ta xác định được kiểu dữ liệu của `value` và sau đó chúng ta sẽ thể các handle logic của mình.
        
    - Bạn không thể gán trực tiếp giá trị của một `variable` có **unknown** cho một biến có kiểu khác mà không kiểm tra kiểu dữ liệu trước đó.
        
        ```tsx
          let unknownValue: unknown = 10;
          let numberValue: number;
        
          numberValue = unknownValue; // Compiler Error: Type 'unknown' is not assignable to type 'number'
        ```
        
        Để gán giá trị của một biến có kiểu **unknown** cho một **variable** có kiểu khác, bạn cần kiểm tra kiểu dữ liệu trước đó và đảm bảo kiểu dữ liệu phù hợp.
        
        ```tsx
        let unknownValue: unknown = 10;
        let numberValue: number;
        
        if (typeof numberValue === 'number') {
          numberValue = unknownValue;
        } else {
          console.log('Invalid value');
        }
        ```
        
        Trong đoạn mã đó, **TS** không báo lỗi vì bạn đã kiểm tra kiểu dữ liệu của `unknownValue` bằng cách sử dụng `typeof` trước khi gán giá trị của nó cho `numberValue`.
        
3. **"never"**: là một **type** đặc biệt dùng để chỉ ra các hàm hoặc biểu thức không bao giờ trả về kết quả hoặc gây ra các **exception**.
    
    ```tsx
    function throwError(message: string): never {
       throw new Error(message);
     }
    
     function infiniteLoop(): never {
       while (true) {
         // Do something
       }
     }
    ```
    
    Trong ví dụ trên, hàm `throwError` gây ra một exception bằng cách ném một đối tượng `Error`, trong khi hàm `infiniteLoop` lặp vô hạn mà không bao giờ kết thúc. Cả hai hàm đều có kiểu trả về là `never`, vì chúng không bao giờ hoàn thành việc thực thi.
    
4. Sự khác biệt giữa **Void** và **Never**
    - **void** vẫn có thể là undefined hoặc null trong khi **never** không nhận bất cứ giá trị nào.
        
        ```tsx
        let result: void
        result = null
        result = undefined
        
        let errors: never
        errors = null //Type 'null' is not assignable to type 'never'
        errors = undefined //Type 'undefined' is not assignable to type 'never'
        
        ```
        
# [lesson 3: Combining Types ](03-combining-types.md)