---
title: 管理您的帳戶設定
description: 了解如何為您的Data Warehouse自訂帳戶設定。
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# 自訂您的帳戶設定

>[!NOTE]
>
>需要 [管理權限。](../../administrator/user-management/user-management.md)

在 [!DNL MBI] 帳戶，您就可以自訂Data Warehouse的帳戶設定。 您可以在任何畫面的右上角選取您的組織名稱，然後選擇 **[!UICONTROL Account Settings]** 中。

* **[!UICONTROL Client Name:]** 此設定會顯示在所有控制面板的右上角，以及帳戶中其他地方。 如果您想要變更 **[!UICONTROL "Vandelay Industries Co., Ltd]** 只 **[!UICONTROL "Vandelay]**，這是該做的。

* **[!UICONTROL Currency:]** 這是 *預設貨幣* 以取得帳戶中的所有貨幣值。 每當將小數或貨幣值同步至Data Warehouse時，此設定會決定報表中該值之前所放置的符號。

* **[!UICONTROL Blackout Hours:]** 此設定可確保在一天中的所選小時內，您的Data Warehouse不會訪問您連接的資料庫。 所有小時都以零小時表示，並以東部標準時間(EST)表示。 例如，如果您不希望在東部標準時間上午9:00到下午1:00之間訪問生產資料庫，則應鍵入以下數字陣列： **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** 此設定可確保Data Warehouse更新自動在您的帳戶中開始 *在那個小時* 您已指定。 與封鎖時間一樣，這些時間也在ET中。 例如，如果您希望Data Warehouse更新自動在 **午夜** 和 **中午** EST，您應輸入以下位數陣列： **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** 此選項可管理排程傳送電子郵件摘要的情況 *在其報表中的資料之前* 會重新整理。 如果您選擇 **否**，您的帳戶會略過在排程時間傳送電子郵件。 而是在資料更新後，您的帳戶就會傳送。 如果您選擇 **[!UICONTROL Yes]**，您的帳戶會傳送電子郵件，並包含說明資料已過時的訊息，並在資料更新後傳送另一封電子郵件。

* **[!UICONTROL Enable data updates:]** 此選項可確保在您的帳戶上執行資料更新。 如果您將設定變更為 **[!UICONTROL No]**，資料同步和欄計算會在您的帳戶中暫停。

>[!NOTE]
>
>請務必選取 **[!UICONTROL Save Customizations]** 進行任何變更。
