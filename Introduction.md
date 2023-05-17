---


---

<h1 id="introduction">Introduction</h1>
<p>Node.js is a JS runtime built on Chrome’s V8 JS engine.</p>
<h2 id="usage">Usage</h2>
<ol>
<li>Developing Web Application: <strong>Express</strong></li>
<li>Cross-platform Desktop Application: <strong>Electron</strong></li>
<li>Create API Application: <strong>restify</strong></li>
</ol>
<h2 id="composition">Composition</h2>
<p>JS + Node.js internal API Modules (fs, path, http) + Tird-party Modules (Express, mysql).</p>
<h1 id="internal-modules">Internal Modules</h1>
<h2 id="fs">fs</h2>
<p>Operating the document</p>
<h3 id="import">Import</h3>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> fs <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'fs'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="fs.readfile">fs.readFile()</h3>
<pre class=" language-javascript"><code class="prism  language-javascript">fs<span class="token punctuation">.</span><span class="token function">readFile</span><span class="token punctuation">(</span><span class="token string">'path'</span><span class="token punctuation">[</span><span class="token punctuation">,</span><span class="token string">'utf8'</span><span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token keyword">function</span><span class="token punctuation">(</span>err<span class="token punctuation">,</span>dataStr<span class="token punctuation">)</span><span class="token punctuation">{</span>
	<span class="token keyword">if</span><span class="token punctuation">(</span>err<span class="token punctuation">)</span><span class="token punctuation">{</span>
		<span class="token keyword">return</span> console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">"failed to open"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token punctuation">}</span>
	console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>dataStr<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span>
</code></pre>
<h3 id="fs.writefile">fs.writeFile()</h3>
<pre class=" language-javascript"><code class="prism  language-javascript">fs<span class="token punctuation">.</span><span class="token function">writeFile</span><span class="token punctuation">(</span><span class="token string">'path'</span><span class="token punctuation">,</span> data<span class="token punctuation">[</span><span class="token punctuation">,</span><span class="token string">'utf8'</span><span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token keyword">function</span><span class="token punctuation">(</span>err<span class="token punctuation">)</span><span class="token punctuation">{</span>
	<span class="token keyword">if</span><span class="token punctuation">(</span>err<span class="token punctuation">)</span><span class="token punctuation">{</span>
		<span class="token keyword">return</span> console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">"failed to write"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token punctuation">}</span>
	console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">"Succeed"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span>
</code></pre>
<p>When recall the function, old content will be replaced.</p>
<h3 id="‘path’">‘path’</h3>
<p>Recommend for <strong>absolute path</strong> but not relative path;<br>
Reason: Relative path will give run-path as as reference not file-path.</p>
<p><strong>__dirname</strong> : Current file directory</p>
<h2 id="path">path</h2>
<h3 id="import-1">Import</h3>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> path <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'path'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="path.join">path.join()</h3>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> pathStr <span class="token operator">=</span> path<span class="token punctuation">.</span><span class="token function">join</span><span class="token punctuation">(</span>__dirname<span class="token punctuation">,</span><span class="token string">"relative path"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="path.basename">path.basename()</h3>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> path <span class="token operator">=</span> <span class="token string">'/a/b/c/index.html'</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> fullName <span class="token operator">=</span> path<span class="token punctuation">.</span><span class="token function">basename</span><span class="token punctuation">(</span>path<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> nameWithoutExt <span class="token operator">=</span> path<span class="token punctuation">.</span><span class="token function">basename</span><span class="token punctuation">(</span>path<span class="token punctuation">,</span> <span class="token string">".html"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>fullName<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">//index.html</span>
console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>nameWithoutExt<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">//index</span>
</code></pre>
<h3 id="path.extname">path.extname()</h3>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> path <span class="token operator">=</span> <span class="token string">'/a/b/c/index.html'</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> ext <span class="token operator">=</span> path<span class="token punctuation">.</span><span class="token function">extname</span><span class="token punctuation">(</span>path<span class="token punctuation">)</span><span class="token punctuation">;</span>
console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>ext<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">//.html</span>
</code></pre>
<h2 id="http">http</h2>
<h3 id="import-2">Import</h3>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> http <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'http'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="http.createserver">http.createServer()</h3>
<p>Create web server Instance:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> server <span class="token operator">=</span> http<span class="token punctuation">.</span><span class="token function">createServer</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="server.on">server.on()</h3>
<p>Bind a event to server.</p>
<h4 id="request-event">request event</h4>
<p>Call when client request the server:</p>
<pre class=" language-javascript"><code class="prism  language-javascript">server<span class="token punctuation">.</span><span class="token function">on</span><span class="token punctuation">(</span><span class="token string">'request'</span><span class="token punctuation">,</span><span class="token punctuation">(</span>req<span class="token punctuation">,</span>res<span class="token punctuation">)</span><span class="token operator">=&gt;</span><span class="token punctuation">{</span>
	console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">"Someone visit the server"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span>
</code></pre>
<p><strong>req</strong>: request object including Client data and properties.</p>
<ul>
<li><strong>req.url</strong> — client request URL</li>
<li><strong>req.mehod</strong> — client request method</li>
<li><strong>req.headers</strong> — client request headers</li>
</ul>
<p><strong>res</strong>: request object including Server data and properties.</p>
<ul>
<li><strong>res.end</strong> — send data to client (only String)</li>
<li><strong>req.send</strong> — send data to client (can be Sting/Object/Array)</li>
<li><strong>req.setHeader</strong> — set headers</li>
</ul>
<h3 id="server.listen">server.listen()</h3>
<p>Open the server:</p>
<pre class=" language-javascript"><code class="prism  language-javascript">server<span class="token punctuation">.</span><span class="token function">listen</span><span class="token punctuation">(</span><span class="token number">80</span><span class="token punctuation">,</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token operator">=&gt;</span><span class="token punctuation">{</span>
	console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">"Server running at 127.0.0.1:80"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span>
</code></pre>

