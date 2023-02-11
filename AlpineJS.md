* 上位層でx-dataで宣言した変数は子要素内でも使用可能。bladeが分かれていても、使用可能。
* @entangleの対象変数がPHP側で`$hoge = []`の場合はAlpineJSはArrayと認識する。`$hoge = ['' => '']`の場合はObjectと認識する。AlpineJS側でObjectと認識されていれば、AlpineJSでプロパティ追加・削除など操作してもPHP側で反映される。
* JSファイルに記述した関数を呼び出したい場合は、関数をグローバルにしておく必要がある。
