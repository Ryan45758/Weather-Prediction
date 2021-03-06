# Weather-Prediction Using LSTM
## 目的:<br>
分析台中市龍井區近8年來天氣資料，來預測龍井區未來天氣
## 模型:![](https://1.bp.blogspot.com/-6hyAXQfTrXY/WNn2G3CUtbI/AAAAAAAADHA/EaaANM6G1fg460fQccTNmwa8gp9k_IS7wCLcB/s1600/fig04_2c_LSTM.png)利用LSTM輸入該13筆特徵，輸出13筆預測。
## 分析:<br>
為何要用LSTM? LSTM顧名思義:Long short-term memory，中文翻譯為長短期記憶，該模型具有時序性，藉由學習後者修正前者。天氣有時序性視為已知，為求正確我們來確認一下天氣是否真的與季節有關，我們在jupyter秀出圖片!我們的資料確實與時間有關[](https://i.ibb.co/16XB0TN/2020-09-19-143102.png)
### 步驟:<br>
手動蒐集CSV檔 → 匯入資料 → 合併資料 → 資料前處理 <br>
→ 匯出資料 → 切分資料 → 載入模型 → 訓練模型 <br>
→ 保存模型 → 觀看準確度 → 畫圖 → 修正與改善。<br>
### 1. 蒐集資料:<br>
From https://e-service.cwb.gov.tw/HistoryDataQuery/index.jsp 下載台中市龍井區近8年來天氣資料<br>
![](https://i.ibb.co/qdxVjqV/1.png)<br>
### 2. 下載完畢後，遍歷所有檔案並新增我們所需的特徵，春夏秋冬<br>
![](https://i.ibb.co/x7PmJd3/2020-09-19-135516.png)
### 3. 最後將所有資料合併成一個檔案Weather.csv<br>
### 4. 因為很多欄位為空，因該觀測站無安裝該欄位所需sensor故無資料<br>
![](https://i.ibb.co/pZb0xq4/2020-09-19-140452.png)
### 5. 接著對資料進行前處理，刪除不需要的特徵<br>
![](https://i.ibb.co/GVjJ8Fn/2020-09-19-140835.png)
### 6. 移除缺失值
![](https://i.ibb.co/gJz04Fr/2020-09-19-141020.png)
### 7. 擴增資料特徵，將資料擴增為當天的前七天資料，並移除缺失值
![](https://i.ibb.co/MkvjbyQ/2020-09-19-141148.png)
### 8.將資料正規化提升收斂模型的速度，將資料切分為訓練資料與測試資料，前13行為測試資料13行之後為預測訓練資料
![](https://i.ibb.co/0Jc81vy/2020-09-19-141524.png)
### 9.建構LSTM模型，並且引入early-stopping(每個epoch結束後（或每N個epoch後)： 在驗證集上獲取測試結果，隨著epoch的增加，如果在驗證集上發現測試誤差上升，則停止訓練)
![](https://i.ibb.co/x3RG48N/2020-09-19-143939.png)
### 10. 訓練模型
![](https://i.ibb.co/xYjnwzY/2020-09-19-144330.png)
### 11. 繪圖，我們總共輸出的預測資料為13筆，在此用Temperature表示。
![](https://i.ibb.co/86vLWtF/image.png)
### 12. 修正與改善 <br>
我所做的嘗試 :<br>
1.前3天預測當天<br>
2.加入4季變化，前7天預測當天<br>
3.加入4季變化，前1~5年的前2天預測當天<br>
4.未正規化的預測<br>
5.正規化後的預測<br>
5.將17種特徵最後輸出1筆資料Temperature<br>
## 結論:<br>
天氣預測當然不只一種方法，但要預測準確必須顧及到全面的資料，更不止利用前七天預測後一天而已，我認為可以加入更多的手法，例如前五年的當天去預測當天+前五年的當天的前七天去預測當天等等的這些都是可以去嘗試的!我認為準確度勢必會提升，在這過程中我學會資料的前處理，操作pandas、numpy、LSTM...，有興趣的人可以去研究看看如何提升準度吧!裡面有報告的PPT也可以參考一下，感謝各位收看。
