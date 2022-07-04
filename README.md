# JavaWebNotebook

# Tomcat(記得安裝9，不要安裝10)

開不起來的話，有可能是
1. Java環境變量沒有配置
2. 閃退問題：需要配置兼容性
3. 亂碼問題：


# Http講解

## 什麼是Http?

Http(超文本傳輸協議)是一個簡單的請求(request)回應(response)協議，它通常運行在TCP之上
+ 文本：html,字符串...
+ 超文本：圖片,音樂,視頻,定位,地圖...

### 兩個時代
+ http1.0
    + HTTP/1.0：客戶端可以與Web服務器連接後，只能獲得`一個`web資源，之後斷開連結
+ http2.0
    + HTTP/1.1：客戶端可以與Web服務器連接後，只能獲得`多個`web資源，之後斷開連結

### HTTP請求
+ 客戶端>發請求>服務器

請求行：

`Request URL: https://www.gstatic.com/_/mss/boq-one-google/_/js/k=boq-one-google.OneGoogleWidgetUi.zh_TW.eaCkIVPshwY.es5.O/am=PgAABA/d=1/excm=_b,_r,_tp,appwidgetauthview/ed=1/dg=0/wt=2/rs=AM-SdHvQCXFnUNpJ4gNFm6oKEynFpPGBAQ/m=_b,_tp,_r`

`Request Method: GET`
+ 請求行中的請求方式：GET
+ 請求方式的種類：GET,Post,HEAD/DELETE,PUT,TRACT...
    + GET：請求能攜帶的參數比較`少`，`大小有限制`，`會`在瀏覽器的URL地址欄顯示數據內容，`不安全`，但是`高效`，常用於`獲取數據`
    + POST：請求能攜帶的參數`沒有限制`，`大小沒有限制`，`不會`在瀏覽器的URL地址欄顯示數據內容(POST的請求的參數放在RequestBody中)，`安全`，`不高效`，常用於`提交、修改資料`



請求頭：
```
Accept: 告訴瀏覽器，它所支持的數據類型
Accept-Encoding:支持哪種編碼格式 (UTF-8,ISO8859-1)
Accept-Language: 告訴瀏覽器，它的語言環境
Cache-Control: 緩存控制
Connection: 告訴瀏覽器，請求完成是斷開還是保持連接
HOST:主機
```

### HTTP響應
+ 服務器>響應>客戶端
```
Cache-Control:private 緩存控制
Connection:Keep-Alive 連結
Content-Encoding:gzip 編碼
Contetnt-Type:text/html 類型
```

響應體:
```
Accept: 告訴瀏覽器，它所支持的數據類型
Accept-Encoding:支持哪種編碼格式 (UTF-8,ISO8859-1)
Accept-Language: 告訴瀏覽器，它的語言環境
Cache-Control: 緩存控制
Connection: 告訴瀏覽器，請求完成是斷開還是保持連接
HOST:主機
Refresh：告訴客戶端，多久刷新一次
Location：讓網頁重新定位
```

響應狀態碼
+ 200：請求響應成功
+ 3**：請求重定向
    + 重定向：你重新到我給你的新位置去
+ 404：找不到資源
    + 資源不存在
+ 5**：服務器代碼錯誤 500 502(網關錯誤)

```常見面試題```

當你的瀏覽器中地址欄輸入地址並按下Enter的一瞬間到頁面能夠展示回來，經歷了什麼?


# MAVEN

> 我為什麼要學習這個技術?
1.  在Javaweb開發中，需要使用大量的jar包，我們手動去導入
2.  如何能夠讓一個東西自動幫我們導入和配置這個jar包
    因此，MAVEN誕生了!

## MAVEN項目架構管理工具
我們目前用來方便導入jar包的 
MAVEN核心思想就是:`約定大於配置`
+ 有約束，不要去違反
MAVEN會規定好你該如何如何去編寫我們JAVA代碼，必須要按照這個規範來

# Servlet

Servlet介面Sun公司有兩個默認的實現類：HttpServlet,GenericServlet
## 簡介
+ Sun公司開發動態WEB的一門技術
+ Sun在這些API中提供一個介面叫做`Servlet`，如果你想開發一個Servlet城市，只需要完成兩個小步驟
    + 編寫一個類，實現Servlet介面
    + 把開發好的Java類部屬到web服務器中
把實現了Servlet介面的Java程式叫做Servlet

## HelloServlet！

1. 建構一個MAVEN項目


# Cookie,Session(會話)

## 會話

+ Session：用戶打開一個瀏覽器，點擊了很多超連結，訪問多個web資源，關閉瀏覽器，這個過程稱為會話。

+ 有狀態會話：一個網站，怎麼證明你來過?
1. 服務端給客戶端一個cookie(可以理解為信件)，客戶端下次訪問服務端時，帶上Cookie就可以了*cookie*
2. 服務器登記你來過了，下次你來的時候，我來匹配*Session*

## 保存會話的兩種技術
1. cookie(本質上是種鍵值對，是一種session的實現方式)
    + 客戶端技術(Response,request)
2. session
    + 服務器技術，利用這個技術，可以保存用戶的會話訊息，我們可以把訊息或是數據，放在session中

    `常見場景`：網站登入後，下次訪問不需要重新再輸入一次帳號密碼，即可自動登入。

## cookie

cookie程式碼
```java
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
	req.setCharacterEncoding("UTF-8");
    resp.setCharacterEncoding("UTF-8");
    PrintWrite out=resp.getWriter();
    //Cookie，服務器端從客戶端獲取呀
    Cookie[] cookies =req.getCookies(); //這裡返回Array，說明Cookie可能存在多個
    //判斷Cookie是否存在

    if(cookies!=null){
        //如果存在怎ㄇ辦?
        out.write("您上一次訪問的時間是:");
        for(Cookie cookie:cookies){
            //1.獲得Cookie的名字
            if(cookie.getName().equals("LastLoginTime")){
                //獲取cookie中的值
                cookie.getValue();
                long lastLoginTime=Long.parseLong(cookie.getValue());
                Date date=new Date(lastLoginTime);
                out.write(date.)
            }
        }

    }else{
        out.write("這是您第一次訪問這個網站");
    }
    //服務器給客戶端響應一個cookie

   Cookie cookie =new Cookie("LastLoginTime",System.currentTimeMillis());
   //cookie的最大存活時間(一天)
   cookie.setMaxAge(24*60*60);
   resp.addCookie(cookie);
	}
```
1. 從請求中拿到cookie訊息
2. 服務器回應給客戶cookie

```java
常用方法
Cookie[] cookies = req.getCookies();//獲得cookie
cookie.getName(); //獲得cookie中的key
cookie.getValue(); //取得cookie的值
Cookie cookie=new Cookie(key,value); //設置cookie的鍵值對
cookie.setMaxAge(24*60*60); //有效期間
resp.addCookie(cookie);
```

cookie:一般會保存在本地的用戶目錄下 appData

一個網站cookie是否存在上限呢？**細節問題**
+ 一個Cookie只能保存一個訊息
+ 一個web站點可以給瀏覽器發送多個cookie,上限大概為20個
+ 瀏覽器能儲存的cookie上限為300個
+ cookie大小不可超過4KB

刪除Cookie
+ 不設置有效期間，關閉瀏覽器，自動失效
+ 將有效期間設置為0，立刻消亡
+ 


