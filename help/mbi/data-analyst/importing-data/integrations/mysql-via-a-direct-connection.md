---
title: 透過直接連線連線MySQL
description: 瞭解如何透過直接連線來連線 [!DNL MongoDB] 。
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# 透過直接連線連線[!DNL MySQL]

## 在此主題中

* [允許存取 [!DNL Commerce Intelligence] IP位址](#allowlist)
* [為 [!DNL MySQL] 建立 [!DNL Commerce Intelligence]使用者](#steptwo)
* [在 [!DNL Commerce Intelligence]中輸入連線資訊](#stepthree)

## 跳轉到

* [[!DNL MySQL]透過 &#x200B;](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL]透過 [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe]建議您使用[SSH](../integrations/mysql-via-ssh-tunnel.md)或其他加密形式來保護您的資料！ 如果這不是選項，您仍然可以使用本主題中的指示直接將[!DNL Commerce Intelligence]連線到您的資料庫。

此主題會逐步引導您將[!DNL MySQL]資料庫直接連線至[!DNL Commerce Intelligence]。 這些設定也可以搭配使用MySQL的[!DNL Adobe Commerce]或其他電子商務資料庫使用。

## 允許存取[!DNL Commerce Intelligence] IP位址 {#allowlist}

為了連線成功，您必須將防火牆設定為允許從IP位址存取。 它們是`54.88.76.97`和`34.250.211.151`，但它也位於[!DNL MySQL]認證頁面上：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 建立[!DNL MySQL]的[!DNL Commerce Intelligence]使用者

為`MySQL`建立[!DNL Commerce Intelligence]使用者最簡單的方法是在以`MySQL`許可權登入`GRANT`時執行下列查詢。 將`Commerce Intelligence IP Address`取代為[!DNL Commerce Intelligence] IP位址，並將`secure password`取代為您選擇的安全密碼：

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

若要限制此使用者存取特定資料庫、表格或欄中的資料，您可以改為執行`GRANT`查詢，僅允許存取您允許的資料。

**使用相同使用者和密碼重新執行所有必要IP的GRANT查詢。**

## 在Commerce Intelligence中輸入連線資訊

若要完成工作，您必須在[!DNL Commerce Intelligence]中輸入連線和使用者資訊。 您是否讓[!DNL MySQL]認證頁面保持開啟狀態？ 如果沒有，請移至&#x200B;**[!UICONTROL Data** > **Connections]**&#x200B;並按一下&#x200B;**[!UICONTROL Add New Data Source]**，然後按一下[!DNL MySQL]圖示。 別忘了將`Encrypted`切換變更為`Yes`。

在此頁面中輸入下列資訊，從`Database Connection`區段開始：

* `Connection Nickname`：輸入整合的名稱（例如E-commerce Store）
* `Username`： [!DNL Commerce Intelligence] [!DNL MySQL]使用者的使用者名稱
* `Password`： [!DNL Commerce Intelligence] [!DNL MySQL]使用者的密碼
* `Port`：伺服器上的MySQL連線埠（預設為`3306`）
* `Host`：預設為localhost。 一般而言，這是[!DNL MySQL]伺服器的繫結位址值，預設值為`127.0.0.1 (localhost)`，但也可能為某些本機網路位址（例如`192.168.0.1`）或伺服器的公用IP位址。

  值可在您的`my.cnf`檔案（位於`/etc/my.cnf`）中讀取`\[mysqld\]`的行下找到。 若該檔案中的繫結位址列被註解，則您的伺服器將會受到外部連線嘗試的保護。

完成時，按一下&#x200B;**[!UICONTROL Save & Test]**&#x200B;以完成設定。

## 相關檔案

* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=zh-Hant)
