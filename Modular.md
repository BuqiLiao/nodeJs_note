---


---

<h1 id="modular">Modular</h1>
<h2 id="clasification">Clasification</h2>
<ol>
<li>Internal Module (fs, path, http)</li>
<li>self-created Module (Every self .js document)</li>
<li>Third-party Module</li>
</ol>
<h2 id="load-module">Load Module</h2>
<h3 id="require">require()</h3>
<p>Will excute code of Modules while loading Modules</p>
<h2 id="module-scope">Module Scope</h2>
<p>Variables and Methods defined in Modules can only be accessed in the Modules.</p>
<h2 id="module-object">“module” object</h2>
<p>Every .js document has internal module object including document’s properties:</p>
<pre class=" language-javascript"><code class="prism  language-javascript">console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>module<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="module.exports">module.exports</h3>
<p>Share the member inside Modules externally (When using <strong>require()</strong>, will get the object that module.exports points):</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> age <span class="token operator">=</span> <span class="token number">20</span><span class="token punctuation">;</span>
module<span class="token punctuation">.</span>exports<span class="token punctuation">.</span>age <span class="token operator">=</span> age<span class="token punctuation">;</span>
module<span class="token punctuation">.</span>exports<span class="token punctuation">.</span>username <span class="token operator">=</span> <span class="token string">'Frosty'</span><span class="token punctuation">;</span>
module<span class="token punctuation">.</span>exports<span class="token punctuation">.</span><span class="token function-variable function">helloWorld</span> <span class="token operator">=</span> <span class="token keyword">function</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">{</span>
	console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">"Hello World!"</span><span class="token punctuation">)</span>
<span class="token punctuation">}</span>
</code></pre>
<p>If the object pointed by module.exports is replace then the result of <strong>require()</strong> will be the replacing one:</p>
<pre class=" language-javascript"><code class="prism  language-javascript">module<span class="token punctuation">.</span>exports<span class="token punctuation">.</span>username <span class="token operator">=</span> <span class="token string">'Frosty'</span><span class="token punctuation">;</span>
module<span class="token punctuation">.</span>exports <span class="token operator">=</span> <span class="token punctuation">{</span>
	nickname <span class="token punctuation">:</span> <span class="token string">"Ben"</span><span class="token punctuation">,</span>
	<span class="token function">sayHi</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">{</span>
		console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span><span class="token string">"Hi!"</span><span class="token punctuation">)</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<span class="token comment">//Result: {nickname : "Ben",sayHi(){console.log("Hi!")}};</span>
</code></pre>
<h2 id="export-object">“export” object</h2>
<p>Pointing to same object as module.exports:<br>
<code>export === module.exports</code><br>
<strong>Notice</strong>: <strong>require()</strong> always get the object from <strong>module.exports</strong> not <strong>export</strong></p>
<pre class=" language-javascript"><code class="prism  language-javascript">module<span class="token punctuation">.</span>exports<span class="token punctuation">.</span>username <span class="token operator">=</span> <span class="token string">'Frosty'</span><span class="token punctuation">;</span>
<span class="token keyword">export</span> <span class="token operator">=</span> <span class="token punctuation">{</span>username<span class="token punctuation">:</span> <span class="token string">'Ben'</span><span class="token punctuation">}</span>
<span class="token comment">//Result: {username : 'Frosty'};</span>
</code></pre>
<h2 id="specification">Specification</h2>
<p>Node.js follows CommonJS Modular<br>
Specification, which specifies feature of Module and Interdependence of each Module.</p>
<h3 id="commonjs-specification">CommonJS Specification</h3>
<ol>
<li>Inside each Module, variable “module” represents current Module.</li>
<li>“module” is an object, with its “export” property(module.exports) as external interface.</li>
<li>Once using require() to load Module, its essence is to load a module.exports</li>
</ol>
<h2 id="package">Package</h2>
<p>Also called Third-party Modules.</p>
<h3 id="links">Links</h3>
<p><strong>Search</strong>: <a href="https://www.npmjs.com">https://www.npmjs.com</a><br>
<strong>Install</strong>: <a href="https://registry.npmjs.org">https://registry.npmjs.org</a></p>
<h3 id="install-package">Install Package</h3>
<p>Use <strong>Node Package Manager</strong> to install pakage.<br>
Check Version:</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> -v
</code></pre>
<p>Install <strong>newest</strong> Package:</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> <span class="token function">install</span> <span class="token string">"package full name"</span>
</code></pre>
<p>OR</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> i <span class="token string">"package full name"</span>
</code></pre>
<p>Install certain version:</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> i <span class="token string">"package full name"</span>@<span class="token string">"version"</span>
</code></pre>
<p>Install several Packages:</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> i <span class="token string">"package1"</span> <span class="token string">"package2"</span> <span class="token string">"package3"</span>
</code></pre>
<h3 id="uninstall-package">Uninstall Package</h3>
<p>will auto delete Package info in dependencies.</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> uninstall <span class="token string">"package full name"</span>
</code></pre>
<h2 id="dateformat-practice">DateFormat Practice</h2>
<h3 id="without-package">Without Package</h3>
<p>Create self Module:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">function</span>  <span class="token function">dateFormat</span><span class="token punctuation">(</span>dtStr<span class="token punctuation">)</span><span class="token punctuation">{</span>
	<span class="token keyword">const</span> dt <span class="token operator">=</span> <span class="token keyword">new</span>  <span class="token class-name">Date</span><span class="token punctuation">(</span>dtStr<span class="token punctuation">)</span><span class="token punctuation">;</span>
	
	<span class="token keyword">const</span> y <span class="token operator">=</span> <span class="token function">padZero</span><span class="token punctuation">(</span>dt<span class="token punctuation">.</span><span class="token function">getFullYear</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token keyword">const</span> m <span class="token operator">=</span> <span class="token function">padZero</span><span class="token punctuation">(</span>dt<span class="token punctuation">.</span><span class="token function">getMonth</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token keyword">const</span> d <span class="token operator">=</span> <span class="token function">padZero</span><span class="token punctuation">(</span>dt<span class="token punctuation">.</span><span class="token function">getDate</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token keyword">const</span> hh <span class="token operator">=</span> <span class="token function">padZero</span><span class="token punctuation">(</span>dt<span class="token punctuation">.</span><span class="token function">getHours</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token keyword">const</span> mm <span class="token operator">=</span> <span class="token function">padZero</span><span class="token punctuation">(</span>dt<span class="token punctuation">.</span><span class="token function">getMinutes</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token keyword">const</span> ss <span class="token operator">=</span> <span class="token function">padZero</span><span class="token punctuation">(</span>dt<span class="token punctuation">.</span><span class="token function">getSeconds</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

	<span class="token keyword">const</span> newDtStr <span class="token operator">=</span> <span class="token template-string"><span class="token string">`</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>y<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">-</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>m<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">-</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>d<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string"> </span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>hh<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">:</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>mm<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">:</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>ss<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">`</span></span><span class="token punctuation">;</span>
	<span class="token keyword">return</span> newDtStr<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
<span class="token keyword">function</span>  <span class="token function">padZero</span><span class="token punctuation">(</span>n<span class="token punctuation">)</span><span class="token punctuation">{</span>
	<span class="token keyword">return</span> n <span class="token operator">&lt;</span> <span class="token number">10</span> <span class="token operator">?</span> <span class="token string">'0'</span> <span class="token operator">+</span> n <span class="token punctuation">:</span> n<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
module<span class="token punctuation">.</span>exports <span class="token operator">=</span> <span class="token punctuation">{</span>
	dateFormat
<span class="token punctuation">}</span><span class="token punctuation">;</span>
</code></pre>
<p>Call the Module:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> TIME <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">"./dateFormat.js"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> dt <span class="token operator">=</span> <span class="token keyword">new</span>  <span class="token class-name">Date</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>TIME<span class="token punctuation">.</span><span class="token function">dateFormat</span><span class="token punctuation">(</span>dt<span class="token punctuation">)</span><span class="token punctuation">)</span>
</code></pre>
<h3 id="using-package">Using Package</h3>
<p>Import  moment Package:</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> i moment
</code></pre>
<p>Call the moment:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> moment <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'moment'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> dt <span class="token operator">=</span> <span class="token function">moment</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">format</span><span class="token punctuation">(</span><span class="token string">'YYYY-MM-DD HH:mm:ss'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>dt<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h2 id="npm-configuration">npm Configuration</h2>
<h3 id="project-sharing">Project Sharing</h3>
<p>When sharing project, add “<strong>node_modules</strong>” to “<strong>.gitignore</strong>” as it occupies huge space.<br>
Package information is stored in “<strong>package.json</strong>” where now npm will auto create it in your base directory.</p>
<p>If not, using code:</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> init -y
</code></pre>
<p>After getting project without  “<strong>node_modules</strong>”, need to install all the Packages recorded by “<strong>package.json</strong>”  in <strong>dependencies</strong> node:</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> i
</code></pre>
<h3 id="devdependencies-node">devDependencies node</h3>
<p>If some Packages will only be used in <strong>development stage</strong>, suggest to record those Packages to <strong>devDependencies</strong> node;<br>
If some Packages  will be used in all stages, suggest to record those Packages to <strong>dependencies</strong> node.</p>
<h4 id="record-to-devdependencies">record to devDependencies:</h4>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> <span class="token function">install</span> <span class="token string">"package"</span> --save-dev
</code></pre>
<p>OR</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> i <span class="token string">"package"</span> -D
</code></pre>
<h2 id="package-specification">Package Specification</h2>
<ul>
<li>Package must be a <strong>single</strong> directory.</li>
<li>Package top dorctory must contain “<strong>package.json</strong>”.</li>
<li>“package.json” must contain 3 properties: <strong>name</strong>, <strong>version</strong>, <strong>main</strong>. (<strong>main</strong> is the index document)</li>
</ul>
<h2 id="create-self-package">Create self Package</h2>
<p>Create basic files:</p>
<ul>
<li>package.json</li>
<li>index.js</li>
<li><a href="http://README.md">README.md</a></li>
</ul>
<h3 id="initiate-package.json">Initiate package.json</h3>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
	<span class="token string">"name"</span><span class="token punctuation">:</span> <span class="token string">"bliao-tools-test1"</span><span class="token punctuation">,</span>
	<span class="token string">"version"</span><span class="token punctuation">:</span> <span class="token string">"1.0.0"</span><span class="token punctuation">,</span>
	<span class="token string">"main"</span><span class="token punctuation">:</span> <span class="token string">"index.js"</span><span class="token punctuation">,</span>
	<span class="token string">"description"</span><span class="token punctuation">:</span> <span class="token string">"Formate date, HTMLEscape"</span><span class="token punctuation">,</span>
	<span class="token string">"keywords"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
		<span class="token string">"date"</span><span class="token punctuation">,</span>
		<span class="token string">"format"</span><span class="token punctuation">,</span>
		<span class="token string">"html"</span><span class="token punctuation">,</span>
		<span class="token string">"escape"</span>
	<span class="token punctuation">]</span><span class="token punctuation">,</span>
	<span class="token string">"author"</span><span class="token punctuation">:</span> <span class="token string">"bliao"</span><span class="token punctuation">,</span>
	<span class="token string">"license"</span><span class="token punctuation">:</span> <span class="token string">"ISC"</span><span class="token punctuation">,</span>
<span class="token punctuation">}</span>
</code></pre>
<h3 id="separate-functions-to-different-modules">Separate functions to different Modules</h3>
<ul>
<li>function of formatting date: “src” -&gt; “dateFormat.js”</li>
<li>function of dealling html: “src” -&gt; “htmlEscape.js”</li>
<li>Import  “dateFormat.js”, “htmlEscape.js” to “index.js”</li>
</ul>
<p><strong>index.js</strong>:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> date <span class="token operator">=</span> <span class="token function">request</span><span class="token punctuation">(</span><span class="token string">'./src/dateFormat.js'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">const</span> escape <span class="token operator">=</span> <span class="token function">request</span><span class="token punctuation">(</span><span class="token string">'./src/htmlEscape.js'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
module<span class="token punctuation">.</span>exports <span class="token operator">=</span> <span class="token punctuation">{</span>
   <span class="token comment">//Use ... to share all members of objects</span>
   <span class="token operator">...</span>date<span class="token punctuation">,</span>
   <span class="token operator">...</span>escape
<span class="token punctuation">}</span>
</code></pre>
<h3 id="write-readme.md">Write <a href="http://README.md">README.md</a></h3>
<p>Typically include:</p>
<ul>
<li>Install</li>
<li>Import</li>
<li>Functions’ method</li>
<li>Open Source Protocols</li>
</ul>
<h3 id="publish-package">Publish Package</h3>
<h4 id="login-npm-in-terminal">login npm in terminal:</h4>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> login
</code></pre>
<h4 id="publish">publish:</h4>
<p>goto Package’s root directory</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> login
</code></pre>
<h4 id="update">update:</h4>
<p>Change version of the Package first:<br>
<strong>1.0.0 -&gt; 1.0.1</strong></p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> version patch
</code></pre>
<p><strong>1.0.0 -&gt; 1.1.0</strong></p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> version minor
</code></pre>
<p><strong>1.0.0 -&gt; 2.0.0</strong></p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> version major
</code></pre>
<p>Then publish the Package.</p>
<h4 id="unpublish">unpublish</h4>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">npm</span> unpublish <span class="token string">"package"</span> --force
</code></pre>
<p><strong>Notice</strong>:</p>
<ul>
<li>Unpublish can only delete package within 72 hours;</li>
<li>Deleted package cannot be published within 24 hours;</li>
</ul>
<h2 id="module-loading-mechanism">Module Loading Mechanism</h2>
<h3 id="priority-loading-from-the-cache">Priority loading from the cache</h3>
<p>Module will be cached after first loading (Call <strong>require()</strong> multiple times will only excute once).</p>
<h3 id="customized-modules">Customized Modules</h3>
<p>When use <strong>require()</strong> to import Customized Modules, path identifiers should be included ("./", “…/”).</p>
<p>If extension is omitted, Node.js will try to load module in such order:<br>
“.js” -&gt; “.json” -&gt; “.node” -&gt; failed to load</p>
<h3 id="third-party-modules">Third-party Modules</h3>
<p>If Module transfered to <strong>require()</strong> is not a internal Module and is not started with “./”, “…/”, then Node.js will try to load module in such order:<br>
i.e. In ‘C:\Users\bliao\project\index.js’ called <code>require("tools")</code></p>
<ol>
<li>C:\Users\bliao\project\node_modules\tools</li>
<li>C:\Users\bliao\node_modules\tools</li>
<li>C:\Users\node_modules\tools</li>
<li>C:\node_modules\tools</li>
</ol>

