![Index](http://www.syinchung.com/asset/yof.png "Title")

<H3>特点</H3>

> 1: 基于YAF 和 Orange 开发的一个PHP 框架, 简单, 易用, 高效

> 2: 底层使用的鸟哥的 YAF, MySQL 封装使用的是 Orange 的PDO 类, 支持链式操作! 调用非常方便

> 3: 支持多种运行环境, 根据运行环境决定域名常量,MySQL参数, 错误报告等

> 4: 支持默认模型 [可以不创建模型文件也能对表进行CURD] 

> 5: DEMO 中包括用户的简单登录,注册,注销.文章的发布,管理,分页.个人资料修改

> 6: 后台管理登录,注销,修改密码, 文章&用户管理, 权限分配 

> 7: DEV 下MySQL 和PHP 错误全部都打印出来, 方便调试, TEST , WWW 下将不打印, 分别记录在对应的文件里 

> 8: 简易省市区三级联动

> 9: 三个模块:User, Api, Admin 

> 10: 一些常用的函数封装,位于 function 目录

<H3>安装 [建议在Linux下使用]</H3>

> 1: 安装YAF 扩展

> 2: 配置好 conf/DB_config.php 里的MySQL参数并将 dym.sql 导入自己的数据库

> 3: 配置虚拟主机, 写对应的HOSTS

> 4: 解压文件至指定目录,运行

> 5: WEB 服务器开启 URL Rewrite 功能, Apache 下有 .htaccess, Nginx 下按如下需配置
###
    location / {
        if (!-e $request_filename) {
            rewrite ^/(.*)$ /index.php?$1 last;
        }
    }
###

<H3>设置</H3>
> 1: MySQL 参数 conf/DB_config.php: 默认支持读写分离, 若不分离, 设置为一样的值即可

> 2: 环境设置: environment.php

>> A: 开发环境请设置为 DEV, 此时所有错误将打印出来

>> B: 线上测试环境设置为 TEST, 此时 PHP 的错误将记录在 APP_PATH 下的 $当天日期_php.log, SQL 的错误将记录在 APP_PATH 下的 $当天日期_sql.log

>> C: 正式生产环境设置为 WWW, 此时 PHP 的错误将记录在 APP_PATH 下的 $当天日期_php.log, SQL 的错误将记录在 APP_PATH 下的 $当天日期_sql.log

>> D: 维护情况下设置为 MAINTAINCE, 此时访问网站将只显示一句话: 服务器正在维护, 请稍候访问. 当时可以自定义得更好些

>> <b>注:正式生产环境千万不能设置为 DEV, 切记!!!</b>

> 3: 配置网站域名, 图片域名, 静态文件域名等, 避免硬编码

>> 请打开 init.php, 根据 DEV, TEST, WWW 自行对 $SERVER_DOMAIN, $STATIC_DOMAIN, $IMG_DOMAIN 根据情况设置


<H3>目录结构</H3>

> applicatoin => 程序主目录

>> componment => 封装好的组件, 现包括 验证码, 省市区三级联动, HTML, 微信, 可自行加入

>> controllers => 不使用modules 情况下的控制器目录

>> function => 封装好的函数目录, 包括 F_Array.php , F_Basic.php, F_String.php, F_Network.php, F_File.php,等

>> library => 封装好的类库, 包括助手类 Helper.class.php, 短信示例类 L_SMS.class.php, PDO 类 M_Model.pdo.php

>> model => 模型文件, 默认一个模型对应一个表

>> modules => YAF 默认的模块文件, 示例有三个:User, Api, Admin

>> plugins => YAF 默认的插件位置, 示例有 Router.php, Admin.php

>> views => 视力文件默认目录

> conf => 配置文件目录, application.ini, DB_config.php

> public => 公用文件, JS, CSS 等一般位于此

<H3>内置常量</H3>
> APP_PATH => 根目录

> ENVIRONMENT => 运行环境

> TB_PREFIX => 表前缀

> APP_NAME => APP 名称

> CONFIG_PATH => 配置文件的目录, 即 APP_PATH.'/conf'

> LIB_PATH => 类目录, 即 APP_PATH.'/application/library'

> MODEL_PATH => 模型目录, 即 APP_PATH.'/application/model'

> FUNC_PATH => 函数目录, 即 APP_PATH.'/application/function'

> ADMIN_PATH => Admin 模块目录, APP_PATH.'/application/modules/Admin'

> CSS_PATH => CSS 路径, 即 /css 

> JS_PATH => JS 路径, 即 /js

> IMG_PATH => IMG 路径, 即 /img

> ADMIN_CSS_PATH => 管理后台 CSS 路径, '/admin/css'

> ADMIN_JS_PATH => 管理后台 JS 路径, '/admin/js'

> CUR_DATE => 当前日期, 格式 Y-m-d

> CUR_TIMESTAMP => 当前时间戳

> SERVER_DOMAIN => 网站域名

> STATIC_DOMAIN => 静态文件域名

> IMG_DOMAIN => 图片域名

> SITE_PROVINCE => 三级联动中默认显示的省份, 440000 是广东

> SITE_CITY => 三级联动中默认显示的城市, 440100 是广州

> SITE_REGION => 三级联动中默认显示的省份, 440106 是珠江新城

<H3>使用</H3>

> 一: 控制器
    
>> A:不是模块下的情况: 在 APP_PATH.'/controllers' 目录下按 YAF 规则创建控制器, 如示例中的 Article.php

>> B: 模块下的情况: 在 APP_PATH.'/modules/模块/controllers' 目录下按 YAF 规则创建控制器, 如示例中的 User/controllers/User.php

>> C: 基本控制器: APP_PATH.'/controllers/Basic.php', 对 request, session 中的方法进行了简易封装, 令业务控制器可以少写不少的代码!

> 二: 模型
    
>> A: 常规模型: 在 APP_PATH.'/model' 目录下按 M_$模型名称.php 规则创建, 指定对应的表, 如示例中的 M_Admin, M_Role.php等

>> B: 不创建模型, 使用默认模型, 这种情况下不需要创建模型文件. 如示例中并没有 M_Articles.php,也可以操作 article 表, 按默认模型的方式调用即可

>> <H5>模型的调用: 控制器中调用基础控制器 C_Basic.php 的 load($模型名)  </H5>

>> A: 常规模型: $this->m_role = $this->load('Role');

>> B: 默认模型: $this->m_article = $this->load('Article');, 示例中并没有 M_Articles.php 也可以加载, 但参数 Article 必须与表名对应, 即对应的表名必须是 TB_PREFIX.'article'

>> <H5>执行 CURD</H5>

>> 1:先借助 Field($field), Where($where), Order($order), Limit($limt)拼接好 SQL 语句, 不调用这几个方法代表不设置对应的条件

>> 2: 调用 Select, SelectOne, Update, Delete, Insert

>> 3: 便捷方法: SelectByID($field, $id), UpdateByID($m, $id), DeleteByID($id), SelectFieldByID($field, $id), 

>> <H5>Select:如示例 Index控制器Select 出登录用户的 10 个文章:</H5>
###
    $buffer['articles'] = $m_article->Where($where)->Order($order)->Limit($limit)->Select();
###

>> <H5>登录的Select</H5>
###
    $field = array('id');
    $where = array('username' => $username, 'password' => $password);
    $data = $this->m_user->Field($field)->Where($where)->SelectOne(); 
###
>> <H5>Update:示例中的修改个人资料使用了 UpdateByID</H5>
###
    $code = $this->m_user->UpdateByID($m, USER_ID); // $code 是所影响的行数
###
>> <H5>Insert: 示例中的添加文章</H5>
###
    $articleID = $this->m_article->Insert($m); // $m 是一个数组, key 是表中的字段名, $articleID 是返回的自增长ID
###
>> <H5>Delete: 示例中的删除文章使用了 DeleteByID</H5>
###
    $code = $this->m_article->DeleteByID($articleID); // $code 是所影响的行数
###
>> <H5>通用的方法, 联表查询或复杂的SQL 语句</H5>

>> 由于鄙人觉得复杂的 SQL 用函数来拼接有以下问题 1: 新手难以掌握, 2: 学习成本高  3: 效率低和难以维护, 故复杂的SQL, 如联表查询等用如下方式实现

>>> 1: 在模型里新建一个方法, 接收参数, 写原生的SQL, 并调用 Query($sql) , 如 M_Admin.php 的
###
    // 查询文章列表 [建议将此方法写在 M_Article 里]
    public function getUserArticles($userID){
        $sql = 'SELECT u.username, a.* FROM '.TB_PREFIX.'user AS u '
        . ' LEFT JOIN '.TB_PREFIX.'article AS a ON a.userID = u.id '
        . ' WHERE a.userID = "'.$userID.'" ORDER BY a.addTime DESC LIMIT 10';
        return $this->Query($sql);
    }
###
>>> 控制器里调用: $data = $this->load('Admin')->getUserArticles($userID)

>>> 2:通用的方法,如经常会调用到的 SQL 语句, 请在模型里封装, 如 M_City.php 里的 getCityNameById()

> 三: 视图
    
>> A: 在 YAF 指定的视图目录里创建与 Action 一样的文件名.php|.html

>> B: 控制器调用 $this->getView()->assign($buffer);

>> C: 视图文件里用模板引擎或原生PHP 展示数据就可以了

> 四: function 目录里文件的引用

>> 如要导入 F_File.php 里的函数, 使用 Helper::import('File') 即可

> 五: 组件 Componment 的使用

>> A; 加载 => 控制器中使用 Helper::loadComponment($组件名), 如示例中修改个人资料的省市区三级联动
###
    $buffer['cityElement'] = Helper::loadComponment('City')->generateCityElement($provinceID, $cityID, $regionID, 1);
###

<H3>模块的调用 </H3>

> 1: 先在 APP_PATH.'/conf/application.ini' 中添加模拟, DEMO 中有 Index,User,Admin,Api 四个模块. 注 Index模块 必不可少

> 2: 在 APP_PATH.'/application/modules' 中创建模块目录, 比如说DEMO 中的 Api 

> 3: 建立 controllers, views 目录

> 4: 按 http://你的域名/模块名/控制器/方法 的规则调用, 如调用 Api 模块 Article 中的index 
###
    http://dev.yaf.com/api/article/index
###

<H3>管理后台 Admin </H3>

> DEMO 中处理方式是增加一个Module, 名为 Admin, 按照基本的 MVC 模式去写就好了

<H3>API </H3>

> DEMO 中处理方式是增加一个Module, 名为 Api, 按照基本的 MVC 模式去写就好了, 当然了别忘了给接口作安全验证

> Q:如果又有网站,又有 APP,还要出手机端网站,如果只调用一次数据就能满足?

> A: 借助 Componment, 让其调用模型,出统一的数据. API,网站,手机网站的控制器调用 Componment 中的方法即可

> B: 如 APP_PATH.'/application/modules/User/controllers/User.php' 中的 ProfileAction 调用省市区三级联动
###
    $buffer['cityElement'] = Helper::loadComponment('City')->generateCityElement($provinceID, $cityID, $regionID, 1);
###

<H3>事务支持</H3>

> 1: 先加载一个模型,比如 $m_article = $this->load('Article');

> 2: 启动事务: $m_article->beginTransaction();

> 3: 执行业务 SQL ....

> 4: 调用 Commit: $m_article->Commit(); 或 Rollback : $m_article->Rollback();

<H3>关于M_Model.pdo.php</H3>

> 1:该文件是 MySQL 的PDO 封装类

> 2:读者可能有这么一个疑问, 复杂的 WHERE 该如何调用呢? 我的回答是: 自行写原生的 WHERE. 如查询 username 为 abc, password 为 cba 的 WHERE 可以用
###
    $where = array('username' => 'abc', 'password' => 'cba');
###
> 但如果是 username 为 abc 或 cba, ID < 100 的 WHERE 呢? 用字符串模式
###
    $where = ' `username` = "abc" OR `username` = "cba" '
    $where = ' `id` < "100"'
###

> 3: 特殊的 Update 语句, 比如 id 为 1 的文章的阅读数要加 1, 按如下方式调用
###
    $m = array('views' => 'views+1');
    $where = array('id' => 1);
    $this->m_article->Where($where)->Limit(1)->Update($m, TRUE); // Update 加第二个参数: TRUE
###

<H3>扩展</H3>

> 可自行扩展组件 Componment

> 根据 YAF 规则扩展插件

> 自行编写类库

其他: 若发现有BUG 或更好的建议,请联系大眼猫 QQ: 381345509, 谢谢
