#net/http

##檢查是否為Root範例
```go
func main() {
    http.HandleFunc("/", rootHandle)
    http.ListenAndServe(":8000", nil)
}

func rootHandle(w http.ResponseWriter, r *http.Request) {
    if r.URL.Path != "/" {
        http.NotFound(w, r)
        return
    }
}
```

##檢查Request型態範例
```go
func rootHandle(w http.ResponseWriter, r *http.Request) {
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
