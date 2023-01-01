# 第１回
```
type NamePair = {
    int: number,
    name: string,
}
const NAME_INT_PAIR: NamePair[] = [
    { int: 0, name: 'zero' },
    { int: 1, name: 'one' },
    { int: 2, name: 'two' },
    { int: 3, name: 'three' },
    { int: 4, name: 'four' },
    { int: 5, name: 'five' },
    { int: 6, name: 'six' },
    { int: 7, name: 'seven' },
    { int: 8, name: 'eight' },
    { int: 9, name: 'nine' },
    { int: 10, name: 'ten' },
    { int: 11, name: 'eleven' },
    { int: 12, name: 'twelve' },
    { int: 13, name: 'thirteen' },
    { int: 14, name: 'fourteen' },
    { int: 15, name: 'fifteen' },
    { int: 16, name: 'sixteen' },
    { int: 17, name: 'seventeen' },
    { int: 18, name: 'eighteen' },
    { int: 19, name: 'nineteen' },
    { int: 20, name: 'twenty' },
    { int: 30, name: 'thirty' },
    { int: 40, name: 'forty' },
    { int: 50, name: 'fifty' },
    { int: 60, name: 'sixty' },
    { int: 70, name: 'seventy' },
    { int: 80, name: 'eighty' },
    { int: 90, name: 'ninety' },
    { int: 100, name: 'hundred' },
];
const NAME_3DIGIT_OVER_PAIR: NamePair[] = [
    { int: 1000, name: 'thousand' },
    { int: 1000000, name: 'million' },
    { int: 1000000000, name: 'billion' },
];

function getNameLe100(value: number): string {
    let index: number = NAME_INT_PAIR.findIndex(x => x.int === value);
    return index > -1 ? NAME_INT_PAIR[index].name : '';
}

function sortDescInt(a: NamePair, b: NamePair): number {
    return b.int - a.int;
}

function addNameLe100(num: number, result: string[]): { num: number, result: string[] } {

    NAME_INT_PAIR.sort(sortDescInt).forEach(x => {

        if (num === 0) {
            return true;
        }

        let q: number = Math.floor(num / x.int);

        if (q === 0) {
            return true;
        }

        if (x.int === 100) {
            result.push(getNameLe100(q));
        }

        result.push(x.name);
        num -= q * x.int;
    });

    return { num: num, result: result };
}

function numberToWords(num: number): string {

    let result: string[] = [];

    if (num === 0) {
        result.push(getNameLe100(num));
    }

    // 100超過
    NAME_3DIGIT_OVER_PAIR.sort(sortDescInt).forEach(x => {

        let division: number = x.int;
        let q: number = Math.floor(num / division);

        if (q > 0) {
            let resultLt100 = addNameLe100(q, result);
            result = resultLt100.result;
            result.push(x.name);
            num -= q * division;
        }

    });

    // 100以下
    let resultLt100 = addNameLe100(num, result);
    num = resultLt100.num;
    result = resultLt100.result;

    return result.map(x => x.charAt(0).toUpperCase() + x.substring(1).toLowerCase()).join(' ');
};
```
* 解説動画見ずにできた。
* 処理速度は早いが、メモリ使用量が高かった
* 改善したいところ
 * メソッド名を変えたい。とくにaddNameLe100
 * 繰り返し処理の数が多いので減らしたい。
