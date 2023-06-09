# #10: Advanced Types

### Mapped Types

Bản chất của Mapped Types trong TypeScript là ánh xạ qua từng thuộc tính của một loại hiện có và tạo ra một loại mới dựa trên thuộc tính đó. Nó cho phép chúng ta thực hiện các biến đổi phức tạp trên các loại dữ liệu hiện có và tạo ra các loại dữ liệu mới phù hợp với yêu cầu của chúng ta.

Khi sử dụng Mapped Types, chúng ta sử dụng toán tử **`keyof`** để lấy danh sách các thuộc tính của một loại hiện có. Sau đó, chúng ta ánh xạ qua từng thuộc tính và áp dụng một biểu thức hoặc biến đổi để tạo ra thuộc tính mới trong loại mới.

Cú pháp chung của Mapped Types trong TypeScript như sau:

```tsx
type MappedType = {
  [Property in ExistingType]: NewType;
}
```

VD:

```tsx
type OptionsFlags<Type> = {
  [Property in keyof Type]: boolean;
};

type Features = {
  darkMode: () => void;
  newUserProfile: () => void;
};
 
type FeatureOptions = OptionsFlags<Features>;
```

### ****Conditional Types****

tính năng cho phép chúng ta xử lý các logic điều kiệu để có trả về một type theo logic đó

```tsx
Type extends Condition ? TrueType : FalseType
```

vd

```tsx
type TypeName<T> =
  T extends string ? "string" :
  T extends number ? "number" :
  T extends boolean ? "boolean" :
  "unknown";

const name1: TypeName<string> = "string"; // "string"
const name2: TypeName<number> = "number"; // "number"
const name3: TypeName<boolean> = "boolean"; // "boolean"
const name4: TypeName<Date> = "unknown"; // "unknown"
```

### Literal Types

Là một tính năng cho phép chúng ta chỉ định rõ giá trị cụ thể và giới hạn các giá trị có thể gán cho một biến hoặc một thuộc tính trong một kiểu dữ liệu.

```tsx
let status: "success" | "error" | "pending";
status = "success"; // Ok
status = "error"; // Ok
status = "pending"; // Ok
status = "in progress"; // Error

====================================================================
type Age = 42;

let age: Age = 42; // ok
let age: Age = 43; // error
```

### ****Recursive Types****

một tính năng cho phép chúng ta định nghĩa các kiểu dữ liệu đệ quy, tức là kiểu dữ liệu có thể tham chiếu đến chính nó. Điều này cho phép chúng ta xây dựng cấu trúc dữ liệu phức tạp và linh hoạt trong TypeScript.

chú ý khi sử dụng Recursive Types để tránh lặp vô hạn và xác định điều kiện dừng để kết thúc đệ quy. Điều này giúp đảm bảo tính hợp lệ và xác thực trong việc sử dụng Recursive Types.

```tsx
type Tree<T> = {
  value: T;
  left?: Tree<T>;
  right?: Tree<T>;
};

const tree: Tree<number> = {
  value: 1,
  left: {
    value: 2,
    left: {
      value: 4
    },
    right: {
      value: 5
    }
  },
  right: {
    value: 3
  }
};
```

Trong ví dụ này, chúng ta định nghĩa một Recursive Type là **`Tree<T>`**. Mỗi nút trong cây có thuộc tính **`value`** để lưu trữ giá trị và thuộc tính **`left`** và **`right`** để tham chiếu đến các nút con có cùng kiểu **`Tree<T>`**.

Điều kiện dừng để kết thúc đệ quy là khi không có nút con nào (cả **`left`** và **`right`** đều không được định nghĩa).