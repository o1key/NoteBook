# 1: Introduction To TypeScript

![what-is-typescript](https://d2ms8rpfqc4h24.cloudfront.net/uploads/2021/12/Understand-Typescript.jpg )

**TS** được định nghĩa là "Một **JS** dùng cho phát triển dự án quy mô lớn".

**TS** là ngôn ngữ nâng cấp dự trên **JS** nó có thể làm mọi thứ mà **JS** có thể làm và kèm theo một số tính năng bổ sung.

## **Install TS using NPM**

**NPM (Node.js package manager)** được sử dụng để install gói **TS** trên máy cục bộ hoặc dự án của bạn. Hãy đảm bảo rằng bạn đã install **Node.js** trên máy của mình. Nếu bạn đang sử dụng các **framework JS** cho ứng dụng của mình thì việc install **Node.js** là cần thiết.

`npm install -g typescript`

Câu lệnh trên sẽ install và update phiên bản **TS** mới nhất cho máy tính của bạn. Với `-g` bạn có thể dùng **TS** bất kỳ dự án nào. Để kiểm tra phiên bản đã cài đặt **TS** bằng câu lệnh sau:

`tsc -v`

## **The tsconfig.json file**

**tsconfig.json** là một tiệp cấu hình **TS**, được sử dụng để định cấu hình các tùy chọn trình biên dịch và các thiết lập cho dự án. Khi chạy lệnh `tsc` **TS compiler** sẽ tìm kiếm tệp **tsconfig.json** từ thư mục hiện tại và các thư mục cha cho đến khi nó tìm thấy **tsconfig.json**. Nếu tìm thấy **TS compiler** sẽ sự dụng cấu hình được chỉ đinh trong đó để biên dịch dự án.

**Một số options quan trọng trong tsconfig.json**

1. "**[compilerOptions](https://www.typescriptlang.org/tsconfig#compilerOptions)**" : Đây là phần quan trọng nhất của **tsconfig.json**, nơi chúng ta có thể cấu hình các tùy chọn biên dịch cho **TS** . Ví dụ, chúng ta có thể xác định phiên bản **ECMAScript** mục tiêu, đặt các tùy chọn liên quan đến kiểm tra kiểu, cấu hình điểm dừng và rất nhiều tùy chọn khác.
2. "[include](https://www.typescriptlang.org/tsconfig#include)" và "**exclude**": Các trường này xác định tệp nguồn **TS** cần được bao gồm hoặc loại trừ khỏi quá trình biên dịch. Chúng ta có thể sử dụng các mẫu đường dẫn hoặc đường dẫn tới các thư mục cụ thể.
3. **"files"**: Đây là danh sách các tệp TypeScript được liệt kê một cách rõ ràng. Nếu chúng ta sử dụng trường "files", TypeScript compiler chỉ biên dịch các tệp được liệt kê trong danh sách này.
4. **"extends"**: Chúng ta có thể mở rộng một tệp **tsconfig.json** khác bằng cách sử dụng trường "**extends**". Điều này cho phép chúng ta tái sử dụng các cài đặt cấu hình từ một tệp cấu hình khác.

**Tại sao tsconfig.json quan trọng?**

Có một số lý do tại sao **tsconfig.json** là một yếu tố quan trọng trong môi trường phát triển **TS**:

1. **Quản lý dự án dễ dàng**: **tsconfig.json** giúp quản lý các thiết lập dự án một cách rõ ràng và có tổ chức. Chúng ta có thể định nghĩa các tệp gốc, tùy chọn biên dịch và các thiết lập khác trong một tệp duy nhất.
2. **Tích hợp dễ dàng với công cụ phát triển**: Các công cụ phát triển tích hợp, chẳng hạn như trình biên dịch **TS** trong IDE hoặc các công cụ kiểm tra kiểu **TS**, sẽ đọc và sử dụng **tsconfig.json** để cung cấp trợ giúp và phân tích tốt hơn cho dự án.

**Example**

```tsx
project/
  |- src/
  |    |- main.ts
  |- tsconfig.json
```

Giả sử chúng ta có một dự án TypeScript đơn giản với cấu trúc thư mục như sau:

```tsx
{
  "compilerOptions": {
    "target": "es6",
    "outDir": "./dist"
  },
  "include": [
    "./src/**/*"
  ]
}
```

Trong phần `"compilerOptions"`, chúng ta đã đặt `"target"` là `"es6"` để chỉ định phiên bản **ECMAScript** mục tiêu là **ES6**. Chúng ta cũng đã đặt `"outDir"` là `"./dist"` để chỉ định thư mục đích cho kết quả biên dịch.

Phần `"include"` chỉ định rằng chúng ta muốn bao gồm tất cả các tệp trong thư mục `"src"` và các thư mục con của nó trong quá trình biên dịch.

Bây giờ, khi chúng ta chạy lệnh `tsc` để biên dịch dự án, **TS compiler** sẽ sử dụng cấu hình trong tệp **tsconfig.json** và biên dịch tệp `main.ts` thành **JS**, sau đó đặt kết quả trong thư mục `dist`.

**[Compiler Options](https://www.typescriptlang.org/tsconfig)**

# [lesson 2: Typescript types ](02-typescript-types.md)