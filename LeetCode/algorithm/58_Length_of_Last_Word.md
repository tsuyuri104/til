https://note.com/tsuyuri104/n/n413ec07cfbd5?magazine_key=mdb17e3fc1457

# 1回目
```
function lengthOfLastWord(s: string): number {
    const x: string[] = s.split(" ");
    const y: string[] = x.filter(z => z !== "");
    return y[y.length - 1].length;
};
```

* マイベスト。66ms。
* Input: s = " fly me to the moon "のインプットに対応するため、配列xから空文字以外の要素を抽出して配列yを作成している。
