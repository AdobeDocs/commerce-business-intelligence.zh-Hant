---
title: 管理您的帳戶設定
description: 瞭解如何為您的Data Warehouse自訂帳戶設定。
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# 自訂您的帳戶設定

>[!NOTE]
>
>需要 [管理員許可權。](../../administrator/user-management/user-management.md)

在您的 [!DNL Commerce Intelligence] 帳戶，您可以為Data Warehouse自訂帳戶設定。 您可以在任何畫面的右上角選取您的組織名稱，然後選擇 **[!UICONTROL Account Settings]** 下拉式清單中的。

* **[!UICONTROL Client Name:]** 此設定會顯示在您帳戶中所有控制面板的右上角，以及其他地方。 如果您想要變更 **[!UICONTROL "Vandelay Industries Co., Ltd]** 轉換成 **[!UICONTROL "Vandelay]**，則位於此處。

* **[!UICONTROL Currency:]** 這是 *預設貨幣* 您帳戶中的所有貨幣值。 無論小數或貨幣值何時同步至Data Warehouse，此設定都會決定報表中置於該值之前的符號。

* **[!UICONTROL Blackout Hours:]** 此設定可確保在一天中的選定小時內，您的Data Warehouse不會存取您連線的資料庫。 所有時數都會以零時和東部標準時間(EST)表示。 例如，如果您不希望在EST上午9:00到下午1:00之間存取生產資料庫，則應輸入下列數字陣列： **9， 10， 11， 12**.

* **[!UICONTROL Forced update hours:]** 此設定可確保帳戶中的Data Warehouse更新自動開始 *時段* 您已指定。 和中斷時間一樣，這些也會出現在ET中。 例如，如果您希望Data Warehouse更新自動開始於 **午夜** 和 **中午** EST，您應該輸入下列位數陣列： **0， 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** 此選項可管理排程傳送電子郵件摘要的情況 *在其其中一個報表中的資料之前* 已重新整理。 如果您選擇 **否**，您的帳戶會在其排程時間略過傳送電子郵件。 而是在資料更新後，由您的帳戶立即傳送。 如果您選擇 **[!UICONTROL Yes]**，您的帳戶會傳送電子郵件、包含說明資料已過時的訊息，並在您的資料更新後傳送另一封電子郵件。

* **[!UICONTROL Enable data updates:]** 此選項可確保資料更新會在您的帳戶上執行。 如果您將設定變更為 **[!UICONTROL No]**，您的帳戶會停止資料同步和欄計算。

>[!NOTE]
>
>請務必選取 **[!UICONTROL Save Customizations]** 進行任何變更之後。
