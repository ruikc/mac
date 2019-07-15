# mac下常用的开发环境


## 一、必须要安装的基础环境

#### [Homebrew](https://brew.sh/)

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```shell
brew up #更新成最新的版本
```

#### [Oh-my-zsh](https://ohmyz.sh/)

```shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

#### [Auto_suggestions](https://github.com/zsh-users/zsh-autosuggestions)

1. Clone this repository into `$ZSH_CUSTOM/plugins` (by default `~/.oh-my-zsh/custom/plugins`)

   ```shell
   git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
   ```

2. Add the plugin to the list of plugins for Oh My Zsh to load (inside `~/.zshrc`):

   ```
   plugins=(zsh-autosuggestions)
   ```

3. Start a new terminal session.



##  二、PHP基础环境的安装



### 三、前端免费的CDN加速

1. BootCDN [https://www.bootcdn.cn/](https://www.bootcdn.cn/)
2. Staticfile CDN [https://www.staticfile.org/](https://www.staticfile.org/)



###  四、前端插件库

#### 视频插件

1. clappr.js 

   [http://clappr.io/](http://clappr.io/) 

   [https://www.toutiao.com/a6713415883122803214](https://www.toutiao.com/a6713415883122803214)

   > - 360角度视频
   > - 缩略图模式
   > - 视频进度条标记
   > - 清晰度调整