---
title: 'Giới Thiệu Ngôn Ngữ Golang'
layout: post
date: 2017-01-28 21:20
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

Hiện tại có rất nhiều ngôn ngữ mạnh mẻ cho việc xây dựng ứng dụng web phía back-end như Java, C#, Php, Javascript(Node.js), Ruby, Python…, trước đó thì mình làm việc với Javascript-Node.js tuy nhiên hôm nay, mình sẻ giới thiệu với các bạn một ngôn ngữ có vẻ mới một chút đó là Golang(Go).

Go là ngôn ngữ lập trình được phát triển bởi Google và cộng đồng mã nguồn mở bắt đầu từ năm 2007 và ra phiên bản đầu tiên vào tháng 12 năm 2012. Go là một ngôn ngữ tỉnh, có khả năng tự động dọn dẹp rác, biên dịch tự nhiên, concurrent và rất giống C về cú pháp. Sau đây là một vài đặc điểm đáng chú ý của nó:

### Go là ngôn ngữ tối giản với thiết kế thực dụng :

Ngôn ngữ lập trình Go có thể được mô tả đơn giản bằng ba từ: **đơn giản–tối thiểu–thực dụng**.

Nếu bạn nhìn sâu vào thiết kế ngôn ngữ của Go, bạn sẽ thấy cách tiếp cận đơn giản và tối giản của nó, cùng với thiết kế thực dụng. Bạn có thể quan sát sự đơn giản này với tất cả các tính năng của Go bao gồm cả hệ thống kiểu dữ liệu. Nhiều ngôn ngữ lập trình cung cấp quá nhiều tính năng làm cho nó trở nên phức tạp hơn cho các nhà phát triển nên mục tiêu thiết kế của Go là một ngôn ngữ đơn giản và chỉ cung cấp tất cả các tính năng cần thiết tối thiểu để phát triển các hệ thống phần mềm hiệu quả.

Mặc dù Go có ít tính năng hơn nhưng năng suất không bị ảnh hưởng bởi thiết kế thực dụng của nó. Một lập trình viên Go mới có thể nhanh chóng học được ngôn ngữ và có thể dễ dàng bắt đầu phát triển các ứng dụng chất lượng.

Trên thực tế có thể gọi Go là một ngôn ngữ lập trình hướng đối tượng (OOP). Tuy nhiên cách tiếp cận hướng đối tượng của Go khác với các ngôn ngữ lập trình như C++, Java và C #. Trên lí thuyết Go không phải là một ngôn ngữ OOP chính thống. Không giống như các ngôn ngữ OOP hiện có, Go không hỗ trợ thừa kế và thậm chí không có từ khóa class. Nó sử dụng các thành phần thừa kế thông qua hệ thống kiểu đơn giản của nó(kế thừa làm sao thì mình sẻ trình bày trong các bài sau). Thiết kế kiểu interface của Go cho thấy tính độc đáo của nó khi so sánh với các ngôn ngữ lập trình hướng đối tượng khác(mình cũng sẻ giới thiệu sâu sau). Đến đây chắc bạn tự hỏi Go có phãi là một ngôn ngữ OOP? Câu trả lời là có thể có cũng có thể không. Ngôn ngữ Go bao gồm tất cả các quy tắc cần thiết để viết các ứng dụng bằng một phương pháp hướng đối tượng, nhưng nó không phải là một ngôn ngữ OOP hoàn chỉnh vì nó thiếu một số tính năng OOP truyền thống.

### Ngôn ngữ tĩnh với hiệu suất cao

Go là một ngôn ngữ lập trình tĩnh, với cú pháp giống gần như 70% ngôn ngữ C. Giống như C và C ++, nó tự động biên dịch mã nguồn thành máy cho nên biên dịch just-In-Time (JIT) là không cần thiết để chạy chương trình của nó(Các ngôn ngữ lập trình như Java và C # sử dụng biên dịch JIT để chạy các ứng dụng.)

Đối với việc viết ứng dụng, một ngôn ngữ động cho ta rất nhiều năng suất và sự thoải mái bởi vì bạn không phải lo lắng về các kiểu dữ liệu của các biến bạn sử dụng. Nhưng khi làm việc với một ngôn ngữ động, hiệu suất và khả năng maintain của các ứng dụng bị ảnh hưởng. Đôi khi việc debug của một ứng dụng được viết bằng một ngôn ngữ động rất khó khăn do chúng thiếu các kiểu an toàn. Ngay cả bây giờ, các nhà phát triển sử dụng ngôn ngữ tĩnh để tạo code cho ngôn ngữ động của họ ví dụ như các nhà phát triển JavaScript sử dụng ngôn ngữ tĩnh TypeScript để đảm bảo an toàn cho kiểu dữ liệu, cuối cùng biên dịch ra code JavaScript.

Mặc dù ngôn ngữ tĩnh có thể cung cấp sự an toàn và hiệu suất của kiểu dữ liệu, nhưng làm việc với chúng có thể ảnh hưởng đến năng suất phát triển ứng dụng và việc biên soạn các chương trình lớn có thể mất nhiều thời gian. Sẽ rất tuyệt khi có một ngôn ngữ cung cấp sức mạnh của cả tĩnh và ngôn ngữ động để kết hợp hiệu suất và an toàn của một ngôn ngữ tĩnh với năng suất của một ngôn ngữ động.

Go là sự kết hợp hoàn hảo của sức mạnh của ngôn ngữ tĩnh và năng suất của ngôn kiểu động. Go có thể được gọi là ngôn ngữ C hiện đại cung cấp hiệu suất gần như C, cùng với năng suất của một ngôn ngữ kiểu động.

### Concurrency - Xử lí đồng thời

Ngày nay phần cứng máy tính đã phát triển để có nhiều lõi CPU và nhiều sức mạnh hơn, nhưng sức mạnh của máy tính hiện đại không thể được tận dụng bằng cách sử dụng các ngôn ngữ lập trình hiện tại và các công cụ. Khi các ứng dụng được chạy trên các máy chủ công suất cao, có những vấn đề về hiệu suất, mặc dù mới chỉ sử dụng một ít CPU. Trong một số môi trường lập trình, concurrency(sự đồng thời) và parallelism(song song) cho hiệu quả và hiệu năng tốt hơn, nhưng các tính năng này là một thư viện hay framework riêng biệt, chứ không phải là một tính năng tích hợp sẳn ở cấp độ ngôn ngữ, làm tăng thêm sự phức tạp khi bạn viết các ứng dụng concurrent.

Trong Go, concurrency được xây dựng sẳn và được thiết kế để viết các ứng dụng concurrent hiệu suất cao cho các máy tính hiện đại. Concurrency là một trong những tính năng độc đáo của ngôn ngữ Go và nó được coi là điểm mạnh lớn nhất của ngôn ngữ này.

Concurrency trong Go được thực hiện bằng hai tính năng độc đáo đó là : goroutines và channel. Một goroutine là một chức năng có thể chạy đồng thời với goroutines khác. Đây là một thread gọn nhẹ(tốn khoản 2kb stack size), trong đó nhiều goroutines thực hiện trong một thread duy nhất cho phép thực thi chương trình và hiệu quả. Tính năng quan trọng nhất của goroutine là nó được quản lý và thực thi bởi Go runtime.

Nhiều ngôn ngữ lập trình cung cấp hỗ trợ viết các chương trình đồng thời, nhưng chúng chỉ giới hạn trong giao tiếp và đồng bộ hóa giữa các threads đang được thực thi. Và hầu hết các ngôn ngữ hiện tại cung cấp hỗ trợ cho đồng thời thông qua một framework, nhưng không phải là một tính năng tích hợp trong ngôn ngữ, vì vậy nó làm hạn chế khi concurrency được implemented với các ngôn ngữ này.

Go cung cấp các channel(kênh) cho phép giao tiếp giữa các goroutines và đồng bộ hóa các hành động của chúng. Với các channel, bạn có thể gửi dữ liệu qua lại giữa các goroutine khác nhau. Channel cũng cung cấp mức độ đồng bộ hóa cao hơn giữa các goroutines và đảm bảo rằng hai goroutines đang chạy trong một state xác định. Concurrency là lý do chính cho việc sử dụng Go như một ngôn ngữ để xây dựng các hệ thống phần mềm hiệu quả cao với hiệu năng cao hơn. Mình sẻ giới thiệu cách dùng các chức năng này trong các bài viết tiếp theo.

### Go biên dịch nhanh hơn

Một trong những thách thức khi viết các ứng dụng C/C ++ là thời gian cần thiết cho việc biên dịch chương trình, điều này rất khó chịu đối với các nhà phát triển khi họ làm việc với các ứng dụng C và C ++ lớn. Go là một ngôn ngữ được thiết kế để giải quyết các thách thức lập trình của các môi trường lập trình hiện tại. Trình biên dịch của nó rất hiệu quả cho việc biên dịch các chương trình một cách nhanh chóng; một ứng dụng Go lớn có thể được biên dịch trong vài giây, điều đó là hấp dẫn đối với nhiều nhà phát triển C và C ++ chuyển sang môi trường lập trình Go.

### Go là ngôn ngữ đa năng

Các ngôn ngữ khác nhau được dùng để phát triển các loại ứng dụng khác nhau với ưu nhược điểm khác nhau. C và C++ thường được sử dụng cho các chương trình hệ thống và cho các hệ thống đòi hỏi hiệu suất cao nhưng làm việc với C/C++ ảnh hưởng đến năng suất phát triển ứng dụng. Một số ngôn ngữ lập trình khác, chẳng hạn như Ruby, Node.js và Python, cho phép phát triển ứng dụng nhanh chóng và tăng năng suất ví dụ như nền tảng Node.js tốt cho việc xây dựng các API JSON và các ứng dụng real-time, nhưng nó sẽ thất bại khi các CPU-intensive programming tasks được thực hiện. Một số ngôn ngữ khác được dùng để xây dựng native mobile app như Objective C hay Swift tuy nhiên hai ngôn ngữ này dường như chỉ có thể làm mobile. Nhiều ngôn ngữ lập trình được dùng cho nhiều trường hợp sử dụng như lập trình hệ thống, hệ thống phân tán(distributed computing), lập trình web app, xây dựng ứng dụng doanh nghiệp(ERP), mobile app… Thì Go là ngôn ngữ làm được điều đó, nó có thể được dùng để xây dựng một loạt các loại ứng dụng bao gồm hệ thống đòi hỏi hiệu năng cao, mobile app, web app…đặc biệt nó được sử dụng để xây dựng các ứng dụng doanh nghiệp và các máy chủ back-end mạnh mẻ. Go cung cấp hiệu suất cao đồng thời vẫn giữ được năng suất cao cho việc phát triển ứng dụng nhờ thiết kế đơn giản và thiết thực. Hệ sinh thái Go (bao gồm Go tool, thư viện chuẩn Go và thư viện của bên thứ ba đi) cung cấp các công cụ và thư viện thiết yếu để xây dựng một loạt các ứng dụng Go. Dự án Go Mobile hỗ trợ xây dựng ứng dụng di động cho cả nền tảng Android và iOS, cho phép nhiều cơ hội hơn với Go.

Trong thời đại điện toán đám mây, Go là một ngôn ngữ lập trình hiện đại có thể được sử dụng để xây dựng các ứng dụng hệ thống; các ứng dụng phân tán(distributed applications); các chương trình networking; Trò chơi; ứng dụng web; RESTful services; back-end servers; các ứng dụng di động; và cloud-optimized – thế hệ ứng dụng kế tiếp . Go là sự lựa chọn của nhiều hệ thống cách tân sáng tạo như Docker và Kubernetes. Phần lớn các công cụ về hệ sinh thái Docker đang được viết bằng Go.

OK! chúng ta là dân TIN-HỌC, nghĩa là tin đã rồi mới học, đến đây có lẻ bạn đã thấy được sức mạnh và xu hướng của Golang đồng thời nắm được những đặc điểm chính của Golang, tin rồi thì học thôi nào, cùng tiếp tục đọc các bài viết về Golang tiếp theo của mình nhé! cám ơn các bạn.
