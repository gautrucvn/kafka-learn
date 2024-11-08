# Apache Kafka là gì ?

Apache Kafka là hệ thống phân tán mã nguồn mở bao gồm máy chủ và máy khách được sử dụng chủ yếu để xây dựng các data streaming pipeline thời gian thực.

## Thách thức tích hợp dữ liệu

Các tổ chức thường có nhiều nguồn dữ liệu với định dạng khác nhau, từ các ứng dụng như kế toán, thanh toán, CRM, v.v. Việc tích hợp dữ liệu từ các nguồn này gặp nhiều thách thức như giao thức truyền tải, định dạng và lược đồ dữ liệu, dễ dẫn đến sự phức tạp.

Apache Kafka giúp đơn giản hóa quá trình này bằng cách đóng vai trò lớp tích hợp dữ liệu. Các nguồn dữ liệu gửi dữ liệu đến Kafka, và các hệ thống đích lấy dữ liệu từ đó, giúp tách rời và giảm phức tạp trong tích hợp dữ liệu.

![thách thức tích hợp dữ liệu](/images/kafka-01.png)

### Data Stream trong kafka là gì ?

Trong Apache Kafka, data streaming là một chuỗi dữ liệu không giới hạn, có thể truy cập ngay khi được tạo. Mỗi ứng dụng trong tổ chức có thể tạo ra một data streaming riêng với lưu lượng biến động, từ hàng nghìn bản ghi mỗi giây đến chỉ một vài bản ghi mỗi giờ.

Apache Kafka lưu trữ các data streaming này dưới dạng topics, cho phép xử lý dòng – tức là xử lý dữ liệu liên tục và theo thời gian thực. Sau khi được xử lý và lưu trong Kafka, dữ liệu có thể được chuyển sang các hệ thống khác như cơ sở dữ liệu. Kafka giúp tạo ra một đường dẫn dữ liệu theo thời gian thực, có khả năng xử lý hàng triệu sự kiện mỗi giây từ nhiều ứng dụng kinh doanh khác nhau.

![What is a data stream in Apache Kafka](/images/kafka-02.png)

### Ví dụ về Data Stream

Phân tích nhật ký (Log Analysis): Các ứng dụng hiện đại gồm hàng chục đến hàng nghìn microservices, tất cả đều tạo ra nhật ký (logs). Nhật ký chứa nhiều thông tin có thể khai thác cho phân tích kinh doanh, dự đoán lỗi và gỡ lỗi. Các công ty đưa dữ liệu nhật ký vào một dòng dữ liệu để xử lý liên tục.

Phân tích web (Web Analytics): Các ứng dụng web hiện đại theo dõi hầu hết các hoạt động của người dùng, như nhấp chuột và lượt xem trang. Các hoạt động này tăng lên nhanh chóng. Xử lý dòng dữ liệu giúp các công ty xử lý dữ liệu ngay khi được tạo ra thay vì chờ hàng giờ sau đó.

### Apache Kafka có nhiều trường hợp sử dụng, bao gồm:

Hệ thống nhắn tin (Messaging Systems)
Theo dõi hoạt động (Activity Tracking)
Thu thập số liệu từ nhiều nguồn: Chẳng hạn, thu thập dữ liệu từ các thiết bị IoT phân tán.
Phân tích nhật ký ứng dụng (Application Logs Analysis): Thu thập và phân tích nhật ký từ các ứng dụng để giám sát và gỡ lỗi.
Tách rời các phụ thuộc hệ thống: Kafka cho phép các hệ thống không phụ thuộc trực tiếp vào nhau, tăng khả năng mở rộng và bảo trì.
Tích hợp với công nghệ Big Data: Kết hợp với Spark, Flink, Storm, Hadoop để xử lý và phân tích dữ liệu lớn.
Kho lưu trữ dựa trên sự kiện (Event Sourcing Store): Lưu trữ các sự kiện để xử lý sau này.
Apache Kafka là nền tảng lưu trữ quan trọng cho nhiều framework xử lý dòng dữ liệu như Apache Flink và Samza.

### Apache Kafka không phải là lựa chọn lý tưởng cho một số trường hợp sau:

Proxy cho hàng triệu thiết bị di động hoặc IoT: Giao thức Kafka không được thiết kế để phục vụ trực tiếp lượng lớn các thiết bị, mặc dù có một số proxy giúp kết nối.
Cơ sở dữ liệu với chỉ mục: Kafka là hệ thống nhật ký sự kiện, không có khả năng phân tích tích hợp sẵn hoặc mô hình truy vấn phức tạp như một cơ sở dữ liệu.
Công nghệ nhúng thời gian thực cho IoT: Các hệ thống nhúng có thể sử dụng những giải pháp nhẹ và cấp thấp hơn phù hợp hơn Kafka.
Hàng đợi công việc (Work Queues): Kafka sử dụng topics chứ không phải hàng đợi (queues) như RabbitMQ hay SQS. Kafka không tự động xóa dữ liệu sau khi xử lý, và số lượng consumer không thể vượt quá số phân vùng trong một topic.
Blockchain: Kafka có một số đặc điểm giống blockchain (dữ liệu có thể là bất biến), nhưng thiếu các tính năng quan trọng như xác minh mật mã và bảo toàn bộ lịch sử.

## Định nghĩa các khái niệm cốt lõi của Apache Kafka

![producer, topic and consumer](/images/kafka-03.png)

### Kafka Topic

Trong Apache Kafka, topic giúp tổ chức các sự kiện liên quan. Ví dụ, một topic có tên "logs" có thể chứa các bản ghi (logs) từ một ứng dụng. topic có thể xem tương tự như các bảng trong SQL, nhưng không thể truy vấn trực tiếp. Thay vào đó, cần tạo các Kafka producer và consumer để sử dụng dữ liệu.

Dữ liệu trong các topic được lưu trữ dưới dạng cặp khóa-giá trị (key-value) và ở định dạng nhị phân.

Tìm hiểu thêm tại [Kafka Topics, Partitions & Offsets](/docs/kafka-topics.md)

### Kafka Producer

Kafka Producer là các ứng dụng gửi dữ liệu vào một topic trong Kafka. Khi một topic được tạo ra, bước tiếp theo là gửi dữ liệu vào topic đó. Các ứng dụng này được gọi là Kafka producers.

Có nhiều cách để tạo sự kiện (events) trong Kafka, nhưng thông thường, các ứng dụng sẽ tích hợp với các thư viện khách hàng (client libraries) của Kafka bằng các ngôn ngữ như Java, Python, Go, và nhiều ngôn ngữ khác.

Cần lưu ý rằng Kafka producers được triển khai bên ngoài Kafka và chỉ tương tác với Apache Kafka bằng cách gửi dữ liệu trực tiếp vào các topic của Kafka.

Tìm hiểu thêm tại [Kafka Producers.](/docs/kafka-producers.md)

### Kafka Consumer

Sau khi một topic được tạo và dữ liệu được gửi vào đó, các ứng dụng có thể tiêu thụ dữ liệu từ topic này. Những ứng dụng kéo dữ liệu sự kiện từ một hoặc nhiều topic Kafka được gọi là Kafka consumers.

**Cách Hoạt Động của Kafka Consumers**
**Tiêu thụ sự kiện:** Kafka consumers đọc dữ liệu từ một hoặc nhiều topic Kafka.
**Client Libraries:** Các ứng dụng thường tích hợp các thư viện client Kafka bằng nhiều ngôn ngữ phổ biến như Java, Python, Go, v.v., để dễ dàng tương tác với Kafka.
**Tiêu thụ theo thời gian thực:** Theo mặc định, consumer chỉ tiêu thụ dữ liệu được tạo ra sau khi consumer kết nối lần đầu với topic. Điều này có nghĩa là consumer sẽ không đọc lại các sự kiện cũ trừ khi cấu hình lại để làm như vậy.

**Đặc điểm của Kafka Consumers**
**Độc lập với Kafka Broker:** Consumers được triển khai bên ngoài hệ thống Kafka và chỉ tương tác với Kafka bằng cách đọc dữ liệu trực tiếp từ các topic.
**Duy trì Offset:** Mỗi Kafka consumer lưu trữ một offset để theo dõi vị trí trong một phân vùng, giúp đảm bảo rằng không có sự kiện nào bị bỏ sót hoặc bị đọc lại trừ khi được yêu cầu.

Kafka consumers là thành phần chính trong việc tạo ra các ứng dụng luồng dữ liệu thời gian thực, từ việc xử lý dữ liệu log, phân tích hành vi người dùng, đến tích hợp dữ liệu lớn và các hệ thống sự kiện.

Tìm hiểu thêm tại [Kafka Consumers.](/docs/kafka-consumers.md)

## The Kafka Ecosystem

Apache Kafka hiện nay không chỉ là một hệ thống truyền message, mà đã phát triển thành một hệ sinh thái phong phú với các công cụ và thư viện bổ trợ, cho phép xử lý và truyền tải dữ liệu phức tạp hơn. Dưới đây là một số thành phần nổi bật trong hệ sinh thái Kafka:

1. **Kafka Connect**

   - **Mục đích**: Kafka Connect đơn giản hóa việc tích hợp dữ liệu từ các nguồn bên ngoài vào Kafka.
   - **Cách sử dụng**: Kafka Connect cung cấp khung làm việc để kết nối Kafka với các nguồn dữ liệu và bến đỗ dữ liệu, như cơ sở dữ liệu, lưu trữ đám mây, giúp nhập và xuất dữ liệu một cách hiệu quả.
   - **Lợi ích**: Có nhiều bộ kết nối dựng sẵn, giúp dễ dàng đưa dữ liệu từ nhiều nguồn vào Kafka mà không cần viết mã tuỳ chỉnh.
     ![Kafka Connect](/images/kafka-15.png)

2. **Kafka Streams**

   - **Mục đích**: Kafka Streams là một thư viện nhẹ để xử lý dữ liệu thời gian thực trong Kafka.
   - **Cách sử dụng**: Cho phép các ứng dụng thực hiện tính toán trên dữ liệu trong các topic Kafka và lưu kết quả trở lại Kafka.
   - **Lợi ích**: Là thư viện khách, Kafka Streams không yêu cầu cụm xử lý riêng, thuận tiện cho việc triển khai trong các dịch vụ microservices và các ứng dụng khác.
     ![Kafka Streams](/images/kafka-14.png)

3. **KSQL (Kafka SQL)**

   - **Mục đích**: KSQL cung cấp giao diện giống SQL cho Kafka Streams.
   - **Cách sử dụng**: Cho phép người dùng truy vấn và xử lý dữ liệu trong Kafka bằng các câu lệnh SQL.
   - **Lợi ích**: KSQL đơn giản hóa việc xử lý luồng dữ liệu, giúp những ai quen thuộc với SQL dễ dàng thao tác với dữ liệu thời gian thực và thực hiện các phân tích, biến đổi.

4. **Schema Registry**

   - **Mục đích**: Quản lý và kiểm soát các schema (lược đồ) dữ liệu cho các topic Kafka.
   - **Cách sử dụng**: Đảm bảo tính tương thích giữa các nhà sản xuất và người tiêu dùng dữ liệu, đặc biệt cho các định dạng như Avro, JSON Schema, và Protobuf.
   - **Lợi ích**: Ngăn ngừa sự không nhất quán trong dữ liệu và đơn giản hóa việc quản lý các lược đồ dữ liệu đang phát triển trong các topic Kafka.

5. **ZooKeeper**

   - **Mục đích**: Ban đầu được sử dụng để quản lý metadata, cấu hình và điều phối các broker của Kafka.
   - **Cách sử dụng**: Dù Kafka đang chuyển sang chế độ tự quản lý không cần ZooKeeper, nhưng ZooKeeper vẫn được yêu cầu trong nhiều triển khai Kafka hiện nay.
   - **Lợi ích**: Cung cấp khả năng chịu lỗi và quản lý các hoạt động quan trọng như bầu chọn lãnh đạo giữa các broker.

6. **MirrorMaker**
   - **Mục đích**: Hỗ trợ sao chép dữ liệu giữa các cụm Kafka.
   - **Cách sử dụng**: MirrorMaker được dùng cho việc khôi phục dữ liệu khi có thảm họa, tạo bản sao dữ liệu tại các vị trí địa lý khác nhau hoặc duy trì dữ liệu giống nhau trên nhiều cụm.
   - **Lợi ích**: Giúp xây dựng các kiến trúc chịu lỗi và có tính sẵn sàng cao bằng cách sao chép dữ liệu Kafka qua các vùng hoặc trung tâm dữ liệu.

Những công cụ này giúp mở rộng đáng kể khả năng của Kafka, biến nó không chỉ là một hệ thống truyền tải thông điệp mà còn thành một nền tảng toàn diện cho tích hợp dữ liệu thời gian thực, xử lý luồng dữ liệu và phân tích. Điều này cho phép các tổ chức sử dụng Kafka cho nhiều ứng dụng khác nhau, từ xây dựng luồng dữ liệu đến hệ thống ra quyết định thời gian thực.

# Các thành phần trong Apache Kafka

Chúng ta đã tìm hiểu về luồng sự kiện dữ liệu, Apache Kafka và các thành phần khác nhau của nó ở cấp độ cao.
Bây giờ, chúng ta sẽ đi sâu và tìm hiểu cách thức hoạt động của từng phần của Apache Kafka.

![Apache Kafka Components](/images/kafka-16.png)

- [**Kafka Consumer Groups & Offsets.**](/docs/kafka-consumer-groups-and-consumer-offsets.md)
- [**Kafka Brokers.**](/docs/kafka-brokers.md)
- [**Kafka Topic Replication.**](/docs/kafka-topic-replication.md)
- [**Zookeeper with Kafka.**](/docs/zookeeper-with-kafka.md)
- [**Kafka KRaft Mode.**](/docs/kafka-kraft-mode.md)
