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
pattern裡最後有加上斜線的話，沒斜線的訪問會被自動加上斜線，所以不管有沒有加都會match到：  
（不管用`example.com/hello`還是`example.com/hello/`訪問，都會自動導向到`example.com/hello/`）
```go
http.HandleFunc("/hello/", handler)
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
