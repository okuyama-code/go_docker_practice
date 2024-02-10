## 課題1
### 仕様
1(int), "2"(string), 10, "11"のスライスをループして、一桁なら01のように0をいれて2桁にして表示する。 Go better play groundで動作確認するといい。スライスをループ→fmt.Println()で表示というイメージ。

日本語に翻訳
ループの中で型が文字列の場合と数値型の場合で分けて処理を書く

スライス内の要素の値を変更するには、インデックスを使って値を更新する必要があります。

完成コード
```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	slice := []interface{}{1, "2", 10, "11"}
	// fmt.Println(slice)

	for i, item := range slice {
		// fmt.Println(i)
		// fmt.Println(item) //1 2 10 11

		if str, ok := item.(string); ok {
			// fmt.Println(str) // 2 11
			// 文字列を数値に変換
			if num, err := strconv.Atoi(str); err == nil {
				//一桁の場合、前に"0"を追加して2桁にする
				if num < 10 {
					str = "0" + str
					slice[i] = str
				}
				// ２桁にした結果を表示
				// fmt.Println(str)
			}
		}  else if num, ok := item.(int); ok {
			if num < 10 {
				str := strconv.Itoa(num)
				str = "0" + str
				slice[i] = str // スライスの値を更新
				// fmt.Println("変換された文字列:", str)
			}
		}
	}
	fmt.Println(slice)
}
```

## 課題２
mapのvalueからkeyを取得する問題。引数にmapとvalueを受け取り、対応するkeyがあればkeyを返却する関数を実装する。 mapの型はkeyをint, valueをstringにすること。もし対応するkeyがなければerrorを返すこと。

```go
func main() {
  m := map[int]{
    1: "01",
    2: "02",
    3: "03",
  }

  key, err := findKeyByValue(m, "03") // key→3, err→nil
  key, err := findKeyByValue(m, "05") // key→0にすること(初期値なので), errはある
}
```


