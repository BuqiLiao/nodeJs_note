---


---

<h1 id="router">Router</h1>
<p>Router is essentially the <strong>Mapping Relationships</strong>.</p>
<h2 id="router-in-express">Router in Express</h2>
<p>Router is the Mapping Relationships between <strong>Client request</strong> and <strong>Server response function</strong>, which is Composed of 3 parts:</p>
<ol>
<li>Request Method</li>
<li>Request URL</li>
<li>Responce Function</li>
</ol>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token function">METHOD</span><span class="token punctuation">(</span>PATH<span class="token punctuation">,</span> HANDLER<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="router-example">Router example</h3>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token punctuation">(</span><span class="token string">'URL'</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span><span class="token string">'This is a GET request'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
app<span class="token punctuation">.</span><span class="token function">post</span><span class="token punctuation">(</span><span class="token string">'URL'</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span><span class="token string">'This is a POST request'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="router-matching-mechanism">Router Matching Mechanism</h3>
<p>In each Client request send to Server, Router will match in <strong>defined order</strong> in your code.</p>
<h2 id="modular-router">Modular Router</h2>
<p>It is recommended to modular router for covinient management:</p>
<ol>
<li>Create Modular Router “.js” file</li>
<li>Call <strong>express.Router()</strong> to create Router object</li>
<li>Mount certain Router to Router object</li>
<li>Call <strong>module.exports</strong> to share Router object</li>
<li>Call <strong>app.use()</strong> to resgister Modular Router</li>
</ol>
<h3 id="modular-router-file">Modular Router file</h3>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span> express <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'express'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> router <span class="token operator">=</span> express<span class="token punctuation">.</span><span class="token function">Router</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
router<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token punctuation">(</span><span class="token string">'/user/:age/:name'</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	<span class="token keyword">var</span> name <span class="token operator">=</span> req<span class="token punctuation">.</span>params<span class="token punctuation">.</span>name<span class="token punctuation">;</span>
	<span class="token keyword">var</span> age <span class="token operator">=</span> req<span class="token punctuation">.</span>params<span class="token punctuation">.</span>age<span class="token punctuation">;</span>
	res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span><span class="token string">'Hello '</span> <span class="token operator">+</span> name <span class="token operator">+</span> <span class="token string">' you are '</span> <span class="token operator">+</span> age <span class="token operator">+</span> <span class="token string">' years old'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
router<span class="token punctuation">.</span><span class="token function">post</span><span class="token punctuation">(</span><span class="token string">'/user/add'</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span><span class="token string">'Added a new user'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
module<span class="token punctuation">.</span>exports <span class="token operator">=</span> router<span class="token punctuation">;</span>
</code></pre>
<h3 id="entrance-file">Entrance file</h3>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span>  express <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'express'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span>  app <span class="token operator">=</span> <span class="token function">express</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span>  router <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'./modularRouting.js'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token comment">//Add /api to all request URL</span>
app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span><span class="token string">'/api'</span><span class="token punctuation">,</span>router<span class="token punctuation">)</span><span class="token punctuation">;</span>
app<span class="token punctuation">.</span><span class="token function">listen</span><span class="token punctuation">(</span><span class="token number">80</span><span class="token punctuation">,</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">'http://localhost'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>

