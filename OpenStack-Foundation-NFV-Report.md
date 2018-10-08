### Acclerating NFV Delivery with Openstack

"Network Functions Virtualizaon (NFV) hiện tại đồng nghĩa với Openstack. Khi mọi người nói về NFV có nghĩa là mọi người đang nói về Openstack."

### Tổng quan

Đắt đỏ, độc quyền không linh hoạt. Đây là một số ý kiến của các nhà lãnh đạo kinh doanh trải nghiệm với mạng truyền thống và điều gì đã thúc đẩy liên kết các nhà khai thác mạng để phát triển một cái gì đó mới. Network Functions Virtualization (NFV) cho phép các nhà khai thác mạng viễn thông và doanh nghiệp kiểm soát các chức năng mạng của họ, Network Functions Virtualization (NFV) — sử dụng phần cứng thương mại có sẵn và phần mềm mã nguồn mở như một bảng điều khiển duy nhất để quản lý và phối hợp. 

Ban đầu, các công ty viễn thông và nhà cung cấp mạng đã nhận ra tiềm năng cho OpenStack làm nền tảng cho NFV, vì vậy họ bắt đầu làm việc với các nhà cung cấp và các nhà phát triển trong cộng đồng OpenStack để tối ưu hóa phần mềm OpenStack cho trường hợp sử dụng NFV.

Cả Viện Tiêu chuẩn Viễn thông Châu Âu (European Telecommunications Standards Institute) và Linux Foundation cùng hợp tác dự án OPNFV đã xác định các thông số kỹ thuật và phát hành nền tảng tham khảo cho NFV chọn OpenStack làm trình quản lý cơ sở hạ tầng ảo hóa. Ngoài ra, OpenStack là lựa chọn hợp lí cho các chức năng quản lý và phối hợp bổ sung.

Một nhóm đánh giá độc lập đã kiểm tra khả năng tương tác giữa bốn cơ sở hạ tầng NFV nền tảng sử dụng OpenStack và các chức năng mạng ảo khác nhau. Trong khi người đánh giá lưu ý rằng khả năng tương tác vẫn là một công việc đang được tiến hành, đặc biệt là với việc công nghệ mới nổi NFV, phần lớn các cấu hình đã vượt qua kỳ vọng của người đánh giá một "kết quả tuyệt vời".

Bài viết này mô tả về NFV, giá trị kinh doanh của nó, và cách OpenStack hỗ trợ NFV. Nó trình bày chi tiết các dự án cụ thể, các trường hợp sử dụng và kinh nghiệm của các hãng viễn thông và doanh nghiệp lớn như AT&T, Verizon, NTT Group, SK Telecom và Bloomberg. Mặc dù NFV đang trong giai đoạn mới phát triển, NFV trên OpenStack cung cấp một nền tảng phát triển nhanh, có khả năng mở rộng và nhanh chóng với các lợi ích kinh doanh và kỹ thuật hấp dẫn cho các nhà cung cấp viễn thông và các doanh nghiệp lớn.

### Tìm hiểu về NFV

Chức năng ảo hóa mạng (NFV) là gì? Nói một cách đơn giản, đó là một cách mới để định nghĩa, tạo và quản lý mạng bằng cách thay thế các thiết bị mạng chuyên dụng bằng phần mềm và tự động hóa. Để đưa nó vào sử dụng, đó là sự tiếp nối của sự thay đổi cốt lõi CNTT từ phần cứng vật lý không linh hoạt, độc quyền và đắt tiền. Trong môi trường NFV, một chức năng mạng ảo (VNF) chịu trách nhiệm xử lý các chức năng mạng cụ thể chạy trên một hoặc nhiều máy ảo (VM) hoặc trong các containers, trên cơ sở hạ tầng mạng vật lý. VNF bao gồm các triển khai trên thiết bị di động, nơi các cổng di động (ví dụ: SGW, PGW, v.v.) và các chức năng liên quan (ví dụ: MME, HLR, PCRF, v.v.) được triển khai dưới dạng VNF, để triển khai thiết bị "virtual" customer premise equipment (CPE), tunnelling (ví dụ cổng VPN), firewall hoặc cổng cấp ứng dụng và gateways (ví dụ: bộ lọc lưu lượng truy cập web và email) đến thiết bị kiểm tra và giám sát dịch vụ.

**NFV functional overview**

<img src="/img/6.jpg">

**Example physical network functions for VNF replacement**

<img src="/img/7.jpg">

NFV và software-defined networking (SDN) bổ sung cho nhau nhưng giải quyết các vấn đề khác nhau trong môi trường khác domains. SDN nổi lên để làm cho các thiết bị mạng có thể lập trình và điều khiển được từ một khối trung tâm.NFV nhằm thúc đẩy đổi mới dịch vụ và cung cấp bằng cách sử dụng các công nghệ ảo hóa CNTT tiêu chuẩn. SDN yêu cầu giao diện mới, module điều khiển và ứng dụng, trong khi NFV thường liên quan đến việc di chuyển các ứng dụng mạng sang các VM hoặc các containers chạy trên hardware. NFV rất bổ sung cho SDN, nhưng không phụ thuộc vào SDN, mặc dù hai khái niệm và giải pháp có thể được kết hợp và giá trị có khả năng lớn hơn được tích luỹ.

Để tìm hiểu sâu hơn về NFV thông qua ETSI NFV và tổng quan về kỹ thuật của OPNFV, hãy truy cập https://portal.etsi.org/NFV/NFV_White_Paper.pdf và https://www.opnfv.org/software/technical-overview

Lợi ích của NFV xuất phát từ thực tế là nó chạy trên các máy chủ và các thiết bị switches trong các VM hoặc các containers và được xây dựng với các API mở tiêu chuẩn. NFV dựa vào phát triển nguồn mở và cung cấp một loạt các khả năng kết nối động và tương thích. Nói chung, mục đích của NFV là cung cấp sự nhanh nhẹn, linh hoạt và đơn giản. Các lợi ích hoạt động và kỹ thuật chi tiết mà các nhà khai thác mạng mong đợi từ việc thực hiện NFV bao gồm:

+ Network linh hoạt thông qua lập trình.

+ Dựa vào tốc độ phát triển của mã nguồn mở những cải tiến chưa từng có trong cả lĩnh vực viễn thông và IT.

+ Nhiều lựa chọn khả năng điều kiển và plugin hỗ trợ.

+ Khả năng truy cập thông qua API, cho phép thời gian giải quyết nhanh hơn.

+ Giảm chi phí bằng cách thay thế COTS phần cứng, giá/hiệu suất tốt hơn.

+ Giảm tiêu thụ điện năng và không gian sử dụng.

+ Hiệu quả hoạt động trên các trung tâm dữ liệu thông qua điều phối quản lí hàng ngàn thiết bị từ 1 bảng điều khiển.

+ Khả năng hiển thị: tự động theo dõi xử lí sự cố và các hành động trên các thiết bị vật lí và ảo.

+ Tăng hiệu suất bằng cách tối ưu hóa việc sử dụng thiết bị mạng ảo.

+ Phân bổ tài nguyên theo khu vực.

+ Qos: Hiệu suất, khả năng mở rộng, tích hợp, quản lý.

+ Chính sách dự phòng.

+ Hỗ trợ cơ sở hạ tầng ở mức ứng dụng.

<img src="/img/8.jpg">

NFV là một xu hướng chủ đạo đang được các nhà khai thác viễn thông chấp nhận nhanh chóng. Một cuộc khảo sát năm 2015 do OPNFV thực hiện cho thấy gần 60% các chuyên gia viễn thông đang tích cực nghiên cứu NFV. Công ty tư vấn IHS ® Infonetics dự báo thị trường phần cứng, phần mềm và dịch vụ NFV toàn cầu sẽ tăng gấp 10 lần lên 11,6 tỷ USD vào năm 2019 0,95 tỷ đô la trong năm 2014.

"OpenStack đóng một vai trò quan trọng trong OPNFV — trong cộng đồng, các dự án và nền tảng. Chúng tôi mong muốn được tiếp tục hợp tác khi chúng tôi chuyển đổi hướng đến với mã nguồn mở NFV"

**Jonathan Bryce, Executive Director, OpenStack Foundation, January 2016**

OPNFV, được xây dựng trên sự hợp tác phát triển rộng rãi trên nhiều nhà cung cấp viễn thông và doanh nghiệp, có vị trí tốt để tích hợp tiêu chuẩn của OPNFV vào các cơ quan tiêu chuẩn, cộng đồng mã nguồn mở và các nhà cung cấp thương mại để cung cấp nền tảng NFV mã nguồn mở chuẩn. Các thành viên của dự án OPNFV, bao gồm AT&T, China Mobile,  NTT DOCOMO, Telecom Italia, Vodafone, Ericsson, Huawei, Red Hat, Intel, CenturyLink, KT, Orange, SK Telecom và Sprint ban đầu tập trung vào cơ sở hạ tầng NFV, bao gồm hạ tầng ảo hóa ( NFVI) và trình quản lý cơ sở hạ tầng ảo hóa (VIM). Vào tháng 12 năm 2015, OPNFV đã mở rộng phạm vi của mình để bao gồm MANO trong các bản phát hành trong tương lai. OPNFV cung cấp sự tích hợp đầu cuối cho ngành và triển khai một nền tảng module cho NFV. Ngoài OpenStack, các dự án mã nguồn mở OpenDaylight, OpenvSwitch và KVM được sử dụng trong phiên bản đầu tiên của nền tảng tham khảo.

### Tại sao Openstack dành cho NFV/NFV_White_Paper

Nền tảng OpenStack cung cấp nền tảng cho kiến trúc NFV, về cơ bản là một cloud phù hợp cho mục đích triển khai, phối hợp và quản lý các chức năng mạng ảo. OpenStack cho phép quản lý nhiều trung tâm dữ liệu từ một dashboard,hoàn chỉnh với bảo mật thông thường, dịch vụ xác thực, API và giao diện người dùng. Khả năng tương tác của các OpenStack project cung cấp cho các công ty viễn thông và doanh nghiệp khả năng thiết kế hệ thống NFV mà họ lựa chọn, mà không cần các thành phần không cần thiết.

### Tại sao OpenStack là "đồng nghĩa" với NFV:

+ Kiến trúc được thiết kế cho các public cloud lớn.

+ Giao diện chuẩn hóa giữa hạ tầng và NFV.

+ Kiến trúc với các APIs,UIs, shared services, operations và các lựa chọn hoạt động cho VNFs và các tích hợp các chức năng khác.

+ Dự án networking OpenStack Neutron được phát triển và sử dụng trong hầu hết các thành phần cài đặt.

+ Tính năng NFV được phát hành trong các phiên bản từ năm 2013.

+ Tài nguyên bao gồm tất cả các tài nguyên được hỗ trợ trong mạng.

<img src="/img/9.jpg">

OpenStack được xác định là một thành phần chính trong khung kiến trúc ETSI NFV. Là một tham chiếu thực hiện đặc tả kỹ thuật ETSI NFV, dự án OPNFV đã triển khai OpenStack cho các thành phần của Virtualization Infrastructure Manager (VIM) trong bản phát hành đầu tiên, Arno (bản phát hành được đặt tên cho các con sông), ở phía dưới bên phải của hình. lưu ý rằng sơ đồ NFV của ETSI không có nghĩa là một kiến trúc được chính thức hoá - đó là một mô hình. Đây là lý do tại sao hình (Arno) trông không giống như việc thực hiện (đặc tả ETSI), mặc dù vậy. Với việc phát hành Arno, OPNFV đã thực hiện bước đầu tiên để thực hiện tầm nhìn của NFV mà ETSI đã mô tả lần đầu tiên. Bản phát hành đầu tiên tập trung vào VIM và NFVI với 5 dự án.

Việc thực hiện nguồn mở ban đầu này nhằm đẩy nhanh sự phát triển của các VNF và các thành phần NFV khác bằng cách xác định một chồng chức năng nhất quán mà các nhà phát triển sẽ áp dụng như một tiêu chuẩn thực tế. Arno cũng cung cấp cho doanh nghiệp viễn thông với cơ sở để tích hợp và thử nghiệm, cho phép lặp lại nhanh hơn trong tương lai. Bản phát hành tiếp theo, Brahmaputra8, dự kiến phát hành tháng 2 năm 2016, được lên kế hoạch là bản phát hành “lab-ready” đầu tiên, tích hợp nhiều cải tiến trong các lĩnh vực như cài đặt, tạo tác cài đặt, tích hợp liên tục, tài liệu được cải tiến và các kịch bản thử nghiệm template. Dự án đang phát triển theo hướng labreadiness cho thử nghiệm và khả năng tương tác của chức năng NFV và các trường hợp sử dụng. Ngoài việc hỗ trợ cho nhiều giải pháp mạng ảo, kế hoạch Brahmaputra cũng bao gồm hỗ trợ cho các trung tâm dữ liệu, quản lý lỗi bổ sung, và các giải pháp nâng cấp và triển khai. Nó sẽ bao gồm khoảng 30 dự án, thể hiện mối liên hệ hiệu quả với một số cộng đồng thượng nguồn. Brahmaputra sẽ bao gồm việc phát hành Liberty OpenStack, OpenStack vẫn là nền tảng VIM duy nhất.

Phần tiếp theo sẽ mô tả dự án OpenStack cho NFV, bao gồm cả “tại sao và như thế nào”. Nó cũng sẽ cung cấp về các tính năng và kế hoạch của NFV trong tương lai gần đây.

<img src="/img/10.jpg">

### Telecom Requirements  for NFV with OpenStack

Trong ETSI NFV và OPNFV, OpenStack là nền tảng cho trình quản lý cơ sở hạ tầng ảo hóa (VIM). VIM là một phần của chức năng Quản lý và Điều phối (MANO) kiểm soát việc phân bổ các tài nguyên tính toán, lưu trữ và mạng ảo từ NFVI để hỗ trợ các VNF. Các dự án OpenStack chính có liên quan là:

+ OpenStack Compute (code named Nova) để quản lý các máy chủ ảo. Một dự án — Magnum — sử dụng các Nova VM để chạy các containers ứng dụng.

+ OpenStack Block Storage (code named Cinder) cho lưu trữ ảo, hỗ trợ bất kỳ lưu trữ backend.

+ OpenStack Networking (code named Neutron) cung cấp mạng ảo.

Từ thời điểm này trở đi, chúng tôi sẽ sử dụng tên mã phổ biến cho mỗi dự án OpenStack. Các dự án mới hơn chỉ được biết đến với tên mã của chúng. Có quá nhiều tính năng nâng cao NFV trong OpenStack để liệt kê. Các yêu cầu viễn thông chính sẽ đi kèm với một vài ví dụ về các tính năng của OpenStack bao gồm các kế hoạch hiện tại và tương lai. Môi trường viễn thông và NFV có các yêu cầu nghiêm ngặt trong các lĩnh vực mở rộng, hiệu suất và phản hồi nhanh hơn và mang tính quyết định hơn đối với các lỗi, cũng như IPv6 và nhiều tính năng cụ thể hơn. Yêu cầu đối với các phản hồi xác định đề cập đến hiệu suất dự đoán, bao gồm cách tránh các thay đổi bất thường của trình quản lý hypervisor và máy chủ lưu trữ OS ảnh hưởng đến các ứng dụng nhạy cảm với hiệu năng.

OpenStack đã liên tục cải tiến về hiệu suất, khả năng mở rộng. Tất cả các dự án đều có tính ưu tiên cho khả năng mở rộng, khả năng phục hồi, khả năng quản lý, module và khả năng tương tác trong bản phát hành của Mitaka và hơn thế nữa.9 Ủy ban kỹ thuật OpenStack đã bắt đầu cuộc trò chuyện để xác định thêm một khuôn khổ mở rộng phù hợp dựa trên kỳ vọng của người dùng. Tất cả các dự án sẽ thực hiện các tính năng.

### Performance

Yêu cầu về hiệu năng phần lớn là xử lý gói hiệu năng cao: cách lấy gói tin ra khỏi mạng,đi vào máy ảo, xử lý nhanh và đi ra ngoài mạng. Một trong những kỹ thuật có sẵn là cung cấp cho máy ảo truy cập trực tiếp vào mạng thông qua SR-IOV. OpenvSwitch tăng tốc DPDK để xử lý gói nhanh và người dùng vhost nhiều hàng đợi với các chuyển mạch ảo tăng tốc cũng được hỗ trợ trong Neutron.
 
Một loạt các cải tiến liên quan cho phép các nhà khai thác mạng xác định các flavors và chủ sở hữu ứng dụng để xác định các thuộc tính hình ảnh, giữa chúng kiểm soát những thứ như vCPU topology, vCPU, pCPU , vị trí ứng dụng liên quan đến NUMA nodes và làm cho các trang lớn có sẵn cho các ứng dụng .

Trong tương lai, chúng ta có thể mong đợi sự hỗ trợ thời gian thực cho Cloud Radio Access Networks và điều chỉnh hiệu năng hơn nữa của hypervisor và mạng (tương ứng với Nova và Neutron) cũng như cấu guest. https://wiki.openstack.org/wiki/VirtDriverGuestCPUMemoryPlacement liệt kê những điều quan trọng có thể giúp tối ưu hóa hiệu suất.

Mặc dù có vẻ tự nhiên khi Network Function Virtualization xuất hiện dưới sự kết nối mạng, phần lớn công việc liên quan đến Nova. Nova quản lý vòng đời của các VM tính toán trong môi trường OpenStack. Trách nhiệm bao gồm khởi tạo, lên lịch và ngừng hoạt động của các máy theo yêu cầu. Hầu hết Nova đều liên quan đến các trường hợp sử dụng NFV. Ví dụ, lịch trình là rất quan trọng cho hiệu suất và khả năng phục hồi. Nó phải khởi động các phiên bản mới nhanh chóng, cả ban đầu và đặc biệt là trong phản ứng phát hiện lỗi.

### Scalability, High Availability  and Resiliency

Theo truyền thống, doanh nghiệp viễn thông nhấn mạnh sự cần thiết cho cơ sở hạ tầng “nhà cung cấp dịch vụ”, đòi hỏi độ tin cậy rất cao đối với từng thành phần cơ sở hạ tầng. Một trong những nguyên lý kiến trúc của nền tảng cloud (bao gồm OpenStack) là cả khả năng mở rộng và độ tin cậy đều đạt được thông qua quy mô lớn. Đây là một cách tiếp cận mới cho nhiều doanh nghiệp viễn thông ở chỗ nó đẩy nhiều yêu cầu HA lên đến ứng dụng. Trong môi trường cloud, một máy chủ cá nhân không thể tự cung cấp “five nines” thời gian hoạt động, nhưng một ứng dụng có nhiều phiên bản trên nhiều máy chủ trong một cloud phân tán. Nhận ra rằng những thất bại nhất định xảy ra, NFV trên OpenStack phải tập trung vào giám sát khả năng phục hồi, phát hiện lỗi và phản hồi.

Cells (groups of hosts)  quản lý thành phần Nova. Cell cho phép triển khai các OpenStack cloud lớn hơn bằng cách cung cấp một cách để nhóm các tài nguyên lại với nhau để được quản lý dễ dàng hơn. Quản trị viên có thể phân vùng tài nguyên hiện có thành các cell và hệ thống sẽ biết nơi tìm chúng.

OpenStack tiếp tục kết hợp tính khả dụng cao và khả năng phục hồi trong mọi bản phát hành. Gần đây nhất, bản phát hành Liberty bao gồm các ví dụ cụ thể về mạng này:

+ Tính sẵn sàng cao của bộ định tuyến (L3 HA/VRRP) khi kích hoạt lớp 2 (l2pop)

+ Trình điều khiển tham chiếu VPNaaS với bộ định tuyến HA

+ Các mạng được sử dụng cho lưu lượng VRRP cho các bộ định tuyến HA có thể được cấu hình để sử dụng một loại segmentation cụ thể hoặc physical network tag.

+ Có thể khởi động lại OVS agent mà không ảnh hưởng đến kết nối dữ liệu.

+ Cảnh báo sự kiện kích hoạt một hành động khi một sự kiện được nhận.






















