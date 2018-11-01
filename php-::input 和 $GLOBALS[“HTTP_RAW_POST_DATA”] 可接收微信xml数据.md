- `Coentent-Type`仅在取值为`application/x-www-data-urlencoded`和`multipart/form-data`两种情况下，`PHP`才会将`http`请求数据包中相应的数据填入全局变量`$_POST `

- `PHP`不能识别的`Content-Type`类型的时候，会将`http`请求包中相应的数据填入变量`$HTTP_RAW_POST_DATA`

- 只有`Coentent-Type`不为`multipart/form-data`的时候，`PHP`不会将`http`请求数据包中的相应数据填入`php://input`，否则其它情况都会。填入的长度，由`Coentent-Length`指定。 

- 只有`Content-Type`为`application/x-www-data-urlencoded`时，`php://input`数据才跟`$_POST`数据相一致。 

- `php://input`数据总是跟`$HTTP_RAW_POST_DATA`相同，但是`php://input`比`$HTTP_RAW_POST_DATA`更凑效，且不需要特殊设置`php.ini`

- `PHP`会将`PATH`字段的`query_path`部分，填入全局变量`$_GET`。通常情况下，`GET`方法提交的`http`请求，`body`为空。