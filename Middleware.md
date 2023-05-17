---


---

<h1 id="middleware">Middleware</h1>
<p>Middleware is the intermediate processing links in the business process.</p>
<h2 id="middleware-in-express">Middleware in Express</h2>
<p>After a Client request is send to Server, middlewares can be called before Server response.</p>
<h3 id="format">Format</h3>
<p>Middleware in Express is essentially a <strong>function</strong> with “<strong>req</strong>”, “<strong>res</strong>”, “<strong>next</strong>” (compared to Router function with only “req”, “res”):</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span> <span class="token function-variable function">mw</span> <span class="token operator">=</span> <span class="token keyword">function</span><span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">,</span> next<span class="token punctuation">)</span><span class="token punctuation">{</span>
	console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">"This is a middleware function"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token function">next</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span> 
<span class="token punctuation">}</span>
</code></pre>
<h2 id="next">next</h2>
<p>It is the key of calling between Middleware and Middleware or Router.</p>
<h2 id="global-middleware">Global Middleware</h2>
<p>Global Middleware will be called after each Client request reaches Server.<br>
Use <strong>app.use()</strong> to register Global Middleware</p>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span>mw<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>OR</p>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span><span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">,</span> next<span class="token punctuation">)</span><span class="token operator">=&gt;</span><span class="token punctuation">{</span>
	console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">"This is a middleware function"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token function">next</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span> 
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h2 id="features">Features</h2>
<p>All the middlewares share same “<strong>req</strong>” and “<strong>res</strong>”, thus we can create some properties methods for “<strong>req</strong>” and “<strong>res</strong>” in upper middlewares which can be used in lower middlewares and router</p>
<h2 id="order">Order</h2>
<p>Global Middlewares will be called in order in the code.</p>
<h2 id="partial-middleware">Partial Middleware</h2>
<p>Partial Middleware will be called in sepecific router.<br>
Not using <strong>app.use()</strong> but add parameter in <strong>router function</strong>:</p>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token punctuation">(</span><span class="token string">'/'</span><span class="token punctuation">,</span> mw<span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span><span class="token string">'Home Page'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>Create several Partial Middlewares:</p>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token punctuation">(</span><span class="token string">'/'</span><span class="token punctuation">,</span> mw1<span class="token punctuation">,</span> mw2<span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span><span class="token string">'Home Page'</span><span class="token punctuation">)</span><span class="token punctuation">;</span><span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>OR</p>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token punctuation">(</span><span class="token string">'/'</span><span class="token punctuation">,</span> <span class="token punctuation">[</span>mw1<span class="token punctuation">,</span> mw2<span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span><span class="token string">'Home Page'</span><span class="token punctuation">)</span><span class="token punctuation">;</span><span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h2 id="notice">Notice</h2>
<ol>
<li>Middleware should be defined and registered before Router</li>
<li>Should always contain <strong>next()</strong></li>
<li>Do not write extra code after <strong>next()</strong></li>
<li>Middlewares share “<strong>req</strong>” and “<strong>res</strong>”</li>
</ol>
<h2 id="clasification">Clasification</h2>
<h3 id="application-level">Application Level</h3>
<ul>
<li>app.use(mw)</li>
<li>app.get(’/’, mw, function())</li>
<li>app.post(’/’, mw, function())</li>
</ul>
<h3 id="router-level">Router Level</h3>
<ul>
<li>router.use(mw)</li>
<li>router.get(’/’, mw, function())</li>
<li>router.post(’/’, mw, function())</li>
</ul>
<h3 id="error-level">Error Level</h3>
<p>Error level middleware will be called when Error is occured:</p>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span><span class="token punctuation">(</span>err<span class="token punctuation">,</span> req<span class="token punctuation">,</span> res<span class="token punctuation">,</span> next<span class="token punctuation">)</span><span class="token operator">=&gt;</span><span class="token punctuation">{</span>
	console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">"Error: "</span> <span class="token operator">+</span> err<span class="token punctuation">.</span>message<span class="token punctuation">)</span><span class="token punctuation">;</span>
	res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span><span class="token string">"Error: "</span> <span class="token operator">+</span> err<span class="token punctuation">.</span>message<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p><strong>notice</strong>: Do not have <strong>next()</strong>, and must should be registered <strong>after</strong> Router</p>
<h2 id="internal-middleware-in-express">Internal Middleware in Express</h2>
<h3 id="express.static">express.static()</h3>
<h3 id="express.json">express.json()</h3>
<p>Parse JSON data</p>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span>express<span class="token punctuation">.</span><span class="token function">json</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p><strong>notice</strong>: In default, Server cannot prase JSON data and <code>req.body == undefined</code>.</p>
<h3 id="express.urlencoded">express.urlencoded()</h3>
<p>Parse URL-encoded data</p>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span>express<span class="token punctuation">.</span><span class="token function">urlencoded</span><span class="token punctuation">(</span><span class="token punctuation">{</span>extended<span class="token punctuation">:</span> <span class="token boolean">false</span><span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p><strong>notice</strong>: In default, Server cannot prase urlencoded data and <code>req.body == {}</code>.</p>
<h2 id="thir-party-middleware">Thir-party Middleware</h2>
<p>Use Thir-party Middleware in 3 steps:</p>
<ol>
<li><code>npm i body-parser</code></li>
<li><code>const parser = require('body-parser')</code></li>
<li><code>app.use(parser.urlencoded({extended: false}))</code></li>
</ol>
<h2 id="self-created-middleware">Self-created Middleware</h2>
<p>Create self Middleware in 6 steps (create a simple express.urlencoded):</p>
<ol>
<li>Define Middleware</li>
<li>Listen “<strong>data</strong>” event of “<strong>req</strong>”</li>
<li>Listen “<strong>end</strong>” event of “<strong>req</strong>”</li>
<li>Use “<strong>querystring</strong>” Module to parse request body</li>
<li>Mount the parsed data to “<strong>req.body</strong>”</li>
<li>Package the Middleware as Module</li>
</ol>
<h3 id="bodyparser.js">bodyParser.js</h3>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span> qs <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'querystring'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token keyword">const</span> <span class="token function-variable function">bodyParser</span> <span class="token operator">=</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">,</span> next<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	<span class="token keyword">let</span> str <span class="token operator">=</span> <span class="token string">''</span><span class="token punctuation">;</span>
	req<span class="token punctuation">.</span><span class="token function">on</span><span class="token punctuation">(</span><span class="token string">'data'</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>chunk<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
		str <span class="token operator">+=</span> chunk<span class="token punctuation">;</span>
	<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	req<span class="token punctuation">.</span><span class="token function">on</span><span class="token punctuation">(</span><span class="token string">'end'</span><span class="token punctuation">,</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
		<span class="token keyword">const</span> body <span class="token operator">=</span> qs<span class="token punctuation">.</span><span class="token function">parse</span><span class="token punctuation">(</span>str<span class="token punctuation">)</span><span class="token punctuation">;</span>
		req<span class="token punctuation">.</span>body <span class="token operator">=</span> body<span class="token punctuation">;</span>
		<span class="token function">next</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
module<span class="token punctuation">.</span>exports <span class="token operator">=</span> bodyParser<span class="token punctuation">;</span>
</code></pre>
<h3 id="index.js">index.js</h3>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span> express <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'express'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> app <span class="token operator">=</span> <span class="token function">express</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token keyword">const</span> bodyParser <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'./bodyParser.js'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span>bodyParser<span class="token punctuation">)</span><span class="token punctuation">;</span>

app<span class="token punctuation">.</span><span class="token function">post</span><span class="token punctuation">(</span><span class="token string">'/book'</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span>req<span class="token punctuation">.</span>body<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
app<span class="token punctuation">.</span><span class="token function">listen</span><span class="token punctuation">(</span><span class="token number">80</span><span class="token punctuation">,</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">'http://localhost'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>

