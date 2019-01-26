## GPU ảo – vGPU (virtual GPU) là gì?

<img src="/img/1.png">

* Công nghệ ảo hóa cho các ứng dụng và máy tính để bàn đã tồn tại trong một thời gian dài, nhưng không phải lúc nào công nghệ này cũng được ủng hộ như người ta đã cường điệu về nó. Lỗi lớn nhất: trải nghiệm người dùng kém.

Và cho đến khi GPU ảo – vGPU (virtual GPU) – xuất hiện.

<img src="/img/12.jpg">

* Trên một thiết bị máy tính vật lý truyền thống như workstations, PC hoặc laptops, một GPU thường thực hiện tất cả việc chụp, mã hóa và hiển thị để thực hiện các tác vụ phức tạp, chẳng hạn như ứng dụng 3D và video. Với các phiên bản ảo hóa đầu tiên chỉ dừng lại ở mức ảo hóa CPU. Và do đó, nó chỉ đáp ứng được cho một số ứng dụng cơ bản. Ảo hóa CPU chưa đáp ứng trải nghiệm nguyên vẹn từ gốc và mức hiệu suất mà hầu hết người dùng cần.

* Điều đó đã thay khi NVIDIA công bố về GPU ảo. Ảo hóa một hệ thống có GPU bên trong tức là cho phép GPU được chia sẻ trên nhiều máy ảo (VM – virtual machines). Với hiệu suất được cải thiện đáng kể dành cho các applications và desktop, các tổ chức có thể ứng dụng để xây dựng cơ sở hạ tầng cho máy tính để bàn ảo (hoặc VDI) một cách hiệu quả hơn.

* Vậy, GPU làm gì?

<img src="/img/2.png">


* Một đơn vị xử lý đồ họa có hàng ngàn lõi máy tính để xử lý công việc song song. Các ứng dụng 3D, video và hiển thị hình ảnh là những ứng dụng đòi hỏi cao tính năng xử lý song song.
Khả năng xử lý các tác vụ song song của GPU giúp tăng tốc các ứng dụng. Các kỹ sư dựa vào chúng cho những ứng dụng hạng nặng như dựng phim 3D, CAE, CAD, phân tích toán học, deep learning, machine learning….

* Tất nhiên, bất kỳ bộ xử lý nào cũng có thể hiển thị đồ họa. 4, 8 hoặc 16 lõi có thể thực hiện công việc này. Nhưng với hàng nghìn lõi chuyên dụng trên GPU, không phải chờ đợi lâu, các ứng dụng được hỗ trợ tốt hơn và chạy nhanh hơn.

* Phần mềm tạo ra GPU ảo:

* Phần mềm này biến đổi một GPU vật lý được cài đặt trên một máy chủ để tạo các GPU ảo (vGPU) có thể được chia sẻ trên nhiều máy ảo (VM) khác nhau. Nó không còn là mối quan hệ một – một giữa GPU với người dùng, mà là một – nhiều.

* Phần mềm NVIDIA vGPU cũng bao gồm một trình điều khiển đồ họa cho máy ảo. Điều này cho phép mỗi máy ảo có được những lợi ích của một GPU giống như một máy tính để bàn vật lý. Nhưng bởi vì các workloads trước đây thường được thực hiện bởi CPU thì giờ chúng đã được tải xuống GPU, người dùng có trải nghiệm tốt hơn và hỗ trợ được nhiều người dùng hơn.

* NVIDIA vGPU bao gồm bộ 3 sản phẩm được thiết kế để đáp ứng những thách thức của nơi làm việc kỹ thuật số:

<ul>

– Máy tính ảo NVIDIA GRID (GRID vPC) dành cho Office Users

– Ứng dụng ảo GRID của NVIDIA (GRID vApps) dành cho knowledge users

– Trung tâm dữ liệu ảo Quadro (Quadro vDWS) cho nhà thiết kế , kỹ sư và kiến trúc sư.

</ul>

* NVIDIA GRID mang lại trải nghiệm tuyệt vời cho mọi người dùng

Yêu cầu đồ họa của người dùng doanh nghiệp đang tăng lên. Windows 10 yêu cầu tới 32% tài nguyên CPU hơn Windows 7, theo một báo cáo từ Lakeside Software, Inc. Và các phiên bản cập nhật của các ứng dụng văn phòng cơ bản như Chrome, Skype và Microsoft Office đòi hỏi mức đồ họa máy tính cao hơn nhiều so với trước đây .

Xu hướng này hướng tới các không gian làm việc chuyên sâu về đồ họa kỹ thuật số, và các ứng dụng cần tăng tốc đồ họa. Với môi trường ảo chỉ có CPU không thể hỗ trợ nhu cầu của người dùng chuyên nghiệp, hiệu suất tăng tốc GPU với NVIDIA GRID đã trở thành yêu cầu cơ bản của nơi làm việc kỹ thuật số ảo và doanh nghiệp sử dụng Windows 10.


* NVIDIA Quadro vDWS mang lại hiệu suất an toàn

Mỗi ngày, có hàng chục đến hang trăm người dùng cần phải chạy các workloads đòi hỏi tốc độ xử lý rất cao, truy cập từ bất kỳ thiết bị nào, làm việc ở mọi nơi và tương tác với các tập dữ liệu lớn – tất cả đều giữ an toàn cho thông tin của họ. Đó có thể là một bác sĩ tim mạch cung cấp tư vấn từ xa và truy cập hình ảnh chất lượng cao trong khi tại một hội nghị; hoặc một cơ quan chính phủ cung cấp các trải nghiệm đào tạo mô phỏng, nhập vai; hoặc một kỹ sư R & D làm việc trên một thiết kế xe mới, những người cần đảm bảo sở hữu trí tuệ và thiết kế độc quyền vẫn an toàn trong trung tâm dữ liệu trong khi cộng tác với những người khác trong văn phòng của khách hàng.

Đối với những người có nhu cầu khắc khe về đồ họa mạnh mẽ như thế, Quadro vDWS cung cấp máy trạm ảo mạnh mẽ nhất từ trung tâm dữ liệu hoặc đám mây đến bất kỳ thiết bị nào, ở bất cứ đâu.

* Cách vGPUs đơn giản hóa quản trị CNTT

Làm việc với VDI, quản trị viên CNTT có thể quản lý tài nguyên tập trung thay vì hỗ trợ các máy trạm riêng lẻ. Thêm vào đó, số lượng người dùng có thể được thu nhỏ hoặc tăng them dựa trên nhu cầu của dự án và ứng dụng.

Chức năng monitoring GPU ảo của NVIDIA cung cấp cho các phòng CNTT các công cụ và thông tin chi tiết để họ có thể dành ít thời gian xử lý sự cố hơn và tập trung nhiều hơn vào các dự án chiến lược. Quản trị viên CNTT có thể hiểu được cơ sở hạ tầng của họ xuống cấp ứng dụng, cho phép họ thực nghiệm vấn đề trước khi bắt đầu.

Với VDI, CNTT cũng có thể hiểu rõ hơn về các yêu cầu của người dùng và điều chỉnh phân bổ nguồn lực. Điều này tiết kiệm chi phí hoạt động trong khi cho phép trải nghiệm người dùng tốt hơn. Ngoài ra, các tính năng di chuyển trực tiếp của các máy ảo tăng tốc NVIDIA GPU cho phép CNTT thực hiện các dịch vụ quan trọng như nâng cấp năng lực tính toán, khả năng phục hồi cơ sở hạ tầng và nâng cấp phần mềm máy chủ mà không cần bất kỳ thời gian ngừng máy ảo nào. Nó cho phép CNTT thực sự cung cấp trải nghiệm người dùng chất lượng với tính sẵn sàng cao.




