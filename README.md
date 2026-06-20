# jmeter-performance-testing
# Báo cáo thực hành kiểm thử hiệu năng với Apache JMeter

## 1. Thông tin sinh viên

* Họ và tên: Đỗ Trịnh Lệ Quyên
* Mã sinh viên: 23010485
* Lớp: K17-KTPMEL2 
* Môn học: Đánh giá và kiểm định chất lượng kiểm định
* Chủ đề: Học công cụ kiểm thử Apache JMeter và thực hiện kiểm thử hiệu năng website Wikipedia

---

## 2. Mục tiêu bài thực hành

Bài thực hành nhằm tìm hiểu và sử dụng công cụ Apache JMeter để kiểm thử hiệu năng của một website Wikipedia.
Thông qua bài thực hành, sinh viên có thể:

* Hiểu được chức năng cơ bản của Apache JMeter.
* Biết cách tạo một Test Plan trong JMeter.
* Biết cách cấu hình Thread Group để mô phỏng nhiều người dùng truy cập hệ thống.
* Biết cách tạo HTTP Request để gửi yêu cầu đến website cần kiểm thử.
* Biết cách xem và phân tích kết quả kiểm thử thông qua View Results Tree, Summary Report và Aggregate Report.
* Biết cách lưu sản phẩm thực hành và báo cáo trên GitHub.

---

## 3. Giới thiệu về Apache JMeter

Apache JMeter là một công cụ mã nguồn mở được sử dụng phổ biến trong kiểm thử hiệu năng, kiểm thử tải và kiểm thử khả năng chịu tải của hệ thống. Công cụ này cho phép mô phỏng nhiều người dùng cùng truy cập vào một website, API hoặc dịch vụ để đánh giá khả năng phản hồi của hệ thống.

Một số thành phần chính trong JMeter gồm:

| Thành phần       | Mô tả                                       |
| ---------------- | ------------------------------------------- |
| Test Plan        | Kế hoạch kiểm thử tổng thể                  |
| Thread Group     | Nhóm người dùng ảo được mô phỏng            |
| Sampler          | Thành phần gửi request đến hệ thống         |
| HTTP Request     | Gửi request HTTP/HTTPS đến website hoặc API |
| Listener         | Hiển thị và tổng hợp kết quả kiểm thử       |
| Summary Report   | Báo cáo tổng hợp kết quả kiểm thử           |
| Aggregate Report | Báo cáo thống kê chi tiết hơn về hiệu năng  |

---

## 4. Công cụ và môi trường thực hiện

* Hệ điều hành: Windows
* Công cụ kiểm thử: Apache JMeter
* Java: JDK 8 trở lên
* Trình duyệt: Google Chrome
* Nền tảng nộp bài: GitHub

---

## 5. Kịch bản kiểm thử

Website được chọn để kiểm thử:

```text
https://www.wikipedia.org
```

Mục tiêu kiểm thử:

* Gửi request GET đến trang chủ website.
* Mô phỏng nhiều người dùng truy cập cùng lúc.
* Ghi nhận thời gian phản hồi, số lượng request thành công, lỗi và throughput.

Cấu hình kiểm thử:

| Thông số                | Giá trị |
| ----------------------- | ------- |
| Number of Threads       | 5       |
| Ramp-up Period          | 5 giây  |
| Loop Count              | 2       |
| Tổng số request dự kiến | 10      |

---

## 6. Các bước thực hiện

### Bước 1: Cài đặt và mở Apache JMeter

Sau khi tải Apache JMeter, giải nén thư mục và mở file:

```text
bin/jmeter.bat
```

Ảnh minh họa:

---

### Bước 2: Tạo Test Plan

Trong JMeter, tạo một Test Plan mới để quản lý toàn bộ kịch bản kiểm thử.

Ảnh minh họa:

---

### Bước 3: Tạo Thread Group

Thêm Thread Group vào Test Plan:

```text
Test Plan → Add → Threads (Users) → Thread Group
```

Cấu hình Thread Group:

* Number of Threads: 5
* Ramp-up Period: 5
* Loop Count: 2

Thread Group giúp mô phỏng số lượng người dùng ảo truy cập vào hệ thống.

---

### Bước 4: Tạo HTTP Request

Thêm HTTP Request:

```text
Thread Group → Add → Sampler → HTTP Request
```

Cấu hình HTTP Request:

| Trường      | Giá trị     |
| ----------- | ----------- |
| Protocol    | https       |
| Server Name | example.com |
| Method      | GET         |
| Path        | /           |

Ảnh minh họa:

---

### Bước 5: Thêm Listener để xem kết quả

Thêm các Listener sau:

```text
Thread Group → Add → Listener → View Results Tree
Thread Group → Add → Listener → Summary Report
Thread Group → Add → Listener → Aggregate Report
```

Các Listener giúp hiển thị kết quả kiểm thử sau khi chạy Test Plan.

---

### Bước 6: Chạy kiểm thử

Nhấn nút Start để chạy kiểm thử. Sau khi chạy xong, xem kết quả trong các Listener.

Ảnh View Results Tree:

Ảnh Summary Report:

---

## 7. Kết quả kiểm thử

Kết quả kiểm thử thu được:

| Chỉ số     | Ý nghĩa                                     | Kết quả            |
| ---------- | ------------------------------------------- | ------------------ |
| Samples    | Tổng số request đã gửi                      | 10                 |
| Average    | Thời gian phản hồi trung bình               | 127 ms             |
| Min        | Thời gian phản hồi nhỏ nhất                 | 56 ms              |
| Max        | Thời gian phản hồi lớn nhất                 | 207 ms             |
| Error %    | Tỷ lệ request lỗi                           | 100 %              |
| Throughput | Số request xử lý trong một đơn vị thời gian | 2.4 request/second |

Nhận xét:

* Hệ thống phản hồi được các request do JMeter gửi đến.
* Nếu Error % bằng 100%, các request chưa được xử lý thành công.
* Thời gian phản hồi trung bình cho biết tốc độ phản hồi của website.
* Throughput càng cao thì khả năng xử lý request của hệ thống càng tốt.

---

## 8. Nhận xét và đánh giá

Qua bài thực hành, em đã hiểu được cách sử dụng cơ bản công cụ Apache JMeter trong kiểm thử hiệu năng. Em đã biết cách tạo Test Plan, cấu hình Thread Group, tạo HTTP Request và xem kết quả kiểm thử bằng các Listener.

Apache JMeter là công cụ hữu ích trong kiểm thử phần mềm, đặc biệt là kiểm thử hiệu năng website, API và các hệ thống web. Công cụ này giúp đánh giá khả năng phản hồi của hệ thống khi có nhiều người dùng truy cập cùng lúc.

---

## 9. Kết luận

Bài thực hành đã giúp em nắm được quy trình cơ bản khi sử dụng Apache JMeter để kiểm thử hiệu năng. Kết quả kiểm thử cho thấy JMeter có thể mô phỏng nhiều người dùng ảo, gửi request đến website và thống kê các chỉ số quan trọng như thời gian phản hồi, tỷ lệ lỗi và throughput.

Thông qua việc tạo GitHub Repo và viết báo cáo trong file README.md, em cũng biết cách lưu trữ, trình bày và nộp sản phẩm thực hành một cách rõ ràng, khoa học.

---

## 10. Tài liệu tham khảo

* Apache JMeter Official Website
* Apache JMeter User Manual
* Apache JMeter Getting Started Guide
