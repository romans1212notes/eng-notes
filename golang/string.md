# string
* check empty string
```go
// both are ok: https://stackoverflow.com/questions/18594330/what-is-the-best-way-to-test-for-an-empty-string-in-go
if len(s) == 0 { ... }
if s == "" { ... }
```