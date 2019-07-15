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

#### Composer 国内源

1. 阿里云Composer(推荐)

   镜像地址：https://mirrors.aliyun.com/composer/

   官方地址：[https://developer.aliyun.com/composer](https://developer.aliyun.com/composer)

2. phpcomposer

   镜像地址：[https://packagist.phpcomposer.com](https://packagist.phpcomposer.com)

   官方地址： [https://pkg.phpcomposer.com/](https://pkg.phpcomposer.com/)

3. 安畅网络镜像

   镜像地址：[https://php.cnpkg.org](https://php.cnpkg.org)

   官方地址：[https://php.cnpkg.org](https://php.cnpkg.org)

4. 配置命令如下:

   ```shell
   #全局配置
   composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
   或
   #项目配置
   composer config repo.packagist composer https://mirrors.aliyun.com/composer/
   ```

#### Yii2 常用扩展整理





#### Laravel常用扩展整理





### 三、前端免费的CDN加速

1. BootCDN [https://www.bootcdn.cn/](https://www.bootcdn.cn/)
2. Staticfile CDN [https://www.staticfile.org/](https://www.staticfile.org/)



###  四、前端插件库

#### 视频插件

1. clappr.js 

   [http://clappr.io/](http://clappr.io/) ，[https://www.toutiao.com/a6713415883122803214](https://www.toutiao.com/a6713415883122803214)

   > - 360角度视频
   > - 缩略图模式
   > - 视频进度条标记
   > - 清晰度调整