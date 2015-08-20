#net/http

##HandleFunc
這樣會Match所有請求：
```go
http.HandleFunc("/", handler)
```

以下可以檢查是否為root：
```go
func main() {
    http.HandleFunc("/", rootHandler)
    http.ListenAndServe(":8000", nil)
}

func rootHandler(w http.ResponseWriter, r *http.Request) {
    if r.URL.Path != "/" {
        http.NotFound(w, r)
        return
    }
}
```

如果最後面沒有加斜線，就不會match到最後有加斜線的訪問。下面的範例如果是`example.com/hello/`就訪問不到：
```go
http.HandleFunc("/hello", handler)
```
*pattern裡最後有加上斜線的話，沒斜線的訪問會被自動加上斜線*，所以不管有沒有加都會match到：  
（不管用`example.com/hello`還是`example.com/hello/`訪問，都會自動導向到`example.com/hello/`）
```go
http.HandleFunc("/hello/", handler)
```

以下範例函式同時處理兩種情況，不管訪問`/hello`還是`/hello/`都能處理，且網址不會被跳轉：
```go
func main() {
    handle("/hello", helloHandler)
    handle("/world/", worldHandler)
    http.ListenAndServe(":8000", nil)
}

func handle(pattern string, handler func(http.ResponseWriter, *http.Request)) {
	http.HandleFunc(pattern, handler)
	
	if len(pattern) == 1 {
		return
	}

	if pattern[len(pattern) - 1:] == "/" {
	    //如果傳進來的pattern是像 /example/
	    //就補上沒有斜線版本的 /example
		http.HandleFunc(pattern[:len(pattern) - 1], handler)
	} else {
	    //反之補上有斜線版本的
		http.HandleFunc(pattern + "/", handler)
	}
}
```

##Serve一個static資料夾範例
```go
func main() {
    http.HandleFunc("/public/", publicHandler)
}

func publicHandler(w http.ResponseWriter, r *http.Request) {
    http.ServeFile(w, r, r.URL.Path[1:])
}
```

##檢查Request型態範例
```go
func handler(w http.ResponseWriter, r *http.Request) {
    switch r.Method {
        case "GET":
            // ...
        case "POST":
            // ...
        case "PUT":
            // ...
        case "DELETE":
            // ...
        default:
            // error message
    }
}
```

##簡易的取得參數
```go
func main() {
    http.HandleFunc("/hello/", handler)
    http.ListenAndServe(":8000", nil)
}

func handler(w http.ResponseWriter, r *http.Request) {
    remainPart := r.URL.Path[len("/hello/"):]
    fmt.Fprintf(w, "%s", remainPart)
}
```
remainPart會拿到`example.com/hello/`以後的所有東西

```go
func handler(w http.ResponseWriter, r *http.Request) {
    value := r.FormValue("name")
    fmt.Fprintf(w, "%s", value)
}
```

##Mux
```go
func main() {
    mux := http.NewServeMux()
    mux.HandleFunc("/", hello)
    http.ListenAndServe(":8000", mux)
}

func hello(w http.ResponseWriter, r *http.Request) {
    // ...
}
```

#html/template

##基本Layout用法

layout.html: 
```html
<html>
<head>
    <title>hello</title>
</head>
<body>
    <header>
        Hello world
    </header>
    <main>
        {{template "content"}}
    </main>
</body>
</html>
```

index.html: 
```html
{{define "content"}}
    Main content goes here
{{end}}
```

main.go:
```go
func handler(w http.ResponseWriter, r *http.Request) {
    tmpl, err := template.ParseFiles("layout.html", "index.html")
    err = tmpl.Execute(w, nil)
    
    // ...
}
```
