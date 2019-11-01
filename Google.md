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


### Thuật toán google đã thay đổi nên cần dùng cách này.

- Ctrl + U tìm đến link có từ `viewerng`

- Paste link vào đây `https://r12a.github.io/app-conversion/` click convert 

- Open link ở ô Character sau đó tìm link dạng `https://doc-0s-5k-apps-viewer.googleusercontent.com/viewer/secure/pdf/9ntm91lgck0jhplteddaakrhuvvov99d/p0h5ed89hp35sivu7en1haabsbghjprq/1570963575000/drive/15111333470000695821/ACFrOgDW4kZ_W_HgNN2VWPdzVd9kCk6e99xpmma2kwy1HABJM60eLmJorchioNCPV39-Nao3y8yOJmSOlaU-lROb8PLOJ1Wkl3McluIt5qnvGzvAaHH5__UyG9EeJLA=` và open link. Enjoy !

### Download file google báo antivirus

`https://drive.google.com/file/d/1anuzyb7GREvGm6SLeN8ob8p8nAuvrflr/view?usp=sharing`

ID: `1anuzyb7GREvGm6SLeN8ob8p8nAuvrflr`

Paste ID to xxx
`https://drive.google.com/uc?export=download&confirm=no_antivirus&id=XXX`

Note: `https://drive.google.com/uc?export=download&id=`








