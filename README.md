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
