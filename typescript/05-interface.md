# #5: Interface

**Interface** trong ****TS**** được defined cấu trúc của **đối tượng (object),** bao gồm các ******properties****** và ****methods**** mà objects có thể có 

Để khai báo một **interface**, ta sử dụng `interface` keyword trong một tệp **TS** (.ts).

```tsx
interface Dismension {
	width:string;
	height:string;
}
```

Sau khi đã khai báo **interface**, chúng ta có thể sử dụng nó bằng các tạo các objects thỏa mãn với interface đó:

```tsx
interface Dismension{
	widht:string;
	heigth:string;
}

const imagedim: Dismension = {
	widht:"200px",
	heigh:"200px",
}

```

Tương tự với một **interface** chứa **methods**. Ta khao báo một **interface** với tên là `User` với các **properties**: `id, fistName, lastName`, và một method: `getFullName`.

```tsx
interface User {
	id: number;
	firstName: string;
	lastName: string;
	getFullName(): string;
}

const user: Use = {
	id:12,
	fistName:"John",
	lastName:"Dee",
	getFullName: ()=> `${fistname} ${lastName}`
}
```

Việc sử dụng **interface** giúp **compiler TS** biết thông tin chính xác về các **properties, methods** mà **object** có. Nếu một **property** bị thiếu hoặc value của nó không phù với **type** đã được định nghĩa trước đó, **compiler TS** sẽ báo lỗi.

### Class Implementing Interface

Một **class** có thể **implement** một **interface** đồng nghĩa với việc class đó phải tuân thủ các yêu câu của interface đó, tức là cung cấp các properties và methods đã được định nghĩa sẵn.

Để một class implementing interface, ta sử dụng `implements` keyword và sau đó tên của các interface.

```tsx
interface Shape {
  calculateArea(): number;
}

interface Resizable {
  resize(scale: number): void;
}

class Rectangle implements Shape, Resizable {
  // Implementing the interface methods
  calculateArea() {
    // Calculation logic for rectangle area
    // Return the calculated area
  }

  resize(scale: number) {
    // Logic for resizing the rectangle
  }
}

```

Vd trên, ta có hai **interfaces** `Shape, Resizable`. . Chúng ta muốn tạo một **class** `Rectangle` có khả năng thay đổi kích thước và cũng có thể tính diện tích. Để làm điều đó, chúng ta khai báo lớp `Rectangle` và sử dụng từ khóa `implements` để chỉ ra rằng lớp này thực hiện cả hai **interface** `Shape` và `Resizable`

## Working with Interfaces

### Optional Properties

Trong đoạn mã ví dụ trước, tất cả các **properties** trong **Interface** đều là **required**. Nếu chúng ta tạo một **object** mới với **interface** đó và bỏ qua một vài **properties**, trình biên dịch **TS** sẽ báo lỗi.

Tuy nhiên, có những trường hợp mà chúng ta mong đợi các **objects** của mình có các **properties** có thể **optional**. Chúng ta có thể làm điều này bằng cách đặt một dấu hỏi (?) ngay trước kiểu dữ liệu của **property** khi khai báo **interface**:

```tsx
interface Post {
  title: string;
  content: string;
  tags?: string[];
}

```

Trong trường hợp cụ thể này, chúng ta cho biết cho trình biên dịch rằng có thể bỏ qua `ags` **property** của **Post**.

```tsx
const validPostObj: Post {
title: 'Post title',
content: 'Some content for our post',
};

const invalidPostObj: Post = {
	title: 'Invalid post',
	content: 'Hello',
	meta: 'post description', // this will throw an error

/* Type '{ title: string; content: string; meta: string; }' is not assignable to type 'Post'.

	Object literal may only specify known properties, and 'meta' does not exist in type 'Post'.
*/
};
```

### Read-only properties

Trong **TS**, chúng ta có thể đánh dấu một **property** trong **interface** là (read-only). Điều này có nghĩa là sau khi **property** đó được gán giá trị, ta không thể thay đổi giá trị của nó.

```tsx
interface FulfilledOrder {
  itemsInOrder: number;
  totalCost: number;
  readonly dateCreated: Date;
}
```

chúng ta có **interface** `FulfilledOrder` có ba thuộc tính: `itemsInOrder` (số lượng hàng hóa trong đơn hàng), `totalCost` (tổng chi phí) và `dateCreated` (ngày tạo). . `dateCreated` được đánh dấu là (read-only) bằng cách thêm từ khóa `readonly` trước khai báo.

Khi tạo một **object** dựa trên **interface** `FulfilledOrder`, ta phải cung cấp giá trị cho các **properties** bắt buộc như `itemsInOrder` và `totalCost`,  `dateCreated` khi tạo đối tượng:

```tsx
const order: FulfilledOrder = {
  itemsInOrder: 1,
  totalCost: 199.99,
  dateCreated: new Date(),
};
```

Sau khi object  `order` được tạo, ta không thể thay đổi giá trị của `dateCreated`. Nếu ta cố gắng gán lại giá trị mới cho **property** này, trình biên dịch sẽ báo lỗi:

```tsx
order.dateCreated = new Date(2021, 10, 29); 
// Error! Read-only Proprety can't be changed
```

### Function types and Class types

**Interface** cũng có thể được sử dụng để **function types** và kiểm tra cấu trúc của **classes**

Để mô tả **function types** bằng một interface, chúng ta sử dụng khai báo gọi function (**call signature**) trong interface. Điều này tương tự như việc khai báo một **function** cùng với những parameter và trả về type.

Ví dụ, chúng ta có interface `SumFunc` định nghĩa một **function** có hai **parameters** là `number` ****và trả về một `number`:

```tsx
interface SumFunc {
  (a: number, b: number): number;
}

const add: SumFunc = (a, b) => {
  return a + b;
}
```

Chúng ta cũng có thể sử dụng **interface** để định rõ kiểu của **class** được tạo. Để làm điều này, chúng ta cần tạo một **interface**. (ví dụ: `CarInterface`) chứa các **properties** và **methods** mà một **class** (ví dụ: `Car`) phải triển khai. Sau đó, chúng ta sử dụng từ khóa `implements`  để xác định rằng **class** đó tuân thủ **interface** đã định nghĩa.

```tsx
interface CarInterface {
  model: string;
  year: string;
  getUnitsSold(): number;
}

class Car implements CarInterface {
  model: string;
  year: string;

  getUnitsSold() {
    // Logic ...
    return 100;
  }

  constructor(model: string, year: string) {
    this.model = model;
    this.year = year;
  }
}
```

### Generic Interfaces

**Generic interfaces** cho phép bạn định nghĩa một **interface** mà có thể áp dụng cho nhiều loại dữ liệu khác nhau. Điều này giúp tăng tính linh hoạt và tái sử dụng mã.

Khi muốn tạo một **generic interface**, bạn sử dụng **type parameter** trong khai báo **interface** bằng: `<>`.  T**ype parameter** này với mục sẽ được thay thế bằng một **type** cụ thể khi tái sử dụng **generic interface** này.

```tsx
interface List<T> {
  items: T[];
  addItem(item: T): void;
  removeItem(item: T): void;
}
```

`MyList` là một **class** triển khai dựa trên **generic interface** `List<T>`. Chúng ta đã truyền `number` và `string` làm kiểu cụ thể cho `T`, và tạo ra các **objects** `numberList` và `stringList` dựa vào **class** `MyList`

```tsx
class MyList<T> implements List<T> {
  items: T[] = [];

  addItem(item: T) {
    this.items.push(item);
  }

  removeItem(item: T) {
    const index = this.items.indexOf(item);
    if (index !== -1) {
      this.items.splice(index, 1);
    }
  }
}

const numberList: List<number> = new MyList<number>();
numberList.addItem(1);
numberList.addItem(2);
numberList.addItem(3);
console.log(numberList.items); // Output: [1, 2, 3]

const stringList: List<string> = new MyList<string>();
stringList.addItem('Hello');
stringList.addItem('World');
console.log(stringList.items); // Output: ['Hello', 'World']
```

Sử dụng **generic interface** cho phép bạn tạo ra mã linh hoạt và tái sử dụng, vì bạn có thể sử dụng cùng một **interface** cho nhiều loại dữ liệu khác nhau. Điều này giúp mã của bạn trở nên dễ đọc, bảo trì và kiểm tra kiểu.

### Indexable Types

**Indexable Type** là một khái niệm cho phép chúng ta mô tả các đối tượng có khả năng được truy cập thông qua **chỉ mục (index)** thay vì truy cập thông qua tên **property** cố định.

Khi chúng ta sử dụng **Indexable Types**, chúng ta định nghĩa một "**index signature**" trong **interface** hoặc **type**. **Index signature** cho phép chúng ta chỉ định kiểu dữ liệu của **index** và kiểu dữ liệu trả về khi truy cập thông qua **index** đó.

Có hai loại **index signature**:

1. **String Index Signature**: Sử dụng khi chỉ mục là một chuỗi (string).
    
    ```tsx
    interface MyObject {
      [key: string]: valueType;
    }
    ```
    
    **Application State Management**: Khi phát triển ứng dụng lớn, việc quản lý **state** ứng dụng có thể trở nên phức tạp. Sử dụng **Indexable Type**, chúng ta có thể xây dựng một hệ thống quản lý trạng thái linh hoạt và có khả năng mở rộng. Ví dụ:
    
    ```tsx
    interface AppState {
       [key: string]: any;
     }
    
     const state: AppState = {
       user: {
         name: "John",
         age: 30,
       },
       cart: {
         items: [
           { id: 1, name: "Product 1", price: 10 },
           { id: 2, name: "Product 2", price: 20 },
         ],
       },
     };
    
     console.log(state.user.name); // Output: "John"
     console.log(state.cart.items.length); // Output: 2
    ```
    
2. **Number Index Signature**: Sử dụng khi chỉ mục là một số (number).
    
    ```tsx
     interface MyArray {
       [index: number]: elementType;
     }
    ```
    
    **Biểu đồ Dữ liệu (Data Charts):** Trong các ứng dụng hiển thị dữ liệu biểu đồ, chúng ta thường cần xử lý dữ liệu động có cấu trúc không đều
    
    Trong ví dụ này, chúng ta sử dụng **Indexable Type** để mô tả dữ liệu biểu đồ, cho phép chúng ta có các chuỗi dữ liệu (series) có tên không định trước và mỗi chuỗi chứa một mảng các điểm dữ liệu (DataPoint).
    
    ```tsx
    interface DataPoint {
       x: number;
       y: number;
     }
    
     interface ChartData {
       [seriesName: string]: DataPoint[];
     }
    
     const chartData: ChartData = {
       series1: [
         { x: 1, y: 5 },
         { x: 2, y: 10 },
         { x: 3, y: 8 },
       ],
       series2: [
         { x: 1, y: 3 },
         { x: 2, y: 6 },
         { x: 3, y: 4 },
       ],
     };
    
     console.log(chartData.series1[0].y); // Output: 5
     console.log(chartData.series2.length); // Output: 3
    
    ```
    

**Indexable Types** là cung cấp khả năng định nghĩa và sử dụng các **object** có thể truy cập thông qua **index**, cho phép chúng ta xử lý các dạng dữ liệu phức tạp và linh hoạt trong **TS**.

### Extending an Interface

Trong **TS**, chúng ta có thể **mở rộng (extend)** một **interface** bằng cách tạo ra một **interface** mới dựa trên **interfaces** hiện có. Khi chúng **extends** một **interface**, **interface** mới sẽ **kế thừa (inherit)** tất cả các thành viên (**properties và methods**) của **interface** gốc

Cú pháp để **exten** một **interface** trong **TS** là sử dụng từ khóa `extends` sau tên **interface** và liệt kê các **interface** mà chúng ta muốn

```tsx
interface Shape {
  color: string;
}

interface Size {
  width: number;
  height: number;
}

interface Rectangle extends Shape, Size {
  area: number;
}

const rectangle: Rectangle = {
  color: "blue",
  width: 10,
  height: 20,
  area: 200,
};
```

Trong ví dụ trên, chúng ta có ba **interfaces** là `Shape`, `Size` và `Rectangle`. **Interface** `Rectangle` **extends** từ cả `Shape` và `Size`, nghĩa là nó kế thừa cả thuộc tính `color` từ `Shape` và properties `width` và `height` từ `Size`, và có thêm một thuộc tính `area`.

Khi chúng ta tạo một đối tượng `rectangle` từ interface `Rectangle`, đối tượng đó phải có cả thuộc tính `color`, `width`, `height` và `area`.

Việc **extends nhiều interface** cho phép chúng ta tạo ra các **interface phức tạp hơn**, kết hợp các tính chất từ nhiều nguồn khác nhau để định nghĩa các đối tượng phong phú hơn và tái sử dụng code hiệu quả.