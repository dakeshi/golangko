# 개요
[Getting Started](https://golang.org/doc/install)에는 workspace 위치를 나타내는 GOPATH 환경변수에 관한 설명이 빠져있습니다.
대신, [Go Wiki](https://github.com/golang/go/wiki/SettingGOPATH) 문서로 링크되어 있지요.

문제는 GOPATH 환경변수에 관한 설명들이 여러 곳에 흩어져 있고 설명이 약간씩 달라서 혼동을 줄 수 있다는 점입니다.

이 문서는 GOPATH, GOBIN에 대한 설명들을 종합한 글입니다. 이 글이 Go 프로그래밍을 시작하는데 조금이나마 도움이 되었으면 합니다.

> 이 문서는 macOS를 기준으로 작성되었습니다.

# GOPATH
GOPATH는 Go의 workspace 위치를 정의하는 환경변수입니다. Unix 시스템은 workspace 기본 디렉터리로 `$HOME/go`를 제공합니다. go와 관련된 환경변수는 `go env` 명령어를 통해서 확인할 수 있습니다.

```bash
$ go env | grep GOPATH
GOPATH=`/Users/UserName/go`
```

GOPATH를 환경변수로 명시적으로 설정하지 않았지만, GOPATH가 `$HOME/go` 디렉터리로 설정된 것을 확인할 수 있습니다.

만일, 터미널에서 GOPATH 환경변수를 사용하면 어떤 결과가 나올까요?

```bash
$cd $GOPATH
```

GOPATH 디렉터리로 이동하지 않네요. 왜 그럴까요? go env에는 GOPATH 경로가 있지만 터미널에서는 GOPATH 환경변수를 모르기 때문에 경로 이동을 하지 못한 것입니다. 따라서, GOPATH 환경변수를 터미널에서 활용하고 싶다면 기본경로를 사용하더라도 명시적으로 GOPATH에 경로를 추가하는 것이 좋습니다.

> .bash_profile 또는 .profile에 아래 코드 추가

```bash
# Add GOPATH env
export GOPATH=$HOME/go
```

GOPATH를 정의할 때는 몇 가지 주의사항이 있습니다.

* GOROOT(go가 설치된 디렉터리)와는 다른 경로를 지정해야 합니다.
* 환경변수 GOROOT를 사용하면 안됩니다.
* `~/some/path`와 같은 설정은 동작하지 않습니다. 대신, `$HOME/some/path` 로 설정하세요.

# GOBIN
GOBIN은 `go install` 명령을 실행했을 때 바이너리 파일이 생성되는 디렉터리를 설정하는 환경변수입니다. Unix에서는 기본적으로 $HOME/go/bin 디렉터리가 설정됩니다.

```bash
$ go env | grep GOBIN
GOBIN=“"
```

GOPATH와는 다르게 GOBIN이 기본 디렉터리로 설정되어 있지 않고 비어있는 것을 확인할 수 있습니다. 터미널에서 $GOBIN 환경변수를 사용하고 싶거나 시스템에서 제공하는 기본 디렉터리 이외에 다른 장소를 지정하고 싶다면 GOBIN 환경변수를 설정하세요.

```bash
# Add GOBIN path to generate binary file when `go install` is run
# https://github.com/golang/go/wiki/SettingGOPATH
export GOBIN=$HOME/go/bin
````

# 설정 파일 예제
Go를 시작하기 위해 기본적으로 필요한 설정은 다음과 같습니다. 

> .bash_profile 또는 .profile에 추가된 go 관련 설정

```bash
# Add GOPATH env
export GOPATH=$HOME/go

# Add GOBIN path to generate binary file when `go install` is run
# https://github.com/golang/go/wiki/SettingGOPATH
export GOBIN=$HOME/go/bin

# Add GO lang path in your path
# (Optionally) For convenience, add GOBIN directory in your path
# https://golang.org/doc/code.html#GOPATH
export PATH=$PATH:/usr/local/go/bin:$(go env GOBIN)
```

# GOPATH 관련 문서들

* [How to Write Go Code](https://golang.org/doc/code.html#GOPATH)
* [Go Wiki](https://github.com/golang/go/wiki/SettingGOPATH)
* [another GO Wiki](https://github.com/golang/go/wiki/InstallTroubleShooting)