Express 4.0接收Post資料
```javascript
var express = require('express'),
    bodyParser = require('body-parser');
    
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

app.post('/', function (req, res) {
	//req.body.xxx
	console.log(req.body);
});
```

如果要支援multipart/form-data
```javascript
var multer = require('multer');
app.use(multer());
```
