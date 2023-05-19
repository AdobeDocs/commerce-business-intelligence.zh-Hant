---
title: 管理帳戶設定
description: 瞭解如何為Data Warehouse自定義帳戶設定。
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
source-git-commit: 8d4e71363edad0613cc0ab277c2a43aad000965e
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# 自定義帳戶設定

>[!NOTE]
>
>需要 [管理權限。](../../administrator/user-management/user-management.md)

在 [!DNL Commerce Intelligence] 帳戶，您可以自定義帳戶設定以進行Data Warehouse。 通過選擇任何螢幕右上角的組織名稱，然後選擇 **[!UICONTROL Account Settings]** 的下界。

* **[!UICONTROL Client Name:]** 此設定顯示在所有儀表板的右上角，並顯示在帳戶的其他位置。 如果要更改 **[!UICONTROL "Vandelay Industries Co., Ltd]** 只 **[!UICONTROL "Vandelay]**&#x200B;這是該做的。

* **[!UICONTROL Currency:]** 這是 *預設貨幣* 所有貨幣值。 當小數值或貨幣值同步到您的Data Warehouse中時，此設定將確定在報告中該值之前放置的符號。

* **[!UICONTROL Blackout Hours:]** 此設定可確保在一天的選定時間內，您的Data Warehouse無法訪問您連接的資料庫。 所有小時均以零小時和東部標準時間(EST)表示。 例如，如果您不希望在東部標準時間上午9:00到東部標準時間下午1:00之間訪問生產資料庫，則應鍵入以下數字陣列： **9、10、11、12**。

* **[!UICONTROL Forced update hours:]** 此設定可確保Data Warehouse更新在帳戶中自動開始 *在幾小時內* 你已經指定了。 與封鎖時間一樣，這些也在ET中。 例如，如果希望Data Warehouse更新在 **午夜** 和 **中午** EST，應鍵入以下數字陣列： **0、12**。

* **[!UICONTROL Send email summaries if the data has not updated yet:]** 此選項可管理計畫發送電子郵件摘要的情況 *報告中資料之前* 按鈕。 如果您選擇 **否**，您的帳戶將跳過在其預定時間發送電子郵件的過程。 相反，您的帳戶會在資料更新後發送它。 如果您選擇 **[!UICONTROL Yes]**，您的帳戶將發送電子郵件，其中包含一條消息，說明資料已過時，並在資料更新後發送另一封電子郵件。

* **[!UICONTROL Enable data updates:]** 此選項確保資料更新在您的帳戶上運行。 如果將設定更改為 **[!UICONTROL No]**，資料同步和列計算在帳戶中暫停。

>[!NOTE]
>
>確保選擇 **[!UICONTROL Save Customizations]** 進行任何更改。
