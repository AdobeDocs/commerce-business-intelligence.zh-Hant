---
title: 管理您的帳戶設定
description: 瞭解如何自訂Data Warehouse的帳戶設定。
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
role: Admin, User
feature: Accounts
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b6935462-7263-4ced-a703-60de6a5aeb2d
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
subfeature_v2:
  - id: a763c1a2-1d0a-40d7-9617-8139636fd12e
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 4e01225a6bd285afbe988b9c24e07e2ea34649fc
workflow-type: tm+mt
source-wordcount: 349
ht-degree: 0%

---

# 自訂您的帳戶設定

>[!NOTE]
>
>需要[管理員許可權。](../../administrator/user-management/user-management.md)

您可以在您的[!DNL Commerce Intelligence]帳戶中自訂Data Warehouse的帳戶設定。 您可以在任何熒幕的右上角選取您的組織名稱，然後從下拉式清單中選擇&#x200B;**[!UICONTROL Account Settings]**&#x200B;來存取這些組織。

* **[!UICONTROL Client Name:]**&#x200B;此設定會顯示在您帳戶中所有控制面板的右上角。 若您想將&#x200B;**[!UICONTROL "Vandelay Industries Co., Ltd]**&#x200B;變更為僅&#x200B;**[!UICONTROL "Vandelay]**，請在這裡執行。

* **[!UICONTROL Currency:]**&#x200B;這是您帳戶中所有貨幣值的&#x200B;*預設貨幣*。 只要小數或貨幣值同步至Data Warehouse，此設定就會決定報表中置於該值之前的符號。

* **[!UICONTROL Blackout Hours:]**&#x200B;此設定可確保在一天中選定的時間內，您的Data Warehouse不會存取您連線的資料庫。 所有時數都會以零時和東部標準時間(EST)表示。 例如，如果您不希望在EST上午9:00到下午1:00之間存取生產資料庫，您應該輸入下列位數陣列： **9、10、11、12**。

* **[!UICONTROL Forced update hours:]**&#x200B;此設定可確保Data Warehouse更新在您指定的小時&#x200B;*內在您的帳戶*&#x200B;中自動開始。 和中斷時間一樣，這些也會出現在ET中。 例如，如果您希望Data Warehouse更新在&#x200B;**午夜**&#x200B;和&#x200B;**中午** EST自動開始，您應輸入下列位數陣列： **0、12**。

* **[!UICONTROL Send email summaries if the data has not updated yet:]**&#x200B;此選項會管理排程在其中一個報告&#x200B;*中的資料重新整理之前*&#x200B;傳送電子郵件摘要的情況。 如果您選擇&#x200B;**否**，您的帳戶會在其排程時間略過傳送電子郵件。 而是在資料更新後，由您的帳戶立即傳送。 若您選擇&#x200B;**[!UICONTROL Yes]**，您的帳戶會傳送電子郵件、包含說明資料已過時的訊息，並在您的資料更新後傳送另一封電子郵件。

* **[!UICONTROL Enable data updates:]**&#x200B;此選項可確保資料更新會在您的帳戶上執行。 如果您將設定變更為&#x200B;**[!UICONTROL No]**，您的帳戶將會停止資料同步和欄計算。

>[!NOTE]
>
>進行變更後，請務必選取&#x200B;**[!UICONTROL Save Customizations]**。
