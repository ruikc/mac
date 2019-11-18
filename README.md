# mac下常用的开发环境


## 一、必须要安装的基础环境

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

   

#### [Homebrew](https://brew.sh/)

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```
brew up #更新成最新的版本
```

#### 

##  二、PHP开发

#### 安装php环境

1. 安装php7.1版本

   ```
   brew install php@7.1 #安装php7.1版本
   ```

2. 默认文件所在路径

   ```
   /usr/local/etc/php/7.1
   ```

3. 安装xdebug调试扩展

   ```
   mv /usr/local/etc/php/7.1/pecl /usr/local/etc/php/7.1/pecl_old #不知道为什么，原pecl不是目录
   mkdir /usr/local/etc/php/7.1/pecl #先创建目录
   pecl install xdebug #安装扩展
   ```

   xdebug相关配置：

   ```ini
   [xdebug]
   zend_extension="/usr/local/etc/php/7.1/pecl/20160303/xdebug.so"
   xdebug.remote_enable=On
   xdebug.remote_handler="dbgp"
   xdebug.remote_port=9100
   xdebug.remote_host="localhost"
   xdebug.idekey=PHPSTORM
   xdebug.var_display_max_children=512
   xdebug.var_display_max_data=1024
   xdebug.var_display_max_depth=30
   ```

4. 其他扩展可以使用直接使用pecl进行安装

   ```
   比如pecl install mongodb 等
   ```



#### 安装Apache服务器

1. 安装apache服务

   ```
   brew install httpd
   ```

2. 默认配置文件所在路径

   ```
   /usr/local/etc/httpd
   ```

3. 添加域名配置目录

   ```
   mkdir /usr/local/etc/httpd/vhost
   ```

4. 修改配置文件 /usr/local/etc/httpd/httpd.conf，在510左右添加以下代码

   ```
   Include /usr/local/etc/httpd/vhost/*.conf
   ```

5. 在vhost目录中创建对应域名的conf文件，例如创建dev.abc.com.conf，模板如下：

   ```ini
   <VirtualHost *:80>
       DocumentRoot "/Users/zhiyuan/Project/web/dev.abc.com"
       ServerName dev.abc.com
       #ServerAlias 172.16.14.27
       ErrorLog "/usr/local/var/log/httpd/dev.abc.com-error_log"
       #CustomLog "/usr/local/var/log/httpd/dummy-host.example.com-access_log" common
   </VirtualHost>
   ```

   



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

   ```
   #全局配置
   composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
   或
   #项目配置
   composer config repo.packagist composer https://mirrors.aliyun.com/composer/
   ```

#### Yii2 常用扩展整理

1. Httpclient  - 发起远程get,post等请求
   Github：[https://github.com/yiisoft/yii2-httpclient](https://github.com/yiisoft/yii2-httpclient)
   安装：
   ```
   composer require --prefer-dist yiisoft/yii2-httpclient
   ```
   例子：
   ```
use yii\httpclient\Client;
   
   $client = new Client(['baseUrl' => 'http://example.com/api/1.0']);
   $response = $client->createRequest()
       ->setFormat(Client::FORMAT_JSON)
       ->setUrl('articles/search')
       ->addHeaders(['content-type' => 'application/json'])
       ->setData([
           'query_string' => 'Yii',
           'filter' => [
               'date' => ['>' => '2015-08-01']
           ],
       ])
       ->send();
   
   $responseData = $response->getData(); // get all articles
   count($response->data) // count articles
   $article = $response->data[0] // get fir
   ```
   
2. Umeditor  -  百度Umeditor在线Html编辑器
   Github：[https://github.com/shi-yang/yii2-umeditor](https://github.com/shi-yang/yii2-umeditor)
   安装：
   ```
composer require --prefer-dist shiyang/yii2-umeditor "*"
   ```
   例子：
   ```
<?= $form->field($model, 'content')->widget('shiyang\umeditor\UMeditor', [
     'clientOptions' => [
       'imageUrl' => \yii\helpers\Url::to(['/upload/umeditor']), //上传图片的链接
       'initialFrameHeight' => 500,
       'toolbar' => [
         'source | ',
         'justifyleft justifycenter justifyright justifyjustify |',
         'map link unlink anchor image |',
       ],
     ]
   ]) ?>
   ```
   
3. DateTimePicker - bootstrap 时间控件
   Github：[https://github.com/2amigos/yii2-date-time-picker-widget](https://github.com/2amigos/yii2-date-time-picker-widget)
   安装：
   ```
composer require 2amigos/yii2-date-time-picker-widget:~1.0
   ```
   例子：
   ```
<?= $form->field($model, 'birthday')->widget('dosamigos\datetimepicker\DateTimePicker', [
     'options' => ['placeholder' => '', 'readonly' => 'readonly'],
     'clientOptions' => [
       'autoclose' => true,
       'todayHighlight' => true,
       'startView' => 'month',
       'format' => 'yyyy-mm-dd',
       'pickerPosition' => "bottom-left",
       'todayBtn' => 'linked',
       'minView' => 'month',  //最小选择范围（月）
     ]
   ])->label('Date of birth'); ?>
   ```
   
4. PHPExcel - Excel的导入与导出
   Github：https://github.com/moonlandsoft/yii2-phpexcel
   安装：
   ```
composer require --prefer-dist moonlandsoft/yii2-phpexcel "*"
   ```
   例子：
   ```
$fileName = '出纳日记账_' . date('YmdHis') . '.xlsx';
   $fileName = iconv("utf-8", "gb2312//IGNORE", $fileName);
   Excel::widget([
     'models' => $dataProvider->models,
     'mode' => 'export', //default value as 'export'
     'asAttachment' => true,
     'showFooter' => true,
     'columnsWrap' => ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I'],
     'columnsWidth' => [
       'A' => 20,
       'B' => 30,
       'C' => 20,
       'D' => 20,
       'E' => 16,
       'F' => 16,
       'G' => 16,
       'H' => 16,
       'I' => 16,
     ],
     'fileName' => $fileName,
     'columns' => [
       ['header' => '收支', 'value' => function ($model) {
         return $model->type == 3 ? '支出' : '收入';
       }],
       'demo',
       ['header' => '交款人类型', 'value' => function ($model) {
         return $model->type == 3 ? '' : ($model->type == 2 ? '团体' : '个人');
       }],
       ['header' => '交款人身份证号', 'value' => function ($model) {
         return !$model->identity ? '' : "'" . $model->identity;
       }],
       ['attribute' => 'username', 'footer' => '合计：'],
       ['attribute' => 'total', 'footer' => $total],
       ['header' => '收据编号', 'value' => function ($model) {
         return !$model->receipt ? '' : "'" . $model->receipt;
       }],
       'created_at:date',
       'order_user',
       'print_num'
     ],
   ]);
   ```
   
5. QiniuPHPSdk - 七牛云php-sdk
   Github：https://github.com/qiniu/php-sdk
   安装：
   ```
composer require qiniu/php-sdk
   ```
   例子：
   ```
use Qiniu\Storage\UploadManager;
   use Qiniu\Auth;
   ...
       $upManager = new UploadManager();
       $auth = new Auth($accessKey, $secretKey);
       $token = $auth->uploadToken($bucketName);
       list($ret, $error) = $upManager->put($token, 'formput', 'hello world');
   ...
   ```
   
6. Adminlte - adminlte后台管理界面
   Github：https://github.com/dmstr/yii2-adminlte-asset
   安装：
   ```
composer require dmstr/yii2-adminlte-asset "^2.1"
   ```
   例子：
   ```
参照github文档进行就可以
   ```
   
7. Qrcode - 二维码生成
   Github：[https://github.com/2amigos/qrcode-library](https://github.com/2amigos/qrcode-library)
   文档：[https://qrcode-library.readthedocs.io/en/latest/](https://qrcode-library.readthedocs.io/en/latest/)

   安装：
   ```
   composer require 2amigos/qrcode-library:~1.1
   ```
   例子：
   ```
   <?php 
   
   use Da\QrCode\QrCode;
   
   $qrCode = (new QrCode('This is my text'))
       ->setSize(250)
       ->setMargin(5)
       ->useForegroundColor(51, 153, 255);
   
   // now we can display the qrcode in many ways
   // saving the result to a file:
   
   $qrCode->writeFile(__DIR__ . '/code.png'); // writer defaults to PNG when none is specified
   
   // display directly to the browser 
   header('Content-Type: '.$qrCode->getContentType());
   echo $qrCode->writeString();
   
   ?> 
   
   <?php 
   // or even as data:uri url
   echo '<img src="' . $qrCode->writeDataUri() . '">';
   ?>
   ```





#### laravel 常用扩展

1. Laravel-debugbar - 调试工具栏
   Github： [https://github.com/barryvdh/laravel-debugbar](https://github.com/barryvdh/laravel-debugbar)
   安装：
   ```
   composer require barryvdh/laravel-debugbar --dev
   ```

2. Laravel-ide-helper - 代码提示工具
   Github： [https://github.com/barryvdh/laravel-ide-helper](https://github.com/barryvdh/laravel-ide-helper)
   安装：
   ```
   composer require --dev barryvdh/laravel-ide-helper
   ```

3. Laravel-permission - 用户权限管理crud
   Github： [https://github.com/spatie/laravel-permission](https://github.com/spatie/laravel-permission)
   文档：[https://docs.spatie.be/laravel-permission/v3/introduction/](https://docs.spatie.be/laravel-permission/v3/introduction/)
   安装：
   ```
   composer require spatie/laravel-permission
   ```

4. Jwt-auth - jwt用户授权
   Github：[https://github.com/tymondesigns/jwt-auth](https://github.com/tymondesigns/jwt-auth)
   文档：[https://jwt-auth.readthedocs.io/en/develop/](https://jwt-auth.readthedocs.io/en/develop/)
   安装：
   ```
   composer require tymon/jwt-auth
   ```

5. Laravel-medialibrary - 媒体管理库
   Github：[https://github.com/spatie/laravel-medialibrary](https://github.com/spatie/laravel-medialibrary)
   文档：[https://docs.spatie.be/laravel-medialibrary/v7/introduction/](https://docs.spatie.be/laravel-medialibrary/v7/introduction/)
   安装：
   ```
   composer require "spatie/laravel-medialibrary:^7.0.0"
   ```

6. Laravel-cors - 跨域库
   Github：[https://github.com/spatie/laravel-cors](https://github.com/spatie/laravel-cors)

7. Laravel-wechat - 微信公众号等
   Github：[https://github.com/overtrue/laravel-wechat](https://github.com/overtrue/laravel-wechat)

8. Laravel-pinyin - 中文转换成拼音
   Github：[https://github.com/overtrue/laravel-pinyin](https://github.com/overtrue/laravel-pinyin)

9. Laravel-lang - 多语言包
   Github：[https://github.com/overtrue/laravel-lang](https://github.com/overtrue/laravel-lang)

10. Laravel-snappy - 网页保存成pdf或图片
    Github：[https://github.com/barryvdh/laravel-snappy](https://github.com/barryvdh/laravel-snappy)

11. Laravel-push-notification - 消息推动，包括ios
    Github：[https://github.com/davibennun/laravel-push-notification](https://github.com/davibennun/laravel-push-notification)

12. Image - 图片操作库
    Github：[https://github.com/Intervention/image](https://github.com/Intervention/image)

13. Laravel-excel - Excel文件操作库
    Github：[https://github.com/Maatwebsite/Laravel-Excel](https://github.com/Maatwebsite/Laravel-Excel)

14. Laravel-flash  - 轻量级消息提示
    Github：[https://github.com/spatie/laravel-flash](https://github.com/spatie/laravel-flash)
    
15. Laravel-LaravelCollective - 表单组件
    Github：[https://github.com/LaravelCollective/html](https://github.com/LaravelCollective/html)
    
16. Laravel-mediable - 另一个图片及多媒体管理库
    Github：[https://github.com/plank/laravel-mediable](https://github.com/plank/laravel-mediable)





## 三、 前端开发

### 前端免费的CDN加速

1. BootCDN [https://www.bootcdn.cn/](https://www.bootcdn.cn/)
2. Staticfile CDN [https://www.staticfile.org/](https://www.staticfile.org/)

### 前端插件库

##### 视频插件

1. clappr.js 

   [http://clappr.io/](http://clappr.io/) ，[https://www.toutiao.com/a6713415883122803214](https://www.toutiao.com/a6713415883122803214)

   > - 360角度视频
   > - 缩略图模式
   > - 视频进度条标记
   > - 清晰度调整



### 常用知识

#### 正则表达式

```
/^(([1-9]{1}\d*)|([0]{1}))(\.(\d){0,2})?$/ - 小数保留两位小数
```

