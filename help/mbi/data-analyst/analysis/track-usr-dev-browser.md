---
title: Google Analytics — 在資料庫中追蹤使用者裝置和瀏覽器資料
description: 了解實際透過行動裝置登入的使用者數量，以及這對這些使用者的期限值有何影響。
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# [!UICONTROL Google Analytics] 追蹤

使用 [!UICONTROL Google Analytics] 您可以 [保存引用源資訊](../analysis/google-track-user-acq.md) 了解最有價值的使用者來自何處。 在本主題中，您將了解您的使用者目前使用的平台（例如裝置或瀏覽器）。 透過此功能，您將能了解實際有多少使用者透過行動裝置登入，以及這對這些使用者期限值的影響。

## 儲存使用者裝置和瀏覽器資料

每次對您的網站提出請求時，使用者的瀏覽器都會傳送「使用者代理」字串，內含提出請求的平台相關資訊。 以下是User-Agent字串的一些範例：

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.
` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

如果您仔細查看，您會看到字串包含有關使用者的作業系統、瀏覽器，以及其所使用裝置名稱的資訊（如果有名稱）。 雖然使用者代理字串在不同平台甚至相同平台的版本之間差異很大，但一般而言，平台名稱會存在於其中某處。 例如，#1上是使用Chrome瀏覽器的Mac,#2上是使用Firefox瀏覽器的Windows電腦，#3是iPhone,#4是iPad,#5是Android裝置。

每次提出請求時，您的伺服器都可存取此資訊。 在PHP中，User-Agent字串儲存在 `$_SERVER['HTTP_USER_AGENT']`. 在Ruby on Rails中，它儲存在 `request.env['HTTP_USER_AGENT']`. 其他語言和環境也可讓您以類似方式存取。

### 您應在何時記錄此資料？

Adobe建議您新增名為 `Platform` 或 `User-Agent` 至 `Customers` 和 `Orders` 資料庫表，用於在每次建立用戶或下訂單時儲存此資訊。 如果使用SQL資料庫，此欄位應為 `VARCHAR(255)`. 

>[!NOTE]
>
>此 `User-Agent` 字串的長度可以遠超此值，但實際上字串的長度很少超過此值。

### 如何剖析有用的區段？

有許多程式庫可協助您剖析 `User-Agent` 串入作業系統、裝置等元件。 請參閱 [ua-parser專案](https://github.com/tobie/ua-parser) 了解更多。

透過這項新資訊，您可更清楚了解使用者存取您網站的方式。 然後，您可以量身打造其體驗，或為特定群組建立行銷活動。

## 相關

* [透過追蹤訂單轉介來源 [!DNL Google Anaytics] 電子商務](../importing-data/integrations/google-ecommerce.md)
* [在您的資料庫中追蹤使用者反向連結來源](../analysis/google-track-user-acq.md)
* [探索您最有價值的贏取來源和管道](../analysis/most-value-source-channel.md)
* [連接您的 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)
* [提高廣告宣傳的投資報酬率](../analysis/roi-ad-camp.md)
* [如何 [!DNL Google Analytics] UTM歸因功能是否正常？](../analysis/utm-attributes.md)
