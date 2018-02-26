# 华农之窗开放平台
网址：<a href="http://open.lushaoming.site">http://open.lushaoming.site</a>，开发者可在华农之窗开放平台申请接入，免去注册的烦恼。欢迎大家加入交流群，群号码：529668978
<h3>更新日志</h3>
<p>2018-02-09更新如下：</p>
<p>1.新增扫码登录，用户使用微信扫一扫即可授权登录，无需输入帐号密码。</p>
<p>2.新增弹框弹出登录页面，无需跳转页面。</p>
<p>3.新增go_to字段，开发者可在跳转链接中加上go_to参数，此参数会原样返回给开发者，方便开发者判断登录前的页面，从而使登录后回到当前页。</p>
<div class="content">
	<div id="read">
		<h3>1、开发前必读</h3>
		<p>本文档是为了方便开发者使用华农之窗进行第三方登录而编写，如有错误之处，请指正。联系邮箱：scauinfoadmin@163.com</p>
		<p>申请的应用不能违反国家法律法规，一经发现，将立即冻结该应用，并且该用户下的所有应用都将被冻结。</p>
		<p>开放平台为第三方应用提供了丰富的API。第三方网站接入后，即可通过调用平台的API实现用户使用华农之窗帐号登录网站，并且可以获取到华农之窗用户的相关信息。</p>
		<p>海量新用户：用户使用已有的华农之窗帐号即可登录网站，大大降低网站注册门槛，给网站带来海量新用户。</p>
		<h3>1.1网站接入方式</h3>
		<p>第三方网站主要通过“华农之窗登录”接入华农之窗开放平台</p>
		<p>详细的接入指引请参见网站接入流程</p>
		<h3>1.2使用华农之窗登录效果展示</h3>
		<p style="color: #F00">展示应用地址：<a href="http://chat.lushaoming.site" target="_blank">聊天室</a></p>
		<p>华农之窗测试帐号：lushao</p>
		<p>华农之窗测试密码：111111</p>
		<p>下面描述了一个网站使用“华农之窗登录”，并访问华农之窗用户个人信息的整个过程。</p>
		<p>1.2.1、网站上设置华农之窗登录入口，图标地址：<a href="https://www.ifour.net.cn/scau_info/scau-info-logo.png" target="_blank">https://www.ifour.net.cn/scau_info/scau-info-logo.png</a></p>
		<p><img src="http://open.lushaoming.site/assets/img/login.png"></p>
		<p>1.2.2、用户选择华农之窗登录，如下图所示：</p>
		<p><img src="http://open.lushaoming.site/assets/img/login-show.png"></p>
		<p>1.2.3、用户成功登录网站，如下图所示：</p>
		<p><img src="http://open.lushaoming.site/assets/img/login-success.png"></p>
	</div>
	<div id="get-app">
		<h3>2、如何获取应用</h3>
		<p>登录华农之窗开放平台进行申请，填写应用信息，审核通过后将获得appId和appSecret，请注意：appSecret不应暴露。</p>
		<p>如没有华农之窗帐号，可扫描以下二维码，进入小程序，在个人中心里绑定帐号</p>
		<p><img src="/assets/img/xcx.jpg"><img src="http://open.lushaoming.site/assets/img/bind.png" style="width: 240px;height: 400px;"></p>
	</div>
	<div id="dev-process">
		<h3>3、开发流程</h3>
		<h3>3.1、引导用户跳转至第三方授权登录页面，登录成功后获取code</h3>
		<p>引导用户跳转至第三方授权登录页面，地址：https://www.ifour.net.cn/scau_info/oauth/v1/web/open/index?app_id=YOUR APPID&redirect_uri=YOUR REDIRECT URI&response_type=code</p>
		<p>说明：app_id和redirect_uri请在个人中心获取，response_type填写code</p>
	</div>
	<div id="get-openid">
		<h3>3.2、获取openid</h3>
		<p>用户登录成功后，系统会重定向至用户申请时填写的回调地址，并会带上<span style="color: #F00;">code</span>参数，使用code参数可以获取用户唯一标识openid。</p>
		<p>接口地址：https://www.ifour.net.cn/scau_info/oauth/v1/web/user/get-openid</p>
		<p>
			<table class="table table-bordered">
				<thead>
					<th>参数名称</th><th>是否必须</th><th>说明</th>
				</thead>
				<tbody>
					<tr>
						<td>app_id</td>
						<td>是</td>
						<td>应用的app_id</td>
					</tr>
					<tr>
						<td>app_secret</td>
						<td>是</td>
						<td>应用的app_secret</td>
					</tr>
					<tr>
						<td>code</td>
						<td>是</td>
						<td>用户登录时返回的code（有效期为5分钟）</td>
					</tr>
					<tr>
						<td>grant_type</td>
						<td>是</td>
						<td>填写为 authorization_code</td>
					</tr>
				</tbody>
			</table>
		</p>
		<p>
			成功返回值示例：
			{"status":"0","msg":"SUCCESS","openid":"用户唯一标识openid"}
		</p>
		<p>
			失败返回值示例：
			{"status":"500","msg":"Invalid app_id"}
		</p>
		<p>通过判断status的值是否为0即可判断是否正确获取到openid。</p>
	</div>
	<div id="get-access-token">
		<h3>3.2、获取access_token</h3>
		<p>接口地址：https://www.ifour.net.cn/scau_info/oauth/v1/web/token/get-token</p>
		<p>
			<table class="table table-bordered">
				<thead>
					<th>参数名称</th><th>是否必须</th><th>说明</th>
				</thead>
				<tbody>
					<tr>
						<td>app_id</td>
						<td>是</td>
						<td>应用的app_id</td>
					</tr>
					<tr>
						<td>app_secret</td>
						<td>是</td>
						<td>应用的app_secret</td>
					</tr>
				</tbody>
			</table>
		</p>
		<p>
			返回值示例：
			{"access_token":"4DF350124B6E9134F7CD71D45BD9C5DA","expire_time":1514955107,"used_times":58}
		</p>
		<p>access_token：获取到的access_token</p>
		<p>expire_time：过期时间戳，单位秒</p>
		<p>used_times：接口已调用次数</p>
		<p>错误返回示例：{"status":"-30015","msg":"Invalid app_id"}</p>
		<p>说明：access_token是您调用其他接口的凭证，请妥善保存，请勿泄露。</p>
		<p>access_token具有有效期（一般为一个月）并可重复获取，一旦获取新的access_token成功，旧的access_token立即失效，为了您的业务不受影响，应该自行保存access_token。</p>
		<p>access_token每个月的调用次数是有限制的（一般为100次），请勿频繁调用此接口，否则可能导致调用此接口权限被封。</p>
		<p>如需测试应用，可以在开放平台申请测试应用帐号，测试应用不会受此限制。</p>
		<!-- <p>为了方便您开发，我在此写了一个PHP版本的SDK，其他版本暂时没有。点击下载<a href="https://www.ifour.net.cn/scau_info/PHP-SDK.rar">PHP-SDK.rar</a></p> -->
	</div>
	<div id="get-user-info">
		<h3>3.3、获取用户信息</h3>
		<p>获取到access_token之后就可以通过openid来获取用户信息了。</p>
		<p>接口地址：https://www.ifour.net.cn/scau_info/oauth/v1/web/user/get-user-info</p>
		<p>
			<table class="table table-bordered">
				<thead>
					<th>参数名称</th><th>是否必须</th><th>说明</th>
				</thead>
				<tbody>
					<tr>
						<td>app_id</td>
						<td>是</td>
						<td>应用的app_id</td>
					</tr>
					<tr>
						<td>access_token</td>
						<td>是</td>
						<td>接口凭证</td>
					</tr>
					<tr>
						<td>openid</td>
						<td>是</td>
						<td>用户登录成功后返回的唯一登录凭证openid</td>
					</tr>
				</tbody>
			</table>
		</p>
		<p>
			返回值示例（json格式）：
			<table class="table table-bordered">
				<thead>
					<th>名称</th><th>说明</th><th>示例</th>
				</thead>
				<tbody>
					<tr>
						<td>nickname</td>
						<td>用户昵称</td>
						<td>爱做菜的程序员</td>
					</tr>
					<tr>
						<td>avatarUrl</td>
						<td>用户头像</td>
						<td>https://wx.qlogo.cn/mmopen/vi_32/mto2aoyAxibBNqk</td>
					</tr>
					<tr>
						<td>country</td>
						<td>国家</td>
						<td>中国</td>
					</tr>
					<tr>
						<td>province</td>
						<td>省份</td>
						<td>广东</td>
					</tr>
					<tr>
						<td>city</td>
						<td>城市</td>
						<td>广州</td>
					</tr>
					<tr>
						<td>gender</td>
						<td>性别</td>
						<td>0-未知，1-男，2-女</td>
					</tr>
					<tr>
						<td>language</td>
						<td>语言</td>
						<td>zh_CN</td>
					</tr>
				</tbody>
			</table>
		</p>
		<p>错误返回示例：{"status":"-30015","msg":"Invalid app_id"}</p>
	</div>
	<div>
		<span style="color: #F00;">如果大家在使用过程中出现什么问题，欢迎大家加入交流群，群号码：529668978</span>
	</div>
	--end--
	<div>
