<pre data-source-line="1"><code class="hljs"><span class="hljs-comment">// 首先建立Ctest目录</span>
$ <span class="hljs-keyword">mkdir</span> Ctest

<span class="hljs-comment">// 进入Ctest文件夹目录下</span>
$ <span class="hljs-keyword">cd</span> Ctest

<span class="hljs-comment">// 编写一个test.c文件</span>
$ vim <span class="hljs-keyword">test</span>.c

  1 #<span class="hljs-keyword">include</span> &lt;stdio.<span class="hljs-keyword">h</span>&gt;  
  2 int main()  
  3 {  
  4     printf(<span class="hljs-string">"Hello World!\n"</span>);  
  5     <span class="hljs-keyword">return</span> 0;  
  6 }

<span class="hljs-keyword">exit</span>
:wq

<span class="hljs-comment">/*
*  将test.c预处理、汇编、编译并链接形成可执行文件test。
*  -o选项用来指定输出文件的文件名。
*/</span> 
$ gcc -o <span class="hljs-keyword">test</span> <span class="hljs-keyword">test</span>.c

<span class="hljs-comment">// 执行test文件</span>
$ ./<span class="hljs-keyword">test</span></code></pre>
<p data-source-line="29">终端输出：
Hello World！</p>