# pleasanter

#ColumnFilterExpressions

#1.発行担当者を発行部署の値で絞り込む(発行部署でコグラフを選択すると佐賀・ナビン・渋谷の3つしか選択できないようにする)
```
[
    {
        "SiteId": 14388,
        "View": {
            "ColumnFilterExpressions": {
                "ClassD": "[@ClassD]"
            }
        }
    }
]
```
SiteId(リンクテーブルのサイトID): 14388(社員テーブルのSiteID)
"ClassD" : リンクテーブルの項目
"@CLASS": 表示するテーブルの項目、でも書く場所はどこの項目のフィルタをしますかの項目(選択版一覧で書くこと)

http://152.165.124.54/pstraining/items/14388/index

![スクリーンショット 2024-10-11 134545](https://github.com/user-attachments/assets/6542be4d-d645-407d-8de0-fcb6c579da04)

2. 現在の日付を取得します。(例：発行日)
![スクリーンショット 2024-10-11 140602](https://github.com/user-attachments/assets/752ca653-94c7-41b4-a8e0-500b4c857e96)



3. 管理№を自動採番する(管理№は「ユニークな頭文字(#SYみたいな) + 今年の年(今だと2024) + 4桁の通し番号」)
   教材フォルダ➔稟議書テーブル➔サバスクリプト

   ```
   if(model.Title == ""){
    let NewYear = new Date().getFullYear();
    let NumData =  items.Get(34496, '{"View":{"ColumnFilterHash":{"Title":"稟議書"}}}');
    if (NumData.Length > 0) {
        if (NumData[0].ClassB == NewYear) {
            var NewNum = NumData[0].NumA + 1;
        } else {
             var NewNum = 1;
        };
        var RtnData = NumData[0].ClassA + NewYear + ("0000" + NewNum).slice(-4);
        model.Title = RtnData;
    };
};
   ```

// 採番テーブルを読み、次の年と連番を取得
```
    let NewYear = new Date().getFullYear();
    let NumData =  items.Get(34496, '{"View":{"ColumnFilterHash":{"Title":"稟議書"}}}');

    if (NumData.Length > 0) {
        if (NumData[0].ClassB == NewYear) {
            var NewNum = NumData[0].NumA + 1;
        } else {
             var NewNum = 1;
        }
```
// 採番テーブル更新
```
        let UpdData = '{"ClassHash": {"ClassB":"' + NewYear + '"}, "NumHash": {"NumA":' + NewNum + '}}';
        let UpdFlg = items.Update(NumData[0].ResultId, UpdData);
```
// 画面の管理№更新
```
        var RtnData = NumData[0].ClassA + NewYear + ("0000" + NewNum).slice(-4);
        model.Title = RtnData;
        model.ClassU = "";
        model.DateA = new Date(); 
        model.Manager = context.UserId;
        model.Owner = context.UserId;
    }
```
