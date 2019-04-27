# KKBox Members' Churn Analysis for KKBox

### 說明與使用工具
* 本次分析為參與資料科學與大數據分析專題(時間約一個月)進行資料探討，主要針對關鍵因子找尋，未進一步針對模型優化與調參等動作，後續如有需要再進行模型調整動作。
* 目前使用工具著重於Jupyter notebook, Rattle套件(for R)

### 0.分析思考流程

<img src="https://github.com/imiKao/KKBoxProject_for_TcfstCourse/blob/master/Images/KKBoxAnalysisProcess.png?raw=true" width="60%">

### 1.收集資料

* 本次分析主要以Kaggle提供資料集(https://www.kaggle.com/c/kkbox-churn-prediction-challenge) 共3份dataset進行流失關鍵因子分析(分類、關聯分析)
* 以是否流失(is_churn)進行討論，經過特徵工程與模型建置後進行討論關鍵因子

### 2.定義問題

* 因為要針對KKBox用戶未來一個月是否會產生流失進行因子討論，故除了跑模型得到與流失(is_churn)較具關係的(特徵)因子外，另針對KKBox不同特徵群體進行關聯分析，找尋流失率最大與最小群體差異，並以交易資料得到不同使用分案與各自關鍵因子差異。

### 3.觀察Raw Data資料

##### Columns(特徵)
* 此次針對Raw Data觀察資料可得到用戶資料(Members_v3.csv)共有6個特徵，分別如下

|特徵名稱|說明|
|--|--|
|msno|用戶ID|
|city|用戶所在城市|
|bd|年齡|
|gender|性別|
|registered_via|使用裝置|
|registration_init_time|註冊時間|
