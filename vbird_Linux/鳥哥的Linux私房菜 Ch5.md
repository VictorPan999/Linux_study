# 鳥哥的Linux私房菜 Ch5
###### tags: `Linux` `鳥哥`

## 權限
### chgrp
Change Group (改變群組)
```
[root@study ~]# chgrp [-R] dirname/filename ...
選項與參數：
-R : 進行遞迴(recursive)的持續變更，亦即連同次目錄下的所有檔案、目錄
     都更新成為這個群組之意。常常用在變更某一目錄內所有的檔案之情況。
範例：
[root@study ~]# chgrp users initial-setup-ks.cfg
[root@study ~]# ls -l
-rw-r--r--. 1 root users 1864 May  4 18:01 initial-setup-ks.cfg
[root@study ~]# chgrp testing initial-setup-ks.cfg
chgrp: invalid group:  `testing' <== 發生錯誤訊息囉～找不到這個群組名～
```
### chown
Change Owner (改變擁有者)
```
[root@study ~]# chown [-R] 帳號名稱 檔案或目錄
[root@study ~]# chown [-R] 帳號名稱:群組名稱 檔案或目錄
選項與參數：
-R : 進行遞迴(recursive)的持續變更，亦即連同次目錄下的所有檔案都變更

範例：將 initial-setup-ks.cfg 的擁有者改為bin這個帳號：
[root@study ~]# chown bin initial-setup-ks.cfg
[root@study ~]# ls -l
-rw-r--r--. 1 bin  users 1864 May  4 18:01 initial-setup-ks.cfg

範例：將 initial-setup-ks.cfg 的擁有者與群組改回為root：
[root@study ~]# chown root:root initial-setup-ks.cfg
[root@study ~]# ls -l
-rw-r--r--. 1 root root 1864 May  4 18:01 initial-setup-ks.cfg
```
複製行為(cp)會複製執行者的屬性與權限，再透過chown讓使用者能夠修改
### chmod
檔案權限的改變
#### 數字類型改變檔案權限
r:4
w:2
x:1
```
[root@study ~]# chmod [-R] xyz 檔案或目錄
選項與參數：
xyz : 就是剛剛提到的數字類型的權限屬性，為 rwx 屬性數值的相加。
-R : 進行遞迴(recursive)的持續變更，亦即連同次目錄下的所有檔案都會變更
[root@study ~]# ls -al .bashrc
-rw-r--r--. 1 root root 176 Dec 29  2013 .bashrc
[root@study ~]# chmod 777 .bashrc
[root@study ~]# ls -al .bashrc
-rwxrwxrwx. 1 root root 176 Dec 29  2013 .bashrc
```
#### 符號類型改變檔案權限
![](https://i.imgur.com/vm23MFG.png)

```
[root@study ~]# chmod  u=rwx,go=rx  .bashrc
# 注意喔！那個 u=rwx,go=rx 是連在一起的，中間並沒有任何空白字元！
[root@study ~]# ls -al .bashrc
-rwxr-xr-x. 1 root root 176 Dec 29  2013 .bashrc
[root@study ~]# ls -al .bashrc
-rwxr-xr-x. 1 root root 176 Dec 29  2013 .bashrc
[root@study ~]# chmod  a+w  .bashrc
[root@study ~]# ls -al .bashrc
-rwxrwxrwx. 1 root root 176 Dec 29  2013 .bashrc
```

## 權限對文件影響
![](https://i.imgur.com/Q4whJd4.png)
## 權限對檔案影響
![](https://i.imgur.com/a2AIQm0.png)
## FHS檔案系統的類型
![](https://i.imgur.com/ZneTfjc.png)
## 目錄樹
![](https://i.imgur.com/cPJ2jtP.png)
## 絕對路徑與相對路徑
絕對路徑：由根目錄(/)開始寫起的檔名或目錄名稱， 例如 /home/dmtsai/.bashrc；
相對路徑：相對於目前路徑的檔名寫法。 例如 ./home/dmtsai 或 ../../home/dmtsai/ 等等。反正開頭不是 / 就屬於相對路徑的寫法
.  ：代表當前的目錄，也可以使用 ./ 來表示；
.. ：代表上一層目錄，也可以 ../ 來代表。
```
cd /var/log   (absolute)
cd ../var/log (relative)
```
## FHS & LSB
創建Linux基礎標準是為了降低支持Linux平臺的總體成本。通過減少各個Linux發行版之間的差異，LSB大大降低了將應用程式移植到不同發行版所涉及的成本，並降低了這些應用程式的售後支持所涉及的成本和工作量。
LSB 其實是 Linux Foundation 下的一個工程，FHS 是屬於 LSB 的一項工作
[Source](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.pdf)  
[Source](https://blog.csdn.net/sunqian666888/article/details/84555146)  
[Source](https://wiki.linuxfoundation.org/lsb/lsb-charter)  

## 第5章習題
### 第一題
早期的UNIX系統文件名最多允許14個字元，而新的UNIX與Linux系統中，文件名最多可以容許幾個字元？
解：由於使用Ext2/Ext3文件系統，單一檔名可達 255字元，完整文件名 (包含路徑)可達 4096 個字元。

### 第二題
當一個一般文件權限為 -rwxrwxrwx則表示這個文件的意義是什麼？
解：任何人皆可讀取、修改或編輯、可以執行，但不一定能刪除。

### 第三題
我需要將一個文件的權限改為-rwxr-xr—，請問該如何執行命令？
解：chmod 754 filename或 chmod u=rwx,g=rx,o=r filename

### 第四題
若我需要更改一個文件的所有者與用戶組，該用什麼命令？
解：chown, chgrp

### 第五題
請問下麵的目錄主要放置什麼數據？
/etc/, /etc/init.d, /boot, /usr/bin, /bin, /usr/sbin, /sbin, /dev, /var/log
解：/etc/：系統主要的配置文件幾乎都放置在這個目錄內，例如人員的賬號密碼文件、各種服務的起始文件等；/etc/init.d：所有服務的默認啟動腳本都是放在這個目錄中；/boot：主要放置在開機會使用到的文件，包括Linux內核文件以及開機菜單與開機所需配置文件等；/usr/bin：絕大部分的用戶可使用命令都在這里，與/bin不同的是這些命令與開機過程無關；/bin：主要放置在開機時，以及進入單用戶維護模式後還能夠被操作的命令；/usr/sbin：非系統正常運行所需要的系統命令，最常見的就是某些網路服務器軟體的服務命令；/sbin：主要放置開機過程中所需要的命令，裡麵包括了開機、修復、還原系統所需要的命令，只有系統管理員能使用；/dev：在Linux系統上，任何設備與介面設備都是以文件的形式存在與這個目錄當中；/var/log：主要放置登錄文件，記錄登錄信息。

### 第六題
若一個文件的文件名開頭為“.”，例如.bashrc這個文件，代表什麼？另外，如何顯示出這個文件名與它的相關屬性？
解：有“.”為開頭的為隱藏文件，需要使用 ls -a這個 -a的選項才能顯示出隱藏文件的內容，而使用 ls -al才能顯示出屬性。  
[Source:](https://blog.csdn.net/qq_41151659/article/details/94491657)
