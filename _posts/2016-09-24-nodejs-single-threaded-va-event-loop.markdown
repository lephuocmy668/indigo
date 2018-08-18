---
title: 'Node.JS – Single Thread Và Event Loop'
layout: post
date: 2016-09-24 22:48
image: /assets/images/
headerImage: false
tag:
    - nodejs
    - eventloop
    - singlethreaded
category: blog
author: My Le Phuoc
description: Markdown summary with different options
# jemoji: '<img class="emoji" title=":ramen:" alt=":ramen:" src="https://assets.github.com/images/icons/emoji/unicode/1f35c.png" height="20" width="20" align="absmiddle">'
---

“Bạn biết gì về Node.js?Nói mình nghe về những thứ bạn biết về Node.js đi nào?” – Đó là câu hỏi phổ biến nhất trong các buổi phỏng vấn lập trình viên Node.js và quan trọng nhất đó cũng là câu hỏi mà các bạn thường phãi đặt ra đầu tiên cho chính mình khi bắt đầu làm việc với Node.js, thế phần đầu tiên mà mình nên biết đó là gì, theo mình đó là một trong những đặc điểm đặc trưng và kiến trúc cơ bản của nodejs – Single Threaded và Event Loop.

Lúc bắt đầu làm việc với Nodejs mình đã tự đặt ra câu hỏi với mình như này: “Nghe nói nodejs nó là Single Threaded thế Single Threaded thì làm sao mà handle được nhiều request cùng lúc được ta?”, ok bây giờ mình sẻ trình bày câu trả lời của mình(có thể sai có thể đúng, mong các bạn góp ý và phản biện bên dưới để giúp nhau hoàn thiện hơn :v)

#### Mô hình xử lý web truyền thống(thread base):

Như chúng ta đã biết thì các hệ thống server của các ngôn ngữ phổ biến như Java, C#,… thường sẻ xử lí các request dựa trên thread base như sau:
![Markdowm Image][1]
Nhìn vào diagram trên bạn sẻ thấy rằng cứ mỗi request tới thì web server của chúng ta sẻ phãi khởi tạo 1 thread để handle request đó, các thread pool này sẻ được thực thi một cách song song và chúng sẻ bị block lại cho đến khi response về cho client.

Việc bạn thao tác các tác vụ blocking I/O như đọc database hay đọc file…. sẻ khiến thread bạn bị block lâu hơn, mà ví dụ như Java thì stack size dành cho 1 thread trên JVM mặc định là 1MB, như thế thì theo logic có thể để xử lí 1 request chúng ta sẻ tốn ít nhất 1MB và với n request đồng thời thì chúng ta sẻ phãi tốn ít nhất n(MB) đắt đỏ vcl đúng không nào, vì sự đắt đỏ đó nên số lượng thread pool thường được set cứng một số lượng cố định.

Tuy nhiên nếu là một hệ thống có lượng truy cập lớn thì chúng ta sẻ đối mặt ngay với vấn đề là nếu thread pool của chúng ta duy trì quá nhiều thread thì hệ thống của chúng ta sẻ rất khó kiểm soát đồng thời cost dành cho context switch(mình sẻ nói về vấn đề này sau nếu có cơ hội :v) tăng lên.

Nhưng nếu chúng ta duy trì quá ít thread trong thread pool thì lại làm tăng độ trể, khó đáp ứng cho người dùng. Hơn nữa việc xây dựng ứng dụng dựa trên thread lại đối mặt thêm một vấn đề đó là callstack, quá khó đúng không nào.
Ngoài ra trong thực tế việc xử lí tác vụ multi threads cũng chẳng như lí thuyết chúng ta thường nghĩ đâu, liên tưởng như hình dưới đây :v
![Markdowm Image][2]

Node.js và event base sẻ phần nào giải quyết các vấn đề nói trên tuy nhiên sẻ có những điểm yếu khác sẻ lòi ra với Node.js mình sẻ nói sau.

### Node.js và event base:

Có thể chúng ta đã nghe nhiều về Node.js và có nhiều nhận định và câu hỏi trong đầu như sau: Nodejs là một Javascript runtime chạy trên máy chủ V8 của chrome, Nodejs sử dụng mô hình event-driven với cơ chế callback của Javascript và mô hình non blocking I/O giúp cho nó nhẹ và hiệu quả, nodejs không dựa trên mô hình đa threads mà là đơn thread với Event Loop.

OK, khi mình đọc ngang đó thì đéo hiểu gì hết ahihi. Mô hình event-driven trong Node.js nó như thế nào, Event Loop là gì, non blocking i/o nó ra sao, nghe nói nó single thread màsao nó xử lí được nhiểu request đồng thời…., đó là những điều mình thắc mắc khi mới tìm hiểu. Bây giờ chúng ta sẻ bàn vào kiến trúc của Nodejs để làm rõ điều đó.

Thực ra, Node.js vẫn duy trì một thread pool có số thread giới hạn để phục vụ các yêu cầu từ client.
Để xử lí các request từ client, đầu tiên Nodejs sẻ tiếp nhận các request đó một cách tuần tự và đặt vào một cái queue chúng ta có thể gọi nó là event queue. Nodejs có một thành phần mà nó được coi là trái tim của Node đó là Event Loop, cũng như cái tên của nó, event loop sử dụng một vòng lặp vô hạn để tiếp nhận và xử lí các yêu cầu. Event loop kiểm tra trong event queue xem có request nào không, nếu không có thì cứ lặp mãi, nếu có thì sẻ có hai hướng sử lí sau:

– Nếu request không có yêu cầu gì đến blocking io thì xử lí mọi thứ từ yêu cầu sau đó event loop phản hồi lại cho client.

– Nếu request có một hoặc nhiều yêu cầu blocking i/o như đọc file/query database thì nó phãi kiễm tra xem trong Thread Pool có sẳn thread nào không, nếu có thread sẳn thì quăng request đó cho nó xử lí, xử lí xong thì quăng ngược lại cho event loop trả về cho client.
Để dễ hiểu các bạn tham khảo diagram sau:

![Markdowm Image][3]

Đến đây có lẽ bạn đã hiểu kiến trúc Nodejs làm việc nhưng có thể bạn sẻ thắc mắc rằng thread pool của Nodejs nó giới hạn bao nhiêu threads, điều này phụ thuộc vào các thành phần blocking io mà Nodejs sẻ handle, ví dụ như handle file system, node sẻ dùng libuv để xử lí dụ đó và theo một số tài liệu thì số theads “mặc định” mà libuv giới hạn sẻ là 4. Có nghĩa là khi có 5 request yêu cầu làm việc với file system dồng thời thì request thứ 5 sẻ bị block cho đến khi 4 thread xử lí 4 request đầu tiên thực hiện xong.

Đến đây có thể là các bạn đã có thể hiểu một cách tương đối đầy đủ cách thức hoạt động của Node.js, cám ơn các bạn đọc bài viết, nếu có thắc mắc mong các bạn góp ý và phản biện bên dưới, cám ơn.

[1]: /assets/images/2016-09-24-nodejs-single-threaded-va-event-loop/1.jpg
[2]: /assets/images/2016-09-24-nodejs-single-threaded-va-event-loop/2.jpg
[3]: /assets/images/2016-09-24-nodejs-single-threaded-va-event-loop/3.jpg
