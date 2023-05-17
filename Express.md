---


---

<h1 id="express">Express</h1>
<p>Express is a powerful Web framework based on Node.js.</p>
<h2 id="usage">Usage</h2>
<h3 id="install">Install</h3>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> i express
</code></pre>
<h3 id="create-web-server">Create Web Server</h3>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span> express <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'express'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> app <span class="token operator">=</span> <span class="token function">express</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
app<span class="token punctuation">.</span><span class="token function">listen</span><span class="token punctuation">(</span><span class="token number">8080</span><span class="token punctuation">,</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">=&gt;</span><span class="token punctuation">{</span>
	console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">'Server running on port 8080'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="listen-get-request">Listen GET request</h3>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token punctuation">(</span><span class="token string">'URL'</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span><span class="token string">'This is a GET request'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="listen-get-request-1">Listen GET request</h3>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token function">post</span><span class="token punctuation">(</span><span class="token string">'URL'</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span><span class="token string">'This is a POST request'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h2 id="get-static-parameters">Get static parameters</h2>
<h3 id="req.query">req.query</h3>
<p>In default, “req.query” is a blank object.<br>
If Client use format like “<strong>?name=bliao&amp;age=19</strong>” as parameters send to Server, use <strong>req.query</strong> to visit them.</p>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token punctuation">(</span><span class="token string">'/user'</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	<span class="token keyword">var</span> name <span class="token operator">=</span> req<span class="token punctuation">.</span>query<span class="token punctuation">.</span>name<span class="token punctuation">;</span>
	<span class="token keyword">var</span> age <span class="token operator">=</span> req<span class="token punctuation">.</span>query<span class="token punctuation">.</span>age<span class="token punctuation">;</span>
	res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span><span class="token string">'Hello '</span> <span class="token operator">+</span> name <span class="token operator">+</span> <span class="token string">' you are '</span> <span class="token operator">+</span> age <span class="token operator">+</span> <span class="token string">' years old'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h2 id="get-dynamic-parameters">Get dynamic parameters</h2>
<h3 id="req.params">req.params</h3>
<p>In default, “req.params” is a blank object.<br>
If Client use format like “<strong>/:id</strong>” as dynamic parameters send to Server, use <strong>req.params</strong> to visit it.</p>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token punctuation">(</span><span class="token string">'/user/:id/:name'</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>req<span class="token punctuation">.</span>params<span class="token punctuation">)</span><span class="token punctuation">;</span>
	res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span>req<span class="token punctuation">.</span>params<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h2 id="hosting-static-resources">Hosting static resources</h2>
<h3 id="express.static">express.static()</h3>
<p>Open static resources in certain directory to public.<br>
i.e. Open all files in “public” to pubic:</p>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span>express<span class="token punctuation">.</span><span class="token keyword">static</span><span class="token punctuation">(</span><span class="token string">'./public'</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>Then client can visit resources by going:</p>
<ol>
<li><a href="http://localhost:8080/html/index.html">http://localhost:8080/html/index.html</a></li>
<li><a href="http://localhost:8080/css/style.css">http://localhost:8080/css/style.css</a></li>
<li><a href="http://localhost:8080/js/index.js">http://localhost:8080/js/index.js</a><br>
…</li>
</ol>
<p><strong>Notice</strong>: directory name “public” will not appear in URL.</p>
<h4 id="open-serveral-directories">Open serveral directories</h4>
<p>When client visit certain file, <strong>express.static()</strong> will query file in order of the sentence:</p>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span>express<span class="token punctuation">.</span><span class="token keyword">static</span><span class="token punctuation">(</span><span class="token string">'./public'</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span>express<span class="token punctuation">.</span><span class="token keyword">static</span><span class="token punctuation">(</span><span class="token string">'./files'</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>If there are both “index.html” in “public” and “files”, then visit “<a href="http://localhost:8080/index.html">http://localhost:8080/index.html</a>” will direct to “public”.</p>
<h4 id="mount-path-prefix">Mount path prefix</h4>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span><span class="token string">'/public'</span><span class="token punctuation">,</span> express<span class="token punctuation">.</span><span class="token keyword">static</span><span class="token punctuation">(</span><span class="token string">'./public'</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>Then client can visit resources by going:</p>
<ol>
<li><a href="http://localhost:8080/public/html/index.html">http://localhost:8080/public/html/index.html</a></li>
<li><a href="http://localhost:8080/public/css/style.css">http://localhost:8080/public/css/style.css</a></li>
<li><a href="http://localhost:8080/public/js/index.js">http://localhost:8080/public/js/index.js</a><br>
…</li>
</ol>
<h2 id="nodemon">nodemon</h2>
<p>A tool that will listen to the change of code and restart the project automatically.</p>
<h3 id="install-1">Install</h3>
<p>Install nodemon in global:</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> i -g nodemon
</code></pre>
<h3 id="useage">Useage</h3>
<p>Change command “node” to “nodemon” when start the project:</p>
<pre class=" language-bash"><code class="prism  language-bash">nodemon index.js
</code></pre>

