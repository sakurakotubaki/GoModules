# Goで別ファイルから関数を呼び出す

1. 環境構築をする
```bash
go mod init example/main
```

2. lib.goを作成する
```go
package main

import "fmt"

func LibFunc() {
  fmt.Println("これは、lib.goのLibFunc()です。")
}
```

3. main.goを作成する
```go
package main

func main() {
 LibFunc()
}
```

4. 実行するときは、main.goとlib.go指定する必要がある
```bash
go run main.go lib.go
# 実行結果
これは、lib.goのLibFunc()です。
```

## subディレクトリにlib.goを作成する

1. subディレクトリを作成する
```bash
mkdir sub
```

2. subディレクトリに移動して、go mod initを実行する
```bash
cd sub
go mod init example/sub
```

3. sub/lib.goを作成する
```go
package sub

import (
	"fmt"
)

func SubFunc() {
	fmt.Println("こんにちわ、世界！")
}
```

プロジェクト直下の`go.mod`を編集する
```go
module example/main

go 1.20

require (
	sub v0.0.0
)

replace (
	sub => ./sub
)
```

4. main.goを編集する
```go
package main

import (
	"sub"
)

func main() {
	sub.SubFunc()
}
```

5. 実行する
```bash
go run main.go
# 実行結果
こんにちわ、世界！
```