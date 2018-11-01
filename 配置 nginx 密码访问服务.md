<pre data-source-line="1"><code class="hljs"><span class="hljs-comment">//在nginx目录下生成密码用户名文件</span>
htpasswd -c passwd.<span class="hljs-keyword">db</span> username

<span class="hljs-comment">//修改nginx的配置文件 xxx.conf</span>
auth_basic <span class="hljs-string">"Restricted"</span>;
auth_basic_user_file /usr/<span class="hljs-keyword">local</span>/etc/nginx/password.<span class="hljs-keyword">db</span>;

<span class="hljs-comment">//平滑重启nginx服务</span>
$ sudo nginx -s reload</code></pre>