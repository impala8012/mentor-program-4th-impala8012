## 什麼是 DNS？Google 有提供的公開的 DNS，對 Google 的好處以及對一般大眾的好處是什麼？
DNS (Domain Name System)，是網域名稱系統，它將人們可讀取的網域名稱 (例如，www.amazon.com) 轉換為機器可讀取的 IP 地址 (例如，192.0.2.44)，也就是把網域名稱翻譯成IP位址，讓電腦能夠分辨網際網路設定的位置。
DNS 就像是以前的查號台，詢問服務人員 X 公司的電話，服務人員把 X 公司的電話，告訴我們讓我們可以與該公司取的聯繫。

Google 所提供的 DNS 伺服器 IP位址為「8.8.8.8」與「8.8.4.4」，如果有自己的網址，改完網域名稱的 IP 之後，可以很快生效（介於 6 至 24 小時內），如果 Google Public DNS 的使用者多的話，網站搬家就不用耗太久時間等待

IPv4 位址
- 主DNS伺服器 8.8.8.8 
- 次DNS伺服器IP 8.8.4.4 

IPv6 位址
- 主DNS伺服器 2001:4860:4860::8888
- 次DNS伺服器IP2001:4860:4860::8844

Google 的好處：
- 透過廣泛的上網行為統計資訊，為其搜尋引擎精準率提供更具體、可信的數字的數據分析

一般大眾的好處：
- 快速：上網速度加快，因為加速了查詢 DNS 的速度，他們在快取(Caching)機制不一樣，會在 TTL 到期之前預抓(Prefetch)過
- 安全：提升網路透過這些廣泛的上網行為統計資訊，為其搜尋引擎精準率提供更具體、可信的數字確： Google 遵守 DNS 各種協定來走，並且Google Public DNS查詢所得到的資訊也不會有一堆有的沒有的垃圾資訊
- 層級：Google Public DNS主機是位於 DNS root 下來的第一層 DNS 主機，所以當一個查詢送出時，最多往上一層就可以得到答案了，因此直接取得 DNS 查詢結果，

資料來源
[全新的 Google Public DNS 服務](https://gordon168.tw/google-public-dns/)

## 什麼是資料庫的 lock？為什麼我們需要 lock？
當同一筆資料，同時由多個使用者在操作時，可以 用 lock 將此筆資料先鎖住，由先發出要求的使用者執行，資料更新之後才會解除 (unlock)，交由下一位使用者執行，以預防其他人先存取到此筆資料。

例如當搶票時只剩一張票，這時候如果多個使用者同時發出 query，若沒有 lock 可能造成資料不正確的情況，像是超賣。


## NoSQL 跟 SQL 的差別在哪裡？
**資料模型：**
- SQL： 必須事先定義好 Schema，像是資料庫的規格書。資料庫裡面要有哪些欄位、每一個欄位的資料型態是什麼。在建立 Table 的時候，也是要用資料庫指令去新建的：
- NoSQL： 沒有 schema ，所以不必事先知道要存哪些資料。好處比較彈性，可是相對的你在查詢資料的時候速度也會比較慢一點。而且這些 NoSQL 系統，儲存資料的格式通常都是 JSON。

**ACID 屬性：**
- SQL：關聯式資料庫則提供單元性、一致性、隔離性和耐用性 (ACID) 的屬性：
- NoSQL：由於更彈性化與靈活，所以會犧牲掉 ACID 的標準。NoSQL 中只要CAP(一致性，可用性，分區容錯性)中的任意兩項中選擇，因為在基於節點的分散式系統中，很難做到三項都滿足。
一致性（Consistency）：等同於所有節點訪問同一份最新的數據副本
可用性（Availability）：每次請求都能獲取到非錯的響應——但是不保證獲取的數據為最新數據
分區容錯性（Partition tolerance）：以實際效果而言，分區相當於對通信的時限要求。系統如果不能在時限內達成數據一致性，就意味著發生了分區的情況，必須就當前操作在C和A之間做出選擇。
[CAP定理-維基百科](https://zh.wikipedia.org/wiki/CAP%E5%AE%9A%E7%90%86)

**資料處理：**
- SQL：資料庫可以可靠的儲存和處理資料，並且儲存較為重要的資料，例如交易資料。
- NoSQL：由於 NoSQL 的資料模型是非結構化的形式，因此非常適合處利巨量資料。

**擴充性：**
- SQL：擴充能力弱、成本高。關聯式資料庫通常透過增加硬體運算能力向上擴展，或以新增唯讀工作負載複本的方式向外擴展。
- NoSQL：擴充能力強、成本低。NoSQL 資料庫通常可分割，因為存取模式可透過使用分散式架構來向外擴展，以近乎無限規模的方式提供一致效能來增加資料吞吐量。

資料來源
[AWS-什麼是 NoSQL？](https://aws.amazon.com/tw/nosql/)
[SQL與NoSQL（關係型與非關係型）資料庫的區別](https://iter01.com/158511.html)

## 資料庫的 ACID 是什麼？
為了保證 Tranction 的正確性，需要符合以下四個特性
1. 原子性(atomicity)：交易是一個不可分割的完整個體，他不是全部成功就是全部失敗
2. 一致性(consistency)：指我們交易前與交易後要有一致性，例如：錢的總數要一樣
3. 隔離性(isolation)：多筆交易間不會互相影響(不能同時改同一個值)，例如：在某交易執行期間所用的資料，直到交易被確認為止前，都不能讓其他交易讀取或寫入。
4. 持久性(durability)：一旦交易執行，在交易成功之後，即使未來系統當機或者毀損，寫入的資料不會不見。
