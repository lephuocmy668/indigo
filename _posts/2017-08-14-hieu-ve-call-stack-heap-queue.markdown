---
title: 'Hiểu Về Call Stack - Heap - Queue'
layout: post
date: 2017-08-14 12:45
image: /assets/images/
headerImage: false
tag:
    - solid
    - ood
    - oop
category: blog
author: Le Phuoc My
description: Markdown summary with different options
# jemoji: '<img class="emoji" title=":ramen:" alt=":ramen:" src="https://assets.github.com/images/icons/emoji/unicode/1f35c.png" height="20" width="20" align="absmiddle">'
---

## 1. Stack:

Ứng với mỗi thread (hoặc 1 goruntine đối với Golang) của chương trình thường có một call stack. Khi ứng dụng bắt đầu được thực thi, các biến cục bộ, địa chỉ hàm, biến tham chiếu đối tượng....sẻ được lưu trữ trong Stack, tùy theo thứ tự gọi mà các thành phần đẩy vào stack được sắp xếp theo đúng thứ tự.
Khi 1 phương thức kết thúc cũng là lúc các giá trị biến và các tham chiếu đối tương được hủy bỏ — và địa chỉ hàm cũng được hủy bỏ ngay sau đó. Stack lưu trữ dung lượng thấp hơn rất nhiều so với heap.

Khi lập trình với các ngôn ngữ như Java, Golang... chúng ta thường quan tâm đến stack size. Với Java trong môi trường 64-bit thì JVM mặc định có stack size cho mỗi thread là 1MB và Golang thì mặc định là 2kb.

Trong Javascript, Golang và đa số các ngôn ngữ lập trình khác, khi chúng ta gọi một hàm để thực thi đồng nghĩa với việc chúng ta push một hàm vào stack, đến khi nào hàm đó thực thi xong và trả về thì mới được pop ra khỏi stack. Thao tác đó được mô tả như sau:

![Markdowm Image][1]

Như hình trên, khi chúng ta thực thi một chương trình, đầu tiên chúng ta sẻ tìm đến hàm main, nơi mà mọi thực thi đều bắt đầu từ đây. Trong chương trình trên ta sẻ có các bước như sau:

-   **console.log(bar(6))** được đưa vào stack. Hàm này gọi đến hàm **bar**

-   Tiếp theo, **bar(6)** được đưa vào stack, hàm **bar** lại tiếp tục gọi hàm **foo**

-   Tiếp đó **foo(x,y)** lại được đưa vào stack.

-   Hàm **foo** thực thi xong trả kết quả về cho hàm **bar** và được pop ra khỏi stack.

-   Hàm **bar** nhận được kết quả từ hàm foo, thực thi xong trả về kết quả cho hàm **console.log()** và được loại bỏ ra khỏi stack.

-   Hàm **console.log()** thực thi và được loại bỏ ra khỏi stack.

-   Cuối cùng hàm **main** cũng được loại bỏ ra khỏi stack, chương trình kết thúc.

Đôi lúc chúng ta tạo ra một vòng lặp vô hạn khi chúng ta gọi nhiều đệ quy, với chrom thì thường giới hạn bởi 16.000 frames, nếu vượt ra khỏi con số đó thì sẻ sinh ra lỗi như sau :v

![Markdowm Image][2]

### 2. Heap:

Bộ nhớ Heap dùng để cấp phát bộ nhớ cho object, biến toàn cục.
Bất cứ khi nào khai báo đối tượng thì các giá trị của đối tượng sẽ được lưu trữ trong Heap (chú ý giá trị đối tượng chứ ko phải biến tham chiếu đối tượng) và có thể truy cập bất cứ khi nào trong chương trình, bộ nhớ tồn tại trong suốt quá trình thực thi chương trình

Khi kết thúc 1 phương thức các biến tham chiếu đối tượng bị hủy trong stack và các tham chiếu tới các dữ liệu lưu trong Heap cũng bị hủy bỏ javascript sẻ dùng trình thu dọn rác để thực hiện kiểm tra các tham chiếu.. nếu ko còn tham chiếu nào tới biến lưu trữ trên vùng nhớ Heap thì các vùng nhớ đó sẽ được thu gom.

### 3. Queue:

Đối với Javascript runtime thì có thêm một thành phần nữa đó là queue, đây là danh sách các message cần được sử lí và các hàm callback liên quan thực thi. Nói dễ hiểu hơn là các message này sẻ được lưu vào queue để phản hồi các sự kiện async bên ngoài chẳng hạn như sự kiện nhấp chuột hay một http reuquest với một callback được cung cấp.

[1]: /assets/images/2017-08-14-hieu-ve-call-stack-heap-queue/1.gif
[2]: /assets/images/2017-08-14-hieu-ve-call-stack-heap-queue/2.png
