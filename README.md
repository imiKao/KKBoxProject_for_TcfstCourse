# KKBox Members' Churn Analysis for KKBox

### 說明與使用工具
* 本次分析為參與資料科學與大數據分析專題(時間約一個月)進行資料探討，主要針對關鍵因子找尋，未進一步針對模型優化與調參等動作，後續如有需要再進行模型調整動作。
* 目前使用工具著重於Jupyter notebook, Rattle套件(for R)

### 0.分析思考流程

<img src="https://github.com/imiKao/KKBoxProject_for_TcfstCourse/blob/master/Images/KKBoxAnalysisProcess.png?raw=true" width="80%">

### 1.收集資料

* 本次分析主要以Kaggle提供資料集(https://www.kaggle.com/c/kkbox-churn-prediction-challenge) 選取共3份dataset進行流失關鍵因子分析(分類、關聯分析)
* 以是否流失(is_churn)進行討論，經過特徵工程與模型建置後進行討論關鍵因子

### 2.定義問題

* 因為要針對KKBox用戶未來一個月是否會產生流失進行因子討論，故除了跑模型得到與流失(is_churn)較具關係的(特徵)因子外，另針對KKBox不同特徵群體進行關聯分析，找尋流失率最大與最小群體差異，並以交易資料得到不同使用分案與各自關鍵因子差異。

### 3.觀察Raw Data資料

##### 流失資料(train.csv & train_v2.csv)
* 用戶流失/非流失資料，後續用來進行模型監督式學習y值與關聯分析分群差異指標

|特徵名稱|欄位特徵說明|欄位資料說明|
|--|--|--|
|msno|用戶ID|離散型資料，RawData採用特殊編碼區別各用戶ID，無缺失值|
|is_churn|是否流失|離散型資料，1(流失)，0(無流失)|

##### 用戶資料(Members_v3.csv)
* 觀察用戶RawData資料(Members_v3.csv)，共6個特徵欄位、677萬筆資料，整理如下

|特徵名稱|欄位特徵說明|欄位資料說明|
|--|--|--|
|msno|用戶ID|離散型資料，RawData採用特殊編碼區別各用戶ID，無缺失值|
|city|用戶所在城市|離散型資料，RawData已進行編碼(1~22)，猜測為台灣22個縣市，其中無編碼2，無缺失值|
|bd|年齡|連續型資料，含各種不合理值(如負值與不合乎常理年齡)|
|gender|性別|離散型資料，含male與female，缺失值比例達60%|
|registered_via|使用裝置|離散型資料，含17種經編碼資料|
|registration_init_time|註冊時間|日期資料，需經過轉換為datatime型式|

##### 交易資料(transactions.csv & transactions_v2.csv)
* 觀察交易RawData資料，共9個特徵欄位、2297萬筆資料，整理如下

|特徵名稱|欄位特徵說明|欄位資料說明|
|--|--|--|
|msno|用戶ID|離散型資料，RawData採用特殊編碼區別各用戶ID，無缺失值|
|payment_method_id|交易付款方式|離散型資料，共40種付款方式，已經過編碼|
|payment_plan_days|交易方案天數|離散型資料，共37種方案天數|
|plan_list_price|方案價格|離散型資料，共55種方案價格|
|actual_amount_paid|交易實際付款金額|離散型資料，共65種實際付款金額|
|is_auto_renew|自動續約|離散型資料，1(自動續約)，0(非自動續約)|
|transaction_date|交易日期|連續型資料|
|membership_expire_date|方案到期日|連續型資料|
|is_cancel|手動取消方案|離散型資料，1(手動取消)，0(無手動取消)|

### 4. 資料前處理
