---
title: 'Solid Principle'
layout: post
date: 2017-12-12 1:01
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

Hệ thống phần mềm tốt phãi bắt đầu bằng code sạch. Cũng giống như việc xây nhà, bắt đầu chúng ta cần những viên gạch tốt đã, nhưng những viên gạch đã không tốt thì kiến ​​trúc của tòa nhà không còn quan trọng nữa vì nó đã dễ dàng sụp đổ rồi. Một mặt khác, khi bạn có các viên gạch tốt rồi nhưng đôi lúc từ chúng bạn vẫn tạo ra một mớ hổn độn từ những viên gạch tốt đó. Do đó Solid đến và giúp chúng ta xây dựng các kiến trúc tốt dựa trên các viên gạch tốt.

Nguyên tắc SOLID cho chúng ta biết cách sắp xếp các hàm, cấu trúc dữ liệu của chúng ta vào các lớp và kết nối chúng lại với nhau để xây dựng nên hệ thống. Việc sử dụng từ class không có nghĩa rằng các nguyên tắc này chỉ áp dụng cho phần mềm hướng đối tượng. Một class đơn giản là một nhóm các hàm và dữ liệu được ghép đôi. Mọi hệ thống phần mềm đều có các nhóm như vậy cho dù chúng có được gọi là các class hay không thì nguyên tắc SOLID vẫn sẻ áp dụng được cho các nhóm đó.

Vậy mục tiêu của các nguyên tắc trong SOLID là gì? Là tạo ra các cấu trúc ở mức mid-level của phần mềm có các yêu cầu như dễ dàng tiếp nhận sự thay đổi, dễ hiểu cho người mới, dễ sử dụng lại. Từ mid-level đề cập đến thực tế là các nguyên tắc này được áp dụng bởi các lập trình viên làm việc ở cấp modules, SOLID được áp dụng ngay trên mức của code implement và giúp xác định các loại cấu trúc phần mềm được sử dụng trong các modules và các components.

Chỗ này hơi khó hiểu nhể, có thể tưởng tượng rằng một ngôi nhà nên được chia đầu tiên thành các components như các bức tường nhỏ, sau đó ghép nối lại thì SOLID được dùng ở mức các Engineer tạo nên các bức tường đó. Nói cách khác, khi muốn xây dựng kiến trúc tốt cho một ngôi nhà hay phần mềm chúng ta phãi thiết kế tốt từ từng bức tường, từng modules từng component để sao cho nó có thể dễ dàng tiếp nhận sự thay đổi, dễ dùng dễ hiểu cho người mới và hơn nữa là dễ dàng tái sử dụng module/component đó.

**SOLID** được **Robert C. Martin** đưa ra với năm nguyên tắc thiết kế hướng đối tượng (OOD) sau:

**– Single responsibility principle (SRP)**

**– Open/closed principle (O)**

**– Liskov substitution principle (L)**

**– Interface segregation principle (I)**

**– Dependency inversion principle (D)**

Chúng ta sẻ tiếp tục phân tích rõ từng nguyên tắc.

### 1. The Single Responsibility Principle(SRP):

**The Single Responsibility Principle(SRP)**: Mỗi một class chỉ đảm nhiệm một trách nhiệm duy nhất,một hệ thống phần mềm có cấu trúc tốt là hệ thống có các module/component mà chúng chỉ có một và chỉ một lý do để thay đổi.
Đọc đến đây chúng ta sẻ có thể dễ nhầm lẩn với một nguyên tắc khác đó là việc các hàm nên làm một và chỉ một việc duy nhất, đó là một nguyên tắc chúng ta thường sử dụng khi tái cấu trúc các hàm lớn thành các hàm nhỏ. Đó không phãi là SRP.

Để hiểu rõ nguyên tắc này chúng ta sẻ xét một ví dụ mà ta đã vi phạm nguyên tắc này:
Giả sử hệ thống quản lí tiền lương nhân viên của chúng ta có chứa 4 thực thể sau: Employee, CTO, CFO, COO. Class Employee của chúng ta sẻ có chứa ba phương thức sau:

-   caculatePay()

-   reportHours()

-   save()

Cách thiết kế class Employee của chúng ta đã vi phạm SRP bởi vì nó có ba phương thức chịu trách nhiệm với 3 thực thể rất khác nhau.

-   Phương thức caculatePay() được gọi bởi phòng kế toán và báo cáo cho CFO.

-   Phương thức reportHours() được gọi bởi phòng HR và báo cáo cho COO.

-   Phương thức save() được gọi bởi database admin và báo cáo cho CTO.

Bằng việc đưa ba phương thức trên vào một class Employee đơn lẻ, chúng ta đã vô tình kết hợp sự phụ thuộc của các thực thể khác lại với nhau, ở đây có thể là CFO, COO, CTO đã vô tình phụ thuộc vào nhau. Lấy ví dụ như sau:

Giả xử rằng hàm **caculatePay()** và hàm **reportHours()** cần có giờ làm việc của từng nhân viên và chúng dùng chung một thuật toán để tính giờ làm việc, rõ ràng là khi đó chúng ta sẻ không muốn việc duplicate code xãy ra ở đây, chúng ta sẻ viết một hàm **regularHours()** cho việc sử dụng của hai hàm **caculatePay()** và **reportHours()**.

Đến một ngày đẹp trời, nhóm CFO quyết định rằng việc tính toán giờ làm việc **regularHours()** cần được tinh chỉnh lại trong lúc nhóm COO vẫn thấy hàm **regularHours()** như thế là ổn rồi không muốn bất cứ thay đổi gì đối với nó nữa.

Một developer được giao nhiệm vụ tinh chỉnh lại hàm **regularHours()** theo một mục đích mới nào đó, anh ta làm việc nhưng đâu biết rằng hàm **reportHours()** cũng gọi đến nó, việc tinh chỉnh được thực hiện xong, hàm **caculatePay()** chạy trơn tru đúng yêu cầu và được áp dụng ngay. Sau một thời gian người ta nhận thấy hàm **reportHours()** đã đi sai hướng, các số liệu báo cáo lên sai lệch ảnh hưởng đến tài chính công ty.

Đó là một ví dụ vi phạm, khi gặp các trường hợp đó chúng ta nên phân tách các phương thức ra các class riêng lẻ và ngược lại, cách dễ nhất để phá các ứng dụng là tạo ra các GOD classes(một GOD class là một class biết quá nhiều hoặc làm quá nhiều, GOD class là một ví dụ về một ví dụ về anti pattern), một God class giữ reference đến nhiều thực thể khác cũng như giữ nhiều trách nhiệm đâm ra dễ gây ra các vấn đề tương tự như ví dụ trên.

### 2. Open/closed principle (OCP):

**Theo nguyên lý này, mỗi khi ta muốn thêm chức năng cho chương trình, chúng ta nên viết class mới mở rộng từ class cũ ( bằng cách kế thừa hoặc sở hữu class cũ) không nên sửa đổi class cũ:**

Tất nhiên rồi phãi không nào, đây là lý do cơ bản nhất mà chúng ta nghiên cứu software architecture. Rõ ràng là nếu muốn mở rộng chức năng một cách đơn gỉan mà phãi thay đổi lớn đối với phần mềm thì các kiến ​​trúc sư của hệ thống phần mềm đó đã thất bại rồi.

![Markdowm Image][1]

Mục đích là thế nhưng làm thì như nào để đạt được mục đích nguyên tắc đó, chúng ta cùng xét một ví dụ như sau:

Giả xử hệ thống của bạn đang có một chức năng báo cáo tóm tắt tài chính, dữ liệu được hiển thị trên giao diện web và có thể cuộn cho bản tóm tắt dài. Rồi một ngày đẹp trời khách hàng muốn bạn thêm chức năng thể hiện báo cáo đó trên trên PDF với tiêu đề và phân trang hợp lí, các số liệu cần được làm nổi bật và gửi cho người dùng.

Rõ ràng, một lượng code sẻ phãi được viết lại để đáp ứng yêu cầu trên nhưng bao nhiêu code củ sẻ phãi thay đổi? Kiến trúc tốt sẻ giảm thiểu lượng code phãi thay đổi xuống mức tối thiểu nhất và lí tưởng nhất là không có dòng code nào phãi thay đổi.

Làm thế nào để đạt được điểu đó? Đầu tiên phãi tách biệt những thực thể mà chúng có thể phãi thay đổi vì các lí do khác nhau(áp dụng SRP) sau đó bố trí sự phụ thuộc của chúng đúng cách(sử dụng DIP nói sau). Bằng cách đó chúng ta sẻ đưa luồng dữ liệu hướng như dưới, mô tả một số quy trình kiểm tra xử lí dữ liệu có thể trình bày, sau đó trình bày theo định dạng phù hợp để thể hiện trên web và trên PDF.

Thông tin chi tiết cần thiết ở đây là việc tạo báo cáo liên quan đến hai trách nhiệm riêng biệt: tính toán thông tin số liệu tài chính và việc trình bày data đó thành các model thân thiện với web và pdf.

Sau khi thực hiện sự tách biệt này, chúng ta cần phải tổ chức các phụ thuộc code để đảm bảo rằng những thay đổi đối với một trong những trách nhiệm đó không gây ra những thay đổi ở bên kia. Ngoài ra, cách tổ chức mới phải đảm bảo rằng hành vi có thể được mở rộng mà không huỷ bỏ các sửa đổi.

![Markdowm Image][2]

Chúng ta thực hiện điều này bằng cách phân vùng các quy trình thành các class và tách các class đó thành các component, như được thể hiện bằng các dòng kép trong sơ đồ trong hình dưới.

Trong hình này, thành phần ở phía trên bên trái là Controller, phía trên bên phải là Interactor, phía dưới bên phải là database, ở phía dưới bên trái có bốn thành phần đại diện cho đối tượng hiển thị và data hiển thị.

Các  được đánh dấu bằng <I> là các interface; những người được đánh dấu bằng <DS> là các cấu trúc dữ liệu.

Các mũi tên đang sử dụng để thể hiện các mối quan hệ. Đầu mũi tên trỏ tới thể hiện mối quan hệ thừa kế. Điều đầu tiên cần lưu ý là tất cả các phụ thuộc là các phụ thuộc code. Một mũi tên chỉ từ class A đến class B có nghĩa là code của lớp A reference đế class B, nhưng class B không cần biết gì đến class A.

Như vậy, trong hình trên, FinancialDataMapper reference đến FinancialDataGateway thông qua một mối quan hệ implement interface, nhưng FinancialGateway không biết gì về FinancialDataMapper.
![Markdowm Image][3]

Điều tiếp theo cần lưu ý là tất cả mỗi quan hệ đều là một chiều và mỗi đối tượng chỉ chịu sự phụ thuộc đến duy nhất một thực thể khác như thể hiện trong hình dưới, những mũi tên hướng tới các thành phần mà chúng ta muốn bảo vệ khỏi thay đổi.

Nghĩa là sao? là nếu thành phần A cần được bảo vệ khỏi những thay đổi trong thành phần B, thì thành phần B sẽ phụ thuộc vào thành phần A. Chúng ta muốn bảo vệ Controller khỏi những thay đổi trong Presenters. Chúng ta muốn bảo vệ các Presenters khỏi những thay đổi trong Views. Chúng tôi muốn bảo vệ Interactor khỏi những thay đổi trong bất cứ điều gì. Interactor ở vị trí phù hợp nhất với OCP.

Các thay đổi đối với Database hoặc Controller hoặc Presenters hoặc Views sẽ không ảnh hưởng đến Interactor.
Tại sao Interactor nên giữ một vị thế đặc quyền như vậy? Bởi vì nó chứa các business rule. Interactor chứa các chính sách cao nhất của ứng dụng. Tất cả các thành phần khác đang xử lý các mối quan tâm ngoại vi còn interactor giao dịch với mối quan tâm trung tâm. Mặc dù Controller là ngoại vi với Interactor, nhưng nó vẫn là trung tâm của các Presenters và Views. Và trong khi các diễn giả có thể là ngoại vi với Controller nhưng chúng là trung tâm của Views.

Lưu ý cách thức này tạo ra một hệ thống phân cấp bảo vệ dựa trên khái niệm “level”. Các tác nhân tương tác là khái niệm mức cao nhất, vì vậy chúng được bảo vệ nhất. View nằm trong số các khái niệm cấp thấp nhất, vì vậy chúng được bảo vệ ít nhất. Presenters có cấp độ cao hơn Views nhưng cấp thấp hơn Controller hoặc Interactor.

Đây là cách OCP hoạt động ở cấp kiến ​​trúc. Các kiến trúc chia chức năng riêng biệt dựa trên cách thức – tại sao và khi nào chúng thay đổi, sau đó tổ chức chức năng được phân tách thành một hệ thống phân cấp các thành phần. Các thành phần cấp cao hơn trong phân cấp đó được bảo vệ khỏi những thay đổi được thực hiện cho các thành phần cấp thấp hơn.

Nói tóm lại OCP là một trong nhưng sức mạnh đứng đằng sau kiến trúc hệ thống tốt, giúp hệ thống dễ dàng mở rộng mà không phãi chịu sức ép từ những thay đổi trong mã nguồn, mục tiêu này đạt được khi chúng ta chia phân vùng hệ thống thành các component và sắp xếp chúng thành một hệ thống phân cấp sự phụ thuộc để bảo vệ các thành phần cấp cao khỏi sự thay đổi của các thành phần cấp thấp.

### 3. Liskov Substitution Principle(LSP):

Nguyên tắc này được phát biểu như sau:

**Trong một chương trình, các object của class con có thể thay thế class cha mà không làm thay đổi tính đúng đắn của chương trình**

Không hiểu đúng không nào? Có thể nghĩ như này: Khi các class A kế thừa từ class B thì phãi có hai điều kiện sau:

– Class B có các behaviors nào thì A phãi có các behaviors đó.

– Các phương thức của class cơ sở thì phãi đảm bảo có thể sử được trong các class con của nó hay nói cách khác các phương thức của các class cha phãi luôn hoạt động được và chính xác trên tất cả các class kế thừa từ nó.

Để hiểu hơn ta xét ví dụ như sau:

Giả xử ta có class Chim có phương thức là Bay()

– Class Đại Bàng thừa kế class Chim cũng có đủ phương thức Bay() và hoạt động đúng như class chim() trường hợp này thoả mãn LSP.

– Class Chim Cánh cụt thừa kế class Chim nhưng phương thức Bay không khả dụng cho nên là vi phạm LSP.

– Class Chim Điện thừa kế class Chim cũng có phương thức bay, nhưng phương thức Bay này có thêm yêu cầu là phãi có điện thì mới bay được cho nên vi phạm LSP.

LSP cần được mở rộng đến mức kiến trúc. Một sự vi phạm đơn giản về khả năng thay thế, có thể làm cho kiến trúc của hệ thống bị ô nhiễm với một số lượng đáng kể các cơ chế bổ sung.

### 4. Interface segregation principle(ISP):

![Markdowm Image][4]

Nguyên tắc này có thể nói ngắn gọn là thay vì dùng 1 interface lớn, ta nên tách thành nhiều interface nhỏ, với nhiều mục đích cụ thể, để dễ hiểu hơn chúng ta cùng xét ví dụ như hình trên, mỗi user sử dụng các phương thức của class OPS, giả sử rằng User1 chỉ sử dụng op1, User2 chỉ sử dụng op2, User3 chỉ sử dụng op3.

Khi đó User1 vô tình phụ thuộc vào op2 và op3 mặc dù nó không gọi chúng, sự phụ thuộc này khiến cho User1 phãi được implement lại khi op2 và op3 bị thay đổi mặc dù nó không dùng hai hàm đó, hơn thế nữa việc gom quá nhiều phương thức vào một đối tượng khiến cho chúng ta nhọc nhằng trong việc implement cho nên chúng ta nên giải quyết bằng cách tách biệt các phương thức thành các interface nhỏ như hình bên dưới.

![Markdowm Image][5]

Nếu vấn đề này được triển khai trên ngôn ngữ tỉnh như Golang thì code của User1 sẻ phụ thuộc vào U1Ops và op1 nhưng sẻ không phụ thuộc vào OPS do đó khi có thay đổi đối với OPS mà User1 không quan tâm sẻ không làm cho User1 bị biên dịch lại và triển khai lại.

### 5. DEPENDENCY INVERSION PRINCIPLE(DIP):

Nguyên tắc này cho chúng ta biết rằng các hệ thống linh hoạt nhất là các hệ thống phụ thuộc vào mã nguồn chỉ tham chiếu đến trừu tượng hóa, chứ không chỉ các concretions.

Hãy tưởng tượng phần mềm của chúng ta sẻ như thế nào trước khi có một cơ chế an toàn và thuận tiện cho đa hình, luồng đi của phần mềm này sẻ như cây mô tả bên dưới, các hàm main được gọi là các hàm level cao chúng gọi các hàm level trung bình và các hàm level trung bình gọi các hàm ở level thấp. Tuy nhiên có thể thấy rằng trong cây đó các phụ thuộc code không đi theo hướng của luồng gọi.

![Markdowm Image][6]

![Markdowm Image][7]

Để hàm main gọi một trong các hàm level cao, nó phải reference đến tên của module chứa hàm đó. Trong C chúng ta dùng #include trong Java và Go ta dùng câu lệnh import. Thật vậy, mỗi phần chứa hàm gọi buộc phải refer đến tên của module có chứa hàm được gọi. Rõ ràng sự phụ thuộc được thể hiện rằng hàm Main sẻ phụ thuộc vào các hàm dưới nó. Tuy nhiên, khi đa hình được đưa vào sử dụng, một điều rất khác sẻ xảy ra như sau.

Chúng ta có thể thấy rằng module HL1 vẫn gọi hàm F () trong module ML1 nhưng thực tế là nó gọi hàm này thông qua một interface mà khi chạy thì interface thực sự không tồn tại. HL1 đơn giản gọi F () trong ML1 mặc dù là thể hiện gián tiếp.

Tuy nhiên lưu ý rằng sự phụ thuộc mã nguồn (mối quan hệ thừa kế) giữa ML1 và interface trỏ theo hướng ngược lại so với luồng điều khiển. Điều này được gọi là sự đảo ngược phụ thuộc và các tác động của nó đối với kiến trúc phần mềm là rất sâu sắc. Thực tế là các ngôn ngữ OOP cung cấp tính đa hình an toàn và thuận tiện cho nên bất kỳ sự phụ thuộc mã nguồn nào bất kể nó ở đâu đều có thể đảo ngược.

Bây giờ hãy nhìn lại luồng đi trong hình 6 và các phụ thuộc mã nguồn của nó thì bất kỳ phụ thuộc mã nguồn nào đều có thể được quay lại bằng cách chèn một interface giữa chúng. Với cách tiếp cận này các kiến trúc implement trong các hệ thống được viết bằng ngôn ngữ OOP có thể kiểm soát hướng của tất cả các phụ thuộc mã nguồn trong hệ thống. Đó là sức mạnh mà OOP cung cấp. Bạn có thể làm gì với sức mạnh đó? Ví dụ, bạn có thể sắp xếp lại các phụ thuộc mã nguồn của hệ thống để cơ sở dữ liệu và giao diện người dùng (UI) phụ thuộc vào các quy tắc nghiệp vụ chứ không phải là cách khác.

![Markdowm Image][8]

Điều này có nghĩa là gì? Là giao diện người dùng và cơ sở dữ liệu có thể được implement để bổ sung cho thể hiện các business logic, mã nguồn của business logic không bao giờ cần biết đến giao diện người dùng hoặc cơ sở dữ liệu. Kết quả là, các business logic cũng như giao diện người dùng và cơ sở dữ liệu có thể được biên dịch thành ba thành phần hoặc đơn vị triển khai riêng biệt và thành phần chứa business logic sẽ không phụ thuộc vào các thành phần có chứa giao diện người dùng và cơ sở dữ liệu, các thay đổi đối với giao diện người dùng hoặc cơ sở dữ liệu không có bất kỳ ảnh hưởng nào đến business logic. Tóm lại, khi mã nguồn trong một thành phần thay đổi thì chỉ thành phần đó cần phải được triển khai lại. Đây là khả năng triển khai độc lập, nếu các module trong hệ thống của bạn có thể được triển khai độc lập, thì chúng có thể được phát triển độc lập bởi các nhóm khác nhau.

Qua việc tìm hiểu nguyên tắc này chúng ta cũng có thể thấy được sức mạnh của OOP đặc biệt là tính đa hình, thông qua việc sử dụng đa hình chúng ta có thể giành quyền kiểm soát tuyệt đối đối với mọi phụ thuộc mã nguồn trong hệ thống.

[1]: /assets/images/2017-12-12-solid-principle/1.jpg
[2]: /assets/images/2017-12-12-solid-principle/2.jpg
[3]: /assets/images/2017-12-12-solid-principle/3.jpg
[4]: /assets/images/2017-12-12-solid-principle/4.jpg
[5]: /assets/images/2017-12-12-solid-principle/5.jpg
[6]: /assets/images/2017-12-12-solid-principle/6.jpg
[7]: /assets/images/2017-12-12-solid-principle/7.jpg
[8]: /assets/images/2017-12-12-solid-principle/8.jpg
