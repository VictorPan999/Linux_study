# 鳥哥的Linux私房菜 Ch0
###### tags: `Linux` `鳥哥`
習題參考解答：https://blog.csdn.net/qq_41151659/article/details/94491657
## Intel AMD x86架構重要的微指令集
x86 instruction listings
https://en.wikipedia.org/wiki/X86_instruction_listings

单指令流单数据流机器（SISD）

SISD机器是一种传统的串行计算机，它的硬件不支持任何形式的并行计算，所有的指令都是串行执行。并且在某个时钟周期内，CPU只能处理一个数据流。因此这种机器被称作单指令流单数据流机器。早期的计算机都是SISD机器，如冯诺.依曼架构，如IBM PC机，早期的巨型机和许多8位的家用机等。

单指令流多数据流机器（SIMD）

SIMD是采用一个指令流处理多个数据流。这类机器在数字信号处理、图像处理、以及多媒体信息处理等领域非常有效。

Intel处理器实现的MMXTM、SSE（Streaming SIMD Extensions）、SSE2及SSE3扩展指令集，都能在单个时钟周期内处理多个数据单元。也就是说我们现在用的单核计算机基本上都属于SIMD机器。

多指令流单数据流机器（MISD）

MISD是采用多个指令流来处理单个数据流。由于实际情况中，采用多指令流处理多数据流才是更有效的方法，因此MISD只是作为理论模型出现，没有投入到实际应用之中。

多指令流多数据流机器（MIMD）

MIMD机器可以同时执行多个指令流，这些指令流分别对不同数据流进行操作。最新的多核计算平台就属于MIMD的范畴，例如Intel和AMD的双核处理器等都属于MIMD。
![](https://i.imgur.com/LDdZavK.png)
[Source](https://zh.wikipedia.org/wiki/%E8%B2%BB%E6%9E%97%E5%88%86%E9%A1%9E%E6%B3%95)


## 查詢內部元件資訊
查看 Linux 系統資訊常用指令  
lspci -v => 檢查系統 PCI 介面的各項裝置  
lsusb => 檢查系統USB介面的裝置  
lsscsi => 檢查系統SCSI介面的裝置  
cat /proc/cpuinfo => 顯示CPU的資訊  
cat /proc/meminfo => 顯示記憶體的資訊  
free => 顯示記憶體的相關資訊  
dmidecode => 查看硬體的相關資訊  
hdparm -i /dev/hda => 硬碟的各項資訊  
dmesg => Linux Kernel 運作過程當中所顯示的各項訊息記錄  
uname -a => 顯示Linux系統資訊  
cat /proc/version => 查看 Linux 核心  
cat /etc/issue => 查看 Linux 系統版本  
smartctl -a /dev/sda => 查看硬碟詳細資訊及型號  
[Source](https://taiwanwolf.blogspot.com/2009/02/linux.html)  
參考資料  
https://book.51cto.com/art/201004/197185.htm#book_content  
https://www.linuxprobe.com/intel-vt-amd-svm.html  
http://linux.vbird.org/linux_basic/0105computers.php  

## 第0章習題
### 第一題
根據本章中的說明，請找出目前全世界跑得最快的超級電腦的：（1）系統名稱；（2）所在位置；（3）使用的CPU型號與規格；（4）總共使用的CPU數量；（5）全功率運行1天時，可能使用的電費。  
（1）Summit超級計算機（IBM研發）  
（2）所在位置：美國能源部橡樹嶺國家實驗室  
（3）由4608台計算服務器組成，每個服務器含2個22核Power9處理器（IBM生產）和6個Tesla V100圖形處理單元（NVIDIA生產）。  
（4）總計使用了9216塊CPU  
（5） Power9 CPU的功耗為150W到180W左右，取中間數165W；  
Tesla V100最大功率300W；  
其他的功耗如主板，電源內耗，顯示器忽略不計；  
Summit超算的總功耗約為9815kW  
運行一天所耗的電量為：235560千瓦時。  
以工業用電0.5元/千瓦時來計算，該機器全功率運行一天至少花費11萬7180元！  
[Source](https://blog.csdn.net/weixin_42188287/article/details/114262758)
### 第二題 第三題

### CPU
-------------------------------
`cat /proc/cpuinfo`
processor　：系統中邏輯處理核的編號。對於單核處理器，則課認為是其CPU編號，對於多核處理器則可以是物理核、或者使用超線程技術虛擬的邏輯核  
vendor_id　：CPU製造商  
cpu family　：CPU產品系列代號  
model　　　：CPU屬於其系列中的哪一代的代號  
model name：CPU屬於的名字及其編號、標稱主頻  
stepping　 ：CPU屬於製作更新版本  
cpu MHz　 ：CPU的實際使用主頻  
cache size ：CPU二級緩存大小  
physical id ：單個CPU的標號  
siblings ：單個CPU邏輯物理核數  
core id ：當前物理核在其所處CPU中的編號，這個編號不一定連續  
cpu cores ：該邏輯核所處CPU的物理核數  
apicid ：用來區分不同邏輯核的編號，系統中每個邏輯核的此編號必然不同，此編號不一定連續  
fpu ：是否具有浮點運算單元（Floating Point Unit）  
fpu_exception ：是否支持浮點計算異常  
cpuid level ：執行cpuid指令前，eax寄存器中的值，根據不同的值cpuid指令會返回不同的內容  
wp ：表明當前CPU是否在內核態支持對用戶空間的寫保護（Write Protection）  
flags ：當前CPU支持的功能  
bogomips ：在系統內核啟動時粗略測算的CPU速度（Million Instructions Per Second）  
clflush size ：每次刷新緩存的大小單位  
cache_alignment ：緩存地址對齊單位  
address sizes ：可訪問地址空間位數  

[Source](https://blog.csdn.net/oy5348/article/details/84112396)

### 記憶體
-------------------------------
`cat /proc/meminfo`
MemTotal :總內存  
MemFree :空閑內存   
MemAvailable :可用內存    
Buffers :給文件的緩沖大小   
Cached :高速緩沖存儲器    
SwapCached :被高速緩沖存儲用的交換空間的大小  
Active :活躍使用中的高速緩沖存儲器頁面文件大小  
Inactive :不經常使用中的告訴緩沖存儲器文件大小  
Active(anon) :活躍的匿名內存（進程中堆上分配的內存,是用malloc分配的內存）  
Inactive(anon) :不活躍的匿名內存  
Active(file) :活躍的file內存，//file內存：磁盤高速緩存的內存空間和“文件映射(將物理磁盤上的文件內容與用戶進程的邏輯地址直接關聯)”的內存空間，其中的內容與物理磁盤上的文件相對應  
Inactive(file) :不活躍的file內存  
Unevictable :不能被釋放的內存頁  
Mlocked :mlock()系統調用鎖定的內存大小  
SwapTotal :交換空間總大小  
SwapFree :空閑交換空間  
Dirty :等待被寫回到磁盤的大小  
Writeback :正在被寫回的大小  
AnonPages :未映射頁的大小  
Mapped :設備和文件映射大小  
Shmem :已經被分配的共用內存大小  
Slab 內核數據結構緩存大小  
SReclaimable :可收回slab的大小  
SUnreclaim :不可回收的slab的大小  
KernelStack :kernel消耗的內存  
PageTables :管理內存分頁的索引表的大小  
NFS_Unstable :不穩定頁表的大小  
Bounce :在低端內存中分配一個臨時buffer作為跳轉，把位於高端內存的緩存數據復制到此處消耗的內存  
WritebackTmp :USE用於臨時寫回緩沖區的內存  
CommitLimit :系統實際可分配內存總量  
Committed_AS :當前已分配的內存總量  
VmallocTotal :虛擬內存大小  
VmallocUsed :已經被使用的虛擬內存大小  
VmallocChunk :malloc 可分配的最大的邏輯連續的內存大小  
HardwareCorrupted :刪除掉的內存頁的總大小(當系統檢測到內存的硬體故障時)  
AnonHugePages :匿名 HugePages 數量  
CmaTotal :總的連續可用內存  
CmaFree :空閑的連續內存  
HugePages_Total :預留HugePages的總個數   
HugePages_Free :池中尚未分配的 HugePages 數量  
HugePages_Rsvd :表示池中已經被應用程式分配但尚未使用的 HugePages 數量  
HugePages_Surp :這個值得意思是當開始配置了20個大頁，現在修改配置為16，那麼這個參數就會顯示為4，一般不修改配置，這個值都是0  
Hugepagesize :每個大頁的大小  
DirectMap4k :映射TLB為4kB的內存數量  
DirectMap2M :映射TLB為2M的內存數量  
DirectMap1G :映射TLB為1G的內存數量  
————————————————
[Source](https://blog.csdn.net/shardy0/article/details/113994687)  
### 硬碟
-------------------------------
`sudo smartctl -i /dev/sda`   
`apt-get install smartmontools` 後透過`sudo smartctl -i /dev/sda` 顯示硬碟型號及規格,
或`apt-get install hdparm`後透過`sudo hdparm -i /dev/sda1` 取得更詳細的資訊  
[Source](https://blog.longwin.com.tw/2014/02/linux-query-hardware-2014/)

### 第四題
找出第四代Intel i7 4790 CPU的：（1）與南橋溝通的DMI帶寬有多大？（2）二級緩存的容量有多大？（3）最大PCIe通道數量有多少？並據以說明主板上面PCIe插槽的數量限制。   
[Source](https://www.techpowerup.com/cpu-specs/core-i7-9700.c2183)  

以3.6GHz計算，DMI帶寬為：14.4Gb/s  
四核的二級緩存為：1Mb  
PCIe3.0的速度約為1GB/s, 最多可以PCIe3.0的通道數量為14條。  
[Source](https://blog.csdn.net/weixin_42188287/article/details/114262758)
### 第五題
找出Intel SSD 520固態硬盤相關的功能列表，瞭解：（1）連接介面；（2）最大讀寫速度，以及（3）最大隨機讀寫數據（IOPS）等信息。
Intel SSD 520  
連接介面：SATA 3.0 6G/s  
最大讀/寫速度：550/520MB/s  
最大隨機讀寫數據：50000/60000 IOPS  
[Source](https://blog.csdn.net/weixin_42188287/article/details/114262758)
