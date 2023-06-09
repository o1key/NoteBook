# #9: Utility types

Utility Types trong TypeScript dùng để thực hiện các phép biến đổi và thao tác trên các types khác, giúp ta thay đổi, tạo hoặc truy xuất thông tin từ các types hiện có một cách thuận tiện và linh hoạt.

### Partial<T>:

Tạo ra một **type** mới bằng cách gỡ bỏ tính bắt buộc của tất cả các thuộc tính trong type **`T`**, biến chúng thành các thu Nó được sử dụng để tạo ra một phiên bản tùy chọn (optional) của một type đã có sẵn.

```tsx
type Partial<T> = {
  [P in keyof T]?: T[P];
};
```

Trong đó:

- **`T`** là type nguồn, từ đó chúng ta muốn tạo ra phiên bản tùy chọn.
- **`[P in keyof T]`** duyệt qua từng thuộc tính **`P`** trong **`T`**.
- **`?: T[P]`** biểu thị rằng thuộc tính **`P`** là tùy chọn, tức là có thể có giá trị hoặc không có giá trị.

```tsx
interface User {
  name: string;
  age: number;
  email: string;
}

const partialUser: Partial<User> = {
  name: "John Doe",
};

console.log(partialUser); // Output: { name: 'John Doe' }
```

### **Pick<T, K>**

Tạo ra một **type** mới bằng cách lấy ra chỉ mục các thuộc tính **`K`** từ type **`T`**

```tsx
type Pick<T, K extends keyof T> = {
  [P in K]: T[P];
};
```

Trong đó:

- **`T`** là type nguồn, từ đó chúng ta muốn lựa chọn các thuộc tính.
- **`K`** là một union type chứa tên các thuộc tính mà chúng ta muốn lựa chọn.

```tsx
interface User {
  name: string;
  age: number;
  email: string;
  address: string;
}

type UserBasicInfo = Pick<User, 'name' | 'age'>;

const user: UserBasicInfo = {
  name: "John Doe",
  age: 25,
};

console.log(user); // Output: { name: 'John Doe', age: 25 }
```

### **Exclude**<T, U>

Tạo ra một type mới bằng cách loại bỏ tất cả các thành phần trong type **`T`** mà cũng có mặt trong type **`U`**.

```tsx
type Exclude<T, U> = T extends U ? never : T;
```

Trong đó:

- **`T`** là type nguồn
- **`U`** là union type mà chúng ta muốn loại bỏ các thành phần từ **`T`**.
- Nếu một thành phần trong **`T`** có thể gán được cho một thành phần trong **`U`**, nghĩa là nó trùng khớp với **`U`**, thì loại đó sẽ được xác định là **`never`**. Điều này có nghĩa là thành phần đó sẽ bị loại bỏ khỏi **union type** ban đầu. Ngược lại, nếu một thành phần trong **`T`** không trùng khớp với bất kỳ thành phần nào trong **`U`**, nó sẽ được giữ nguyên trong union type kết quả.

```tsx
type Color = 'red' | 'green' | 'blue';
type PrimaryColor = 'red' | 'blue';

type SecondaryColor = Exclude<Color, PrimaryColor>;

const secondaryColors: SecondaryColor = 'green';

console.log(secondaryColors); // Output: 'green'
```

### Omit<T>

Tạo ra một **type** mới bằng cách gỡ bỏ tính bắt buộc của tất cả các thuộc tính trong type **`T`**, biến chúng thành các thu Nó được sử dụng để tạo ra một phiên bản tùy chọn (optional) của một type đã có sẵn.

```tsx
type Omit<T, K extends keyof T> = Pick<T, Exclude<keyof T, K>>;
```

Trong đó:

- **`T`** là type nguồn, từ đó chúng ta muốn loại bỏ các thuộc tính.
- **`K`** là một union type chứa tên các thuộc tính mà chúng ta muốn loại bỏ.

**`Exclude<keyof T, K>`** là một phép biến đổi type sử dụng Utility Type **`Exclude`**. Nó loại bỏ các thành phần thuộc **`K`** khỏi liên hợp các thuộc tính của **`T`**.

**`Pick<T, Exclude<keyof T, K>>`** sử dụng Utility Type **`Pick`** để lựa chọn các thuộc tính từ **`T`** dựa trên kết quả của **`Exclude<keyof T, K>`**.

Ví dụ sử

```tsx
interface Todo {
  title: string;
  description: string;
  completed: boolean;
  createdAt: number;
}

type TodoPreview = Omit<Todo, "description"> & ;

const todo: TodoPreview = {
  title: "Clean room",
  completed: false,
  createdAt: 1615544252770,
};

type TodoInfo = Omit<Todo, "completed" | "createdAt">;

const todoInfo: TodoInfo = {
  title: "Pick up kids",
  description: "Kindergarten closes at 5pm",
}
```

### ****Readonly****<T>

Nó được sử dụng để tạo ra một phiên bản mới của một type bằng cách đặt thuộc tính (readonly), tức là thuộc tính không thể được thay đổi sau khi khởi tạo.

```tsx
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};
```

- **`T`** là type nguồn
- **`[P in keyof T]`** duyệt qua từng thuộc tính **`P`** trong **`T`**.
- **`readonly`** biểu thị rằng thuộc tính **`P`** sẽ được đặt thành chỉ đọc.
- **`: T[P]`** định nghĩa lại kiểu giá trị cho thuộc tính.
    
    ```tsx
    interface User {
      name: string;
      age: number;
      email: string;
    }
    
    const user: Readonly<User> = {
      name: "John Doe",
      age: 25,
      email: "john@example.com",
    };
    
    console.log(user.name); // Output: "John Doe"
    
    // Cannot assign to 'name' because it is a read-only property
    user.name = "Jane Smith";
    ```
    

### Recored<K,T>

Nó được sử dụng để tạo ra một object mới với các cặp key-value có kiểu dữ liệu cụ thể.

```tsx
type Record<K extends keyof any, T> = {
  [P in K]: T;
};
```

- **`K`** là một union type chứa các key của object mới.
- **`T`** là kiểu dữ liệu của các value trong object mới.

```tsx
 interface CatInfo {
  age: number;
  breed: string;
}

type CatName = 'miffy' | 'boris' | 'mordred';

const cats: Record<CatName, CatInfo> = {
  miffy: { age: 10, breed: 'Persian' },
  boris: { age: 5, breed: 'Maine Coon' },
  mordred: { age: 16, breed: 'British Shorthair' },
};
```

### **Extract<T,>**

Tạo ra một type mới bằng cách chọn ra tất cả các thành phần trong type **`T`** mà cũng có mặt trong type **`U`**.

```tsx
type Extract<T, U> = T extends U ? T : never;
```

- **`T`** là union type nguồn, chứa các thành phần mà chúng ta muốn trích xuất.
- **`U`** là union type mục tiêu, chứa các thành phần mà chúng ta muốn trích xuất từ **`T`**.

```tsx
type T0 = Extract<"a" | "b" | "c", "a" | "b">; // Type T0 = "a"|"b"
type T1 = Extract<string | number | (() => void), Function>; // type T1 = () => void
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "square"; x: number }
  | { kind: "triangle"; x: number; y: number };

type T2 = Extract<Shape, { kind: "circle" }> // T2 = { kind: "circle"; x: number }
```

### **NonNullable<T, U>**

Tạo ra một type mới bằng cách chọn ra tất cả các thành phần trong type **`T`** mà cũng có mặt trong type **`U`**.

```tsx
type NonNullable<T> = T extends null | undefined ? never : T;
```

- **`T`** là union type nguồn

```tsx
type T0 = NonNullable<string | number | undefined>;
// type T0 = string | number

type T1 = NonNullable<string[] | null | undefined>;
// type T1 = string[]
```

# [lesson 10: Advanced Types ](10-advanced-types.md)