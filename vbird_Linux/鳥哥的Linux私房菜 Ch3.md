# 鳥哥的Linux私房菜 Ch3
###### tags: `Linux` `鳥哥`

## 裝置類型 LVM
標準分割區：就是我們一直談的分割槽啊！類似 /dev/vda1 之類的分割就是了。

LVM：這是一種可以彈性增加/削減檔案系統容量的裝置設定，我們會在後面的章節持續介紹 LVM 這個有趣的東西！

LVM 緊張供應：這個名詞翻譯的超奇怪的！其實這個是 LVM 的進階版！與傳統 LVM 直接分配固定的容量不同， 這個『 LVM 緊張供應』的項目，可以讓你在使用多少容量才分配磁碟多少容量給你，所以如果 LVM 裝置內的資料量較少，那麼你的磁碟其實還可以作更多的資料儲存！ 而不會被平白無故的佔用！這部份我們也在後續談到 LVM 的時候再來強調！
## 檔案系統項目
ext2/ext3/ext4：Linux早期適用的檔案系統類型。由於ext3/ext4檔案系統多了日誌的記錄， 對於系統的復原比較快速。不過由於磁碟容量越來越大，ext 家族似乎有點擋不住了～所以除非你有特殊的設定需求，否則近來比較少使用 ext4 項目了！
swap：就是磁碟模擬成為記憶體，由於swap並不會使用到目錄樹的掛載，所以用swap就不需要指定掛載點喔。
BIOS Boot：就是 GPT 分割表可能會使用到的項目，若你使用 MBR 分割，那就不需要這個項目了！
xfs：這個是目前 CentOS 預設的檔案系統，最早是由大型伺服器所開發出來的！ 他對於大容量的磁碟管理非常好，而且格式化的時候速度相當快，很適合當今動不動就是好幾個 TB 的磁碟的環境喔！因此我們主要用這玩意兒！
vfat：同時被Linux與Windows所支援的檔案系統類型。如果你的主機硬碟內同時存在Windows與Linux作業系統，為了資料的交換， 確實可以建置一個vfat的檔案系統喔！

## GPT MBR MSDOS
The options correspond to the various partitioning systems supported in libparted; there's not much documentation, but looking at the source code:

aix provides support for the volumes used in IBM’s AIX (which introduced what we now know as LVM);
amiga provides support for the Amiga’s RDB partitioning scheme;
bsd provides support for BSD disk labels;
dvh provides support for SGI disk volume headers;
gpt provides support for GUID partition tables;
mac provides support for old (pre-GPT) Apple partition tables;
msdos provides support for DOS-style MBR partition tables;
pc98 provides support for PC-98 partition tables;
sun provides support for Sun’s partitioning scheme;
loop provides support for raw disk access (loopback-style) — I’m not sure about the uses for this one.
As you can see, the majority of these are for older systems, and you probably won’t need to create a partition table of any type other than gpt or msdos.

For a new disk, I recommend gpt: it allows more partitions, it can be booted even in pre-UEFI systems (using grub), and supports disks larger than 2 TiB (up to 8 ZiB for 512-byte sector disks). Actually, if you don’t need to boot from the disk, I’d recommend not using a partitioning scheme at all and simply adding the whole disk to mdadm, LVM, or a zpool, depending on whether you use LVM (on top of mdadm or not) or ZFS.
[Source](https://unix.stackexchange.com/questions/289389/what-are-the-differences-between-the-various-partition-tables)

## KDUMP
kdump是Linux核心的一個功能，可在發生核心錯誤時建立核心轉儲。當被觸發時，kdump會匯出一個記憶體映像（也稱為vmcore），該映像可用於除錯和確定崩潰的原因。 主記憶體的轉儲映像作為可執行與可連結格式（ELF）物件匯出，可以在處理核心崩潰時通過/proc/vmcore直接存取，也可以自動儲存到本地可存取的檔案系統、 裸裝置或通過網路存取的遠端系統。
[Source](https://zh.wikipedia.org/zh-tw/Kdump)
## Parted
### Install:
```
$ sudo apt-get install parted           [On Debian/Ubuntu systems]
# yum install parted                    [On RHEL/CentOS and Fedora]
# dnf install parted                    [On Fedora 22+ versions]
```
### Check Version:
`$ parted`
### List Partitions:
`(parted) print`
### List or Switch to Different Disk:
`(parted) select /dev/sdX`
### Create Primary or Logical Partition in Linux:
use `(parted) print` to check using the right disk
give the new disk a label name `(parted) mklabel msdos`
Now create the new partition with `(parted) mkpart`
format new partition in file system using `# mkfs.ext4 /dev/sdb1`
### Resize Linux Disk Partition:
know the number of the partition that you will be resizing by 
`(parted) print` then run the resizepart command `(parted) resizepart`
### Delete Linux Partition:
go to the disk `(parted) select /dev/sdb1`know the number of the partition 
`(parted) print`then use `(parted) rm 1` to delete the partition with number 1 from our secondary drive /dev/sdb1.
### Rescue Linux Disk Partition:
Parted supports a “rescue" utility that helps you recover a lost partition between a starting and ending point. If a partition is found within that range, it will attempt to restore it. `(parted) rescue`
### Change Linux Partition Flag:
Using parted, you can change the state of a flag for disk partitions. The supported flags are:
boot
root
swap
hidden
raid
lvm
lba
legacy_boot
irst
esp
palo
The states can be either "on" or "off". To change a flag simply run "set" command within parted:
`(parted) set 2 lba on`
The above command sets lba flag to on for second partition. Verify the results with print
[Source](https://www.tecmint.com/parted-command-to-create-resize-rescue-linux-disk-partitions/)
## 網路遮罩
基本上你要先有一個認識 就是所謂的IPv4 的IP是有兩個段落 123.456.aaa.bbb 是一個在Class B的網段. 則123.456屬於網路地址 而aaa.bbb屬於主機地址

而在subnetting就可以讓網路管理員(可能是人員或是設備)去將這個網址切割開來. 為何要這樣做呢? 因為實際上的 IP並不是你所見到的格式, 因為設備在訊息交換的過程是採用Binary(二進位)

舉例:

IP: 192.168.100.101
Binary: 11000000.10101000.01100100.01100101
怎樣轉換的 你可以使用 Windows內建的小算盤去試試看, 不然就請研究計算機概論

以上述為例則11000000.10101000 為Class B網段地址
主機地址就是01100100.01100101

而通成Subnet Mask你都怎設定 ?如果設定成 255.255.255.0 就是11111111.11111111.11111111.00000000
然後用AND運算


11000000.10101000.01100100.01100101 (192.168.100.101) IP Address
11111111.11111111.11111111.00000000 (255.255.255.0) Subnet Mask
AND運算後
11000000.10101000.01100100.00000000 (192.168.100.0) Subnet

"""總而言之, Subnet Mask就是為了要讓電腦能夠像帶了一副眼鏡可以看清楚這個IP是屬於哪個網段的主機."""
[Source](https://www.mobile01.com/topicdetail.php?f=110&t=878758)
## 筆電設置
關閉電源管理模組，因筆電可能使用特殊的節電裝置
`nofb apm=off acpi=off pci=noacpi`
apm(Advanced Power Management)是早期的電源管理模組，acpi(Advanced Configuration and Power Interface)則是近期的電源管理模組。這兩者都是硬體本身就有支援的，但是筆記型電腦可能不是使用這些機制， 因此，當安裝時啟動這些機制將會造成一些錯誤，導致無法順利安裝。

nofb則是取消顯示卡上面的緩衝記憶體偵測。因為筆記型電腦的顯示卡常常是整合型的， Linux安裝程式本身可能就不是很能夠偵測到該顯示卡模組。此時加入nofb將可能使得你的安裝過程順利一些。
## Grub
GNU GRUB（簡稱「GRUB」）是一個來自GNU專案的啟動載入程式。GRUB是多啟動規範的實現，它允許使用者可以在電腦內同時擁有多個作業系統，並在電腦啟動時選擇希望執行的作業系統。GRUB可用於選擇作業系統分割區上的不同核心，也可用於向這些核心傳遞啟動參數。

GNU GRUB的前身為Grand Unified Bootloader。它主要用於類Unix系統；同大多Linux發行版一樣，GNU系統也採用GNU GRUB作為它的啟動器。Solaris從10 1/06版開始在x86系統上也採用GNU GRUB作為啟動器。
[Source](https://zh.wikipedia.org/zh-tw/GNU_GRUB)
## 第3章習題
### 第一題
Linux的目錄配置以“樹狀目錄”來配置，至於磁盤分區（partition）則需要與樹狀目錄相配合！請問，在默認的情況下，在安裝的時候系統會要求你一定要分出來的兩個分區是什麼？
解：/和swap兩個分區。
Do you need a separate /home partition? Definitely not. The home partition is where your personal files (Documents, Downloads, Pictures, etc) are stored. If you don't make a separate /home partition, those files will be saved in /home/username folder. So if this is your first time installing Ubuntu, don't try to make it too complicated and don't make a separate partition for /home. When you are more experienced and confident, you can try this.

Do you need a separate /swap partition? Well, it depends. If you want to hibernate you will need a separate /swap partition (see below). /swap is used as a virtual memory. Ubuntu uses it when you run out of RAM to prevent your system from crashing. However, new versions of Ubuntu (After 18.04) have a swap file in /root. There is a workaround way to use the swapfile to hibernate but it is not recommended for new users (See below if you want to know). So you don't need to have a separate /swap partition.


/ (root: All the software you install are stored here)
Size: min. 10 GB (25+GB recommended. I have 40GB)
Type for the new partition: Primary
Location for the new partition: Beginning of this space
Use as: ext4
Mount point: Choose "/"
/home (Only needed if you want to keep your personal files separate from / Root partition)
Size: Remainder of space on the drive or any size you want.
Type for the new partition: Primary
Location for the new partition: Beginning of this space
Use as: ext4
Mount point: Choose "/home"
/swap (Only needed if you want to Hibernate)
Size: Depends on your RAM.
Type for the new partition: Primary
Location for the new partition: Beginning of this space
Use as: swap
[Source](https://askubuntu.com/questions/1234838/is-it-necessary-to-have-a-home-and-swap-partitions-in-20-04)

### 第二題
默認使用MBR分區方式的情況下，在第二塊SATA磁盤中，劃分六個有用的分區（具有文件系統），此外，已知有兩個主分區，請問六個分區的文件名？。
解：（1）P+P+E
（2）/dev/sdb1 /dev/sdb2 /dev/sdb5 /dev/sdb6 /dev/sdb7 /dev/sdb8

### 第三題
什麼是GMT時間？它與北京時間差幾個小時？。
解：GMT為格林尼治時間，與北京時間差8小時。

### 第四題
軟體磁盤陣列的設備文件名是什麼？
解：/dev/md[0-15]

### 第五題
如果我的磁盤分區是使用MBR分區方式，且設置了4個主分區，但是磁盤還有空間，請問我還能不能使用這些空間？
解：不能。由於主分區與擴展分區最多只能有四個，其中擴展分區最多只能有一個，如果想要劃分出四個分區且還要有預留剩餘空間，四個主分區是不適合的，因為，即使硬盤還有剩餘容量，無法再繼續劃分。
[Source](https://blog.csdn.net/qq_41151659/article/details/94491657