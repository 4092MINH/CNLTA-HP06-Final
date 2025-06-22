# Ghi Chú & Nhắc Nhở SwiftUI

Đây là một ứng dụng ghi chú và nhắc nhở đơn giản, được xây dựng hoàn toàn bằng **Swift** và **SwiftUI**. Mục tiêu của dự án là tạo ra một ứng dụng hữu ích đồng thời là một ví dụ tuyệt vời cho những ai đang học và làm quen với lập trình giao diện người dùng khai báo (declarative UI) của Apple.

 <!-- Bạn có thể thay thế bằng ảnh chụp màn hình thực tế của ứng dụng -->

## ✨ Tính năng của sản phẩm

*   **Quản lý Ghi chú:**
    *   📝 **Thêm ghi chú mới:** Dễ dàng tạo ghi chú với tiêu đề và nội dung chi tiết.
    *   👀 **Xem danh sách ghi chú:** Tất cả các ghi chú được hiển thị trong một danh sách trực quan.
    *   ✏️ **Chỉnh sửa ghi chú:** Cập nhật tiêu đề hoặc nội dung của ghi chú đã có.
    *   🗑️ **Xoá ghi chú:** Xoá những ghi chú không còn cần thiết bằng thao tác vuốt.
*   **Chức năng Nhắc nhở:**
    *   ⏰ **Đặt lịch nhắc nhở:** Thêm ngày và giờ nhắc nhở cho từng ghi chú.
    *   ✅ **Đánh dấu hoàn thành:** Đánh dấu một ghi chú/nhiệm vụ là đã hoàn thành.
    *   🎨 **Hiển thị trạng thái:** Các ghi chú có lịch hẹn sắp tới hoặc đã quá hạn sẽ được làm nổi bật.
*   **Giao diện và Trải nghiệm:**
    *   ✨ Giao diện đơn giản, sạch sẽ và hiện đại.
    *   💾 Dữ liệu được lưu trữ cục bộ trên thiết bị, giúp bạn truy cập ghi chú ngay cả khi không có mạng.

## 🏗️ Các thành phần của sản phẩm

Ứng dụng được cấu trúc thành ba phần chính để dễ dàng quản lý và mở rộng:

1.  **Views (Giao diện):** Chịu trách nhiệm hiển thị dữ liệu và nhận tương tác từ người dùng. Đây là tất cả những gì người dùng nhìn thấy trên màn hình.
    *   `NoteListView.swift`: Màn hình chính hiển thị danh sách tất cả các ghi chú.
    *   `NoteDetailView.swift`: Màn hình chi tiết để xem, chỉnh sửa hoặc tạo mới một ghi chú.
2.  **Data Models (Mô hình Dữ liệu):** Định nghĩa cấu trúc dữ liệu cốt lõi của ứng dụng.
    *   `Note.swift`: Định nghĩa đối tượng `Note` với các thuộc tính như `id`, `title`, `content`, `reminderDate`, `isCompleted`.
    *   `NoteStore.swift`: Một lớp đóng vai trò là "nguồn sự thật" (source of truth), quản lý toàn bộ danh sách các ghi chú (thêm, sửa, xoá, lưu trữ).
3.  **Components (Thành phần Tái sử dụng):** Các phần giao diện nhỏ, độc lập có thể được tái sử dụng ở nhiều nơi trong ứng dụng.
    *   `NoteRowView.swift`: Giao diện cho một hàng trong danh sách ghi chú (`NoteListView`).
    *   `ActionButton.swift`: Một nút bấm với style tùy chỉnh được sử dụng chung trong toàn bộ ứng dụng.

## 🧠 Kiến thức SwiftUI được sử dụng (Từ dễ đến khó)

Dự án này tập trung vào các khái niệm cốt lõi và phổ biến nhất của SwiftUI.

#### 1. Cơ bản về Giao diện (UI Basics)
*   **Views & Controls:** Sử dụng các thành phần giao diện cơ bản như `Text`, `TextField`, `TextEditor`, `Button`, `Image`, `Toggle`.
*   **Layout:** Sắp xếp các thành phần giao diện bằng `VStack`, `HStack`, `ZStack`, và `Spacer` để tạo ra các layout linh hoạt.
*   **List:** Hiển thị một danh sách dữ liệu có thể cuộn. Tuyệt vời để hiển thị danh sách ghi chú.
*   **Navigation:** Sử dụng `NavigationStack` và `NavigationLink` để cho phép người dùng di chuyển giữa màn hình danh sách và màn hình chi tiết.
*   **Modal Sheets:** Sử dụng `.sheet()` để hiển thị màn hình thêm/sửa ghi chú dưới dạng một modal view.

#### 2. Quản lý Trạng thái & Dữ liệu (State & Data Management)
*   **`@State`:** Dùng để quản lý trạng thái đơn giản, cục bộ bên trong một View. Ví dụ: lưu trữ văn bản người dùng đang nhập vào `TextField` trước khi lưu ghi chú. `@State` là một *property wrapper* cho phép View tự động cập nhật lại khi giá trị của nó thay đổi.
*   **`@Binding`:** Tạo một kết nối hai chiều giữa một thuộc tính lưu trữ trạng thái (thường là `@State`) và một View con. Khi View con thay đổi giá trị, sự thay đổi đó sẽ được phản ánh ngược lại ở View cha. Ví dụ: `NoteDetailView` nhận một `Binding` tới một ghi chú để khi người dùng chỉnh sửa, danh sách ở `NoteListView` cũng được cập nhật.
*   **`Identifiable` Protocol:** Mô hình `Note` sẽ tuân thủ (conform) theo protocol này để `List` có thể xác định duy nhất từng phần tử, giúp việc cập nhật giao diện hiệu quả hơn.
*   **`ObservableObject` & `@StateObject` / `@ObservedObject`:** Dùng để tạo ra một nguồn dữ liệu phức tạp hơn có thể được chia sẻ giữa nhiều View.
    *   `NoteStore` sẽ là một `class` tuân thủ `ObservableObject`.
    *   `@StateObject` được dùng để tạo và giữ cho instance của `NoteStore` tồn tại trong suốt vòng đời của View chứa nó.
    *   `@ObservedObject` được dùng ở các View con để "lắng nghe" sự thay đổi từ `NoteStore`.

#### 3. Nâng cao hơn một chút
*   **Data Persistence:** Sử dụng `Codable` protocol để mã hóa (encode) danh sách ghi chú thành dữ liệu JSON và giải mã (decode) ngược lại. Dữ liệu này có thể được lưu vào `UserDefaults` hoặc một file trong bộ nhớ của ứng dụng để đảm bảo dữ liệu không bị mất khi đóng ứng dụng.
*   **Computed Properties:** Sử dụng các thuộc tính tính toán trong View để xử lý logic hiển thị. Ví dụ: một thuộc tính để quyết định màu sắc của ghi chú dựa trên ngày nhắc nhở (sắp tới, đã quá hạn, hay bình thường).

## 📁 Cấu trúc thư mục

```
GhiChuApp/
├── Data Models/
│   ├── Note.swift
│   └── NoteStore.swift
│
├── Views/
│   ├── NoteListView.swift
│   └── NoteDetailView.swift
│
├── Components/
│   └── NoteRowView.swift
│
├── App/
│   ├── GhiChuAppApp.swift
│   └── Assets.xcassets
│
└── Preview Content/
    └── Preview Assets.xcassets
```
