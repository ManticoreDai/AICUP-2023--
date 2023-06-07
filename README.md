# 執行環境
* 執行檔案為 "full_pipeline_報告繳交程式碼.ipynb"
* 另需要data與checkpoints兩個資料夾，但檔案太大無法上傳gitgub，請至以下連結下載
 * https://drive.google.com/drive/folders/1pUT-dENhLlaNkCghkO_OfyVSGtDui5YN?usp=sharing
* 使用colab-pro python3
* GPU使用A100並開啟大量RAM模式

# 成果
* Part-1 Document Retrieval 的 recall 約0.93
* Part-2 Sentence Retrieval 的 recall@5 約0.80，recall@100 約0.87
* 最終的strict accuracy約為0.62

# 實作方法
* 修改官方提供的baseline，https://github.com/IKMLab/NCKU-AICUP2023-baseline
* model改用ckiplab/bert-base-chinese
* Part-1 Document Retrieval
  * 保留原有的wiki API的結果
  * 額外使用Google Search API將claim斷句並針對中文的wiki網域做搜尋，將得到的前10個page與上述的wiki結果整合
* Part-2 Sentence Retrieval
  * 維持原本baseline的方法，提高negative ratio到1，並加入class weight讓model在極度不平衡的類別資料中也能學習
  * 取前100個最接近claim的句子
* Part-3 Claim Verification
  * 新增負採樣方法，把訓練資料中支持或反對的資料且證據句數量>=2的evidence，隨機拿掉一些證據句，並將label改為Not Enough Info
  * 訓練時會將有多組enidence的資料拆開，變成多筆資料
  * 訓練時若evidence不滿五句，還是會將句子補滿5句，補的方法是，從第二階段挑出來的句子且不是證據句的集合中抽樣
