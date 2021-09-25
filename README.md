# Go + VSCode(Windows 10) の開発環境（デバッグができるまで）

VSCode でデバッグができるように Go の開発環境を作っていく

## Scoop で Go をインストール

Scoop を使って、次のコマンドで Go をインストールする

``` console
scoop install go
```

## Go 環境変数を確認

次のコマンドを実行すると、Go の環境変数一覧が表示される

``` console
go env
```

この中でも `GOROOT` と `GOPATH` が次の値になっていることを確認する

``` txt
set GOPATH=C:\Users\<ユーザ名>\go
set GOROOT=C:\Users\<ユーザ名>\scoop\apps\go\current
```

## Go 環境変数の変更

上記のように環境変数が設定されていなければ、次のようなコマンドで環境変数を変更する

``` console
go env -w GOPATH=C:\Users\<ユーザ名>\go
```

## 拡張機能をインストール

[golang.Go](https://marketplace.visualstudio.com/items?itemName=golang.Go) 拡張機能を VSCode にインストールする

![golang.Go 拡張機能](./screencapture/01.go-extention.png)

## GO: Install/Update Tools コマンド

VSCode に必要な Go のパッケージをまとめてインストールしていく

コマンドパレットを開き（ `Ctrl` + `Shift` + `p` ）、「GO: Install/Update Tools」 を選択する

![GO: Install/Update Tools コマンド](./screencapture/02.go-install-update-tools.png)

表示されている 10 個のパッケージすべてにチェックを入れて「OK」ボタンを押す

![10 個のパッケージにチェック](./screencapture/03.selected-tools.png)

インストールが成功すれば、OUTPUT コンソールに以下のログが表示される。

``` txt
Tools environment: GOPATH=C:\Users\N_hashimoto\go
Installing 10 tools at C:\Users\N_hashimoto\go\bin in module mode.
  gopkgs
  go-outline
  gotests
  gomodifytags
  impl
  goplay
  dlv
  dlv-dap
  golangci-lint
  gopls

Installing github.com/uudashr/gopkgs/v2/cmd/gopkgs (C:\Users\N_hashimoto\go\bin\gopkgs.exe) SUCCEEDED
Installing github.com/ramya-rao-a/go-outline (C:\Users\N_hashimoto\go\bin\go-outline.exe) SUCCEEDED
Installing github.com/cweill/gotests/gotests (C:\Users\N_hashimoto\go\bin\gotests.exe) SUCCEEDED
Installing github.com/fatih/gomodifytags (C:\Users\N_hashimoto\go\bin\gomodifytags.exe) SUCCEEDED
Installing github.com/josharian/impl (C:\Users\N_hashimoto\go\bin\impl.exe) SUCCEEDED
Installing github.com/haya14busa/goplay/cmd/goplay (C:\Users\N_hashimoto\go\bin\goplay.exe) SUCCEEDED
Installing github.com/go-delve/delve/cmd/dlv (C:\Users\N_hashimoto\go\bin\dlv.exe) SUCCEEDED
Installing github.com/go-delve/delve/cmd/dlv@master (C:\Users\N_hashimoto\go\bin\dlv-dap.exe) SUCCEEDED
Installing github.com/golangci/golangci-lint/cmd/golangci-lint (C:\Users\N_hashimoto\go\bin\golangci-lint.exe) SUCCEEDED
Installing golang.org/x/tools/gopls (C:\Users\N_hashimoto\go\bin\gopls.exe) SUCCEEDED

All tools successfully installed. You are ready to Go :).
```

## 動作確認用のコード

go-demo ディレクトリを作成し、以下の内容の main.go ファイルを作成する

``` golang
package main

import "fmt"

func main() {
	f := func(a []string) ([]string, string) {
		return a[1:], a[0]
	}
	m := []string{
		"one",
		"two",
		"three",
	}
	s := ""
	fmt.Println(m)
	for len(m) > 0 {
		m, s = f(m)
		fmt.Printf("%v -> %v \n", s, m)
	}
}
```

## デバッグの動作確認

実行を止めたい箇所にブレークポイントを張り（赤丸）、F5 を押してデバッグを開始する

![VSCode でのデバッグ](./04.debug-on-vscode.png)

F10 を押すと実行箇所が進むので、エディタ左側のデバッグペインに表示される変数が処理によって変化していくことを確認する

![変数が処理によって変化していく](./05.runing-debug.png)

デバッグの動作確認は以上です
