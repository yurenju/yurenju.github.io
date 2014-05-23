title: \[Ubuntu\] 安裝 OpenCA
date: 2007-04-12 13:47:00
tags: 
- server
- linux
- openca
- ubuntu
---

這文件是我修 Network Security 的作業，因為之前發生很鳥蛋的[抄襲事件](http://yurenju.blogspot.com/2006/05/blog-post.html "抄襲事件") ，所以這次先寫在前面，一樣也是修王老師 network security 別抓下來就直接當作業交出去啦 XD

###    OpenCA 

   <font face="方正明體"><span lang="zh-TW">由於參考資料的</span></font>OpenCA   <font face="方正明體"><span lang="zh-TW">版本</span></font>0.9.2.1<font face="方正明體"><span lang="zh-TW">與現在版本</span></font>0.9.3-rc1<font face="方正明體"><span lang="zh-TW">已有差距功能以及組態設定都與之前版本不同，如組態設定時已取消   </span></font>--with-hierarchy-level   <font face="方正明體"><span lang="zh-TW">參數、</span></font>--with-engine<font face="方正明體"><span lang="zh-TW">參數，並且因</span></font>OpenCA<font face="方正明體"><span lang="zh-TW">必須配合許多週邊軟體，而參考資料中的週邊軟體與環境均與目前不同。故參照</span></font>OpenCA<font face="方正明體"><span lang="zh-TW">原始檔中的</span></font>INSTALL<font face="方正明體"><span lang="zh-TW">檔案進行安裝。</span></font> 

####    Environment 

*   Ubuntu 6.10*   OpenCA 0.9.3-rc1 

####    Prerequisites 

   <font face="方正明體"><span lang="zh-TW">閱讀 </span></font>openca   <font face="方正明體"><span lang="zh-TW">中的   </span></font>INSTALL<font face="方正明體"><span lang="zh-TW">，裡面提到</span></font> 

   Prerequisites 

   =============
   Prerequisites for building the OpenCA software are: 

   o GNU tar (a tar that understands the z option for gzip)
   o GNU make (at minimum for FreeBSD because there are several problems reported   with the OS's own make) 

   Prerequisites for running the OpenCA software are: 

   o OpenSSL ( 0.9.7+ ) (on both CA and external server);
   o Perl (5.6.1+ with DBI support) (on both CA and external server);
   o Apache Web Server (on both CA and external server);
   o mod_ssl (for Apache) (on external server only);
   o OpenLDAP (v2 is recommended) (on external server) 

   <font face="方正明體"><span lang="zh-TW">先確定系統裡面是否安裝了這些軟體。比較要注意到的是因為要編譯軟體，所以安裝時別忘了把名稱尾端為   </span></font>-dev <font face="方正明體"><span lang="zh-TW">的套件安裝。最常會遺漏掉的通常是   </span></font>openssl <font face="方正明體"><span lang="zh-TW">的   </span></font>header <font face="方正明體"><span lang="zh-TW">檔   </span></font>libssl-dev<font face="方正明體"><span lang="zh-TW">；</span></font>Ubuntu   <font face="方正明體"><span lang="zh-TW">的 </span></font>Apache2   <font face="方正明體"><span lang="zh-TW">已經將 </span></font>SSL   <font face="方正明體"><span lang="zh-TW">編入，不需要另外掛載模組。我安裝了以下軟體：</span></font> 

*   tar*   make*   openssl*   libssl-dev*   perl*   libdbi-perl*   apache2*   ldap-utils*   libldap2*   libldap2-dev 

   <font face="方正明體"><span lang="zh-TW">可以使用 </span></font>apt-get   <font face="方正明體"><span lang="zh-TW">安裝以上軟體： </span></font> 
 > `<font color="#ff0000"># apt-get install tar make openssl libssl-dev perl libdbi-perl apache2 ldap-utils libldap2 libldap2-dev</font>` 

####    Apache2 mod_ssl configuration 

   Ubuntu<font face="方正明體"><span lang="zh-TW">最初的</span></font>mod_ssl<font face="方正明體"><span lang="zh-TW">設定檔並無將</span></font>SSL<font face="方正明體"><span lang="zh-TW">啟動，必須先複製</span></font>/usr/share/doc/apache2/example/ssl.conf.gz<font face="方正明體"><span lang="zh-TW">檔案至</span></font>/etc/apache2/mods-available   <font face="方正明體"><span lang="zh-TW">中</span></font> 
 > `cp /usr/share/doc/apache2/example/ssl.conf.gz /etc/apache2/mods-available` 
> 
>    `gzip -d ssl.conf.gz` 

   <font face="方正明體"><span lang="zh-TW">接著新增</span></font>https<font face="方正明體"><span lang="zh-TW">的</span></font>VirtualHost<font face="方正明體"><span lang="zh-TW">站台</span></font> 
 > `cd /etc/apache2/sites-available/` 
> 
>    `cp default ssl` 
> 
>    `cd ../sites-enabled/` 
> 
>    `ln -s /etc/apache2/sites-avaiable/ssl 001-ssl` 

   <font face="方正明體"><span lang="zh-TW">編輯</span></font>001-ssl<font face="方正明體"><span lang="zh-TW">，將以下兩處更改：</span></font> 
 > `NameVirtualHost *:443` 
> 
>    `&lt;VirtualHost *:443&gt;` 

   <font face="方正明體"><span lang="zh-TW">最後產生</span></font>Apache<font face="方正明體"><span lang="zh-TW">的憑證：</span></font> 
 > `apache2-ssl-certificate` 

   <font face="方正明體"><span lang="zh-TW">回答完所有問題即可建立憑證。</span></font> 

####    OpenCA Tools installation 

   <font face="方正明體"><span lang="zh-TW">安裝   </span></font>[OpenCA   Tools](http://www.openca.org/alby/download?target=openca-tools-1.0.0.tar.gz)<font face="方正明體"><span lang="zh-TW">，解壓縮：</span></font>

 > `tar zxvf openca-tools-1.0.0.tar.gz` 

   <font face="方正明體"><span lang="zh-TW">組態設定，我將 </span></font>OpenCA Tools   <font face="方正明體"><span lang="zh-TW">安裝在 </span></font>/usr/local/,   <font face="方正明體"><span lang="zh-TW">並且開啟 </span></font>OpenSSL   <font face="方正明體"><span lang="zh-TW">支援。 </span></font> 
 > `cd openca-tools-1.0.0`
>  `./configure --prefix=/usr/local/ --enable-engine` 

   <font face="方正明體"><span lang="zh-TW">編譯與安裝（標明 </span></font>#   <font face="方正明體"><span lang="zh-TW">的命令代表需要取得 </span></font>root   <font face="方正明體"><span lang="zh-TW">權限。） </span></font> 
 > `make`
>  `<font color="#ff0000"># make install</font>` 

   <font face="方正明體"><span lang="zh-TW">組態設定如下：</span></font> 
 > `./configure --prefix=/usr/local --with-openssl-prefix=/usr --with-web-host=140.130.175.184 --with-httpd-user=www-data --with-httpd-group=www-data --with-htdocs-fs-prefix=/var/www --with-cgi-fs-prefix=/usr/lib/cgi-bin --with-db-type=mysql --with-db-port=3306 --enable-dbi` 

   <font face="方正明體"><span lang="zh-TW">而進行安裝、設定後，發現安裝程序並無將所需之</span></font>script<font face="方正明體"><span lang="zh-TW">檔案複製入目的端，故手動進行複製：</span></font> 
 > `make` 
> 
>    `make install-offline` 
> 
>    `make install-online` 
> 
>    `cd src/scripts` 
> 
>    `cp * /usr/local/bin/` 
> 
>    `rm /usr/local/bin/*.in` 
> 
>    `chmod 755 /usr/local/bin/*` 

   <font face="方正明體"><span lang="zh-TW">接下來對</span></font>config.xml<font face="方正明體"><span lang="zh-TW">設定，並且執行</span></font>./configure_etc.sh<font face="方正明體"><span lang="zh-TW">，啟動   </span></font>OpenCA<font face="方正明體"><span lang="zh-TW">：</span></font> 

   openca_rc start 

   <font face="方正明體"><span lang="zh-TW">接著照著參考資料上的作，最後就可以</span></font>Approved   Request<font face="方正明體"><span lang="zh-TW">。</span></font> 

   ![](http://docs.google.com/File?id=ajd93zkqrjq5_29cd7zmn)

####    Reference 

   Need Apache2 SSL howto,   [http://ubuntuforums.org/archive/index.php/t-4466.html](http://ubuntuforums.org/archive/index.php/t-4466.html) 

   <font face="方正明體"><span lang="zh-TW">楊中皇</span></font>,   <font face="方正明體"><span lang="zh-TW">網路安全理論與實務</span></font>

 