# example
I want to do this project
Full stack lập trình ứng dụng Web bằng Python phần 1: Giới thiệu
Đây là phần đầu tiên trong series hướng dẫn lập trình ứng dụng Web gồm 20 phần.

Phần 1: Giới thiệu (đang xem)
Phần 2: Kiến trúc ứng dụng và stack
Phần 3: Web server asynchronous với asyncio và Sanic
Phần 4: Authentication bằng JWT với Sanic, chức năng login
Phần 5: Database MongoDB với Motor Driver
Phần 6: Refactor cấu trúc ứng dụng
Phần 6: Giao tiếp với backend qua AMQP: service crawl data và download ảnh
Phần 7: Machine learning và service nhận dạng ảnh với Keras
Phần 8: Machine learning và service nhận dạng ảnh với Keras (tiếp)
Phần 9: Websocket và chức năng nhận dạng ảnh gửi lên client
Phần 10: Deploy service với Docker và Docker-Compose
Phần 11: Sử dụng GraphQL thay cho REST, một API cho mọi client
Phần 12: ReactJS: Giới thiệu cơ bản ReactJS và Ecosystem
Phần 13: Single Page Application với React-Router
Phần 14: State Management với Redux
Phần 15: Caching với Redis
Phần 16: Chức năng Search dùng ElasticSearch
Phần 17: Monitoring và Logging
Phần 18: Triển khai ứng dụng lên Google Cloud Platform
Phần 19: CI và CD
Phần 20: Scale ứng dụng (phần cuối)
Giới thiệu series
Chào mừng đến với series hướng dẫn lập trình ứng dụng Web full stack Python. Mục tiêu của loạt bài này là hướng dẫn một stack công nghệ hoàn chỉnh để build ứng dụng Web hiện đại.

Có rất nhiều tutorial và sách hướng dẫn về “full-stack” hầu hết đều chỉ tập trung vào phần viết ứng dụng frontend, thuật ngữ “full-stack javascript” mang ý nghĩa là web application gồm client phía browser và server nodejs trả về api cho user ở client.

Trong các ứng dụng web hiện đại, yêu cầu nhiều xử lý backend, cpu bound như cần xử lý ngôn ngữ, hình ảnh, xử lý dữ liệu lớn, machine learning thì hệ thống cần một kiến trúc phức tạp hơn, nhiều lớp xử lý phía backend.

Một series 20 bài viết sẽ không thể đi hết chi tiết các vấn đề này, mình sẽ cố gắng thông qua việc build một ứng dụng demo để giới thiệu cơ bản các thành phần bắt buộc có để xây dựng một ứng dụng thông minh, giúp người đọc có keyword để học kỹ năng trở thành một fullstack developer.

Ứng dụng demo sẽ build là “Programmer like Dog or Cat ?"
Đây là ứng dụng demo của Google Cloud Platform, link github dưới đây:

JustinBeckwith/cloudcats

cloudcats - CloudCats is an example of using node.js and various Google Cloud APIs and services to solve the greatest…
github.com	

Programmer like Dogs or Cats?
Chức năng của app này là crawl ảnh một thread /r/programmer trên reddit và nhận dạng phân loại ảnh chó hay mèo. Data được xử lý liên tục phía backend và push lên client qua websocket.

Phiên bản NodeJS của Google chỉ handle phần frontend server, sử dụng API Machine Learning của Google. Trong series này mình sẽ implement toàn bộ app bằng Python cho server và Javascript cho client. Bạn sẽ được học:

Viết ứng dụng client Single Page Application với ReactJS
Viết ứng dụng server Web non-blocking IO bằng Python với asyncio, Sanic, API dùng GraphQL
Viết backend service để xử lý heavy task và giao tiếp qua RabbitMQ
Machine learning xử lý hình ảnh bằng Keras, thư viện wrap Tensorflow và Theano, tích hợp Keras vào ứng dụng thực tế
Websocket và GraphQL Subscription
Deploy microservice bằng Docker lên Google Cloud Platform
Và nhiều vấn đề khác như CI, CD, cache, search engine, monitoring, log, scale ứng dụng …
Why Python ?
Diễn giải về stack này mình sẽ ở phần 2, ở đây mình muốn nói thêm về tại sao lại chọn Python.

Với các hệ thống lớn, tuỳ vào service và kỹ năng của team có nhiều lựa công nghệ khác nhau. Tuy nhiên để build sản phẩm nhanh, và một stack cho cả sản phẩm, phù hợp các dự án startup, thì có 2 lựa chọn hàng đầu là Python và NodeJS.

NodeJS đang là trend, có 2 ưu điểm lớn nhất là Javascript everywhere và tốc độ do Non-blocking IO. Nhưng 2 đặc điểm này chỉ xét đến trong ngữ cảnh là web service chỉ handle request phía frontend, và không xử lý heavy task. Thực tế các công ty lớn như Paypal, NetFlix dùng NodeJS chỉ cho frontend server, backend đều được xây dựng từ trước bằng các ngôn ngữ như Java, Go.

Ưu điểm của Python thì có nhiều trên mạng mình không nói lại ở đây. Có vài điểm mình muốn nhấn mạnh:

Python là ngôn ngữ cho xử lý dữ liệu, machine learning
Về tốc độ, trong các bài benchmark so sánh Python và Node hầu hết đều dùng server WSGI, synchronous hay các server asynchronous cũ như Tornado, Gevent. Từ bản Python 3, hỗ trợ lập trình async với thư viện asyncio, có rất nhiều project server nonblocking io có tốc độ vượt qua NodeJS, thậm chí Go nhiều lần:
uvloop: Blazing fast Python networking

asyncio is an asynchronous I/O framework shipping with the Python Standard Library. In this blog post, we introduce…
magic.io	
A million requests per second with Python

Is it possible to hit a million requests per second with Python? Probably not until recently.
medium.freecodecamp.org	
Asychronous là mô hình lập trình đã có từ lâu, tuy nhiên trước đây khi chưa có asyncio, các thư viện như Gevent, Greenlet, Tornado implement cơ chế async của riêng nó trên, và không có một quy chuẩn, dẫn đến ecosystem không phát triển được.

Các project asynchronous Python đều mới chỉ bắt đầu từ 2016 và đang growth rât nhanh. Lý do là từ phiên bản 3.4 trở đi mới có thư viện asyncio và từ Python 3.6 mới hỗ trợ async/await.

Concurrency là xu hướng của Python, nhưng mình nhận thấy cộng đồng ở Việt Nam có vẻ chưa chú ý đúng mức. Dạo qua một vòng internet mới chỉ thấy các bài viết về coroutine, asyncio ở góc độ giới thiệu kỹ thuật, các ứng dụng về concurrency đều sử dụng multi thread, multi processor để xử lý các bài toán workaround hay đặc thù heavy task, chưa thực sự được nhìn nhận là một programming model. Hi vọng sẽ nhận được phản hồi của các bạn về vấn đề này.

Kết thúc phần giới thiệu tại đây. Mình sẽ tạo project trên github, mỗi phần trong series sẽ có đầy đủ source code, để mọi người follow step by step.

