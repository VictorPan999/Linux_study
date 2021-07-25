# 鳥哥的Linux私房菜 Ch1
###### tags: `Linux` `鳥哥`
## 酷學員討論區
http://phorum.study-area.org/

## 網路學習書籍推薦
http://linux.vbird.org/linux_basic/0120howtolinux/0120howtolinux_1.php

## 第一章習題
### 實踐題第一題
請上網找出目前Linux內核的最新穩定版與開發中版本的版本號碼，請註明查詢的日期與對應的版本。
Linux的內核版本有兩種：穩定版與開發版；
Linux內核版本號是由3個數字構成：a.b.c
a：目前發布版的內核主版本。
b：偶數表權示穩固版本；奇數表示開發中版本。
c：錯誤修補的次數。
其中第一個數字是主版本號，第二個數字是次版本號，第三個數字是修訂版本號。
(註：3.10版本之後就不再用奇數、偶數的編號格式了，所以百度回答的結果5年前還可以適用）
2021年3月2日查詢的最新穩定版是5.12-rc1，在kerne.org網站上可以查到。

其中rc表示“候選發布”，它由開發者進行測試並“打磨”所有的這些很酷的新特性。基於他們這幾輪測試的反饋，Linus 決定最終版本是否已經準備就緒。通常有 7 個每周預發布版本，但是，這個數字經常走到 -rc8，並且有時候甚至達到 -rc9 及以上。當 Linus 確信那個新內核已經沒有問題了，他就製作最終發行版，我們稱這個版本為“穩定版”，表示它不再是一個“候選發布版”。
[參考網站](https://blog.csdn.net/F8qG7f9YD02Pe/article/details/79329760?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&dist_request_id=&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control)
上一個版本為5.11.2，屬於穩定版，5.12-rc1發布背後還有一個故事，有興趣的可以看一下，[鏈接](https://www.phoronix.com/scan.php?page=news_item&px=Linux-5.12-rc1-Released)
可以通過：
`uname -r`
查詢自己機器的內核版本，如果過低可以自己升級一下內核版本。[參考博客](https://blog.csdn.net/qq_18683985/article/details/79961378)
不過不建議自己升級內核版本，因為每個發行版一般對應一個Linux內核版本，如何要升級的話，可能會導致一些舊的軟體不能使用。如果想用新的Linux內核，最好的方式是下載安裝最新的Linux發行版。
另外，電腦上如果存在多個內核的話，一般可以選擇一個內核進入，多餘的內核比較占用空間，可以刪除，[參考博客](https://blog.csdn.net/weixin_42388648/article/details/80623760)
下麵這篇博客完美的解決瞭如何編譯安裝Linux內核，參考[博客](https://www.cnblogs.com/harrypotterjackson/p/11846222.html)
### 實踐題第二題
請上網找出Linux吉祥物企鵝的名字，以及最原始的圖形文件。（www.linux.com）
Tux，該網站上沒有找到原始圖片的文件，下麵這張圖片是必應圖片。關於該吉祥物的來源可以看[博客](https://blog.csdn.net/zzoeey/article/details/76169598)。
### 實踐題第三題
請上網找出Andriod與Linux內核版本間的關系。
Android的內核基於Linux內核的長期支持（LTS）分支。截至2020年，Android使用Linux內核的版本4.4、4.9或4.14。實際使用的內核版本取決於特定的機器。Android的Linux內核變體具有進一步的架構更改，這些更改由Google在典型的Linux內核開發周期之外實施，例如包含設備樹，ashmem，ION等組件以及不同的內存不足（OOM）處理。Google歸還Linux內核的某些功能，特別是稱為“ wakelocks”的電源管理功能，最初被主線內核開發人員拒絕，部分原因是他們認為Google沒有表現出維護自己代碼的意圖。
[wikipedia](https://en.wikipedia.org/wiki/Android_%28operating_system%29)
### 簡答題第一題
你在你的主機上面安裝了一塊網卡，但是開機之後，系統卻無法使用，你確定網卡是好的，那麼可能出現的問題出在哪裡？該如何解決？
確定網卡沒有問題，再排除硬體問題，即PCI插口有沒有虛插，重新插一次。如果問題還沒有解決，可以考慮是不是軟體相關的問題。
a. 需禁用主板自帶網卡，否則新的網卡會無法識別；
b. 網卡驅動未安裝；
c. 網卡驅動過新或者過舊，找到適合自己網卡的驅動程式。
### 簡答題第二題
一個操作系統至少要能夠完整控制整個硬體，請問操作系統應該要控制硬體的哪些單元？
運算單元、控制單元、寄存器組、總線介面單元、輸入/輸出單元。操作系統只是在管理整個硬體資源，包括CPU、內存、輸入輸出設備及文件系統，因此操作系統要控制的就是這些硬體的內部單元。
### 簡答題第三題
我在Windows上面玩的游戲可不可以拿到Linux去玩？
不可以直接玩。游戲屬於應用程式，應用程式是參考操作系統提供的API所開發出來的軟體，不同的操作系統會對應不同版本的應用程式軟體。可以考慮對應的Linux系統的游戲。比如Linux和Window都是可以使用QQ應用程式。
### 簡答題第四題
Linux本身僅是一個內核與相關的內核工具而已，不過，它已經可以驅動所有的硬體，所以，可以算是一個很陽春的操作系統了。經過其他應用程式的開發之後，被整合成為Linux distributions。請問眾多的distributions之間有何異同？
各大Linux Distributions的主要異同在於支持標準。“Linux kernel + Software + Tools + Documentation”組成的可完整安裝的程式被稱為Linux distributions。每一個Linux distributions使用的kernel都是http://www.kernel.org所發布的，而他們所選擇的軟體幾乎都是目前很知名的軟體，重復性相當高。此外，為了讓所有的Linux distributions開發不至於差異太大，且讓這些開發商在開發的時候有所依據，還有Linux Standard Base（LSB）等標準來規範開發者，以及目錄架構的File system Hierarchy Standard（FHS）標準規範，它們的唯一差別可能就是該開發者自家所開發出來的管理工具以及套件管理的模式。所以說，基本上，每個Linux distributions除了架構的嚴謹度與選擇的套件內容外，其實差異並不太大。
每個Linux發行版使用的內核都由https://www.kernel.org網站所發布。
### 簡答題第五題
UNIX是誰寫出來的？GNU項目是誰發起的？
1973年，UNIX正式誕生，Ritchie和Tompson合作用C語言寫出了第一個正式UNIX內核。
1984年，Richard Mathew Stallman發起GNU計劃。
### 簡答題第六題
GNU的全名為何？它主要由哪個基金會支持？
GNU’s Not UNIX
由自由軟體基金會FSF支持。
### 簡答題第七題
何謂多用戶（Multi-user）多任務（Multi-task）?
多用戶是可以在系統上創建多個用戶，且多個用戶可以同時使用系統資源；對於多任務，理論上一個CPU在一個時間內僅能進行一個程式，多任務，即計算機對於多個任務，會在不同的程式間切換，讓用戶感覺多個任務是在同步進行（現在的多核心計算機可以實現真正的多任務同時處理）。Linux是一個真實的、完整的多用戶多任務操作系統，可以在Linux上建立多個用戶，而多個用戶可以在同一時間內登錄同一個系統執行不同的任務而互不影響。所以Linux系統一般用作服務器的系統。
### 簡答題第八題
簡單說明GUN General Public License（GPL）與Open Source的精神。
1.GPL的授權之軟體，乃為自由軟體（Free software），任何人皆可擁有他； 2.開發 GPL 的團體(或商業企業)可以經由該軟體的服務來取得服務的費用； 3.經過 GPL授權的軟體，其屬於 Open source的情況，所以應該公佈其原始碼； 4.任何人皆可修改經由 GPL授權過的軟體，使符合自己的需求； 5.經過修改過後 Open source應該回饋給 Linux社群。
### 簡答題第九題
什麼是POSIX？為何說Linux使用POSIX時對於開發有很好的影響？
書上45,46頁。
POSIX表示可移植操作系統介面(Portable Operating System Interface of UNIX，縮寫為 POSIX )，POSIX標準定義了操作系統應該為應用程式提供的介面標準，是IEEE為要在各種UNIX操作系統上運行的軟體而定義的一系列API標準的總稱，其正式稱呼為IEEE 1003，而國際標準名稱為ISO/IEC 9945。
主要針對在 Unix操作系統上面跑的程式來進行規範。若你的操作系統符合 POSIX，則符合 POSIX的程式就可以在你的操作系統上面運作。 Linux由於支持 POSIX，因此很多 Unix上的程式可以直接在 Linux上運作，因此程式的移植相當簡易！也讓大家容易轉換平臺，提升 Linux的使用率。
### 簡答題第十題
簡單說明Linux成功的因素。
a. 穩定的系統；
b. 免費；
c. 更新頻率高，安全性好，漏洞少；
d. 多任務，多用戶；
e. 用戶與用戶組的規劃；
f. 系統對一些硬體資源消耗較少；
g. 對於便攜嵌入式系統有很好的適用性；
h. 開源，背後有強大的開發團隊，遵循Open Source的開發標準。
————————————————
[Source](https://blog.csdn.net/weixin_42188287/article/details/114286846)