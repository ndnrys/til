# スクレイピング（Cheerio）
## 概要
GASでスクレイピング
## 詳細
### ライブラリ：Cheerio
```
1ReeQ6WO8kKNxoaA_O0XEQ589cIrRvEBA9qcWpNqdOP17i47u6N9M5Xh0
```
```JavaScript
/**
 * リストページ用スクレイピング
 */
function listPageScraping(url){
  let contents = UrlFetchApp.fetch(url).getContentText();
  let $ = Cheerio.load(contents,{
    decodeEntities: false
  });
  // 今のページ情報を取得する
  let ids = $('.auc_del_style td:nth-child(2)');
  for (let i = 0; i < ids.length; i++) {
    allIds.push($(ids[i]).first().text());
  }
}
```