
# Tutorial
## 网站搭建
#### 1.安装Jekyll
##### (1)安装依赖
```bash
sudo apt-get install ruby ruby-dev build-essential
gem install bundler
gem install jekyll-paginate
```
##### (2)修改.bashrc文件,添加下面的内容
```bash
# Install Ruby Gems to ~/gems
export GEM_HOME=$HOME/gems
export PATH=$HOME/gems/bin:$PATH
```
然后保存,在终端输入
```bash
source ~/.bashrc
```
使配置生效
##### (3)开始安装jekyll:
```bash
gem install jekyll bundler
```
##### (4)升级JekyllPermalink
查询版本:
```bash
jekyll --version
```
升级
```bash
gem update jekyll
```
要升级到最新的Rubygems
```bash
gem update --system
```
#### 2.用jekyll生成网页
```bash
 jekyll server
```
#### 3.解析域名
#### 4.修改CNAME文件
#### 5.修改文件
目录结构如下：`_layouts 内的文件为骨架模板`；`_posts `内的 markdown 文件会转化为我们所需发表的文章；`_config.yml` 为配置文件。
###### `_posts`为博客更新处，照片可以放在`img/in-post/`目录下
###### 如果有中英文版的，．md文件放在`include posts/`目录下，相应修改_posts的文件就行了．
##### 6.添加模块
###### (1)动态鼠标曲线
添加模块`canvas-nest.min.js`到js目录下
修改`layouts/post.html`文件在开始添加下面代码
```xml
    <!-- canvas-nest.min.js -->
<script type="text/javascript" src="../../../../js/canvas-nest.min.js"></script>
```
##### (2)要修改照片的话，把
```xml
background-image: url('{{ site.baseurl }}/{% if page.header-img %}{{ page.header-img }}{% else %}{{ site.header-img }}{% endif %}')
```
改为
```xml
background-image: url({{ site.baseurl }}{% if page.header-img %}{{ page.header-img }}{% else %}{{ site.header-img }}{% endif %})
```
就行了
##### (3)打字特效
```xml
<script src="../../../../js/activate-power-mode.js"></script>
<script>
POWERMODE.colorful = true; // 控制开启/开启礼花特效  
POWERMODE.shake = false; // 控制开启/关闭屏幕震动特效  
document.body.addEventListener('input', POWERMODE);
</script>
```
##### (4)返回顶部
把在rocket.css、signature.css和toc.css下载到css的目录下，然后在   include目录下的head.html文件的头部添加下面代码：
```xml
    <link rel="stylesheet" href="/css/rocket.css">
    <link rel="stylesheet" href="/css/signature.css">
    <link rel="stylesheet" href="/css/toc.css">
```
把在totop.js和toc.js下载到js的目录下，然后在include目录下的footer.html的最后添加下面代码：
```xml
<a id="rocket" href="#top" class=""></a>
<script type="text/javascript" src="/js/totop.js?v=1.0.0" async=""></script>
<script type="text/javascript" src="/js/toc.js?v=1.0.0" async=""></script>
```

##### (5)显示站点总访问量
具体教程参考:[不蒜子](http://ibruce.info/2015/04/04/busuanzi/)

##### (6)添加prismjs插件,增加代码高亮
[下载网站](https://prismjs.com/download.html#themes=prism-okaidia&languages=markup+css+clike+javascript+abap+actionscript+ada+apacheconf+apl+applescript+c+arff+asciidoc+asm6502+csharp+autohotkey+autoit+bash+basic+batch+bison+brainfuck+bro+cpp+aspnet+arduino+coffeescript+clojure+ruby+csp+css-extras+d+dart+diff+django+docker+eiffel+elixir+elm+markup-templating+erlang+fsharp+flow+fortran+gedcom+gherkin+git+glsl+gml+go+graphql+groovy+less+handlebars+haskell+haxe+http+hpkp+hsts+ichigojam+icon+inform7+ini+io+j+java+jolie+json+julia+keyman+kotlin+latex+markdown+liquid+lisp+livescript+lolcode+lua+makefile+crystal+erb+matlab+mel+mizar+monkey+n4js+nasm+nginx+nim+nix+nsis+objectivec+ocaml+opencl+oz+parigp+parser+pascal+perl+php+php-extras+sql+powershell+processing+prolog+properties+protobuf+scss+puppet+pure+python+q+qore+r+jsx+typescript+renpy+reason+rest+rip+roboconf+textile+rust+sas+sass+stylus+scala+scheme+smalltalk+smarty+plsql+soy+pug+swift+yaml+tcl+haml+tt2+twig+tsx+vbnet+velocity+verilog+vhdl+vim+visual-basic+wasm+wiki+xeora+xojo+xquery+tap&plugins=line-highlight+line-numbers+show-invisibles+autolinker+wpd+custom-class+file-highlight+toolbar+jsonp-highlight+highlight-keywords+remove-initial-line-feed+previewers+autoloader+unescaped-markup+command-line+normalize-whitespace+keep-markup+data-uri-highlight+show-language+copy-to-clipboard)
在<code>post.html</code>添加下面的代码:
```html
<link rel="stylesheet" href="/css/prism.css" data-noprefix />
<script src="/js/prism.js"></script>
```
下载官方的可能有问题,可以参考这两个:[prism.css](https://github.com/weijunzii/weijunzii.github.io/blob/master/assets/css/prism.css)和[prism.js](https://github.com/weijunzii/weijunzii.github.io/blob/master/assets/js/prism.js)
##### (7)添加搜索功能
在右上角添加搜索功能.参考[Soptq.github.io](https://github.com/Soptq/Soptq.github.io)


