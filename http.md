###### tags: `GitHub同步` `隨手筆記` `Http`

# Http 相關

## Cookie vs Session

> [白話 Session 與 Cookie：從經營雜貨店開始](https://medium.com/@hulitw/session-and-cookie-15e47ed838bc)
>
> [淺談 Session 與 Cookie：一起來讀 RFC](https://github.com/aszx87410/blog/issues/45)
>
> [深入 Session 與 Cookie：Express、PHP 與 Rails 的實作](https://github.com/aszx87410/blog/issues/46)

---

## 重點整理
### cookie 緣由
- HTTP 是無狀態的，所以每一次的 Request & Response 都是不相關的
- 要讓 HTTP 有狀態，有兩個方法
	- Request 的 header 加入 cookie
	- Request 夾帶 data (query string 是一種， request body 也是一種)

### 名詞解釋
- Session: 英文翻譯是指：持續一段時間且具有上、下文關係的會話
- Session: 在 HTTP 協議裡，泛指為「一段時間內 User agent 與 Origin server 間的傳輸過程是有狀態記錄的」
	- User Agent: 通常是透過 Browser，也可以是手機 App。
	- Origin Server: 參與此次網路請求的(起)源 server。(加上 origin 的原因是有可能中間透過代理服務或者轉址之類的狀況)
	- 有狀態記錄: 即上點提到的「有上、下文關係」
	- 傳輸過程: 即上點提到的「會話」
	
    (為方便辨識，我們這裡定義這個 Session 為 HttpSession)
- Cookie: 讓 HttpSession 實現的方法之一
- Cookie-based session: 為了安全，我們會把 cookie 內容加密，這個動作稱為「Cookie-based session」
- session data: 把資料存在 Server 端，cookie 只傳送 session identifier（Session ID) 來取得資料
(這裡就是為什麼會有誤解: 以為 session 是指存放在 server 端的 cookie)

### RFC 定義
- RFC 2109: 定義了兩個新 header
	- Set-Cookie: 它是一個 response header
	- Cookie: 他是一個 request header
	- Session(HttpSession): 基本定義如下
	1. Each session has a beginning and an end.(要有起始、結束時間)
	2. Each session is relatively short-lived.(存在時間是相對短暫)
	3. Either the user agent or the origin server may terminate a session.(user agent or origin server 任一方都可隨時終止這個 session(HttpSession))
	4. The session is implicit in the exchange of state information.(蘊含了交換狀態資訊的概念在裡面)