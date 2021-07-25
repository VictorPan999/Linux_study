# Oh My Zsh setting
###### tags: `Shell` `CommandLine`
## Step

### Install zsh
`sudo dnf install zsh`
check version

### Set zsh as default shell
如果是運行在bash上可以透過vim
`sudo vim ~/.bashrc`
在最下方加上
exec zsh
讓其運行zsh(不建議)

選擇zsh為shell
`sudo usermod -s /bin/zsh username`
Ex:`sudo usermod -s /bin/zsh int99`
或者
`chsh -s /bin/zsh`
設定完成後似乎要重新開機

(切換回去)
`chsh -s /bin/bash`
### Install oh my zsh
`sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`
check update
`upgrade_oh_my_zsh`

### Download font
Download these four ttf files:
(link) [Manual font installation](https://github.com/romkatv/powerlevel10k#manual-font-installation)
MesloLGS NF Regular.ttf
MesloLGS NF Bold.ttf
MesloLGS NF Italic.ttf
MesloLGS NF Bold Italic.ttf

安裝字體的方式,
將你的字體 copy 到 /usr/share/fonts/truetype/ 裡面,
然後執行 sudo fc-cache -f -v (更新字體快取).
透過圖形界面搬移可能會遇到無法貼上的問題，
可以透過`sudo nautilus`來打開權限做搬移
搬移完後去Terminal or Tilix的設定改字形

### Install Powerlevel10k
下載
`git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k`
設定
`cd .oh-my-zsh`後打開新的Terminal用vim打開.zshrc的檔案
`vim .zshrc`打開後將其中的ZSH_THEME用下方內容取代
ZSH_THEME="powerlevel10k/powerlevel10k"


## Source:
Power Level 10K
[沈弘哲 zsh-powerlevel10k 教學 - 漂亮的 terminal](https://www.youtube.com/watch?v=5f8w7gYnnfU&t=44s)
[twtrubiks zsh 搭配 powerlevel10k](https://github.com/twtrubiks/linux-note/tree/master/zsh-powerlevel10k-tutorual)

PowerLevel9k
[baby WOGUE [GNOME 3.28] PowerLevel9k -  The Most Cool Linux Shell EVER!](https://www.youtube.com/watch?v=wM1uNqj71Ko&list=PLMtGfbNkiYy8QuPajgZKUUmNZXMO-EOsi&index=5&t=111s)
[alex285 Get PowerLevel9k — The Most Cool Linux Shell EVER!](https://medium.com/@alex285/get-powerlevel9k-the-most-cool-linux-shell-ever-1c38516b0caa)

Oh-My-ZSH!
[OH My Zsh](https://github.com/ohmyzsh/ohmyzsh)



