
[Source](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0 "Permalink to Master the JavaScript Interview: What is Functional Programming?")

# Bậc thầy về phỏng vấn Javascript : Lập trình chức năng là gì?

![][1]

Structure Synth — Orihaus (CC BY 2.0)

> "Master the JavaScript Interview" là 1 series các bài viết được thiết kế để chuẩn bị cho người xin việc những câu hỏi thông thường mà họ rất dễ gặp khi ứng tuyển cho các vị trí Javascript trình độ từ cấp trung đến cấp cao. Đây đều là những câu hỏi tôi thường sử dụng trong phỏng vấn thực tế.  

Lập trình chức năng đã trở thành một chủ đề rất hot trong thế giới JS. Một vài năm trước, chỉ một vài lập trình viên JS biết function programming là gì, nhưng mọi mã nguồn của các ứng dụng lớn tôi thấy trong 3 năm qua đêu mang nặng tư tưởng của lập trình hàm.  

**Functional programming** (thường viết tắt là FP) là tiến trình xây dựng phần mềm bằng **pure functions**, tránh **shared state,** **mutable data,** và  **side-effects**. Lập trình hàm mang tính **declarative** hơn là **imperative**, và các thuộc tính của ứng dụng sẽ đi theo các pure function. đối lập với lập trình hướng đối tượng, nơi mà thuộc tính của ứng dụng thường chia sẻ và đặt chung với phương thức trong đối tượng.  

Lập trình hàm là một **mô hình lập trình**, có nghĩa là đây là cách suy nghĩ về việc xây dựng phần mềm dựa trên nền móng, các nguyên tắc được định nghĩa cơ bản, (liệt kê bên dưới). Những ví dụ khác về các mô hình lập trình bao gồm lập trình hướng đối tượng và lập trình hàm.  

Lập trình hàm có xu hướng ngắn gọn hơn, dễ đoán hơn, và dễ dàng kiểm thử hơn lập trình imperative hay hướng đổi tượng - nhưng nếu bạn không quen với nó cũng như các pattern liên quan, lập trình hàm có thể nặng nề hơn, và tài liệu liên quan sẽ khó hiểu đối với những người mới.  

Nếu bạn bắt đầu google cụm từ functional programming, bạn sẽ nhanh chóng húc phải bức tường academic lingo mà cực kỳ đáng sợ với người mới bắt đầu. Sẽ là nói dối nếu bảo có cách nhanh chóng để học chúng. Nếu bạn đã lập trình Javascript một thời gian,rất có thể bạn đã sử dụng rất nhiều khái niệm và tiện ích lập trình chức năng trong phần mềm thực tế của bạn.

> Đừng để tất cả từ ngữ mới làm bạn sợ . Nó dễ hơn bạn nghĩ.

Phần khó nhất là tiêu hóa hết tất cả các từ vựng lạ. có rất nhiều nội dung trong các tìm kiếm định nghĩa vu vơ cần được hiểu trước khi bạn có thể bắt đầu nắm lấy ý tưởng của lập trình hàm: 

* Pure functions
* Function composition
* Avoid shared state
* Avoid mutating state
* Avoid side effects

Nói cách khác, nếu bạn muốn biết ý nghĩa của lập trình hàm trong thực tế, bạn phải bắt đầu với việc tìm hiểu những khái niệm căn bản sau:  

**pure function** là hàm mà:
* với input gióng nhau sẽ luôn cho output giống nhau
* Không có side-effects.  

Pure functions có rất nhiều tính chất quan trọng của lập trình hàm, bao gồm **referential transparency** (bạn có thể thay thế lời gọi hàm với kết quả trả về của nó mà không phải thay đổi ý nghĩa của chương trinh). Đọc ["What is a Pure Function?"][2] để biết thêm chi tiết.  

**Function composition** là quá trình gộp 2 hay nhiều hàm để tạo ra 1 hàm mới hay thực hiện một vài tính toán. Ví dụ, gộp hàm `f . g` (dấu chấm nhgiax là) "compose với") tương đương với `f(g(x))` trong JavaScript. Hiểu function composition là một bước quan trọng để hiểu cách xây dựng phần mềm sử dụng lập trình hàm. Đọc ["What is Function Composition?"][3] để biết thêm.

### Shared State

**Shared state** là bất cứ biến, đối tượng, hay vùng nhớ nào tồn tại trong một scope được chia sẻ hoặc một thuộc tính của một đối tượng được truyền vào scope. một scope được chia sẻ bao gồm global scope hoặc closure scopes. Thông thường trong lập trình hướng đối tượng, các đối tượng được chia sẻ trong scope bằng cách thêm các thuộc tính vào các đối tượng khác.

Ví dụ, một trò chơi máy tính có thể có một đối tượng game chính, với các nhân vật và các item trò chơi được lưu thành các thuộc tính trong đối tượng đó. Lập trình hàm thường tránh shared state - thay vì dựa vào các cấu trúc dữ liệu không thay đổi và các phép tính thuần để lấy được các dữ liệu mới từ các dữ liệu sẵn có. Chí tiết hơn về cách mà phần mềm chức năng có thể xử lý các trạng thái của ứng dụng, xem cuốn "[10 Tips for Better Redux Architecture][4]".

Vấn đề với shared state là để hiểu về hiệu lực của một hàm, bạn phải biết toàn bộ lịch sử của mỗi biến được chia sẻ mà hàm sử dụng hay tác động đến.  

Hãy tưởng tượng rằng bạn có 1 đối tượng người dùng cần được lưu. hàm saveUser() của bạn tạo 1 request đến 1 API trên server. Trong khi điều này xảy ra, người dùng lại thay đổi ảnh đại diện với hàm updateAvatar() và gọi 1 request saveUser() khác. Khi được lưu, server trả về 1 đối tượng người dùng được chấp nhận mà nên thay thế bất cứ thứ gì trong bộ nhớ để có thể đồng bộ với những thay đổi xảy ra trên server hay trong response đến 1 lời gọi API khác.  

Thật không may, reponse thứ 2 lại được nhận trước response thứ nhất, vì vậy khi cái thứ nhất (giờ đã bị lỗi thời) được trả về, ảnh đại diện mới được lưu trong bộ nhớ và thay thế cho cái cũ. Đây là một ví dụ 1 của trường hợp - lỗi rất phổ biến liên quan đến share state.  

1 vấn đề phổ thông khác liên quan đến shared state là thay đổi thứ tự mà các hàm được gọi có thể dẫn tới việc những thất bại liên tục vì các hàm thực hiện trên shared state phụ thuộc vào thời gian:  

Ví dụ phụ thuộc thời gian  

Khi bạn tránh việc shared state, thời gian và thứ tự của các hàm gọi không thay đổi kết quả của việc gọi hàm. Với những hàm pure, cùng 1 đầu vào, bạn luốn có được cùng đầu ra. Điều này làm các lời gọi hạm hoàn toàn độc lập với các gọi hàm khác, hoàn toàn đơn giản hóa việc thay đổi và tái cấu trúc. 1 thay đổi trên 1 hàm, hay thời gian hàm gọi không ảnh hưởng và phá vỡ các phần khác của chương trình.  

Trong ví dụ bên trên, chúng tôi sử dụng Object.assign() và truyền nó trong 1 đối tượng rỗng như 1 tham số đầu tiên để sao chếp các thuộc tính của x thay vì biến đổi nó bên trong. Trong trường hợp này, nó tương đương với việc tạo 1 đối tượng với từ scratch, và không cần có Object.assign(), những đây là 1 ví dụ phổ biến trong Javascript để tạo 1 bản sao của trạng thái đang tồn tại thay vì sử dụng các chuyển đổi, mà chúng tôi đã mô tả trong ví dụ đầu tiên.  

Nếu bạn để ý kĩ hơn trong console.log() trong ví dụ này, bạn sẽ nhận thấy 1 vài thứ đã được đề cập : function composition. Nhắc lại 1 chút, function composition giống như kiểu f(g(x)). Trong trường hợp này, húng ta thay f() và g() với x1() và x2() để cho phép gộp x1.x2  

Tất nhiên, nếu bạn thay đổi thứ tự của phép gộp, đầu ra cũng sẽ thay đổi. Thứ tự của việc thực hiện sẽ ảnh hưởng. f(g(x)) không luôn băng `g(f(x))`, nhưng những gì không ảnh hưởng nữa là những thứ xảy ra với các biến bên ngoài hàm - và đây là 1 canh bạc lớn. Với các hàm impure, không thể hoàn toàn hiểu được 1 hàm làm gì trừ khi bạn biết toàn bộ lịch sử của mỗi biến hàm sử dụng hoặc ảnh hưởng,  

Loại bỏ các lời gọi hàm ảnh hưởng bởi thời gian, và loại trừ toàn bộ các lớp của các lỗi tiềm ẩn.  

### Tính bất biến  

Một đối tượng **bất biến** là một đối tượng mà không thể chỉnh sửa sau khi nó được tạo ra. Ngược lại, đối tượng **khả biến** là một đối tượng bất kì có thể chỉnh sửa được sau khi được tạo ra.  

Tính bất biến là một khái niệm trọng tâm của lập trình hàm vì nếu không có nó, luồng dữ liệu trong chương trình của bạn sẽ bị mất mát. Lịch sử trạng thái bị bỏ qua và các lỗi lạ có thể xuất hiện trọng phần mềm của bạn. Để hiểu hơn về ý nghĩa của sự bất biến, đọc ["The Dao of Immutability"][5].  

Trong JavaScript, điều quan trọng là không nhầm lẫn const, với bất biến. const tạo ra một ràng buộc tên biến mà không thể được gán lại sau khi tạo. const không tạo ra các đối tượng bất biến. Bạn không thể thay đổi đối tượng mà ràng buộc đề cập đến, nhưng bạn vẫn có thể thay đổi các thuộc tính của đối tượng, có nghĩa là các ràng buộc được tạo bằng const là có thể thay đổi, không bất biến.  

Các đối tượng bất biến hoàn toàn không thể bị thay đổi. Bạn có thể tạo 1 giá trị hoàn toàn bất biến bằng cách đóng băng đối tượng ở mức rất sâu. Javascript có một phương thức có thể đóng băng đối tượng một mức:  

Nhưng việc đóng băng đối tượng chỉ là sự bất biến ở bề ngoài. Ví dụ, đối tượng sau là không bất biến:  

Như bạn có thể thấy, các thuộc tính nguyên thủy cấp cao nhất của một đối tượng được đóng băng không thể thay đổi, nhưng bất kỳ thuộc tính nào cũng là một đối tượng (bao gồm mảng, vv…) vẫn có thể bị thay đổi - vì vậy ngay cả đối tượng bị đóng băng cũng không phả bất biến trừ khi bạn duyệt qua toàn bộ cây đối tượng và đóng băng mọi thuộc tính của nó.  

Trong nhiều ngôn ngữ lập trình hàm, có cấu trúc dữ liệu bất biến đặc biệt gọi là **cấu trúc dữ liệu trie** (được phát âm là “tree”) được đóng băng một cách hiệu quả — có nghĩa là không có thuộc tính nào có thể thay đổi, bất kể cấp độ của thuộc tính trong hệ thống phân cấp đối tượng.  

Các trie sử dụng chia sẻ cấu trúc để chia sẻ các vị trí bộ nhớ tham chiếu cho tất cả các phần của đối tượng không thay đổi sau khi một đối tượng được sao chép bởi một toán tử, sử dụng ít bộ nhớ hơn và cho phép cải thiện hiệu suất đáng kể cho một số loại hoạt động.  

Ví dụ, bạn có thể sử dụng so sánh định danh tại gốc của cây đối tượng để so sánh. Nếu định danh giống nhau, bạn không phải duyệt qua cả cây để kiểm tra sự khác biệt.  

Có một số thư viện trong JavaScript tận dụng các trie, bao gồm [Immutable.js][6] và [Mori][7].  

Tôi đã thử nghiệm với cả hai, và có xu hướng sử dụng Immutable.js trong các dự án lớn đòi hỏi một lượng khá đáng kể trạng thái bất biến. Để biết thêm về điều đó, hãy đọc ["10 Tips for Better Redux Architecture"][4].  


### Side Effects

Một hiệu ứng phụ là bất kỳ thay đổi trạng thái của ứng dụng nào mà có thể quan sát được bên ngoài hàm được gọi, ngoài giá trị trả về của nó. Các hiệu ứng phụ bao gồm:  

* Sửa đổi bất kỳ biến bên ngoài hoặc thuộc tính đối tượng nào (ví dụ: biến toàn cục hoặc biến trong chuỗi phạm vi hàm chính) 
* Ghi ra console  
* Viết ra màn hình
* Viết ra 1 file
* Viết vào mạng
* Gọi 1 tiến trình bên ngoài
* Gọi các hàm khác với các ảnh hưởng phụ  

Hiệu ứng phụ là thứ nên tránh nhất trong lập trình hàm, làm cho hiệu quả của một chương trình dễ hiểu hơn nhiều, và dễ dàng kiểm tra hơn nhiều.  

Haskell và các ngôn ngữ hàm khác thường xuyên cô lập và đóng gói các tác dụng phụ từ các hàm thuần túy bằng cách sử dụng monads. Chủ đề của các monads đủ sâu để viết một cuốn sách, vì vậy chúng ta sẽ lưu ý cuốn sách đó sau này.  

Những gì bạn cần biết ngay bây giờ là các tác vụ phụ cần phải được cô lập với phần còn lại của phần mềm của bạn. Nếu bạn giữ các hiệu ứng phụ tách biệt với phần còn lại của logic chương trình, phần mềm của bạn sẽ dễ dàng hơn để mở rộng, tái cấu trúc, gỡ lỗi, kiểm tra và bảo trì.  

Đây là lý do mà hầu hết các framework front-end khuyến khích người dùng quản lý hiển thị trạng thái và thành phần trong các modules riêng lẻ, tách biệt nhau.  

### Tái sử dụng thông qua hàm bậc cao  

Lập trình hàm có xu hướng tái sử dụng lại một tập hợp các hàm tiện ích phổ biến để xử lý dữ liệu. Lập trình hướng đối tượng có xu hướng phân bổ phương thức và dữ liệu trong các đối tượng. Những phương thức được phân bổ chỉ có thể hoạt động trên loại dữ liệu mà chúng được thiết kế để hoạt động và thường chỉ có dữ liệu chứa trong cá thể đối tượng cụ thể đó..  

Trong lập trình hàm, bất kỳ loại dữ liệu nào đều là tương đương nhau. Cùng một tiện ích map() có thể ánh xạ đối tượng, chuỗi, số hoặc bất kỳ kiểu dữ liệu nào khác vì nó lấy hàm làm đối số xử lý thích hợp loại dữ liệu đã cho. FP rút ra thủ thuật tiện ích chung của nó bằng cách sử dụng **các hàm bậc cao hơn**.  

JavaScript có **các lớp hàm đầu tiên**, cho phép chúng ta xử lý các hàm như dữ liệu - gán chúng cho các biến, chuyển chúng đến các hàm khác, trả về chúng từ các hàm, v.v.  

Hàm **bậc cao hơn** là bất kỳ hàm nào nhận hàm làm đối số, trả về hàm hoặc cả hai. Các hàm bậc cao thường được sử dụng để:  

* Tóm tắt hoặc cô lập hành động, hiệu ứng hoặc điều khiển luồng không đồng bộ bằng cách sử dụng hàm callback, promise, monad, v.v.  
* Tạo các tiện ích có thể hoạt động trên nhiều loại dữ liệu khác nhau  
* Áp dụng một phần hàm cho các đối số của nó hoặc tạo một hàm được kết hợp với mục đích sử dụng lại hoặc hàm hợp  
* Lấy danh sách các hàm và trả về một số thành phần của các hàm đầu vào đó  

#### Containers, Functors, Lists, and Streams  

Một functor là một thứ có thể được ánh xạ qua. Nói cách khác, nó là một container có một giao diện có thể được sử dụng để áp dụng một hàm cho các giá trị bên trong nó. Khi bạn nhìn thấy từ functor, bạn nên nghĩ rằng "có thể ánh xạ".  

Trước đó chúng ta đã biết rằng cùng một tiện ích `map()` có thể hoạt động trên nhiều kiểu dữ liệu khác nhau. Nó làm điều đó bằng cách nâng hoạt động ánh xạ để làm việc với một API functor. Các hoạt động kiểm soát lưu lượng quan trọng được sử dụng bởi `map()` tận dụng giao diện đó. Trong trường hợp `Array.prototype.map()`, vùng chứa là một mảng, nhưng các cấu trúc dữ liệu khác cũng có thể là các hàm functors - miễn là chúng cung cấp việc ánh xạ API.  

Hãy xem cách `Array.prototype.map()` cho phép bạn trừu tượng kiểu dữ liệu từ tiện ích ánh xạ để làm cho `map()` có thể sử dụng được với bất kỳ kiểu dữ liệu nào. Chúng ta sẽ tạo một ánh xạ `double()` đơn giản, chỉ đơn giản là nhân bất kỳ giá trị nào được truyền vào bởi 2:

Điều gì sẽ xảy ra nếu chúng ta muốn hoạt động trên các mục tiêu trong một trò chơi để tăng gấp đôi số điểm mà họ giành được? Tất cả những gì chúng ta phải làm là tạo ra một thay đổi tinh tế cho hàm `double()` mà chúng ta truyền vào `map()`, và mọi thứ vẫn hoạt động:

Khái niệm sử dụng các phép trừu tượng như hàm functors và các hàm bậc cao hơn để sử dụng các hàm tiện ích chung để thao tác với bất kỳ số lượng các kiểu dữ liệu khác nhau nào là quan trọng trong lập trình hàm. Bạn sẽ thấy một khái niệm tương tự được áp dụng trong [tất cả các cách khác nhau][9].

> "Danh sách được biểu thị theo thời gian là một luồng."

Tất cả những gì bạn cần để hiểu bây giờ là mảng và functors không phải là cách duy nhất mà khái niệm container và giá trị trong các container được áp dụng. Ví dụ, một mảng chỉ là một danh sách. Danh sách được hiển thị theo thời gian là luồng - vì vậy bạn có thể áp dụng cùng một loại tiện ích để xử lý luồng sự kiện tiếp diễn - thứ mà bạn sẽ thấy rất nhiều khi bạn bắt đầu xây dựng phần mềm thực với FP.



### Declarative vs Imperative  

Lập trình hàm là một mô hình declarative, có nghĩa là logic chương trình được biểu diễn mà không mô tả rõ ràng điều khiển luồng.  

Các chương trình **Imperative** dành các dòng code mô tả các bước cụ thể được sử dụng để đạt được kết quả mong muốn - **điều khiển luồng:Cách thực hiện**.  

Các chương trình **Declarative** trừu tượng quá trình kiểm soát luồng, và thay vào đó dành các dòng code mô tả **luồng dữ liệu: Phải làm gì**. Làm thế nào để bị tóm tắt.  

Ví dụ, ánh xạ **Imperative** này lấy một mảng các số và trả về một mảng mới với mỗi số nhân với 2:  

Ánh xạ **Declarative** này cũng làm điều tương tự, nhưng tóm tắt điều khiển luồng bằng cách sử dụng tiện ích hàm `Array.prototype.map()`, cho phép bạn thể hiện rõ ràng luồng dữ liệu:  

Code **Imperative** thường xuyên sử dụng các câu lệnh. Câu lệnh là một đoạn code thực hiện một số hành động. Ví dụ về các câu lệnh thường được sử dụng bao gồm `for`,`if`, `switch`,`throw`, v.v ...  

Code **declarative** dựa nhiều hơn vào biểu thức. Biểu thức là một đoạn mã đánh giá một số giá trị. Biểu thức thường là một số kết hợp của các lời gọi hàm, giá trị và toán tử được đánh giá để tạo ra giá trị kết quả.  

Đây là tất cả các ví dụ về biểu thức:
```
    2 * 2  
    doubleMap([2, 3, 4])  
    Math.max(4, 3, 2)
```

Thông thường trong code, bạn sẽ thấy các biểu thức được gán cho một mã định danh, được trả về từ các hàm, hoặc được chuyển vào một hàm. Trước khi được chỉ định, trả về hoặc được thông qua, biểu thức được đánh giá đầu tiên và giá trị kết quả được sử dụng.  

### Kết luận  

Các dấu hiệu của lập trình hàm:  

* Các hàm thuần túy thay vì các tác dụng phụ và trạng thái được chia sẻ
* Tính bất biến trên dữ liệu thay đổi
* Hàm hợp trên điều khiển lưu lượng bắt buộc
* Rất nhiều tiện ích chung, có thể tái sử dụng sử dụng các hàm bậc cao hơn để hành động trên nhiều loại dữ liệu thay vì các phương thức chỉ hoạt động trên dữ liệu được phân bổ của chúng
* Tuyên bố chứ không phải là code bắt buộc (phải làm gì, hơn là làm thế nào để làm điều đó)
* Diễn đạt chứ không phát biểu  
* Các hàm chứa & hàm bậc cao hơn là ad-hoc đa hình


### Level Up Your Skills

[Learn JavaScript with Eric Elliott][10]. Nếu không phải là thành viên, bạn sẽ bỏ lỡ  

![][11]

[1]: https://cdn-images-1.medium.com/max/1600/1*1OxglOpkZHLITbIKEVCy2g.jpeg
[2]: https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-pure-function-d1c076bec976
[3]: https://medium.com/javascript-scene/master-the-javascript-interview-what-is-function-composition-20dfb109a1a0
[4]: https://medium.com/javascript-scene/10-tips-for-better-redux-architecture-69250425af44
[5]: https://medium.com/javascript-scene/the-dao-of-immutability-9f91a70c88cd
[6]: https://github.com/facebook/immutable-js
[7]: https://github.com/swannodette/mori
[8]: https://en.wikipedia.org/wiki/Monad_%28functional_programming%29
[9]: https://github.com/fantasyland/fantasy-land
[10]: http://ericelliottjs.com/product/lifetime-access-pass/
[11]: https://cdn-images-1.medium.com/max/1600/1*3njisYUeHOdyLCGZ8czt_w.jpeg

  
