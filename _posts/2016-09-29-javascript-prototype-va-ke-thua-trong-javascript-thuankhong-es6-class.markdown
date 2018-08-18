---
title: 'Javascript – Prototype Và Kế Thừa'
layout: post
date: 2016-09-29 12:18
image: /assets/images/
headerImage: false
tag:
    - Javascript
    - Prototype
category: blog
author: My Le Phuoc
description: Markdown summary with different options
# jemoji: '<img class="emoji" title=":ramen:" alt=":ramen:" src="https://assets.github.com/images/icons/emoji/unicode/1f35c.png" height="20" width="20" align="absmiddle">'
---

Prototype là khái niệm rất rất quan trọng mà các Javascript Engineer phãi hiểu và tận dụng nó tốt. Đây là thành phần mà theo bản thân mình nghĩ gần như là cốt lõi của Javascript. Trong bài viết này chúng ta sẻ thảo luận và làm rõ những điểm cơ bản của thành phần này.

Ban đầu Javascript cung cấp hàm Object() và một Object nặc danh có thể được tham chiếu đến bằng cú pháp **Object.prototype**, bật console lên và thử là biết ngay á mà:

{% highlight js %}
console.log(Object);
console.log(Object.prototype);
{% endhighlight %}

Object **Object.prototype** có những thuộc tính có sẳn như **valueOf**, **toString**, **toLocaleString**, **propertyIsEnumerable**, **isPrototypeOf**, **hasOwnProperty**, **constructor**. Trong đó thuộc tính **constructor** là thuộc tính trỏ ngược lại hàm **Object()**, thử cái để thấy nè:

{% highlight js %}
console.log(Object.prototype.constructor); // ƒ Object() { [native code] }
console.log(Object()); // ƒ Object() { [native code] }
{% endhighlight %}

Giả sử vòng tròn đại diện cho hàm **Object()** và hình vuông đại diện cho đối tượng **Object.prototype**. Hình dưới đây minh họa mối quan hệ giữa hàm **Object()** và đối tượng Object:
![Markdowm Image][1]

Ok, bây giờ chúng ta sẻ định nghĩa và sử dụng một cái giống như class trong các ngôn ngữ như Java, C#,…

{% highlight js %}
// Animal class
var Animal = function(name,age) {
this.name = name || "";
this.age = age || 0;
};

//Implement method for animal class
Animal.prototype.getName = function() {
return "my name is "+this.name;
};
Animal.prototype.getAge = function() {
return "my age is "+this.age;
};

// create a new instance of the Animal object.
var texDy = new Animal("TEXDY",3)
texDy.getName(); //my name is TEXDY
texDy.getAge(); //my age is 3
{% endhighlight %}

Trong đoạn code trên ta đã dễ dàng định nghĩa và sử dụng cơ bản môt cái giống như class, đó là hàm Animal(name,age) chấp nhận hai đối số, thêm thuộc tính name và age cho đối tượng và đặt giá trị của thuộc tính name bằng đối số name, age bằng đối số age. Nhìn việc định nghĩa Animal đơn giản như thế, tuy nhiên phía sau nó Javascript thực hiện không hề đơn giản, Javascript tạo ra hàm Animal và thêm một đối tượng nặc danh nữa. Giống như đối tượng hàm Object ban đầu, hàm Animal có một thuộc tính có tên là prototype tham chiếu đến đối tượng nặc danh và đối tượng nặc danh có thuộc tính constructor trỏ về hàm Animal(). Ngoài ra, đối tượng Animal.prototype được liên kết với đối tượng Object.prototype thông qua [[Prototype]], được gọi là prototype linkage. Prototype linkage được ký hiệu bằng [[Prototype]], chúng được mô tả ở hình bên dưới:
![Markdowm Image][2]

Và khi thêm phương thức cho Animal chỉ đơn giản là thêm phương thức cho đối tượng nặc danh mà Animal.prototype tham chiếu đến:
![Markdowm Image][3]
Khi tạo 1 instance của object Animal:
{% highlight js %}
var texDy = new Animal("TEXDY",3)
{% endhighlight %}

Khi thực thi dòng code trên thì Javascript tạo ra một Object mới tên là texDy, object này link đến Animal.prototype thông qua prototype linkage, việc link từ texDy đến Animal.prototype đến Object.prototype được gọi là prototype chain.

Khi một instance của một Object hay một Object nào đó gọi một phương thức, đầu tiên nó sẻ tìm xem nó hiện tại có giữ phương thức thức đó không, nếu không có thì sẻ duyệt từng prototype trong prototype chain từ dưới lên trên để tìm phương thức đó nếu có thì gọi. Lấy ví dụ như chương trình trên, đối tượng texDy vốn dĩ không chứa phương thức getName và getAge nên khi gọi hai phương thức đó texDy sẻ duyệt prototype chain để tìm và duyệt đến Animal.prototype thì gặp hai phương thức và gọi.

Nếu chúng ta gọi lệnh texDy.hasOwnProperty() thì nó sẻ tìm không có trong đối tượng texDy, Animal.prototype nên nó sẻ tìm lên đến Object.prototype, thấy phương thức đó và sẻ gọi Object.prototype,.hasOwnProperty().

Giả xử ta định nghĩa thêm một phương thức mới cho:
{% highlight js %}
texDy.getFullInfo = function(){
return "My name is"+this.name+" ,i'm "+this.age+" years old"
}
{% endhighlight %}

Thì khi gọi phương thức texDy.getFullInfo(); sẻ trả về ngay “My name isTEXDY ,i’m 3 years old”, đây là phương thức đã được định nghĩa ở Object texDy nên Javascript sẻ không phãi tìm trong prototype chain, đồng thời các instance khác của Animal sẻ không dùng được phương thức đó.

Cũng tương tự vậy, nếu chúng ta định nghĩa một phương thức getName mới cho texDy như sau:

{% highlight js %}
texDy.getName = function() { return "Toi la "+this.name; };
{% endhighlight %}

Thì khi gọi texDy.getName() sẻ không còn in ra “my name is TEXDY” nữa mà sẻ in ra “Toi la TEXDY”, vì sao vậy, vì đơn giản là texDy đã có phương thức getName rồi, nó sẻ không phãi gọi lên prototype của cha nó nữa.

Ok, tới đây chắc clear rồi. Tóm lượt lại một lần nữa, Javascript sẻ kế thừa các phương thức, thuộc tính bằng cách tìm trong prototype chain đến các prototype của cha, ông, cố,…. của nó.

[1]: /assets/images/2016-09-29-javascript-prototype-va-ke-thua-trong-javascript-thuankhong-es6-class/1.jpg
[2]: /assets/images/2016-09-29-javascript-prototype-va-ke-thua-trong-javascript-thuankhong-es6-class/2.jpg
[3]: /assets/images/2016-09-29-javascript-prototype-va-ke-thua-trong-javascript-thuankhong-es6-class/3.jpg
