---
title: 啟用 [!DNL MBI] 內部部署訂閱帳戶
description: 了解如何啟用 [!DNL MBI] 內部部署訂閱的帳戶。
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 啟動您的 [!DNL MBI] 內部部署訂閱帳戶

啟用 [!DNL MBI] 針對內部部署訂閱，請先建立 [!DNL MBI] 帳戶，然後連接 [!DNL MBI] 至您的商務資料庫。 如需有關在 `Cloud Starter` 專案，請參閱 [啟用 [!DNL MBI] 帳戶 `Cloud Starter` 訂閱](../getting-started/cloud-activation.md).

1. 建立 [!DNL MBI] 帳戶。

   - 前往 [Adobe Commerce帳戶登入](https://account.magento.com/customer/account/login)

   - 前往 **[!UICONTROL My Account** > **My [!DNL MBI] Instances]**.

   - 按一下 **[!UICONTROL Create Instance]**. 如果您沒有看到此按鈕，請連絡您的客戶成功經理或客戶技術顧問。

   - 輸入您的資訊以建立帳戶。

   ![](../assets/create-account-2.png)

   - 前往收件匣並驗證您的電子郵件地址。 如果你沒有收到電子郵件， [聯絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

   - 建立密碼。

   ![](../assets/create-account-4.png)

   - 建立帳戶後，您可以選擇將使用者新增至新帳戶。 現在可以新增技術管理員以執行下列步驟。

   ![](../assets/create-account-5.png)

1. 輸入有關商店的資訊以設定首選項。

   ![](../assets/create-account-6.png)

1. Connect [!DNL MBI] 使用加密連線連線至您的商務資料庫。

   商務強烈建議您使用 [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md). 不過，如果此選項不可用，您仍可以連結 [!DNL MBI] 使用 [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

1. 成功連接後 [!DNL MBI] 至您的商務資料庫，請連絡您的客戶成功經理以協調後續步驟，例如設定整合和其他設定步驟。

1. 完成配置後，您可以 [登入](../getting-started/sign-in.md) 至 [!DNL MBI] 帳戶。
