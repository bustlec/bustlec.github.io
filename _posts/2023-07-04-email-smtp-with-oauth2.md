---
layout: post
title: 使用 Java 通過 SMTP OAuth2 身份驗證發送電子郵件
categories: Note
tags: Java SMTP OAuth2 Google Microsoft
comments: true
---

Send Email using JavaMail with SMTP OAuth2 authentication 

使用 JAVA 通過 SMTP OAuth2 身份驗證發送電子郵件

--------------------------------
- [Send Email using JavaMail](#send-email-using-javamail)
- [Using Google API](#using-google-api)
  - [Setup OAuth2 with Google](#setup-oauth2-with-google)
  - [Get Authentication Code](#get-authentication-code)
  - [Get Access Token and Refresh Token](#get-access-token-and-refresh-token)
- [Using Microsoft Azure API](#using-microsoft-azure-api)
  - [Setup OAuth2 with Microsoft Azure](#setup-oauth2-with-microsoft-azure)
  - [Get Authentication Code](#get-authentication-code-1)
  - [Get Access Token and Refresh Token](#get-access-token-and-refresh-token-1)
- [Reference](#reference)

## Send Email using JavaMail

- Dependency
   ```
   <dependency>
      <groupId>javax.mail</groupId>
      <artifactId>javax.mail-api</artifactId>
      <version>1.6.2</version>
   </dependency>
   ```

- Code
   ```sql
   try {
      String smtpServerHost = "smtp.office365.com";
      String fromUserEmail = "your_email_account@outlook.com";
      String toEmail = "your_test_account@outlook.com";
      String token = "eyJ0eXAiOiJKV1QiLCJub25jZSI6InFSbmdxMzdvVjdwbkF3TzZ3U2pOemxSU0k0R0tsNzF4..."; // access token		

      Properties props = System.getProperties();
      props.put("mail.smtp.host", smtpServerHost);
      props.put("mail.smtp.port", 587);
      props.put("mail.smtp.starttls.enable", true);
      
      Session session = Session.getDefaultInstance(props);
      session.setDebug(true);

      MimeMessage msg = new MimeMessage(session);
      msg.setFrom(fromUserEmail);
      msg.setRecipient(Message.RecipientType.TO, new InternetAddress(toEmail));
      msg.setSubject("OAuth2 Email Test");
      msg.setContent("Email Sent Successfully", "text/html");
      SMTPTransport transport = new SMTPTransport(session, null);
      transport.connect(smtpServerHost, smtpServerPort, fromUserEmail, null);
      transport.issueCommand(
            "AUTH XOAUTH2 " + BASE64EncoderStream
                  .encode(String.format("user=%s\1auth=Bearer %s\1\1", fromUserEmail, token).getBytes()),
            235);
      transport.sendMessage(msg, msg.getAllRecipients());
   } catch (Exception e) {
      e.printStackTrace();
   }
   ```
## Using Google API
### Setup OAuth2 with Google
- Create a project at https://console.developers.google.com/projectcreate.

- 點選「Enabled APIs & services」, 確認你的 Gmail API 是否已啟用
   
	![](./resources/google/gmail_api_enabled.png)

- 點選「Credentials」, 新增 [ + Create credentials] > [OAuth client ID]

	![](./resources/google/google_create_client_id.png)

- On the Create OAuth client ID page,
   1. Choose the [Web Application] Application Type
   2. Enter the Name of your OAuth 2.0 client
   3. Enter your VigorACS server URL (examples: https://acs.example.com)
   4. Enter your VigorACS server URL with callback path (examples: https://acs.example.com/ACSServer/oauth2/callback)
   5. Click > [CREATE] button.
   
	![](./resources/google/google_create_client_detail.png)

- 取得「Client ID」 and 「Client Secret」, **複製並保存**
   
	![](./resources/google/google_create_client_done.png)

### Get Authentication Code
### Get Access Token and Refresh Token
## Using Microsoft Azure API
### Setup OAuth2 with Microsoft Azure

- 至 https://portal.azure.com/ and navigate to Azure Active Directory.

   ![](https://imgur.com/PSO49GB.png)
   
- 點選「App registration」, 新增「New registration」

	![](https://imgur.com/czLloNB.png)

- 設定以下資訊後
  
   ![](https://imgur.com/fkMabeM.png)

- 註冊後, 取得 「應用程式識別碼 Client ID」和「目錄識別碼 Tenant ID」, 這兩個等等會用到

	![](https://imgur.com/Kd47jTX.png)

- 點選「憑證及秘密」, 新增「新增用戶端密碼」設定描述及到期日後, 按下「新增」.
  
	![](https://imgur.com/XgmcFzJ.png)

- **複製並保存「用戶端密碼值 Secret」 !!!**, 離開此頁面後值就無法查看了
  
   ![](https://imgur.com/Qh6bZll.png)

- 加入以下 API permission
  - [Microsoft Graph]
    - offline_access
    - SMTP.Send
  - [Office 365 Exchange Online]
    - Mail.Send
    - SMTP.SendAsApp
  
   ![](https://imgur.com/y8F52XR.png)

   ![](https://imgur.com/kJAwWXc.png)

- 授權使用, 確認權限的狀態列有綠色勾勾

   ![](https://imgur.com/XIIUzGb.png)

### Get Authentication Code

   ```sql
   https://login.microsoftonline.com/<Tenant ID>/oauth2/v2.0/authorize?prompt=consent&response_type=code&client_id=<Client ID>&redirect_uri=https://127.0.0.1/ACSServer/oauth2/callback&scope=offline_access%20https://outlook.office.com/SMTP.Send
   ```

### Get Access Token and Refresh Token

<!-- 
- 執行 Windows cmd 指令

		python lineNotifyMessage.py

- 即可收到透過LINE Notify 所發送的訊息如下圖
	
	<left>
		<img src="https://imgur.com/Re25EOd.png" width="260" hegiht="540"/>
	</left>
	<right>
		<img src="https://imgur.com/8EqtTjO.png" width="260" hegiht="540"/>
	</right>
	
	 -->



## Reference

- Office 365 Exchange Online permission is not visible for registered application in azure active directory
  - https://stackoverflow.com/questions/75282366/office-365-exchange-online-permission-is-not-visible-for-registered-application

- 535 5.7. 3 Authentication unsuccessful
  - [Enable or disable authenticated client SMTP submission (SMTP AUTH) in Exchange Online](https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission)
