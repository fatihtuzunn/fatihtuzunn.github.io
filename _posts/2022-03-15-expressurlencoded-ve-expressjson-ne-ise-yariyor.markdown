---

layout: post
title: express.urlencoded ve express.json ne işe yarıyor?
date:   2022-03-15 00:30:06 +0300
categories: express


---

Express de POST ile data göndermenin üç temel yöntemi vardır.
*  application/x-www-form-urlencoded
* multipart/form-data
* application/json

Bunlar request body'sin egönderilen veri formatlerıdır.
Content-Type headerında belirtilir.

**application/x-www-form-urlencoded **

key ve value nun `'='` ile ayrıldığı. Ve bu çiftlerinde arasında`'&'` olan veri gönderme şeklidir. 
Sadece text olan verilerin gönderilmesinde kullanılır.

Eğer GET ile bu yöntemi kullanara veri gönderirsek sitemizde şuna benzer bir görüntü ortaya çıkacaktır;
```
http://example.com/path/to/page?isim=fatih&soyisim=tuzun&renk=mavi
```

Expressde bu yöntemle gönderilen body değerlerini yakalamak için express.urlencoded middlewarini kullanır.

```
app.use(express.urlencoded({extended:false}));
```

`"extended"` ayarı gönderilecek verilin yalnızca string olup, olmadığını belirlememize yarıyor. Bu metod üzerinde string dışında veri göndermek istiyorsak bu ayara `true` yapmamız gerekecektir.



**multipart/form-data**

Dosya gönderiminde kullanılır.

Expressde bu data tipini yakalamak için [Multer](https://github.com/expressjs/multer) modülünü kullanırız.



**application/json**
Datanın json veri tipinde gönderimidir.
Bu datanın yakalanması için express.json middlewarei kullanılır.
Bu usulü kullanmak başlangıç için tavsiye ediliyor.

```
var express = require('express');

var app = express();

app.use(express.json());

app.post('/', function(request, response){
  console.log(request.body);      // your JSON
   response.send(request.body);    // echo the result back
});

app.listen(3000);
```







Daha fazlası;
* https://dev.to/effingkay/cors-preflighted-requests--options-method-3024
* https://nkhilv.medium.com/what-does-express-urlencoded-do-anyway-8bdc4e638e1e
* https://stackoverflow.com/questions/9870523/what-are-the-differences-between-application-json-and-application-x-www-form-url?rq=1
* https://codex.so/handling-any-post-data-in-express
