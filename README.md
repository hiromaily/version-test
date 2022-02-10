# version-test
just go dependencies version test

[Go Modules](https://github.com/hiromaily/documents/blob/main/golang-tips/go-modules.md)

## How this module is required in go.mod
1. no git tag version
```
go get github.com/hiromaily/version-test

# go.mod
require github.com/hiromaily/version-test v0.0.0-20220210104236-655dd54d34c3
```

2. add tag version v1.0.0
```
# from referrer
go clean --modcache
# `go get -u` would not upgrade package even if cache is cleaned ...
go get -u github.com/hiromaily/version-test
 or
go get -u github.com/hiromaily/version-test@v1.0.0

# go.mod
require github.com/hiromaily/version-test v1.0.0
```

3. add tag version v1.1.0
```
# from referrer
go get -u github.com/hiromaily/version-test@v1.1.0

# go.mod
require github.com/hiromaily/version-test v1.1.0
```

4. add tag version v2.0.0
- big change is in go.mod
```
module github.com/hiromaily/version-test/v2
```

- change source code in referrer
```
import (
	"fmt"

	v2 "github.com/hiromaily/version-test/v2/version"
	v1 "github.com/hiromaily/version-test/version"
)

func main() {
	fmt.Println(v1.Version())
	fmt.Println(v2.Version())
}
```

```
# from referrer
go get -u github.com/hiromaily/version-test/v2

# go.mod

require (
	github.com/hiromaily/version-test v1.1.0
	github.com/hiromaily/version-test/v2 v2.0.0
)
```

