# 鳥哥的Linux私房菜 Ch4
###### tags: `Linux` `鳥哥` 
## 指令
```
[dmtsai@study ~]$ command  [-options]  parameter1  parameter2 ...
                     指令     選項        參數(1)     參數(2)
```
一行指令中第一個輸入的部分絕對是『指令(command)』或『可執行檔案(例如批次腳本,script)』
command 為指令的名稱，例如變換工作目錄的指令為 cd 等等；
中刮號[]並不存在於實際的指令中，而加入選項設定時，通常選項前會帶 - 號，例如 -h；有時候會使用選項的完整全名，則選項前帶有 -- 符號，例如 --help；
parameter1 parameter2.. 為依附在選項後面的參數，或者是 command 的參數；
指令, 選項, 參數等這幾個咚咚中間以空格來區分，不論空幾格 shell 都視為一格。所以空格是很重要的特殊字元！；
按下[Enter]按鍵後，該指令就立即執行。[Enter]按鍵代表著一行指令的開始啟動。
指令太長的時候，可以使用反斜線 (\) 來跳脫[Enter]符號，使指令連續到下一行。注意！反斜線後就立刻接特殊字符，才能跳脫！
其他：
在 Linux 系統中，英文大小寫字母是不一樣的。舉例來說， cd 與 CD 並不同。

* -a -l這種指令可以合併為 -al 也是一樣的

```

[dmtsai@study ~]$ date    #顯示日期與時間的指令
[dmtsai@study ~]$ cal    #顯示日曆的指令
[dmtsai@study ~]$ bc    #簡單好用的計算機
[dmtsai@study ~]$ locale    #查看語系

#修改語系
[dmtsai@study ~]$ LANG=en_US.utf8
[dmtsai@study ~]$ export LC_ALL=en_US.utf8
#LANG 只與輸出訊息有關，若需要更改其他不同的資訊，要同步更新 LC_ALL 才行！

#求助與查詢
[dmtsai@study ~]# date --help    ＃--help 求助說明
[dmtsai@study ~]$ man date    #
[dmtsai@study ~]$ whatis  [指令或者是資料]   <==相當於 man -f [指令或者是資料]
[dmtsai@study ~]$ apropos [指令或者是資料]   <==相當於 man -k [指令或者是資料]
[dmtsai@study ~]$ info info

#寫入文書編輯器
[dmtsai@study ~]$ nano text.txt

#關機
[root@study ~]# sync #資料同步寫入磁碟
[root@study ~]# /sbin/shutdown [-krhc] [時間] [警告訊息]
選項與參數：
-k     ： 不要真的關機，只是發送警告訊息出去！
-r     ： 在將系統的服務停掉之後就重新開機(常用)
-h     ： 將系統的服務停掉後，立即關機。 (常用)
-c     ： 取消已經在進行的 shutdown 指令內容。
時間   ： 指定系統關機的時間！時間的範例底下會說明。若沒有這個項目，則預設 1 分鐘後自動進行。
範例：
[root@study ~]# /sbin/shutdown -h 10 'I will shutdown after 10 mins'
[root@study ~]# halt      # 系統停止～螢幕可能會保留系統已經停止的訊息！
[root@study ~]# poweroff  # 系統關機，所以沒有提供額外的電力，螢幕空白！
[root@study ~]# systemctl [指令]
指令項目包括如下：
halt       進入系統停止的模式，螢幕可能會保留一些訊息，這與你的電源管理模式有關
poweroff   進入系統關機模式，直接關機沒有提供電力喔！
reboot     直接重新開機
suspend    進入休眠模式

[root@study ~]# systemctl reboot    # 系統重新開機
[root@study ~]# systemctl poweroff  # 系統關機
```
* Tab按鍵可以進行 命令補齊 檔案補齊 選項參數補齊
* super鍵加上方向鍵可以進行視窗的拖曳
* ctrl c可以中斷指令
* ctrl d可以關閉文字界面
* man page 中可以用"/"or"?"加上關鍵字進行查詢
[source](http://linux.vbird.org/linux_basic/0160startlinux.php)
## 第4章習題
### 情景模擬題第一題
1.我們在命令行界面，例如tty2裡面看到的歡迎界面，就是在那個login：之前的頁面（CentOS Linux 7 … ）是怎麼來的？
目標：瞭解到終端的歡迎信息是怎麼來的？
前提：歡迎信息的內容，記錄在/etc/issue當中的。
需求：利用man找到該文件當中的變量內容。
情景模擬題的解決步驟：
歡迎界面是在/etc/issue文件中，你可以使用【nano /etc/issue】看看該文件的內容（註意，不要修改這個文件內容，看完就離開），這個文件的內容有點像下麵這樣：
```
\S
Kernel \r on an \m
```
### 情景模擬題第二題
2.與tty3比較之下，發現到內核版本使用的是\r而硬體等級則是\m來取代，這兩者代表的意義是什麼？由於這個文件的文件名是issue，所以我們使用【man issue】來查看這個文件的格式；
通過上一步的查詢我們會知道反斜杠（\）後面接的字元是與agetty（8）及mingetty（8）有關，故進行【man agetty】這個命令的查詢。
由於反斜杠（\）的英文為escape，因此在上個步驟的man環境中，你可以使用【/escape】來查找各反斜杠後面所接字元所代表的意義是什麼。
請自行找出：如果我想要在/etc/issue文件內表示【時間（localtime）】與【tty號碼（如tty1，tty2的號碼）】的話，應該要找到哪個字元來表示（通過反斜杠的功能）？
解：\t與\l。
### 簡答題第一題
1.簡單查詢一下，Physical console、Virtual console、Terminal的說明是什麼？
解：（1）基於物理設備的連接，稱為物理終端（Pysical Terminal），也可以稱為物理控制台（Pyhsical console）。
（2）一個物理終端（物理控制台），可以支持多個虛擬終端（或虛擬控制台 virtual console）。
（3）隨著X視窗系統的廣泛使用，虛擬控制台的使用需求也越來越少，控制台程式可以在終端模擬器(terminal emulator)中運行，這些被稱為偽終端(Pseudo Terminal)。
### 簡答題第二題
2.請問如果我以命令行模式登錄Linux主機時，我有幾個終端介面可以使用？如何切換各個不同的終端介面？
解：有6個終端介面可以使用切換方式為[Ctrl]+[Alt]+[F1F6]。Linux默認情況下會提供6個terminal，分別命名為tty1tty6。
### 簡答題第三題
3.在Linux系統中，/VBird與/vbird是否為相同的文件？
解：不同。Linux系統區分大小寫。
### 簡答題第四題
4.我想要知道date如何使用，應該如何查詢？
解：兩種方式：man date（UNIX like通用），info date（Linux）。
### 簡答題第五題
5.我想要在今天的1:30讓系統自己關機，要怎麼做？
解：shutdown -h 1:30
### 簡答題第六題
6.如果Linux的X Window突然發生問題而掛掉，但Linux本身還是好好的，那麼我可以按下哪三個按鍵來讓X Window重啟？
解：[Ctrl]+[Alt]+[Backspace]
### 簡答題第七題
7.我想要知道2010年5月2日是星期幾？該怎麼做？
解：cal 5 2010；調出2010年5月日歷查看。
### 簡答題第八題
8.使用man date找出顯示目前的日期與時間的參數，顯示方式類似：2015/10/16-20:03。
解：date +%Y/%m/%d-%H:%M
### 簡答題第九題
9.若以X Window為默認的登錄方式，那請問如何進入Virtual console呢？
解：[Ctrl]+[Alt]+[F1~F6]。
### 簡答題第十題
10.簡單說明在bash shell的環境下，[Tab]按鍵的用途？
解：在命令行模式下[Tab]按鍵具有“命令補全”與“文件補齊”的功能。[Tab]接在一串命令的第一個命令的後面為“命令補全”，接在一串命令的第二個命令以後時則為“文件補齊”。
### 簡答題第十一題
11.如何強制終端一個程式的進行？（利用按鍵，非利用kill命令）
解：[Ctrl]+[C]
### 簡答題第十二題
12.Linux提供相當多的在線查詢，稱為man page，請問，我如何知道系統上有多少關於passwd的說明？可以使用其他的程式來替代man的這個功能嗎？
解：利用man -f passwd來查詢。在Linux上可以用info passwd命令來替代man的在線查詢passwd的功能。
### 簡答題第十三題
13.在man page顯示的內容中，命令（或文件）後面會接一組數字，這個數字若為1，5，8，表示該查詢的命令（或文件）意義是什麼？
解：代表意義為：1)用戶在shell環境中可以操作的命令或可執行文件；5)配置文件或者是某些文件的格式8)；系統管理員能夠使用的管理命令。
### 簡答題第十四題
14.man page顯示的內容的文件是放置在哪些目錄中？
解：不同的Linux distributions可能會有所不同，通常是放在/usr/share/man這個目錄里。
### 簡答題第十五題
15.請問【foo 1 -foo2 foo3 foo4】這一串命令中各代表什麼意義？
解：foo1一定是指令， -foo2則是foo1這個指令的選擇項目參數， foo3與foo4則不一定，可能是foo1的參數設定值，也可能是額外加入的parameters。
### 簡答題第十六題
16.當我輸入man date時，在我的終端卻出現一些亂碼，請問可能的原因是什麼？如何修正？
解：亂碼是由語系導致。可以在終端輸入echo &LANG命令查看當前使用的語言，再輸入LANG=en_CN.UTF-8修改語言（臨時修改）即可。
### 簡答題第十七題
17.我輸入這個命令“ls -al /vbird”，系統回復我這個結果：“ls /vbird: No such file or directory”，請問發生了什麼事？
解：沒有/vbird這個文件或目錄。
### 簡答題第十八題
18.我想知道目前系統有多少命令是以bz為開頭的，可以怎麼做？
解：輸入 bz[Tab][Tab]查看。
### 簡答題第十九題
19.承上題，在出現的許多命令中，請問bzip2是乾嘛用的？
解：使用man bzip2命令查看可以知道是用來壓縮與解壓縮文件用的。
### 簡答題第二十題
20.在終端裡面登錄後，看到的提示符KaTeX parse error: Expected 'EOF', got '#' at position 2: 與#̲有何不同？平時操作應該使用哪一…則代表一般身份使用者。依據提示字元的不同，我們可以約略判斷登入者身份。一般來說，建議日常操作使用一般身份使用者登入，即是$。
### 簡答題第二十一題
21.我使用dmtsai這個賬號登錄系統了，請問我能不能使用reboot來重啟？若不能，請說明原因，若可以，請說明命令如何執行？
解：理論上reboot僅能讓root運行。不過，如果dmtsai是在主機前面以圖形介面登陸時，則dmtsai還是可以透過圖形介面功能來關機。  
[Source](https://blog.csdn.net/qq_41151659/article/details/94491657)
