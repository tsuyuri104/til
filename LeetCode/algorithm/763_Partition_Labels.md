https://note.com/tsuyuri104/n/n3503b1452e63?magazine_key=mdb17e3fc1457

# 1回目
```
function partitionLabels(s: string): number[] {

    let list: Map<string, { start: number, last: number }> = new Map<string, { start: number, last: number }>();
    const len: number = s.length;

    for (let i = 0; i < len; i++) {
        const c: string = s[i];

        if (list.has(c)) {
            list.set(c, { start: <number>list.get(c)?.start, last: i });
        } else {
            list.set(c, { start: i, last: i });
        }

    }

    let part: { start: number, last: number }[] = [];
    list.forEach((value: { start: number, last: number }, key: string) => {

        if (part.find(x => x.start < value.start && value.last < x.last)) {
            return true;
        }

        let index: number = part.findIndex(x => x.start < value.start && x.last < value.last && value.start < x.last && x.last < value.last);
        if (index > -1) {
            part[index].last = value.last;
        } else {
            part.push({ start: value.start, last: value.last });
        }


    });

    return part.map((value: { start: number, last: number }) => {
        return value.last - value.start + 1;
    });
};
```

* 問題ページにあるヒントを見て作成。
* とりあえず解答できて満足。

# 2回目
```
type indexOfS = { start: number, last: number };
function partitionLabels(s: string): number[] {

    let list: Map<string, indexOfS> = new Map<string, indexOfS>();

    for (let i = 0; i < s.length; i++) {
        const c: string = s[i];

        if (list.has(c)) {
            list.set(c, { start: list.get(c)!.start, last: i });
        } else {
            list.set(c, { start: i, last: i });
        }

    }

    let part: indexOfS[] = [];
    list.forEach((value: indexOfS, key: string) => {

        if (part.find(x => x.start < value.start && value.last < x.last)) {
            return true;
        }

        let index: number = part.findIndex(x => value.start < x.last && x.last < value.last);
        if (index > -1) {
            part[index].last = value.last;
        } else {
            part.push({ start: value.start, last: value.last });
        }

    });

    return part.map((value: indexOfS) => {
        return value.last - value.start + 1;
    });
};
```

* マイベスト。
* 何回も登場していた開始インデックス終了インデックスの型をTypeで宣言するように修正した。
* findIndexの条件を見直した。

# 3回目
```
function partitionLabels(s: string): number[] {

    let list: Map<string, number> = new Map<string, number>();
    let arrayS: string[] = [];

    for (let i = 0; i < s.length; i++) {
        const c: string = s[i];
        list.set(c, i);
        arrayS.push(c);
    }

    let result: number[] = [];
    let length: number = 0;
    let index: number = 0;
    arrayS.forEach((c, i) => {

        length += 1;

        const cLastIndex: number = list.get(c)!;

        if (index < cLastIndex) {
            index = cLastIndex;
        }

        if (i === index) {
            result.push(length);
            length = 0;
        }
    });

    return result;
};
```

* [解説動画](https://www.youtube.com/watch?v=B7m8UmZE-vw&feature=youtu.be)を見て修正。
 * 文字の初登場インデックスは不要なので、マップには最後の登場インデックスのみを保持する。
 * 変数sのループ処理の時に１文字ごとの配列を作る。
* 処理速度、使用メモリは2回目とあまり変わらなかった。
