# CORSHeaders_Cookies_Golang

In order to set cookies in CORS headers in Go (also known as Golang), you will need to use the "net/http" package and create a custom handler function. Here is an example of how to set CORS headers and cookies:


```

package main

import (
    "fmt"
    "net/http"
)

func main() {
    http.HandleFunc("/", cors(handleIndex))
    http.ListenAndServe(":8080", nil)
}

func handleIndex(w http.ResponseWriter, r *http.Request) {
    http.SetCookie(w, &http.Cookie{
        Name:  "example_cookie",
        Value: "example_value",
    })
    fmt.Fprint(w, "Hello, World!")
}

func cors(h http.HandlerFunc) http.HandlerFunc {
    return func(w http.ResponseWriter, r *http.Request) {
        w.Header().Set("Access-Control-Allow-Origin", "*")
        w.Header().Set("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE, OPTIONS")
        w.Header().Set("Access-Control-Allow-Headers", "Content-Type, Authorization")
        w.Header().Set("Access-Control-Allow-Credentials", "true")
        h.ServeHTTP(w, r)
    }
}

```


In this example, the 'cors' function is creating a new handler function that sets the necessary CORS headers for the response. The handleIndex function is setting the cookie and handling the index page.

The cors function is then being used as a middleware, wrapping the handleIndex function and adding the CORS headers to the response.

You can add the cookie in the cors function as well and that will be added to the response for every request.
