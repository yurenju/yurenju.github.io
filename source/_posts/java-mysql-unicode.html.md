title: java + mysql + unicode
date: 2005-04-06 01:18:00
tags: 
- development
---

當在 UTF-8 的環境下，java 對 mysql 存取總會是問號 ??。解決的方法也很簡單，只要在 DriverManager.getConnection 時加上參數 useUnicode=true 以及 characterEncoding=utf8 即可。

> DriverManager.getConnection("jdbc:mysql://localhost/test_db?
> useUnicode=true&characterEncoding=utf8", username, password);