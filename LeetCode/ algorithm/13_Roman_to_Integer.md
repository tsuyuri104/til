# 第１回
```
function romanToInt(s: string): number {

    const romanList: { [key: string]: number } = {
        '': 0,
        'I': 1,
        'V': 5,
        'X': 10,
        'L': 50,
        'C': 100,
        'D': 500,
        'M': 1000,
    };

    let result: number = 0;

    let isNextSkip: boolean = false;

    // to Left from Right
    for (let i = s.length - 1; i > -1; i--) {

        const c: string = s[i];
        const leftC: string = s[i - 1] ? s[i - 1] : '';

        const cInt: number = romanList[c];
        const leftCInt: number = romanList[leftC];

        if (isNextSkip) {
            isNextSkip = false;
            continue;
        }

        if (leftCInt < cInt) {
            result += cInt - leftCInt;
            isNextSkip = true;
        } else {
            result += cInt;
        }
    }

    return result;
};

romanToInt('III');
```

* 末尾から先頭に向かって文字列を検証する
* IVのように、次の文字が現在の文字より小さい場合は、差分を加算する
* `romanList`は関数の外で宣言すればよかった
