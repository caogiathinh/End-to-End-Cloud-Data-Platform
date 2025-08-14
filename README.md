# DE-NYC-Taxi: Nền tảng Dữ liệu Hiện đại cho Phân tích Vận tải Đô thị

![Tech Stack Banner](https://user-images.githubusercontent.com/875246/185756770-519a4a3c-531e-4209-9b93-a3344b1c7ba1.png)

Dự án này xây dựng một nền tảng dữ liệu end-to-end, có khả năng mở rộng và tự động hóa, nhằm giải quyết các bài toán phân tích nghiệp vụ và hoạch định chiến lược cho ngành vận tải đô thị tại New York, dựa trên bộ dữ liệu công khai của Ủy ban Taxi và Limousine (TLC).

---

## 1. Bối cảnh & Thách thức (The Problem)

Ngành vận tải đô thị tại New York đang phải đối mặt với những thách thức phức tạp, ảnh hưởng đến cả nhà quản lý (TLC), tài xế và hành khách:

*   **Tắc nghẽn nghiêm trọng:** Một người dân New York mất trung bình **117 giờ mỗi năm** vì kẹt xe, làm giảm hiệu suất của tài xế, tăng chi phí nhiên liệu và ảnh hưởng trực tiếp đến thu nhập.
*   **Thay đổi mô hình nhu cầu (Hậu COVID-19):** Mô hình làm việc hybrid/remote đã làm thay đổi các "điểm nóng" và "giờ cao điểm" truyền thống, khiến các mô hình dự báo cũ trở nên vô giá trị.
*   **Cạnh tranh khốc liệt từ Xe Công nghệ (FHVs):** Sự trỗi dậy của Uber, Lyft với **50,000+ xe** đã phá vỡ thị trường taxi truyền thống (chỉ có ~13,500 taxi vàng), gây ra cuộc khủng hoảng về giá trị huy hiệu taxi và đẩy hàng ngàn tài xế vào cảnh nợ nần.
*   **Phản ứng chậm của nhà quản lý:** TLC thiếu một hệ thống phân tích dữ liệu hiện đại để có cái nhìn toàn cảnh, kịp thời về thị trường. Các quyết định điều tiết (như chính sách định giá tắc nghẽn) cần dữ liệu để đánh giá hiệu quả một cách chính xác.

**Vấn đề cốt lõi:** Sự thiếu hụt một nền tảng dữ liệu tập trung, mạnh mẽ đã khiến các bên liên quan hoạt động với thông tin rời rạc, dẫn đến hiệu quả kinh doanh thấp và khả năng quản lý bị hạn chế.

## 2. Giải pháp & Mục tiêu (The Solution)

Để giải quyết các thách thức trên, dự án này triển khai một **nền tảng dữ liệu hiện đại (Modern Data Platform)** với các mục tiêu chính:

*   **Về mặt Kỹ thuật:**
    1.  **Xây dựng một đường ống dữ liệu (Data Pipeline) hoàn chỉnh và tự động:** Tự động thu thập, làm sạch, biến đổi và nạp dữ liệu hàng tháng.
    2.  **Đảm bảo chất lượng dữ liệu:** Tích hợp các bài kiểm thử tự động (data testing) trong suốt pipeline để đảm bảo dữ liệu luôn chính xác và đáng tin cậy.
    3.  **Tối ưu hóa hiệu năng và khả năng mở rộng:** Sử dụng các công nghệ và kiến trúc có khả năng xử lý lượng dữ liệu tăng thêm 50% mà không cần thay đổi lớn về thiết kế.

*   **Về mặt Nghiệp vụ:**
    1.  **Tối ưu hóa Vận hành:** Cung cấp các báo cáo tương tác để xác định các "điểm nóng" về nhu cầu theo không gian và thời gian.
    2.  **Đo lường Hiệu suất Kinh doanh (KPIs):** Xây dựng các dashboard quản trị để theo dõi các chỉ số cốt lõi như tổng doanh thu, số chuyến đi, thu nhập tài xế.
    3.  **Tạo sân chơi công bằng:** Cung cấp cho TLC năng lực giám sát và điều tiết thị trường dựa trên dữ liệu, giúp cân bằng cạnh tranh giữa taxi truyền thống và xe công nghệ.

## 3. Kiến trúc hệ thống (System Architecture)

Dự án áp dụng kiến trúc **ELT (Extract - Load - Transform)** trên nền tảng cloud, với các thành phần được container hóa để đảm bảo tính nhất quán và khả năng tái lập.



### Tech Stack

| Tầng (Layer)          | Công nghệ                                                               | Vai trò                                                                                                    |
| --------------------- | ----------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **Containerization**  | <img src="https://img.shields.io/badge/Docker-2496ED?logo=docker" />    | Đóng gói ứng dụng và phụ thuộc, đảm bảo môi trường nhất quán từ local đến production.                     |
| **Infrastructure**    | <img src="https://img.shields.io/badge/Terraform-7B42BC?logo=terraform" /> | Quản lý hạ tầng dưới dạng mã (Infrastructure as Code), tự động tạo tài nguyên trên GCP.                  |
| **Data Lake**         | <img src="https://img.shields.io/badge/Google_Cloud_Storage-4285F4?logo=google-cloud" /> | Lưu trữ dữ liệu thô (raw data) với chi phí thấp và khả năng mở rộng gần như vô hạn.                       |
| **Data Warehouse**    | <img src="https://img.shields.io/badge/Google_BigQuery-669DF6?logo=google-bigquery" /> | Kho dữ liệu serverless, hiệu năng cao, tối ưu cho các truy vấn phân tích (OLAP).                           |
| **Transformation**    | <img src="https://img.shields.io/badge/Apache_Spark-E25A1C?logo=apache-spark" /> <img src="https://img.shields.io/badge/dbt-FF694B?logo=dbt" /> | **Spark:** Xử lý dữ liệu thô từ Data Lake. <br/> **dbt:** Biến đổi dữ liệu theo logic nghiệp vụ bên trong BigQuery. |
| **Data Orchestration**| <img src="https://img.shields.io/badge/Kestra-E157F8" />                 | "Nhạc trưởng" điều phối, lập lịch và giám sát toàn bộ pipeline dữ liệu.                                   |
| **Data Testing**      | <img src="https://img.shields.io/badge/dbt-FF694B?logo=dbt" />           | Tích hợp kiểm thử chất lượng dữ liệu (schema, referential integrity, business logic).                     |
| **Data Visualization**| <img src="https://img.shields.io/badge/Looker_Studio-4285F4?logo=looker" /> | Xây dựng các báo cáo và dashboard tương tác để phục vụ người dùng cuối.                                    |

## 4. Mô hình Dữ liệu (Data Model)

Hệ thống triển khai mô hình **Star Schema** trong Data Warehouse (BigQuery) để tối ưu cho các truy vấn phân tích. Mô hình bao gồm một bảng Fact trung tâm (`fct_trips`) và nhiều bảng Dimension xung quanh.



*   **Bảng Fact:** `fct_trips` chứa các chỉ số định lượng của mỗi chuyến đi (ví dụ: `trip_distance`, `total_amount`).
*   **Bảng Dimension:** `dim_datetime`, `dim_locations`, `dim_payment_types`,... cung cấp ngữ cảnh cho dữ liệu trong bảng Fact.

Thiết kế này được tối ưu hiệu năng bằng cách **Partition** bảng Fact theo ngày (`pickup_datetime`) và **Cluster** theo các cột thường được lọc (`service_type`, `pickup_location_id`).

## 5. Cấu trúc dự án

Dự án được tổ chức theo cấu trúc monorepo, nơi mỗi thư mục có một vai trò rõ ràng:
