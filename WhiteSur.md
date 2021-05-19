 # Manjaro WhiteSur配置

#### System Settings

##### Workspace Behavior

Desktop Effects

 ````apl
 Blur: Noise strength调0
 Wobbly Windows  勾选，Woblle when resizing取消勾选 Wobblines 调最大
 Magic Lamp 勾选 400ms
 Touch Screen： 右边No action
 ````



##### Windows Management

````apl
Window Behavior  => Advanced => Window placement: Centered
Task Switcher => Main => Visualization Breeze换成Large Icons
Kwin Scripts : Get New Scripts找Force Blur，下载完切换
````

 

##### Global Theme

````apl
Get New Global Themes => 搜索whitesur => 下载完切换
````



##### Application Style

````apl
Application Style => Download New .....=> GTK 3.x ThemeS => 搜bigsur =>下载完切换macxx的GTK2以及GTK3 theme

Window Decoration => TitleBar Buttons =>图标改 关闭 ， 最小化 ， 最大化



##### 打开software

搜索`kvantum Manager`,下载 ;再下载`latte-dock-git`

然后进入https://www.pling.com/p/1398841,下载File，解压

````apl
 1. Open Kvantum Theme Folder选中解压文件夹 ， install this theme
 2. Change/Delete Theme,选WhiteSur
 3. Configure Active Theme ：   Hacks => Reduce window opactiy by 5
 										 Reduce menu opactiy by 15
 4. Save，然后 Quit										
````





继续回到Application Style 

````apl
Apllication Style 选中 Kvantum
````



鼠标右键桌面 Add Widgets

````apl
下载Appliction title，latte Separator，latte Spacer，latte SideBar Button，Better inline clock，Launchpad Plasma，Mac OSX Inline Battery，Kpple Menu ，mediacontroller_plus =>0.2.4, Ditto Menu
````



进入https://www.pling.com/p/1399346,下载

````apl
mcOS-BigSur-Large.layout.latte.zip
Launchpad.zip
extrasicons.zip
````

 全部解压变成文件夹



````apl
打开latte，右键点击，Layouts => Manage Layouts => export
引入mcOS-BigSur-Large.layout.latte ，选中新加的，switch， Apply

右键上方的latte，
config Latte SideBar Buuton Settings => General,点击空白的icon=>other icons, Browse,进入extrasicons，sideBar.controlCentre.svg    ,Apply,OK

config Menu Settings => General,点击空白的icon=>other icons, Browse,进入extrasicons，dittoMenu-spotlight.svg    ,Apply,OK

打开终端，右键桌面上方的Settings，Edit profile =>Appearance ,Green on Black,Blur background,Background transparency 30% 	,Apply

````

 

另：

* 左下角任务栏搜`Wallpaper`可以切换自己想要的桌面壁纸

* `Login Screen `调登录壁纸
* `Screen Locking` 调锁屏壁纸

