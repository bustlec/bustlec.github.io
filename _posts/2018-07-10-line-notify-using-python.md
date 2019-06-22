---
layout: post
title: 使用 Python 實作發送 LINE Notify 訊息
categories: Note
tags: Python LINE Notify
comments: true
---

Send LINE Notifications using Python

使用 Python 程式將訊息通過 LINE所提供的官方帳號「LINE Notify」向 LINE 群組發送訊息提醒

## Line Notify 介紹

根據 [LINE Notify](https://notify-bot.line.me/zh_TW/ "LINE Notify") 官方網站介紹 ：

> 透過LINE接收其他網站服務通知, 在與與網站服務連動完成後，LINE所提供的官方帳號「LINE Notify」將會傳送通知。 不僅可與多個服務連動，也可透過LINE群組接收通知。

*--MORE--*

## Enviroment

- 需安裝 Python 3.7.0


## 申請 LINE Notify 發行權杖

- 需擁有 LINE 帳號
- 至 [https://notify-bot.line.me/zh_TW/](https://notify-bot.line.me/zh_TW/ "LINE Notify") 進行登入
- 點選右上方 帳號名稱選單中的「個人頁面」

	![](https://imgur.com/S6mEUfi.png)

- 點選「發行權杖」

	![](https://imgur.com/ZWvFHMW.png)

- 輸入自訂「權杖名稱」, 這邊設定的名稱會在出現在提醒訊息的Title
- 選擇分享的群組後 (註：測試用故先選擇第一個), 按下「發行」

	![](https://imgur.com/f88O3eS.png)

- 此時會顯示已發行的權杖, 請將權杖內容「**複製**」並記下來! 等等會用到**很重要** !!!

	![](https://imgur.com/CFQl1bJ.png)

## Python Script

- 建立 lineNotifyMessage.py 檔案

		import requests

		def lineNotifyMessage(token, msg):
		    headers = {
		        "Authorization": "Bearer " + token, 
		        "Content-Type" : "application/x-www-form-urlencoded"
		    }
		
		    payload = {'message': msg}
		    r = requests.post("https://notify-api.line.me/api/notify", headers = headers, params = payload)
		    return r.status_code
		
		# 修改為你要傳送的訊息內容
		message = 'Notify from LINE, HELLO WORLD'
		# 修改為你的權杖內容
		token = 'daaaaaaaaaaaaaaaadvmlsdvjowiesaifwjfklsdjl9ef'

		lineNotifyMessage(token, message)

- 修改「權杖」和「訊息內容」完成後儲存檔案

## Demo

- 執行 Windows cmd 指令

		python lineNotifyMessage.py

- 即可收到透過LINE Notify 所發送的訊息如下圖
	
	<left>
		<img src="https://imgur.com/Re25EOd.png" width="260" hegiht="540"/>
	</left>
	<right>
		<img src="https://imgur.com/8EqtTjO.png" width="260" hegiht="540"/>
	</right>
	
	


