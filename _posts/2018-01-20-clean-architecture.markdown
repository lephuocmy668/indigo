---
title: 'Clean Architecture'
layout: post
date: 2018-01-20 9:01
image: /assets/images/
headerImage: false
tag:
    - solid
    - ood
    - oop
category: blog
author: My Le Phuoc
description: Markdown summary with different options
# jemoji: '<img class="emoji" title=":ramen:" alt=":ramen:" src="https://assets.github.com/images/icons/emoji/unicode/1f35c.png" height="20" width="20" align="absmiddle">'
---

Trước khi đi vào nội dung chính của bài viết này, mình xin nói qua về quá trình mình đã tiếp cận với các kiểu kiến trúc trong việc xây dựng các ứng dụng web.

Điểm xuất phát của mình dường như nó không đi theo con đường “chính đạo” như các bạn các anh chị đi trước thường tiếp cận với Java, C#, PHP,…và đa số những bạn xuất phát theo con đường Java thường có cái nhìn cũng như tư duy về kiến trúc từ sớm, mình thì ngược lại, xuất phát một cách quán tính, mình bắt đầu với Node.js với một kiểu kiến trúc mà vài tháng sau khi học mình Node mới biết nó gọi là MVC(model-view-controller).

Sau đó một thời gian mình có cơ hội tham gia vào một dự án nhỏ chơi chơi mà sau đó mình đã gắn bó được một thời gian dài, dự án này gồm một ứng dụng web single page với hệ thống back end gồm 2 lớp Model và Controller cung cấp các api cho web app gọi, kiến trúc đó ban đầu chạy rất ổn. Tuy nhiên chuyện gì đến cũng đã đến, phần back end ngày một phình to và việc nhồi nhét rất nhiều thứ chỉ trong 2 lớp đã kéo theo nhiều vấn đề và lúc này cũng vì nhiều nguyên nhân mình đã không còn ở lại để giải quyết những vấn đề đó nữa. Sau này mình mới được tiếp cận với Clean architecture của tác giả Uncle Bob mình nhận ra rằng nếu dự án củ ban đầu được dựng code base dựa trên clean architecture thì các vấn đề đã trở nên đơn giản hơn và sẻ đở mất thời gian hơn rất nhiều.

Chính vì thế mình viết lại những tóm tắt sau khi tìm hiểu và implement clean architecture lại đây để có dịp quay lại ôn lại :v hoặc ai đó đang tìm hiểu hoặc đang implement đó đọc được bài này có thể cảm nhận và phản biện giúp mình cũng cố kiến thức hơn.

Hiện nay chúng ta có rất nhiều ý tưởng về kiến trúc hệ thống như Hexagonal Architecture(kiến trúc lục giác) , Onion Architecture(kiến trúc củ hành), Screaming Architecture,….. và kiến trúc mà chúng ta sẻ thảo luận trong bài viết này: Clean Architecture – Kiến trúc sạch. Dù những kiến trúc này có khác nhau đôi chút về chi tiết, tuy nhiên nhìn chung chúng tương tự nhau nhau về mục đích đó là phân tách các thành phần và mối quan hệ, bằng cách chia phần mềm thành các lớp. Thường thì mỗi một kiến trúc trong số đó đều phãi có ít nhất một lớp cho các business rule, và một lớp cho các interfaces thêm nữa mỗi loại kiến trúc đó đều tạo ra hệ thống mà nó đáp ứng các tiêu chuẩn sau:

-   Độc lập framework : Kiến trúc không phụ thuộc vào một số thư viện phần mềm có nhiều tính năng. Điều này cho phép bạn sử dụng các framework như các công cụ thay vì phải nhồi nhét hệ thống của bạn vào các ràng buộc hạn chế của chính chúng.

-   Dễ test mà không phãi phụ thuộc vào giao diện, database hay bất cứ thành phần bên ngoài nào.

-   Độc lập với giao diện người dùng, giao diện người dùng có thể thay đổi dễ dàng, mà không ảnh hưởng đến phần còn lại của hệ thống. Chẳng hạn, một giao diện web có thể được thay đổi thành giao diện command mà không làm ảnh hưởng đến các business rule.

-   Độc lập với Database, bạn có thể thay đổi từ Oracle hoặc Sql Server thành Mongo, BigTable, CouchDB hoặc bất kỳ hệ quản trị cơ sở dữ liệu nào mà không làm ảnh hưởng đến Business rule ban đầu.

-   Độc lập với các chương trình bên ngoài: Business rule không cần biết bất cứ điều gì về thế giới bên ngoài.

Clean Architecture là một kiến trúc có các đặc điểm như trên. Nói chung Clean Architecture cũng chỉ là một loại kiến trúc áp dụng các nguyên tắc thiết kế để xây dựng các hệ thống thoả mãn các yêu cầu trên, nó cũng tương tự như Domain Driven Design(DDD) nhưng lại chia nhỏ các lớp hơn. Biểu đồ sau đây sẻ cho bạn thấy ý tưởng cũng như mô hình cơ bản của clean architecture:
![Markdowm Image][1]

## The Dependency Rule(Quy tắc phụ thuộc)

Các vòng tròn đồng tâm đại diện cho các khu vực khác nhau của phần mềm. Các thành phần càng nằm sâu bên trong hơn là những thành phần quan trọng hơn, vòng ngoài là các cơ chế, các vòng tròn bên trong là các chính sách điều khoản.

Quy tắc này cho rằng mã nguồn chỉ có thể hướng vào bên trong, tức là những thứ ở bên trong không thể biết về những thứ ở bên ngoài.

Cụ thể, tên của một cái gì đó khai báo trong một vòng tròn bên ngoài không được tham chiếu đến hoặc sử dụng bởi mã nguồn trong một vòng tròn bên trong bao gồm, các hàm, các class. biến, hoặc bất kỳ thực thể phần mềm khác. Cũng giống như vậy, các định dạng dữ liệu được sử dụng trong vòng ngoài không nên được sử dụng bởi những thứ ở vòng tròn bên trong, đặc biệt nếu các định dạng đó được tạo ra bởi một framework trong vòng tròn bên ngoài. Chúng ta không muốn bất cứ điều gì trong một vòng tròn bên ngoài tác động vào vòng tròn bên trong.

## Entities(Các thực thể)

Các thực thể sẽ đóng gói các quy tắc nghiệp vụ. Một thực thể có thể là một đối tượng với phương thức hoặc có thể là một tập hợp các cấu trúc dữ liệu và hàm, miễn là nó có thể được sử dụng bởi nhiều ứng dụng khác nhau trong toàn bộ phần mềm.

Nếu bạn chỉ viết một ứng dụng đơn lẻ, thì những thực thể chính là các đối tượng nghiệp vụ của ứng dụng. Chúng đóng gói các quy tắc chung và cao cấp nhất. Chúng ít có khả năng thay đổi do ảnh hưởng từ những thay đổi bên ngoài. Chẳng hạn, bạn không thể mong những đối tượng này bị ảnh hưởng bởi một thay đổi đến từ việc phân trang hoặc bảo mật. Những hoạt động làm thay đổi một ứng dụng cụ thể không nên ảnh hưởng đến tầng thực thể.

## Use Cases

Phần mềm trong lớp này chứa các business rules cụ thể của ứng dụng. Nó đóng gói và implement tất cả các use cases của hệ thống. Các use cases này sẽ điều chỉnh luồng dữ liệu đến và đi từ các entities và chỉ đạo các thực thể đó sử dụng các business rules của doanh nghiệp để đạt được các mục tiêu của use case.

Chúng ta không mong muốn những thay đổi trong lớp này sẽ ảnh hưởng đến các thực thể. Chúng tôi cũng không mong muốn lớp này bị ảnh hưởng bởi những thay đổi của các yếu tố bên ngoài như cơ sở dữ liệu, giao diện người dùng hoặc bất kỳ framework nào. Lớp này bị cô lập với những lo ngại đó.

Tuy nhiên, chúng ta mong đợi rằng những thay đổi đối với hoạt động của ứng dụng sẽ ảnh hưởng đến các use-cases và đến phần mềm trong lớp này. Nếu chi tiết của use-case thay đổi, thì một số mã trong lớp này chắc chắn sẽ bị ảnh hưởng.

## Interface Adapters

Phần mềm trong layer này là một bộ các adapter có nhiệm vụ chuyển dữ liệu từ định dạng thuận tiện nhất cho các use case và thực thể thành định dạng thuận tiện nhất cho các chương trình bên ngoài như Database hoặc Web. Layer này chứa kiến trúc MVC. Presenters, Views và Controllers đều thuộc layer này. Những Model chỉ là cấu trúc dữ liệu được truyền từ Controller đến use case, và sau đó truyền từ use case đến Presenter và View.

Cũng tương tự, dữ liệu được chuyển đổi từ hình thức phù hợp cho entity và use case thành hình thức phù hợp cho framework đang được sử dụng. Những đoạn mã ở trong vòng tròn này không biết gì về cơ sở dữ liệu. Nếu cơ sở dữ liệu là kiểu SQL hay gì đó thì tất cả truy vấn nên được giới hạn cho layer này, cụ thể là các phần của layer này mà phải làm việc với cơ sở dữ liệu.

## Framework và Driver

Layer ngoài cùng là kết hợp các framework và công cụ như cơ sở dữ liệu, web framework,… Nói chung bạn không viết nhiều code trong layer này ngoại trừ các đoạn mã để liên lạc với các vòng tròn tiếp theo ở bên trong. Layer này là nơi tập trung của các chi tiết. Web là một chi tiết. Cơ sở dữ liệu là một chi tiết. Chúng ta giữ những thứ này ở bên ngoài, nơi chúng khó có thể gây ảnh hưởng đến các phần ở vòng tròn bên trong.

## Only Four Circles?(Chỉ 4 vòng tròn đó thôi là đủ ư?)

Các vòng tròn là giản đồ. Nhiều lúc bạn cần nhiều hơn 4 vòng tròn. Không có quy tắc nào nói rằng bạn luôn phải có chỉ 4 vòng tròn. Tuy nhiên, Dependency Rule luôn được áp dụng. Sự phụ thuộc mã nguồn luôn hướng vào bên trong. Khi bạn di chuyển vào tâm vòng tròn, mức độ trừu tượng tăng lên. Vòng tròn ngoài cùng là các chi tiết cụ thể ở mức thấp nhất. Bạn càng di chuyển vào trong, phần mềm càng phát triển trừu tượng hơn, và đóng gói các điều khoản ở cấp cao hơn. Vòng tròn trong cùng chỉ chứa những gì chung nhất, khó có thể chia nhỏ được nữa như các interface chẳng hạn.

## Crossing boundaries

Góc bên phải, phía dưới của sơ đồ đầu bài là ví dụ về cách chúng ta vượt qua những vòng tròn.

Nó chỉ ra rằng, Controllers và Presenters liên lạc với Use Case trong layer kế tiếp. Chú ý luồng điều khiển, nó bắt đầu từ controller, di chuyển qua các use case và sau đó thực thi trong presenter. Cũng lưu ý đối với các dependencies, chúng trỏ vào bên trong ứng với các trường hợp sử dụng.

Tác giả Uncle Bob thường giải quyết vấn đề này bằng cách sử dụng Dependency Inversion Principle(mỗi thành phần hệ thống (class, module, …) chỉ nên phụ thuộc vào các abstractions, không nên phụ thuộc vào các concretions hoặc implementations cụ thể). Trong một ngôn ngữ như Java, tác giả sẽ sắp xếp các interfaces và các mối quan hệ thừa kế sao cho các dependencies phản ánh luồng kiểm soát tại các điểm chính xác trên toàn bộ ranh giới.

## What data crosses the boundaries

Dữ liệu đi qua các vùng ranh giới là cấu trúc dữ liệu đơn giản. Chúng ta không muốn truyền Entity hoặc các bản ghi của cơ sở dữ liệu. Chúng ta cũng không muốn cấu trúc dữ liệu có bất kỳ phụ thuộc nào mà vi phạm Dependency Rule.

Lấy ví dụ, nhiều framework cơ sở dữ liệu trả về định dạng dữ liệu phù hợp cho một truy vấn. Chúng ta có thể gọi nó là một RowStructure. Rõ ràng ta không muốn truyền kiểu định dạng dữ liệu này vào các vòng bên trong vì nó vi phạm Dependency Rule, các vòng tròn bên trong có thể biết được đôi chút về vòng tròn bên ngoài. Chính vì thế, khi truyền dữ liệu vào vòng tròn bên trong, chúng luôn phải là định dạng phù hợp với vòng tròn đó.

## Kết luận

Tuân theo các quy tắc đơn giản này không phải là một việc quá khó khăn nhưng nó sẻ giúp bạn tiết kiệm được nhiều thời gian trong tương lai. Bằng việc tách hệ thống thành các layer, đồng thời tuân theo Dependency Rule, bạn sẽ xây dựng được một hệ thống dế test, cùng với những lợi ích kèm theo như đã đề cập ở trên. Khi bất kỳ bộ phận bên ngoài của hệ thống trở nên lỗi thời, chẳng hạn như database, hoặc web framework, bạn hoàn toàn có thể thay thế chúng với một effort tối thiểu.

[1]: /assets/images/2018-01-20-clean-architecture/1.jpg
