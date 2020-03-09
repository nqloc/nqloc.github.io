---
layout: post
title: Redis là gì
category: Redis
tags: [Redis]
active: true
language: vi
---

> Redis là 1 hệ thống lưu trữ key-value rất mạnh mẽ và phổ biến hiện nay.

> Redis nổi bật bởi việc hỗ trợ nhiều cấu trúc dữ liệu cơ bản(hash, list, set, sorted set, string), giúp việc thao tác với dữ liệu tốt hơn các hệ thống cũ như memcached rất nhiều.

> Bên cạnh lưu trữ key-value trên RAM giúp tối ưu performance, redis còn có cơ chế sao lưu dữ liệu trên đĩa cứng cho phép phục hồi dữ liệu khi gặp sự cố.

## Khái quát

Bạn có thể clone mã nguồn redis về máy tính mình bằng câu lệnh dưới đây:

git clone https://github.com/antirez/redis.git

Bộ nhớ sử dụng:

Mặc định là mất ~ 1MB

1M small keys -> String value sử dụng ~ 100MB

1M Keys -> Hash value, lưu trữ 5 trường dữ liệu, sử dụng ~ 200MB

## Các modules

Redis bao gồm các module sau:

Framework hỗ trợ xử lý bất đồng bộ, networking: ae, anet

Mô tả dữ liệu: sds.c, t_hash.c, t_list.c, t_string.c, t_zset.c, object.c, notify.c (pub-sub)

Lưu trữ dữ liệu, cơ sở dữ liệu: db.c, dict.c, ziplist.c, zipmap.c, adlist.c

Module hỗ trợ IO/persistent redis: rdb.c, aof.c, bio.c, rio.c

Utilities: crc16.c, crc64.c, pqsort.c, lzf_c.c, lzf_d.c

## Persistent redis

Bên cạnh việc lưu key-value trên bộ nhớ RAM, Redis có 2 background threads chuyên làm nhiệm vụ định kỳ ghi dữ liệu lên đĩa cứng.

Có 2 loại file được ghi xuống đĩa cứng:

**RDB (Redis DataBase file)** Cách thức làm việc RDB thực hiện tạo và sao lưu snapshot của DB vào ổ cứng sau mỗi khoảng thời gian nhất định.

Ưu điểm

RDB cho phép người dùng lưu các version khác nhau của DB, rất thuận tiện khi có sự cố xảy ra. Bằng việc lưu trữ data vào 1 file cố định, người dùng có thể dễ dàng chuyển data đến các data centers, máy chủ khác nhau. RDB giúp tối ưu hóa hiệu năng của Redis. Tiến trình Redis chính sẽ chỉ làm các công việc trên RAM, bao gồm các thao tác cơ bản được yêu cầu từ phía client như thêm/đọc/xóa, trong khi đó 1 tiến trình con sẽ đảm nhiệm các thao tác disk I/O. Cách tổ chức này giúp tối đa hiệu năng của Redis. Khi restart server, dùng RDB làm việc với lượng data lớn sẽ có tốc độ cao hơn là dùng AOF.

Nhược điểm

RDB không phải là lựa chọn tốt nếu bạn muốn giảm thiểu tối đa nguy cơ mất mát dữ liệu. Thông thường người dùng sẽ set up để tạo RDB snapshot 5 phút 1 lần (hoặc nhiều hơn). Do vậy, trong trường hợp có sự cố, Redis không thể hoạt động, dữ liệu trong những phút cuối sẽ bị mất. RDB cần dùng fork() để tạo tiến trình con phục vụ cho thao tác disk I/O. Trong trường hợp dữ liệu quá lớn, quá trình fork() có thể tốn thời gian và server sẽ không thể đáp ứng được request từ client trong vài milisecond hoặc thậm chí là 1 second tùy thuộc vào lượng data và hiệu năng CPU.

**AOF (Append Only File)** Cách thức làm việc AOF lưu lại tất cả các thao tác write mà server nhận được, các thao tác này sẽ được chạy lại khi restart server hoặc tái thiết lập dataset ban đầu.

Ưu điểm

Sử dụng AOF sẽ giúp đảm bảo dataset được bền vững hơn so với dùng RDB. Người dùng có thể config để Redis ghi log theo từng câu query hoặc mỗi giây 1 lần. Redis ghi log AOF theo kiểu thêm vào cuối file sẵn có, do đó tiến trình seek trên file có sẵn là không cần thiết. Ngoài ra, kể cả khi chỉ 1 nửa câu lệnh được ghi trong file log (có thể do ổ đĩa bị full), Redis vẫn có cơ chế quản lý và sửa chữa lối đó (redis-check-aof). Redis cung cấp tiến trình chạy nền, cho phép ghi lại file AOF khi dung lượng file quá lớn. Trong khi server vẫn thực hiện thao tác trên file cũ, 1 file hoàn toàn mới được tạo ra với số lượng tối thiểu operation phục vụ cho việc tạo dataset hiện tại. Và 1 khi file mới được ghi xong, Redis sẽ chuyển sang thực hiện thao tác ghi log trên file mới.

Nhược điểm

File AOF thường lớn hơn file RDB với cùng 1 dataset. AOF có thể chậm hơn RDB tùy theo cách thức thiết lập khoảng thời gian cho việc sao lưu vào ổ cứng. Tuy nhiên, nếu thiết lập log 1 giây 1 lần có thể đạt hiệu năng tương đương với RDB. Developer của Redis đã từng gặp phải bug với AOF (mặc dù là rất hiếm), đó là lỗi AOF không thể tái tạo lại chính xác dataset khi restart Redis. Lỗi này chưa gặp phải khi làm việc với RDB bao giờ.

## Data model

Khác với RDMS như MySQL, hay PostgreSQL, Redis không có table (bảng). Redis lưu trữ data dưới dạng key-value. Thực tế thì memcache cũng làm vậy, nhưng kiểu dữ liệu của memcache bị hạn chế, không đa dạng được như Redis, do đó không hỗ trợ được nhiều thao tác từ phía người dùng. Dưới đây là sơ lược về các kiểu dữ liệu Redis dùng để lưu value.

**STRING**: Có thể là string, integer hoặc float. Redis có thể làm việc với cả string, từng phần của string, cũng như tăng/giảm giá trị của integer, float.

**LIST**: Danh sách liên kết của các strings. Redis hỗ trợ các thao tác push, pop từ cả 2 phía của list, trim dựa theo offset, đọc 1 hoặc nhiều items của list, tìm kiếm và xóa giá trị.

**SET**: Tập hợp các string (không được sắp xếp). Redis hỗ trợ các thao tác thêm, đọc, xóa từng phần tử, kiểm tra sự xuất hiện của phần tử trong tập hợp. Ngoài ra Redis còn hỗ trợ các phép toán tập hợp, gồm intersect/union/difference.

**HASH**: Lưu trữ hash table của các cặp key-value, trong đó key được sắp xếp ngẫu nhiên, không theo thứ tự nào cả. Redis hỗ trợ các thao tác thêm, đọc, xóa từng phần tử, cũng như đọc tất cả giá trị.

**ZSET (sorted set)**: Là 1 danh sách, trong đó mỗi phần tử là map của 1 string (member) và 1 floating-point number (score), danh sách được sắp xếp theo score này. Redis hỗ trợ thao tác thêm, đọc, xóa từng phần tử, lấy ra các phần tử dựa theo range của score hoặc của string.

![](/images/posts/redis/redis-data-structure-types.jpeg)

## Kết luận

Redis là một sự lựa chọn tuyệt vời khi ta cần đến một server lưu trữ dữ liệu đòi hỏi tính mở rộng cao (scaleable) và chia sẻ bởi nhiều tiến trình, nhiều ứng dụng và nhiều server khác nhau. Chỉ riêng cơ chế tương tác giữa các tiến trình đã cực kỳ khó nhằn rồi. Do đó việc ta có thể tương tác cross-platform, cross-server, và cross-application đã làm Redis trở thành một lựa chọn đúng đắn cho rất rất nhiều công việc khác nhau. Tốc độ cực cao của Redis cũng có thể được lợi dụng để làm caching layer

