---


---

<h1 id="api">API</h1>
<h2 id="write-api-using-express">Write API using Express</h2>
<h3 id="create-server">Create Server</h3>
<p>app.js:</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span>  express <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'express'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span>  app <span class="token operator">=</span> <span class="token function">express</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
app<span class="token punctuation">.</span><span class="token function">listen</span><span class="token punctuation">(</span><span class="token number">80</span><span class="token punctuation">,</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">'http://localhost'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="create-api-router-module">Create API Router Module</h3>
<p>apiRouter.js:</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span>  express <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'express'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span>  apiRouter <span class="token operator">=</span> express<span class="token punctuation">.</span><span class="token function">Router</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">//bind Router here</span>

module<span class="token punctuation">.</span>exports <span class="token operator">=</span> apiRouter<span class="token punctuation">;</span>
</code></pre>
<p><strong>add</strong> register code to app.js :</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span>  apiRouter <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'./apiRouter.js'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span><span class="token string">'/api'</span><span class="token punctuation">,</span> apiRouter<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="write-get-api">Write GET API</h3>
<p>sample:</p>
<pre class=" language-js"><code class="prism  language-js">apiRouter<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token punctuation">(</span><span class="token string">'/get'</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	<span class="token keyword">const</span> query <span class="token operator">=</span> req<span class="token punctuation">.</span>query<span class="token punctuation">;</span>
	res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
		status<span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">,</span>
		msg<span class="token punctuation">:</span> <span class="token string">'Request GET successfully!'</span><span class="token punctuation">,</span>
		data<span class="token punctuation">:</span> query
	<span class="token punctuation">}</span><span class="token punctuation">)</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="write-post-api">Write POST API</h3>
<p>sample:</p>
<pre class=" language-js"><code class="prism  language-js">apiRouter<span class="token punctuation">.</span><span class="token function">post</span><span class="token punctuation">(</span><span class="token string">'/post'</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	<span class="token keyword">const</span> body <span class="token operator">=</span> req<span class="token punctuation">.</span>body<span class="token punctuation">;</span>
	res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
		status<span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">,</span>
		msg<span class="token punctuation">:</span> <span class="token string">'Request POST successfully!'</span><span class="token punctuation">,</span>
		data<span class="token punctuation">:</span> body
	<span class="token punctuation">}</span><span class="token punctuation">)</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p><strong>notice</strong>: remember to use <code>app.use(express.urlencoded({ extended: true }));</code> to parse data</p>
<h2 id="resolving-cross-origin-issues">Resolving cross-origin issues</h2>
<h3 id="use-cors-middleware">Use CORS Middleware</h3>
<ol>
<li>run <code>npm i cors</code></li>
<li><code>const cors = require('cors')</code></li>
<li>app.use(cors())</li>
</ol>
<p><strong>notice</strong>: Configure cors <strong>before</strong> using Router</p>
<h2 id="what-is-cors">What is CORS</h2>
<p>CORS (Cross-Origin Resource Sharing) is composed of series of <strong>HTTP response Header</strong>, which decide whether browser prevent JS code in frontedn to share resource crossing origin.</p>
<h2 id="cors-responce-header">CORS Responce Header:</h2>
<h3 id="access-control-allow-origin">Access-Control-Allow-Origin</h3>
<p><code>Access-Control-Allow-Origin: &lt;origin&gt; | *</code><br>
<strong>origin</strong>: Acceptable URL that can access resource.<br>
i.e. Only allow request form <a href="https://google.com">https://google.com</a> :</p>
<pre class=" language-js"><code class="prism  language-js">res<span class="token punctuation">.</span><span class="token function">setHeader</span><span class="token punctuation">(</span><span class="token string">'Access-Control-Allow-Origin'</span><span class="token punctuation">,</span><span class="token string">'https://google.com'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="access-control-allow-header">Access-Control-Allow-Header</h3>
<p>In defualt, CORS only supports 9 request Headers from Client:<br>
Accept, Accept-Language, Content-Language, DPR, Save-Data, Viewport-Width, Width, Content-Type (values <strong>only</strong> from text/plain, multipart/form-data, application/x-www-form-urlencoded);</p>
<p>If Client send extra request Header exclude these 9 Headers, we should state <code>Access-Control-Allow-Origin</code> in Server:</p>
<pre class=" language-js"><code class="prism  language-js">res<span class="token punctuation">.</span><span class="token function">setHeader</span><span class="token punctuation">(</span><span class="token string">'Access-Control-Allow-Headers'</span><span class="token punctuation">,</span><span class="token string">'Content-Type, X-Custom-Header'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h2 id="jsonp">JSONP</h2>
<p>JSONP is another method resolving cross-origin issues, but it only supports GET request.</p>
<p>Browser requesting data from Server via “src” in “&lt;script&gt;” while Server return a function calling is called JSONP.</p>
<h3 id="create-jsonp-api">Create JSONP API</h3>
<ol>
<li>Get callback function name from Client</li>
<li>Get data needed to be sent to Client by JSONP</li>
<li>Combine former data and get a String</li>
<li>Send String to Client</li>
</ol>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token punctuation">(</span><span class="token string">'/api/jsonp'</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	<span class="token keyword">const</span> funcName <span class="token operator">=</span> req<span class="token punctuation">.</span>query<span class="token punctuation">.</span>callback<span class="token punctuation">;</span>
	<span class="token keyword">const</span> data <span class="token operator">=</span> <span class="token punctuation">{</span> name<span class="token punctuation">:</span><span class="token string">'bliao'</span><span class="token punctuation">,</span> age<span class="token punctuation">:</span>  <span class="token number">19</span> <span class="token punctuation">}</span><span class="token punctuation">;</span>
	<span class="token keyword">const</span> scriptStr <span class="token operator">=</span> <span class="token template-string"><span class="token string">`</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>funcName<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">(</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>JSON<span class="token punctuation">.</span><span class="token function">stringify</span><span class="token punctuation">(</span>data<span class="token punctuation">)</span><span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">)`</span></span><span class="token punctuation">;</span>
	res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span>scriptStr<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>

