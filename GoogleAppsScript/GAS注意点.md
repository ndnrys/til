# GAS注意点
## 概要
注意点メモ
## 詳細
### 注意点
- 1回の処理で6分を超えることはできない
    - 6分を超えて実行する場合は、手間（5分を計算して1分後に再実行できるようにプログラムからトリガーを設定等）
- ログインが絡むスクレイピングは、Pythonなどで実装したほうが良い
- 表計算のUIは優秀なのでGAS×Pythonなどの連携で対応は強力

### 6分制限解除法
```JavaScript
/**
 * データ抽出実行
 */
function dataExtraction() {
  const ss = SpreadsheetApp.getActiveSpreadsheet();
  const sheet = ss.getSheetByName("取引情報");
  let values = sheet.getDataRange().getValues();

  let updateDatas = [];
  let startIdx = 0;

  var startTime = new Date();
  for (let i = 0; i < values.length; i++) {
    if (i === 0 || values[i][0] === "取得済") {
      startIdx++;
      continue;
    }
    updateDatas.push(detailPageScraping(values[i][1]));
    var diff = parseInt((new Date() - startTime) / (1000 * 60));
    if(diff >= runTime){
      // リスト書き出し
      const range = sheet.getRange(startIdx + 1, 1, updateDatas.length, updateDatas[0].length);
      range.setValues(updateDatas);

      delTrigger();

      var dt = new Date();
      dt.setMinutes(dt.getMinutes() + 1);  //１分後に再実行
  　  ScriptApp.newTrigger('dataExtraction').timeBased().at(dt).create();
      Logger.log(`書き込み件数：${updateDatas.length} 件`);
      Logger.log("1分後に再実行します");
      return;
    }
    Utilities.sleep(sleepTimer);
  }
  if (!updateDatas.length) {
    Logger.log(`データはすべて取得済みです`);
    return;
  }
  const range = sheet.getRange(startIdx + 1, 1, updateDatas.length, updateDatas[0].length);
  range.setValues(updateDatas);
  Logger.log(`データ抽出を完了しました。`);
  Logger.log(`件数： ${updateDatas.length} 件`);
}

 
function delTrigger() {
  const triggers = ScriptApp.getProjectTriggers();
  for(const trigger of triggers){
    if(trigger.getHandlerFunction() == "dataExtraction"){
      ScriptApp.deleteTrigger(trigger);
    }
  }
}
```