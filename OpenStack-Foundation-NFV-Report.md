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

Theo truyền thống, doanh nghiệp viễn thông nhấn mạnh sự cần thiết của cơ sở hạ tầng “nhà cung cấp dịch vụ”, đòi hỏi độ tin cậy rất cao đối với từng thành phần cơ sở hạ tầng. Một trong những nguyên lý kiến trúc của nền tảng cloud (bao gồm OpenStack) là cả khả năng mở rộng và độ tin cậy đều đạt được thông qua quy mô lớn. Đây là một cách tiếp cận mới cho nhiều doanh nghiệp viễn thông ở chỗ nó đẩy nhiều yêu cầu HA lên đến ứng dụng. Trong môi trường cloud, một máy chủ cá nhân không thể tự cung cấp “five nines” thời gian hoạt động, nhưng một ứng dụng có nhiều phiên bản trên nhiều máy chủ trong một cloud phân tán. Nhận ra rằng những thất bại nhất định xảy ra, NFV trên OpenStack phải tập trung vào giám sát khả năng phục hồi, phát hiện lỗi và phản hồi.

Cells (groups of hosts) quản lý thành phần Nova. Cell cho phép triển khai các OpenStack cloud lớn hơn bằng cách cung cấp một cách để nhóm các tài nguyên lại với nhau để được quản lý dễ dàng hơn. Quản trị viên có thể phân vùng tài nguyên hiện có thành các cell và hệ thống sẽ biết nơi tìm chúng.

OpenStack tiếp tục kết hợp tính khả dụng cao và khả năng phục hồi trong mọi bản phát hành. Gần đây nhất, bản phát hành Liberty bao gồm các ví dụ cụ thể về mạng này:

+ Tính sẵn sàng cao của bộ định tuyến (L3 HA/VRRP) khi kích hoạt lớp 2 (l2pop)

+ Trình điều khiển tham chiếu VPNaaS với bộ định tuyến HA

+ Các mạng được sử dụng cho lưu lượng VRRP cho các bộ định tuyến HA có thể được cấu hình để sử dụng một loại segmentation cụ thể hoặc physical network tag.

+ Có thể khởi động lại OVS agent mà không ảnh hưởng đến kết nối dữ liệu.

+ Cảnh báo sự kiện kích hoạt một hành động khi một sự kiện nhận được.

Nhưng những cải tiến này có thể không đảm bảo với mọi công ty đang quan tâm tới NFV trên OpenStack. Một quan điểm độc lập về vai trò của OpenStack trong tính khả dụng của NFV, có tên là “NFV của nhà cung cấp thực sự quan trọng?” Để giải quyết vấn đề, và người dùng phải cài đặt HA với các thành phần dự phòng và VNF, và tăng cường nền tảng để duy trì trạng thái trong quá trình có lỗi xảy ra. Tác giả, Tom Nolle, Chủ tịch CIMI Corp, kết luận rằng OpenStack thực hiện chính xác những gì họ yêu cầu, nhưng các nhà phát triển VNF cần xây dựng HA vào VNF của họ - cũng giống như các nhà phát triển nhận thức về cloud xây dựng HA vào ứng dụng của họ. Có một ví dụ điển hình về điều này trong Dự án Clearwater. Clearwater là một triển khai mã nguồn mở của IMS (Hệ thống con đa phương tiện IP) được thiết kế để triển khai có thể mở rộng theo quy mô lớn trên đám mây. Clearwater là sự kết hợp kinh tế của các nền tảng dịch vụ đỉnh cao với các tiêu chuẩn tuân thủ tiêu chuẩn của các giải pháp mạng truyền thông cấp viễn thông, và thiết kế hướng cloud của nó rất phù hợp để triển khai trong môi trường NFV.

Khả năng tự khôi phục được thực hiện theo nhiều cách khác. Bloomberg, một nhà điều hành mạng lớn và người dùng OpenStack NFV, đang chuyển từ trạng thái đồng bộ sang các chức năng ít độc lập và tự chủ hơn trên nhiều máy tính, để truyền bá khả năng tự khôi phục trong môi trường. Họ đang triển khai nhiều tường firewall và load balancer VNFs như trái ngược với những cái nhỏ hơn. Điều này cung cấp SLA tốt hơn ở cấp độ cao hơn. Sự cân bằng là quản lý nhiều hệ thống hơn nhưng cách tiếp cận làm giảm rủi ro.

Đối với nền tảng OPNFV, Doctor là quản lý dự án và bảo trì lỗi. Mục tiêu của Doctor là xây dựng một khung quản lý và bảo trì lỗi cho tính sẵn sàng cao của các dịch vụ mạng trên cơ sở hạ tầng ảo hóa. Tính năng chính là thông báo ngay lập tức về việc không có tài nguyên ảo hóa từ VIM, để xử lý khôi phục các VNF trên chúng.

Cộng đồng Doctor có ảnh hưởng đến nhiệm vụ này chủ yếu trong dự án Monasca của OpenStack— phản ánh cách tiếp cận “upstream first” của OPNFV. Monasca là một giải pháp Giám sát dung lượng cao, có khả năng mở rộng, đáng tin cậy và có khả năng chịu lỗi cao như một giải pháp Dịch vụ (MONaaS) có quy mô đến mức cung cấp thông số của nhà cung cấp dịch vụ. Hiệu suất, khả năng mở rộng và tính khả dụng cao đã được thiết kế ngay từ đầu.

Monasca có thể xử lý hàng trăm nghìn chỉ số/giây và có thể cung cấp thời gian lưu giữ dữ liệu lớn hơn một năm mà không mất dữ liệu trong khi vẫn xử lý các truy vấn tương tác. Các tính năng chính khác bao gồm:

+ REST API  lưu trữ và truy vấn chỉ số và thông tin lịch sử. Hầu hết các giải pháp giám sát đều sử dụng các giao thức và giao thức đặc biệt, chẳng hạn như CollectD hoặc NSCA (Nagios). Ở Monasca, http là giao thức duy nhất được sử dụng. Điều này đơn giản hóa thiết kế tổng thể và cũng cho phép một cách phong phú hơn nhiều để mô tả dữ liệu thông qua các tham số.

+ Đa nhiệm và được xác thực

+ Số liệu được xác định bằng cách sử dụng một cặp (key, value) được gọi là thứ nguyên.

+ Cảnh báo theo thời gian thực (single and compound alarm) về dữ liệu hệ thống.

+ Giám sát agent hỗ trợ tích hợp hệ thống và dịch vụ kiểm tra và Nagios.

### Multisite

Dịch vụ viễn thông đòi hỏi một cơ sở hạ tầng NFV phân phối trên nhiều khu vực khác nhau. Nền tảng phải có khả năng hỗ trợ dự phòng cấp ứng dụng trên các trung tâm dữ liệu khác nhau, quản lý mạng trên nhiều trang web và giữa cơ sở hạ tầng vật lý và ảo, sao chép hình ảnh nhiều trang và quản lý hạn ngạch toàn cầu và trên mỗi trang.

Nhiều triển khai OpenStack được kết nối như VIM và tính khả dụng cao trong số đó là bắt buộc đối với cơ sở hạ tầng NFV phân bố ở nhiều khu vực. Dự án Cơ sở hạ tầng ảo hóa đa phương tiện OPNFV tập trung vào các cải tiến cho các dự án OpenStack Nova, Cinder, Neutron, Glance (Image), Ceilometer (Telemetry) và Keystone (Identity), do đó OpenStack là VIM có thể hỗ trợ multi-site NFV clouds . Tìm hiểu thêm về dự án MultNFV Multisite tại https://wiki.opnfv.org/multisite.

"Trong các trung tâm dữ liệu hiện tại, việc triển khai một chuỗi dịch vụ là thông qua các cấu hình tĩnh, phức tạp và cứng nhắc vì chúng được kết hợp chặt chẽ với cấu trúc liên kết mạng vật lý và tài nguyên vật lý."

### Service Function Chaining 

Service Function Chaining (SFC) là một cơ chế để chuyển tiếp dựa trên điểm đến cơ bản điển hình của mạng IP. Một ví dụ đơn giản của một chuỗi dịch vụ sẽ là bắt buộc tất cả lưu lượng từ điểm A đến điểm B để đi qua firewall mặc dù firewall không theo nghĩa đen giữa điểm A và B từ bảng định tuyến. Một ví dụ phức tạp hơn là một loạt các hàm được sắp xếp, mỗi hàm được thực hiện trong nhiều máy ảo, như lưu lượng phải qua một máy ảo tại mỗi hop trong chuỗi nhưng sử dụng thuật toán băm để phân phối các luồng khác nhau trên nhiều máy ảo tại mỗi hop.

Trong các trung tâm dữ liệu hiện tại, việc triển khai một chuỗi dịch vụ là thông qua các cấu hình tĩnh, phức tạp và cứng nhắc vì chúng được kết hợp chặt chẽ với cấu trúc liên kết mạng vật lý và tài nguyên vật lý. Việc giới thiệu các dịch vụ mới vào một mạng thường đòi hỏi phải cấu hình lại hầu hết các phần tử mạng (nếu không phải tất cả). Chuỗi vật lý phải được định nghĩa lại cho NFV với thiết lập tự động theo các yêu cầu về chuỗi dịch vụ. Mở rộng quy mô mạng của các chức năng dịch vụ này để xử lý tải bổ sung hoặc mở rộng quy mô để giảm sử dụng tài nguyên là một phần không thể tách rời của giải pháp SFC.

Trong OpenStack, có hai bước trong việc tạo ra một chuỗi dịch vụ. Đầu tiên, các máy ảo dịch vụ, chẳng hạn như các máy ảo tường lửa, cần được tạo và kết nối với một mạng Neutron qua các cổng Neutron. Sau đó, các luồng lưu lượng được chọn cần được điều khiển thông qua một chuỗi thứ tự của các cổng VM dịch vụ này.

Trước khi OpenStack phát hành Liberty OpenStack đã hỗ trợ tạo các máy ảo dịch vụ và đính kèm các máy ảo dịch vụ này vào các cổng mạng Neutron. Trong bản phát hành Liberty, Neutron đã được mở rộng với dự án Sfc của dự án SFC. Các tính năng của networkingsfc là:

+ Tạo các chuỗi chức năng dịch vụ bao gồm chuỗi thứ tự các chức năng dịch vụ. SFs là các máy ảo (hoặc các thiết bị vật lý ) thực hiện chức năng mạng như firewall, bộ nhớ cache , kiểm tra gói hoặc bất kỳ chức năng nào khác yêu cầu xử lý các gói trong flow từ điểm A đến điểm B

+ Thực hiện với Open vSwitch

+ Cơ chế phân loại lưu lượng (khả năng lựa chọn và hành động về traffic)

+ API của nhà cung cấp

+ Kiến trúc trình điều khiển plugin.

Chi tiết tại :http://docs.openstack.org/developer/networking-sfc/

### Addressing the Rest of MANO:  NFVO and VNFM

Vào tháng 12 năm 2015, OPNFV đã chọn mở rộng phạm vi các dự án khi cần thiết để tạo thuận lợi cho việc triển khai NFV. Ví dụ, cộng đồng bây giờ sẽ phát triển và đề xuất các dự án về các chủ đề bổ sung, bao gồm MANO (“heart and brains” của NFV). Ngoài VIM, được đề cập trước đó, NFV MANO bao gồm:


OpenStack Tacker addresses ETSI NFV MANO NFVO and VNFM functions

<img src="/img/11.jpg">

**NFV Orchestrator:** Chịu trách nhiệm đưa vào các gói dịch vụ mạng mới (NS) và các chức năng mạng ảo (VNF); NS quản lý vòng đời, quản lý tài nguyên toàn cầu, xác nhận và ủy quyền các yêu cầu tài nguyên cơ sở hạ tầng ảo hóa các chức năng mạng (NFVI).

**VNF Manager:** Giám sát việc quản lý vòng đời của các trường hợp VNF, vai trò phối hợp và thích ứng cho báo cáo cấu hình và sự kiện giữa NFVI và E/NMS (hệ thống quản lý phần tử hoặc mạng).

Dự án OpenStack Tacker đề cập đến NFVO và VNFM. Tacker đang xây dựng một Open NFV Orchestrator với một mục đích chung tích hợp VNF Manager để triển khai và vận hành các chức năng mạng ảo (VNFs), với Service Function Chaining. Nó dựa trên Khung Kiến trúc ETSI MANO và cung cấp một chồng chức năng đầy đủ để phối hợp các giao diện cuối cùng của VNF (Hình 5). Tacker cung cấp một danh mục VNF cho các mô tả VNF trên (được viết bằng các tiêu chuẩn NFV của OASIS TOSCA) và cung cấp các API để quản lý vòng đời của VNF cùng với các khả năng như giám sát VNF, tự động mở rộng quy mô và tự khôi phục. Tacker có kế hoạch mở rộng sang các khả năng của NFVO như các bộ mô tả dịch vụ mạng (NSD) và bộ mô tả đồ thị chuyển tiếp (VNFFGD) trong các chu kỳ sắp tới. Tacker sử dụng OpenStack Compute (Nova), Neutron và Heat để thực hiện vòng đời của VNF

"Triển khai OpenStack NFV là xu thế của tương lai"

+ API Tacker triển khai VNF từ VNF Catalog 

+ Khởi tạo một hoặc nhiều máy ảo được mô tả trong mẫu TOSCA NFV

+ Tacker tạo điều kiện cho việc cấu hình injection  VNF và cung cấp một khuôn khổ có thể xem để theo dõi và hồi phục KPI

+ Chấm dứt VNF sẽ xóa tất cả các máy ảo và các tài nguyên khác liên quan đến VNF instance.

Tacker có nhiều người ủng hộ và phát triển trong cộng đồng OPNFV và được dự đoán là một lựa chọn trong một bản phát hành OPNFV trong tương lai. Mặc dù không có kế hoạch dứt khoát vào thời điểm này, PTL Tacker nói “bản phát hành C của OPNFV có thể tích hợp độc đáo với bản phát hành OpenStack Mitaka của Tacker.” Có một số video trình diễn Tacker kỹ thuật từ Hội nghị thượng đỉnh OPNFV tháng 11 năm 2015.

Video : https://www.youtube.com/watch?v=EfqWArz25Hg

Chi tiết: https://wiki.openstack.org/wiki/Tacker

### Other Key OpenStack Projects

Một số dự án OpenStack bổ sung hỗ trợ triển khai NFV.

**Astara:** Cung cấp khả năng tích hợp điều phối dịch vụ mạng  (routing, firewall, load balancing, VPN) để kết nối và bảo vệ môi trường OpenStack đa nhiệm.

Wiki: https://wiki.openstack.org/wiki/Astara

**Blazar (previously Climate):** Reservationas-a-Service, bao gồm thiết lập tài nguyên, cập nhật thiết lập và "give me an offer”/best effort reservation và lập lịch trình đặt chỗ. Cung cấp giải pháp cho các yêu cầu từ dự án PromNFV Promise.

Wiki: https://wiki.openstack.org/wiki/Blazar

**Congress:** Chính sách như một dịch vụ. Cung cấp quản trị như một dịch vụ trên bất kỳ collection of cloud services để theo dõi, thực thi và kiểm toán chính sách về cơ sở hạ tầng động.

**Mistral:** Workflow service Cho phép mô tả các quy trình nghiệp vụ phức tạp (quy trình công việc) như một tập hợp các nhiệm vụ và các mối quan hệ công việc, chẳng hạn Mistral quản lý trạng thái quản lý, thứ tự thực hiện đúng, song song, đồng bộ hóa và tính sẵn sàng cao. Mistral cũng cung cấp tính năng lập lịch nhiệm vụ linh hoạt

Wiki: https://wiki.openstack.org/wiki/Mistral.

**Neutron:** Dự án OpenStack cung cấp “kết nối mạng như một dịch vụ” giữa các thiết bị giao diện (ví dụ: vNICs) được quản lý bởi các dịch vụ Openstack khác (ví dụ: Nova). Neutron cung cấp sự linh hoạt và lựa chọn với trình điều khiển và plug-in từ nhiều nhà cung cấp viễn thông hàng đầu để người dùng không phải lo lắng về việc thay đổi API hoặc sửa đổi mã nếu họ quyết định chuyển đổi công nghệ triển khai cơ bản. Bài viết này bao gồm các tính năng Neutron cho hiệu năng NFV (ở trên). 88% người dùng OpenStack đã triển khai Neutron.

Visit http://docs.openstack.org/developer/neutron/

** Neutron “Stadium” subprojects: **Một tập hợp các dự án Neutron chính thức, Stadium bao gồm nhiều dự án liên quan đến NFV và duy trì hỗ trợ cho hầu hết các drivers và plug-ins.

http://governance.openstack.org/reference/projects/neutron.html.

**Senlin:** Một dịch vụ phân cụm và các thư viện để quản lý các nhóm đối tượng đồng nhất được tiếp xúc bởi các dịch vụ OpenStack khác

Wiki: https://wiki.openstack.org/wiki/Senlin.





