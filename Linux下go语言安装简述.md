<h5 id="1-官网下载二进制档案包" data-source-line="1">1. 官网下载二进制档案包</h5>
<p data-source-line="2"><a href="https://golang.org/dl/">https://golang.org/dl/</a></p>

<h5 id="2-使用tar命令将档案包解压到-userlocal-目录下具体如下需要root权限" data-source-line="4">2. 使用tar命令将档案包解压到 /user/local 目录下，具体如下（需要root权限）：</h5>
<p data-source-line="6"><code>$ sudo tar -zxf go1.9.1.linux-amd64.tar.gz -C /usr/local</code></p>

<h5 id="3-验证安装结果进入到-usrlocal-目录中查看是否存在一个名为go的目录在命令行中输入" data-source-line="8">3. 验证安装结果，进入到 /usr/local 目录中查看是否存在一个名为go的目录,在命令行中输入：</h5>
<p data-source-line="10"><code>$ cd /usr/local/go</code>
<code>$ bin/go version</code></p>
<p data-source-line="13">是否出现如下：</p>

<pre data-source-line="15"><code class="hljs">root<span class="hljs-variable">@eson</span><span class="hljs-symbol">:/usr/local/go</span><span class="hljs-comment"># bin/go version</span>
go version go1.<span class="hljs-number">9.1</span> linux/amd64
root<span class="hljs-variable">@eson</span><span class="hljs-symbol">:/usr/local/go</span><span class="hljs-comment">#</span></code></pre>
<h5 id="4-设置四个环境变量goroot-gopath-gobin-以及path需要设置到某个profile文件中~bash_profile或者-etcprofile" data-source-line="19">4. 设置四个环境变量：GOROOT、GOPATH、GOBIN、以及PATH需要设置到某个profile文件中（~./.bash_profile或者 /etc/profile）</h5>
<p data-source-line="21"><code>$ vim /etc/profile</code></p>

<pre data-source-line="23"><code class="hljs"><span class="hljs-comment"># 插入在最后一行  </span>
    <span class="hljs-builtin-name">export</span> <span class="hljs-attribute">GOROOT</span>=/usr/local/go
    <span class="hljs-builtin-name">export</span> <span class="hljs-attribute">GOPATH</span>=~/golib:~/goproject
    <span class="hljs-builtin-name">export</span> <span class="hljs-attribute">GOBIN</span>=~/gobin
    <span class="hljs-builtin-name">export</span> <span class="hljs-attribute">PATH</span>=<span class="hljs-variable">$PATH</span>:$GOROOT/bin:$GOBIN</code></pre>
<p data-source-line="29"><code>$ source /etc/profile</code></p>

<h5 id="5-安装完成如下查看一下版本吧" data-source-line="31">5. 安装完成如下查看一下版本吧：</h5>
<p data-source-line="32"><code>$ go version</code></p>