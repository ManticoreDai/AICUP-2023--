# 執行環境
* 使用colab-pro python3
* GPU使用A100並開啟大量RAM模式

# 實作方法
* 修改官方提供的baseline，https://github.com/IKMLab/NCKU-AICUP2023-baseline
* Part-1 Document Retrieval
  * 保留原有的wiki API的結果
  * 額外使用Google Search API將claim斷句並針對中文的wiki網域做搜尋，將得到的前10個page與上述的wiki結果整合
* Part-2 Sentence Retrieval
  * 維持原本baseline的方法，提高negative ratio到1，並加入class weight讓model在極度不平衡的類別資料中也能學習
* Part-3 Claim Verification
  * ... 
