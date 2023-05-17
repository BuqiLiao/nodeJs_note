---


---

<h1 id="authentication">Authentication</h1>
<h2 id="session">Session</h2>
<p>Recommended for <strong>non-cross-origin</strong> authentication as it need <strong>Cookies</strong> coordination.</p>
<h3 id="express-session">express-session</h3>
<h4 id="import">Import</h4>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span> session <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'express-session'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h4 id="register-as-middleware">Register as Middleware</h4>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span><span class="token function">session</span><span class="token punctuation">(</span><span class="token punctuation">[</span>
	secret<span class="token punctuation">:</span> <span class="token string">'bliao'</span><span class="token punctuation">,</span>
	resave<span class="token punctuation">:</span> <span class="token boolean">false</span><span class="token punctuation">,</span>
	saveUninitialized<span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">,</span>
<span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
</code></pre>
<h4 id="visit-session">Visit Session</h4>
<p>Call <code>req.session</code> to visit session object.</p>
<h4 id="clear-session">Clear Session</h4>
<pre class=" language-js"><code class="prism  language-js">req<span class="token punctuation">.</span>session<span class="token punctuation">.</span><span class="token function">destroy</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
</code></pre>
<h2 id="jwt">JWT</h2>
<p>Best method of solving <strong>cross-origin</strong> authentication</p>
<h3 id="composition">Composition</h3>
<pre><code>Header.Payload.Signature
</code></pre>
<p><strong>Payload</strong>: String of encoded user info<br>
<strong>Header</strong>, <strong>Signature</strong>: Protect JWT safety</p>
<h3 id="storage">Storage</h3>
<p>Client usually store JWT in <strong>localStorage</strong> or <strong>sessionStorage</strong></p>
<h3 id="useage">Useage</h3>
<p>Every connection between Client and Server must carry JWT.</p>
<h4 id="recommendation">Recommendation</h4>
<p>Put JWT in HTTP in <strong>Authorization field</strong> of request Header:</p>
<pre><code>Authorization: Bearer &lt;token&gt;
</code></pre>
<h2 id="jwt-in-express">JWT in Express</h2>
<h3 id="install">Install</h3>
<p>Install <strong>jsonwebtoken</strong> and <strong>express-jwt</strong></p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> i jsonwebtoken express-jwt
</code></pre>
<p><strong>jsonwebtoken</strong>: generate JWT string<br>
<strong>express-jwt</strong>: parse JWT to JSON object</p>
<h3 id="import-1">Import</h3>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span>  jwt <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'jsonwebtoken'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">var</span> <span class="token punctuation">{</span> expressjwt<span class="token punctuation">:</span> expressjwt <span class="token punctuation">}</span> <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">"express-jwt"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="secret-key">Secret Key</h3>
<p>Define a secret key for encoding and decoding JWT:</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span>  secretKey <span class="token operator">=</span> <span class="token string">'bliao'</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="encode">Encode</h3>
<p>Call <strong>sign()</strong> of <strong>jsonwebtoken</strong> to generate encoded JWT.</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span> tokenStr <span class="token operator">=</span> jwt<span class="token punctuation">.</span><span class="token function">sign</span><span class="token punctuation">(</span><span class="token punctuation">{</span> username<span class="token punctuation">:</span> userinfo<span class="token punctuation">.</span>username <span class="token punctuation">}</span><span class="token punctuation">,</span> secretKey<span class="token punctuation">,</span> <span class="token punctuation">{</span> expiresIn<span class="token punctuation">:</span>  <span class="token string">'30s'</span> <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
	status<span class="token punctuation">:</span>  <span class="token number">200</span><span class="token punctuation">,</span>
	message<span class="token punctuation">:</span>  <span class="token string">'Login Success'</span><span class="token punctuation">,</span>
	token<span class="token punctuation">:</span>  tokenStr
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="decode">Decode</h3>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span><span class="token function">expressJwt</span><span class="token punctuation">(</span><span class="token punctuation">{</span> secret<span class="token punctuation">:</span>  secretKey <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">unless</span><span class="token punctuation">(</span><span class="token punctuation">{</span> path<span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token operator">/</span><span class="token operator">^</span>\<span class="token operator">/</span>api\<span class="token operator">/</span><span class="token operator">/</span><span class="token punctuation">]</span> <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p><strong>unless()</strong>: URL that do not need JWT</p>
<p>In the API that have JWT authentication, we use <strong>req.auth</strong> to get the <strong>decoded user info</strong> from JWT:</p>
<pre class=" language-js"><code class="prism  language-js">app<span class="token punctuation">.</span><span class="token keyword">get</span><span class="token punctuation">(</span><span class="token string">'/admin/getinfo'</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>req<span class="token punctuation">,</span> res<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
	console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>req<span class="token punctuation">.</span>auth<span class="token punctuation">)</span><span class="token punctuation">;</span>
	res<span class="token punctuation">.</span><span class="token function">send</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
		status<span class="token punctuation">:</span> <span class="token number">200</span><span class="token punctuation">,</span>
		message<span class="token punctuation">:</span> <span class="token string">'Get Info Success'</span><span class="token punctuation">,</span>
		data<span class="token punctuation">:</span> req<span class="token punctuation">.</span>auth
	<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="catching-errors">Catching errors</h3>
<p>If JWT is expired or illegal, determine <code>err.name === 'UnauthorizedError'</code>:</p>

