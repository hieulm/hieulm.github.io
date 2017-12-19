---


---

<h1 id="login">Login</h1>
<h2 id="determine-components">Determine components</h2>
<ol>
<li>LoginForm: display login from on login page</li>
</ol>
<ul>
<li>create folder <em>LoginForm</em> inside <em>src/routes/login/component</em></li>
<li>inside LoginForm component folder create files:
<ul>
<li>LoginForm.js is the component that we need to create
<ul>
<li>import required components: <em>TextField, RaisedButton, CheckBox</em></li>
<li>declare and set default value for component’s propTypes: <em>username, password, remember</em></li>
<li>export component with style: <code>export default withStyles(s)(LoginForm);</code></li>
</ul>
</li>
<li>LoginForm.scss: contain the styles for current component</li>
<li>package.json: play as index file for the component</li>
</ul>
</li>
</ul>
<h2 id="determine--implement-containers">Determine &amp; implement containers</h2>
<ol>
<li>LoginPage container</li>
</ol>
<ul>
<li>import required components: <em>LoginForm</em></li>
</ul>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">import</span> LoginPage <span class="token keyword">from</span> <span class="token string">"../components/LoginPage"</span><span class="token punctuation">;</span>
</code></pre>
<ul>
<li>determine container states:</li>
</ul>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">this</span><span class="token punctuation">.</span>state <span class="token operator">=</span> <span class="token punctuation">{</span>
      isRequesting<span class="token punctuation">:</span> <span class="token boolean">false</span><span class="token punctuation">,</span>
      isFailure<span class="token punctuation">:</span> <span class="token boolean">false</span><span class="token punctuation">,</span>
      authenticated<span class="token punctuation">:</span> <span class="token boolean">false</span><span class="token punctuation">,</span>
      accesstoken<span class="token punctuation">:</span> <span class="token keyword">null</span><span class="token punctuation">,</span>
      isLoggedIn<span class="token punctuation">:</span> <span class="token boolean">false</span><span class="token punctuation">,</span>
      username<span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
      password<span class="token punctuation">:</span> <span class="token string">""</span><span class="token punctuation">,</span>
      remember<span class="token punctuation">:</span> <span class="token boolean">false</span><span class="token punctuation">,</span>
    <span class="token punctuation">}</span><span class="token punctuation">;</span>
</code></pre>
<ul>
<li>render the container:</li>
</ul>
<pre class=" language-js"><code class="prism  language-js"><span class="token function">render</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  <span class="token operator">...</span>
  <span class="token operator">&lt;</span>LoginForm username<span class="token operator">=</span><span class="token punctuation">{</span><span class="token keyword">this</span><span class="token punctuation">.</span>state<span class="token punctuation">.</span>username<span class="token punctuation">}</span> password<span class="token operator">=</span><span class="token punctuation">{</span><span class="token keyword">this</span><span class="token punctuation">.</span>state<span class="token punctuation">.</span>password<span class="token punctuation">}</span><span class="token operator">/</span><span class="token operator">&gt;</span>
  <span class="token operator">...</span><span class="token punctuation">.</span>
<span class="token punctuation">}</span>
</code></pre>
<ul>
<li>implement container life cycle if needed:</li>
</ul>
<pre class=" language-js"><code class="prism  language-js">	<span class="token function">componentWillReceiveProps</span><span class="token punctuation">(</span>nextProps<span class="token punctuation">)</span> <span class="token punctuation">{</span><span class="token punctuation">}</span>
	<span class="token function">componentDidMount</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">{</span><span class="token punctuation">}</span>
	<span class="token operator">...</span>
</code></pre>
<ul>
<li>make the container to work with Redux</li>
</ul>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">const</span> mapStateToProps <span class="token operator">=</span> state <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token punctuation">{</span>
	<span class="token keyword">const</span> <span class="token punctuation">{</span>isLogged<span class="token punctuation">,</span> requesting<span class="token punctuation">,</span> failure<span class="token punctuation">}</span> <span class="token operator">=</span> state<span class="token punctuation">.</span>login<span class="token punctuation">;</span>
	<span class="token keyword">return</span> <span class="token punctuation">{</span>
		isLogged<span class="token punctuation">,</span>
		requesting<span class="token punctuation">,</span>
		failure<span class="token punctuation">,</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<span class="token keyword">const</span> mapDispatchToProsp <span class="token operator">=</span> dispatch <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token punctuation">{</span>
	login<span class="token punctuation">:</span> <span class="token punctuation">{</span>username<span class="token punctuation">,</span> password<span class="token punctuation">,</span> rememeber<span class="token punctuation">}</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token function">dispatch</span><span class="token punctuation">(</span><span class="token function">login</span><span class="token punctuation">(</span><span class="token punctuation">{</span>username<span class="token punctuation">,</span> password<span class="token punctuation">,</span> remember<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">)</span>l
<span class="token punctuation">}</span>
</code></pre>
<h2 id="handle-state-change-with-redux">Handle state change with Redux</h2>
<ol>
<li>define constants</li>
</ol>
<ul>
<li>actions name: <em>src/routes/login/constants/actions.js</em></li>
</ul>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">export</span> <span class="token keyword">const</span> ACTION_LOGIN_REQUEST <span class="token operator">=</span> <span class="token string">"action_login_request"</span><span class="token punctuation">;</span>
<span class="token keyword">export</span> <span class="token keyword">const</span> ACTION_LOGIN_SUCCESS <span class="token operator">=</span> <span class="token string">"action_login_success"</span><span class="token punctuation">;</span>
<span class="token keyword">export</span> <span class="token keyword">const</span> ACTION_LOGIN_FAILURE <span class="token operator">=</span> <span class="token string">"action_login_failure"</span><span class="token punctuation">;</span>
</code></pre>
<ul>
<li>reducer name: <em>src/constants/reducers.js</em></li>
</ul>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">export</span> <span class="token keyword">const</span> REDUCER_LOGIN <span class="token operator">=</span> <span class="token string">"login"</span><span class="token punctuation">;</span>
</code></pre>
<ol start="2">
<li>create reducer for module</li>
</ol>
<ul>
<li>reducer file: /src/routes/login/reducers/reducer_login.js</li>
</ul>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">import</span> update <span class="token keyword">from</span> <span class="token string">"react-addons-update"</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token operator">*</span> <span class="token keyword">as</span> ACTIONS <span class="token keyword">from</span> <span class="token string">"../../../constants/actions"</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token operator">*</span> <span class="token keyword">as</span> REDUCERS <span class="token keyword">from</span> <span class="token string">"../../../constants/reducers"</span><span class="token punctuation">;</span>
<span class="token keyword">export</span> <span class="token keyword">default</span> <span class="token keyword">function</span> <span class="token function">reducer</span><span class="token punctuation">(</span>state <span class="token operator">=</span> <span class="token punctuation">{</span><span class="token operator">...</span><span class="token punctuation">}</span><span class="token punctuation">,</span>action<span class="token punctuation">)</span> <span class="token punctuation">{</span>
  <span class="token keyword">switch</span> <span class="token punctuation">(</span>action<span class="token punctuation">.</span>type<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">case</span> ACTIONS<span class="token punctuation">.</span>ACTION_LOGIN_REQUEST<span class="token punctuation">:</span> <span class="token punctuation">{</span><span class="token operator">...</span><span class="token punctuation">}</span>
    <span class="token keyword">case</span> ACTIONS<span class="token punctuation">.</span>ACTION_LOGIN_SUCCESS<span class="token punctuation">:</span> <span class="token punctuation">{</span><span class="token operator">...</span><span class="token punctuation">}</span>
    <span class="token keyword">case</span> ACTIONS<span class="token punctuation">.</span>ACTION_LOGIN_FAILURE<span class="token punctuation">:</span> <span class="token punctuation">{</span><span class="token operator">...</span><span class="token punctuation">}</span>
    <span class="token keyword">default</span><span class="token punctuation">:</span> <span class="token keyword">return</span> state<span class="token punctuation">;</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<span class="token keyword">export</span> <span class="token keyword">const</span> REDUCER_NAME <span class="token operator">=</span> REDUCERS<span class="token punctuation">.</span>REDUCER_LOGIN<span class="token punctuation">;</span>
</code></pre>
<ol start="3">
<li>implement action creator
file: <em>src/login/action.js</em></li>
</ol>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">import</span> CryptoJs <span class="token keyword">from</span> <span class="token string">"crypto-js"</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> axios <span class="token keyword">from</span> <span class="token string">"axios"</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> randomstring <span class="token keyword">from</span> <span class="token string">"randomstring"</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token punctuation">{</span>
  ACTION_LOGIN_REQUEST<span class="token punctuation">,</span>
  ACTION_LOGIN_SUCCESS<span class="token punctuation">,</span>
  ACTION_LOGIN_FAILURE<span class="token punctuation">,</span>
<span class="token punctuation">}</span> <span class="token keyword">from</span> <span class="token string">"./constants/login"</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token punctuation">{</span>
  ACTION_REGISTER_REQUEST<span class="token punctuation">,</span>
  ACTION_REGISTER_SUCCESS<span class="token punctuation">,</span>
  ACTION_REGISTER_FAILURE<span class="token punctuation">,</span>
  ACTION_REGISTER_CHOOSEN<span class="token punctuation">,</span>
<span class="token punctuation">}</span> <span class="token keyword">from</span> <span class="token string">"./constants/register"</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token punctuation">{</span>
  API_KEY<span class="token punctuation">,</span>
  API_SECRET_KEY<span class="token punctuation">,</span>
  API_URL_LOGIN<span class="token punctuation">,</span>
  API_URL<span class="token punctuation">,</span>
  API_URL_REGISTER<span class="token punctuation">,</span>
<span class="token punctuation">}</span> <span class="token keyword">from</span> <span class="token string">"../../constants/api"</span><span class="token punctuation">;</span>

<span class="token keyword">export</span> <span class="token keyword">function</span> <span class="token function">login</span><span class="token punctuation">(</span>cred<span class="token punctuation">)</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token punctuation">{</span>
	<span class="token keyword">return</span> <span class="token punctuation">{</span>
		type<span class="token punctuation">:</span> ACTION_LOGIN_REQUEST<span class="token punctuation">,</span>
		payload<span class="token punctuation">:</span> data
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<span class="token keyword">export</span> <span class="token keyword">function</span> <span class="token function">register</span><span class="token punctuation">(</span>cred<span class="token punctuation">)</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token punctuation">{</span><span class="token punctuation">}</span>
</code></pre>
<h2 id="srcroutesloginroutesloginpageroutes.js">src/routes/login/routes/LoginPageRoutes.js</h2>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">import</span> React <span class="token keyword">from</span> <span class="token string">"react"</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token punctuation">{</span> injectAsyncReducer <span class="token punctuation">}</span> <span class="token keyword">from</span> 
<span class="token keyword">import</span> <span class="token punctuation">{</span> initFetchAction <span class="token punctuation">}</span> <span class="token keyword">from</span> <span class="token string">"../../../helper/utils"</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> <span class="token punctuation">{</span> login <span class="token punctuation">}</span> <span class="token keyword">from</span> <span class="token string">"../actions"</span><span class="token punctuation">;</span>
<span class="token keyword">import</span> LoginPage <span class="token keyword">from</span> <span class="token string">"../containers/LoginPage"</span><span class="token punctuation">;</span>
<span class="token keyword">export</span> <span class="token keyword">default</span> <span class="token keyword">async</span> <span class="token keyword">function</span> <span class="token function">LoginPageRoute</span><span class="token punctuation">(</span>context<span class="token punctuation">,</span> serverRendering <span class="token operator">=</span> <span class="token boolean">false</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span>process<span class="token punctuation">.</span>env<span class="token punctuation">.</span>BROWSER <span class="token operator">&amp;&amp;</span> <span class="token operator">!</span>serverRendering<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> <span class="token operator">&lt;</span>div <span class="token operator">/</span><span class="token operator">&gt;</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>
  <span class="token function">injectAsyncReducer</span><span class="token punctuation">(</span>context<span class="token punctuation">.</span>store<span class="token punctuation">,</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">"../reducers/loginReducer"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token keyword">const</span> <span class="token punctuation">{</span> dispatch <span class="token punctuation">}</span> <span class="token operator">=</span> context<span class="token punctuation">.</span>store<span class="token punctuation">;</span>
  <span class="token keyword">const</span> actions <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
  <span class="token keyword">await</span> <span class="token function">initFetchAction</span><span class="token punctuation">(</span>context<span class="token punctuation">,</span> actions<span class="token punctuation">,</span> <span class="token boolean">true</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token keyword">return</span> <span class="token operator">&lt;</span>LoginPage <span class="token operator">/</span><span class="token operator">&gt;</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<h2 id="routing-of-each-page-in-module">routing of each page in module</h2>
<p>filename: <em>src/routes/login/index.js</em></p>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">export</span> <span class="token keyword">default</span><span class="token punctuation">{</span>
	path<span class="token punctuation">:</span><span class="token string">"/"</span><span class="token punctuation">,</span>
	chidlren<span class="token punctuation">:</span><span class="token punctuation">[</span>
		<span class="token punctuation">{</span>
			path<span class="token punctuation">:</span> <span class="token string">"/login"</span><span class="token punctuation">,</span>
			<span class="token keyword">async</span> <span class="token function">action</span><span class="token punctuation">(</span>context<span class="token punctuation">)</span><span class="token punctuation">{</span>
				<span class="token operator">...</span><span class="token punctuation">.</span>
			<span class="token punctuation">}</span>
		<span class="token punctuation">}</span>
	<span class="token punctuation">]</span>
<span class="token punctuation">}</span>
</code></pre>
<h2 id="include-login-route-in-root-route">include login route in root route</h2>
<p>file: <em>src/index.js</em></p>
<pre class=" language-js"><code class="prism  language-js"><span class="token keyword">export</span> <span class="token keyword">default</span><span class="token punctuation">{</span>
	children<span class="token punctuation">:</span> <span class="token punctuation">[</span>
		<span class="token operator">...</span>
		<span class="token function">require</span><span class="token punctuation">(</span><span class="token string">"./login"</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token keyword">default</span><span class="token punctuation">,</span>
		<span class="token operator">...</span>
	<span class="token punctuation">]</span><span class="token punctuation">,</span>
<span class="token punctuation">}</span>
</code></pre>

