### Download file từ google drive tắt chức năng tải xuống

<img src="/img/1.jpg">

Bạn chỉ cần tạo một bookmark trống trên trình duyệt (Chrome, Opera, Cốc Cốc v.v...), sau đó chỉnh sửa tên bất kỳ và dán vào địa chỉ liên kết đoạn mã javascript phía dưới vào.

``` sh
javascript:
function unicodeToChar(text) {
    return text.replace(/\\u[\dA-F]{4}/gi,
        function(match) {
            return String.fromCharCode(parseInt(match.replace(/\\u/g, ''), 16));
        });
}

var bodyHTML = document.body.innerHTML;
var viewerng_link = bodyHTML.slice(bodyHTML.search('https://drive.google.com/viewerng/'), bodyHTML.search('application/pdf') - 6);

var rawLnk = unicodeToChar(viewerng_link);

var http = new XMLHttpRequest,
    url = rawLnk.slice(6, rawLnk.search('ds=') - 1),
    params = rawLnk.slice(rawLnk.search('ds='));
http.open("POST", url, !0), http.setRequestHeader("Content-type", "application/x-www-form-urlencoded"), http.onreadystatechange = function() {
    if (4 == http.readyState && 200 == http.status) {
        var a = http.responseText;
        var b = a.slice(a.search('pdf') + 6, a.length - 2);
        window.location.href = b;
    }
}, http.send(params);
```

### Google Chrome, Cốc Cốc:

B1: Mở trình duyệt > nhấn tổ hợp phím Ctrl + D để tạo bookmark trống

<img src="/img/2.jpg">

B2: Chuột phải vào bookmark trống mới tạo > chọn Edit

<img src="/img/3.jpg">

B3: Đổi tên mà bạn mong muốn và dán đoạn mã javascript ở trên vào mục URL là xong

<img src="/img/4.jpg">

Để sử dụng, bạn mở liên kết chia sẻ file tài liệu bị tắt tính năng download, sau đó nhấn vào bookmark chứa đoạn mã javascript là xong, trình duyệt sẽ tự động quét và chuyển tiếp tới giao diện kèm nút tải về.

<img src="/img/5.jpg">











