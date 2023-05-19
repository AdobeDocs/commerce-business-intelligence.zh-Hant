---
title: Google Analytics — 跟蹤資料庫中的用戶設備和瀏覽器資料
description: 瞭解有多少用戶實際通過移動設備登錄，以及這如何影響這些用戶的生存期價值。
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# [!UICONTROL Google Analytics] 跟蹤

與 [!UICONTROL Google Analytics] 你 [保存參考源資訊](../analysis/google-track-user-acq.md) 瞭解您最有價值的用戶來自何處。 本主題討論您的用戶正在使用的平台（例如設備或瀏覽器）。 通過這種方式，您將能夠瞭解實際通過移動設備登錄的用戶數量，以及這如何影響這些用戶的生存期價值。

## 保存用戶設備和瀏覽器資料

每次向您的網站發出請求時，用戶的瀏覽器都會發送一個用戶 — 代理字串，其中包含有關發出請求的平台的資訊。 以下是User-Agent字串的一些示例：

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.
` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

如果仔細查看，您會看到該字串包含有關用戶的作業系統、瀏覽器以及他們使用的設備名稱（如果它有名稱）的資訊。 儘管User-Agent字串在不同平台甚至同一平台的不同版本之間差異很大，但通常情況下，平台名稱將存在於其中的某個位置。 例如，#1上是帶Chrome瀏覽器的Mac,#2上是帶Firefox瀏覽器的Windows電腦，#3是iPhone,#4是iPad,#5是Android設備。

每次發出請求時，伺服器都可以訪問此資訊。 在PHP中，User-Agent字串儲存在 `$_SERVER['HTTP_USER_AGENT']`。 在Ruby on Rails中，它儲存在 `request.env['HTTP_USER_AGENT']`。 其它語言和環境將允許您以類似方式訪問它。

### 您何時應記錄此資料？

[!DNL Adobe] 建議您添加一個名為 `Platform` 或 `User-Agent` 到 `Customers` 和 `Orders` 資料庫表，用於在建立用戶或下訂單時儲存此資訊。 如果使用的是SQL資料庫，則此欄位應為 `VARCHAR(255)`。 

>[!NOTE]
>
>的 `User-Agent` 字串的長度可以比此長得多，但實際上它很少超過此長度。

### 如何分析有用的段？

有許多庫可幫助您分析 `User-Agent` 串入作業系統、設備等元件。 請參閱 [ua解析器項目](https://github.com/tobie/ua-parser) 來瞭解更多資訊。

利用此新資訊，您可以更好地瞭解用戶如何訪問您的站點。 然後，您可以定制其經驗或為某些組建立市場營銷活動。

## 相關

* [跟蹤訂單推薦來源 [!DNL Google Anaytics] 電子商務](../importing-data/integrations/google-ecommerce.md)
* [跟蹤資料庫中的用戶推薦源](../analysis/google-track-user-acq.md)
* [發現您最有價值的收購來源和渠道](../analysis/most-value-source-channel.md)
* [連接 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)
* [提高廣告活動的ROI](../analysis/roi-ad-camp.md)
* [如何 [!DNL Google Analytics] UTM歸因工作？](../analysis/utm-attributes.md)
