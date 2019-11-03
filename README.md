# go-swagger-example

## Build
```
$ swagger init spec \
  --title "A Todo list application" \
  --description "From the todo list tutorial on goswagger.io" \
  --version 1.0.0 \
  --scheme http \
  --consumes application/io.goswagger.examples.todo-list.v1+json \
  --produces application/io.goswagger.examples.todo-list.v1+json

$ swagger validate ./swagger.yml
$ export GO111MODULE=on
$ go mod init
$ go install ./cmd/todo-list-server/
$ todo-list-server --help
$ todo-list-server
2019/11/04 05:14:49 Serving todo list at http://127.0.0.1:55207

$ curl -i http://127.0.0.1:55207
HTTP/1.1 501 Not Implemented
Content-Type: application/io.goswagger.examples.todo-list.v1+json
Date: Sun, 03 Nov 2019 20:15:16 GMT
Content-Length: 50

"operation TodosGet has not yet been implemented"
```
## Sample Call
```
$ curl -i http://127.0.0.1:55353
HTTP/1.1 200 OK
Content-Type: application/io.goswagger.examples.todo-list.v1+json
Date: Sun, 03 Nov 2019 20:36:18 GMT
Content-Length: 3

$ curl -i http://127.0.0.1:55207 -d "{\"description\":\"message $RANDOM\"}"
HTTP/1.1 415 Unsupported Media Type
Content-Type: application/json
Date: Sun, 03 Nov 2019 20:36:58 GMT
Content-Length: 157

{"code":415,"message":"unsupported media type \"application/x-www-form-urlencoded\", only [application/io.goswagger.examples.todo-list.v1+json] are allowed"}⏎

$ curl -i http://127.0.0.1:55353 -d "{\"description\":\"message $RANDOM\"}" -H 'Content-Type: application/io.goswagger.examples.todo-list.v1+json'
HTTP/1.1 201 Created
Content-Type: application/io.goswagger.examples.todo-list.v1+json
Date: Sun, 03 Nov 2019 20:38:23 GMT
Content-Length: 34

{"description":"message ","id":1}

$ curl -i http://127.0.0.1:55353
HTTP/1.1 200 OK
Content-Type: application/io.goswagger.examples.todo-list.v1+json
Date: Sun, 03 Nov 2019 20:39:45 GMT
Content-Length: 36

[{"description":"message ","id":1}]
```

## Link
https://goswagger.io/tutorial/todo-list.html
