## 这个库是 1c7.me 这个博客的代码.
Jekyll 有写博客和生成静态网站的用途，之前我都是一个库然后用2个分支来管理(code 和 master)
master 就是生成出来的结果，就是 1c7.me 访问的那些东西
code 就是 Jekyll 的博客了。
嫌烦，老是 code master 来回切换。
干脆就把 code 分支放到这里来。
jekyll build 之后的代码扔到另一个库就好了。

### 预览
```
jekyll serve
```
* localhost:4000 访问
* 写 _posts 
* 确认没问题了就 jekyll build 
* 然后生成出来的 _site 复制到另一个库。
* 在另一个库 git push 就完事了，博客就好了。

