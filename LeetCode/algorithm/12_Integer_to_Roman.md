# 第１回
```
type RomanPair = { roman: string, int: number };
const ROMAN_LIST_1: RomanPair[] = [
    { roman: 'M', int: 1000, },
    { roman: 'C', int: 100, },
    { roman: 'X', int: 10, },
    { roman: 'I', int: 1, },
];
const ROMAN_LIST_5: RomanPair[] = [
    { roman: 'D', int: 500, },
    { roman: 'L', int: 50, },
    { roman: 'V', int: 5, },
];

function intToRoman(num: number): string {

    let result: string[] = [];

    let beforePair: RomanPair = { roman: '', int: 0 };
    let afterPair: RomanPair = { roman: '', int: 0 };
    ROMAN_LIST_1.forEach((pair: RomanPair, index: number) => {

        afterPair = ROMAN_LIST_1[index + 1] ? ROMAN_LIST_1[index + 1] : { roman: '', int: 0 };
        let quotient: number = Math.floor(num / pair.int);

        let pair5: RomanPair[] = ROMAN_LIST_5.filter(x => {

            if (quotient === 5) {
                return x.int === quotient * pair.int;
            }

            if (5 < quotient) {
                return x.int < beforePair.int;
            }

            if (quotient === 4) {
                return pair.int < x.int && x.int < beforePair.int;
            }

            return false;
        });

        num -= quotient * pair.int;

        if (quotient === 9) {
            result.push(pair.roman + beforePair.roman);
            quotient -= 9;
        }

        beforePair = pair;

        if (quotient === 4) {
            result.push(pair.roman + pair5[0].roman);
            quotient -= 4;
        }

        if (5 === quotient) {
            result.push(pair5[0].roman);
            quotient -= 5;
        }

        if (5 < quotient) {
            result.push(pair5[0].roman);
            quotient -= 5;
        }

        for (let i = 0; i < quotient; i++) {
            result.push(pair.roman);
        }
    });


    return result.join('');
};
```
* [2018年に挑戦したとき](https://qiita.com/tsuyuri104/items/18162aada296e2f4ab48)には、４と９の分岐点も配列に保持していた。今回は１と５の分岐点のみで結果を取得しようと試みた。
* 処理時間は早い方だったが、メモリ使用量は高かった
