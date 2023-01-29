# SpreadSheetでタブ区切りの注意点
## 概要
Google SpreadSheetにコピペする際にタブ（\t）区切りで文字列を生成した場合、\tが文字列扱いになるケースが存在する
## 詳細
```JavaScript
/* NG例 */
var json = {};
var ary = [];
ary.push('aaa');
ary.push('bbb');
// JSONに入れる（ここがNG)
json.data = ary.join('\t');

console.log(json.data);
```

文字列をJSONに一度入れるとこの現象が起こるケースが存在する

※ 自分の環境ではならなかったが、他の人の画面ではなった

## 対応方法

```JavaScript
/* OK例 */
var ary = [];
ary.push('aaa');
ary.push('bbb');

console.log(json.join('\t');
```

直接配列をjoinでタブ区切りにする