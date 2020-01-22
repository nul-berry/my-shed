/**
 * 以下、スプレッドシート変更通知のプログラム
 */

/**
 * スプレッドシートから必要なデータを取り出す
 *
 * @ param object e
 * @ return data
 */
function getValue(e){  
  // 行を指定しているだけ
  const status_column = 2
  
  // アクティブなシートから値を取得
  var notifySheet = SpreadsheetApp.getActiveSpreadsheet();
  var active_sheet = SpreadsheetApp.getActiveSheet();
  var my_cell = active_sheet.getActiveCell();
  var active_sheet_column = my_cell.getColumn();
  var rowNum = my_cell.getRow();
  
  // B列がタイトル C列が~~~をそれぞれ指定
  var title_str = notifySheet.getRange('B' + rowNum).getValue()
  var summary_str = notifySheet.getRange('C' + rowNum).getValue()
  var URL_str = notifySheet.getRange('D' + rowNum).getValue()
  
  // あとで返す(slackで表示する)データ
  var data =
'タイトル：'+ title_str + '\n' 
+'要約：' + summary_str + '\n' 
+'URL:' + URL_str;

  // 指定した列でなければ、動作しないように
  if (active_sheet_column !== status_column){
    return;
  }

  return data;
}


/**
 * slackにPostする際の詳細の設定
 *
 * @ param object value
 * @ return void
 */
function postMessage(value){
  var options = {
    'method': 'post',
    'headers': {'Content-type': 'application/json'},
    'payload' : JSON.stringify({
    'channel' : '#share-media',
      'attachments':[
       {                                                              
        'fallback': 'media追加通知',
        'color': '#F45B69',
        'title': 'mediaが追加された！今すぐcheck!→',
        'title_link': 'https://docs.google.com/spreadsheets/d/1hp12M5HQ3s120v1wi9BEgbuJmGvxF9YlDj9WhZe-nR4/edit?usp=sharing',
        'text': value,                                                 
       }
      ]
    })
  };
  UrlFetchApp.fetch("https://hooks.slack.com/services/xxxxxhogehogexxxxx", options);  
 }
 
/**
 * メイン処理
 *
 * @ param object e
 * @ return void
 */
function postURLAdded(e){
  　
  const value = getValue(e);
  
  // gasの関数よくわかってないので、再び指定してしまっている(いつか直す)
  var notifySheet = SpreadsheetApp.getActiveSpreadsheet();
  var active_sheet = SpreadsheetApp.getActiveSheet();
  var my_cell = active_sheet.getActiveCell();
  var active_sheet_column = my_cell.getColumn();
  var rowNum = my_cell.getRow();
  
  // B列変更したら通知来る→B列に文字入った時のみ通知くる
  if(notifySheet.getRange('B' + rowNum).getValue() === '') {
    Logger.log('None')
    }else if(value) {
      postMessage(value);
    }else {
      Logger.log('Extra')
    }
}

