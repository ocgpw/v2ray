<div class="post-content">
<p>使用 Cloudflare 中转 V2Ray 流量可以避免 IP 被墙，也可以拯救被封的 IP。</p>

<h2 id="前言">前言</h2>

<p>一般而言，除非真的有需求，要不然不建议套 CF，因为套 CF 中转速度太慢了</p>

<p>使用 Cloudflare 中转的速度相对来说是比较慢的，这个是因为线路的问题，无解。</p>

<p>但是使用移动网络的话，可能会使用 Cloudflare 香港节点，理论上会有不错的速度</p>

<p>只有担心 IP 被墙或者 IP 已经被封了，才建议套 CF 中转流量。</p>

<h2 id="安装脚本">安装脚本</h2>

<p>如果已安装，跳过此部分</p>

<p>登录你的 VPS；执行下面的命令：</p>
<pre><code>bash &lt;(wget -qO- -o- https://git.io/v2ray.sh)</code></pre>
<p>如果安装成功，继续</p>

<h2 id="准备">准备</h2>

<p>必须拥有一个域名。</p>

<p>打开：<a href="https://dash.cloudflare.com/sign-up" target="_blank">https://dash.cloudflare.com/sign-up</a></p>

<p>注册一个 Cloudflare 账号，有账号的话你就登录啊</p>

<h2 id="添加域名">添加域名</h2>

<p>注册成功后，登录</p>

<p>为方便理解，可以在 Cloudflare 后台将语言切换成简体中文；并点击添加站点</p>



<img src="https://vip2.loli.io/2023/05/25/yQ3WcnV7HfXN1uL.png" alt="切换中文"  loading="lazy" referrerPolicy="no-referrer">


<p>然后，输入你的域名，添加站点</p>



<img src="https://vip2.loli.io/2023/05/25/feBEkxsCNRGm3Sq.png" alt="添加站点"  loading="lazy" referrerPolicy="no-referrer">


<p>选择 Free 计划，继续</p>



<img src="https://vip2.loli.io/2023/05/25/LSWA1ilDhjBy5ce.png" alt="Free 计划"  loading="lazy" referrerPolicy="no-referrer">


<p>我们现在就添加一个 DNS 记录，名称：<code>ai</code>，IPv4 地址：<code>写你的 VPS IP</code>，代理状态必须关闭，云朵图标为灰色。</p>

<p>提示：你可以使用 <code>v2ray ip</code> 查看你的 VPS IP。</p>



<img src="https://vip2.loli.io/2023/05/25/OcZ4aVfLtkC8KH1.png" alt="添加 DNS 记录"  loading="lazy" referrerPolicy="no-referrer">


<p>Cloudflare 会自动扫描域名的 DNS，此处可能会不同的显示，反正确保刚才添加的记录，代理状态为关闭即可，继续</p>



<img src="https://vip2.loli.io/2023/05/25/AqHRkfBl7gICzZ1.png" alt="查看 DNS 记录"  loading="lazy" referrerPolicy="no-referrer">


<p>更改域名的 Name Servers 服务器为 Cloudflare 给出两组服务器，不同的域名服务商的操作会有一些不同，此处自己弄</p>



<img src="https://vip2.loli.io/2023/05/25/BKMxYOgku7v2PLV.png" alt="更改 Name Servers"  loading="lazy" referrerPolicy="no-referrer">


<p>改完域名的 Name Servers 就点击，<code>完成，检查名称服务器</code></p>

<h2 id="等待生效">等待生效</h2>

<p>更改域名的 Name Servers 服务器生效的时间会有延迟的，耐心等待即可</p>



<img src="https://vip2.loli.io/2023/05/25/TuaQI4LnlFO3DGB.png" alt="等待域名生效"  loading="lazy" referrerPolicy="no-referrer">


<p>在 Cloudflare 后台主页，如果能看到域名下面显示有 <code>有效</code>，那就是生效了</p>

<p>域名生效了，那就是域名正式托管在 Cloudflare 管理。</p>

<h2 id="添加中转配置">添加中转配置</h2>

<p>登录你的 VPS</p>

<p>使用 <code>v2ray add ws ai.233boy.com</code> 添加一个 vmess-ws-tls 配置；记得把 <code>ai.233boy.com</code> 改成你的域名</p>

<p>就是刚才添加记录的那个域名，假设你的域名是 233boy.com ，添加的名称是 ai，域名就是 ai.233boy.com</p>



<img src="https://vip2.loli.io/2023/05/25/dheFzQmofSw7i1A.png" alt="添加中转配置"  loading="lazy" referrerPolicy="no-referrer">


<p>添加成功的话，会显示类似图片的配置</p>

<h2 id="开启中转">开启中转</h2>

<p>在 Cloudflare 后台主页，点击你的域名进去，在左侧选项菜单选择 <code>SSL/TLS</code></p>



<img src="https://vip2.loli.io/2023/05/25/tsxw6HpD2r7ZR1c.png" alt="设置SSL/TLS：完全"  loading="lazy" referrerPolicy="no-referrer">


<p>将 SSL/TLS 加密模式更改为 <code>完全</code></p>

<p>然后在左侧选项菜单选择 <code>DNS</code></p>



<img src="https://vip2.loli.io/2023/05/25/AZ89f3BYdKMJ2uX.png" alt="打开代理状态"  loading="lazy" referrerPolicy="no-referrer">


<p>编辑添加的那个记录，把代理状态打开，即是 <code>已代理</code>，云朵图标为点亮状态，然后保存</p>



<img src="https://vip2.loli.io/2023/05/25/W1MmVt69sZvQzAu.png" alt="代理状态已打开"  loading="lazy" referrerPolicy="no-referrer">


<p>这是更改后的样子，代理状态，已代理，云朵图标点亮。</p>

<h2 id="好了">好了</h2>

<p>把云朵点亮之后，流量就是走的 Cloudflare 中转了。</p>

<p>提醒，把云朵点亮就是流量通过  Cloudflare 中转，点灰云朵图标就是直连，不走  Cloudflare 中转。</p>

<h2 id="获取真实客户端ip">获取真实客户端IP</h2>

<p>考虑到有些人会有某些特殊需求，因为套 CF 了默认情况在查看日志的时候会显示客户端 IP 是 CF 的。</p>

<p>如果你需要获取真实的客户端IP，得更改一下 Caddy 的配置</p>

<p>在 /etc/caddy/233boy/xxx.conf 找到你的 caddy 配置文件，（xxx 指的是你的域名）</p>

<p>默认配置类似如下：</p>
<pre><code>xxx:443 {
reverse_proxy /56f7be67-809f-4f47-8cae-9bffa908adf5 127.0.0.1:2333
import /etc/caddy/233boy/xxx.conf.add
}</code></pre>
<p>最终更改的配置如下：</p>
<pre><code>xxx:443 {
reverse_proxy /56f7be67-809f-4f47-8cae-9bffa908adf5 127.0.0.1:2333 {
header_up X-Real-IP {header.CF-Connecting-IP}
header_up X-Forwarded-For {header.CF-Connecting-IP}
}
import /etc/caddy/233boy/xxx.conf.add
}</code></pre>
<p>原则上，你仅需要更改增加一下 header_up 选项指定 IP 为 CF 转发就好了，</p>

<p>记得不要瞎改别的啊！</p>

<p>改好了要重启一下 Caddy：<code>v2ray restart caddy</code></p>

<h2 id="测速">测速</h2>

<p>你看这速度还行吧</p>



<img src="https://vip2.loli.io/2023/05/25/5QGRJ4qPmOk9nsE.jpg" alt="测试中转速度"  loading="lazy" referrerPolicy="no-referrer">


<p>不可能，绝对不可能（假的</p>

<h2 id="备注">备注</h2>

<p>如果你的 VPS 位置是在美国西海岸的话，速度应该还算可以吧，如果不是在美国西海岸，那么也许速度会很慢</p>

<p>不过好在能防止 IP 被墙，或者让 IP 起死回生，也挺好的，难道不是么？</p>

<p>如果你使用移动网络的话，那么 Cloudflare 的中转节点可能会在香港，速度也许会不错 (不完全保证)。</p>

<h2 id="其他">其他</h2>

<p>添加 DNS 记录的时候，那个名称你可以随便起的，只要解析到你的 VPS IP，添加中转配置时写上你的域名即可</p>

<p>我们只是用了 ai 名称做为示例</p>

<h2 id="懂的都懂">懂的都懂</h2>

<p>文章只是示例了使用 vmess-ws-tls 中转，其他 *TLS 协议也可以中转的，但是我不想写了，拜托兄弟你头脑灵光一点！星不星呀</p>

<p>提示：记得要在左侧选项菜单 <code>网络</code> 里面把所有的选项都打开，比如说 <code>gRPC</code></p>

<p>你也可以换成 vless-ws-tls 协议，可能速度会快一亿亿点哦！</p>

<p>不懂就算了！真是的</p>

<h2 id="优化速度">优化速度</h2>

<p>你可以弄优选 Cloudflare IP 啊，我没弄过，也不需要弄，毕竟你看我测速也还行，够用了。</p>

<h2 id="v2ray-脚本说明">V2Ray 脚本说明</h2>

<p>请看：<a href="https://github.com/233boy/v2ray/wiki/V2Ray一键安装脚本" target="_blank">V2Ray一键安装脚本</a></p>

<p>哎呀，虽然脚本很好用，但是为了你能更加了解掌握各种使用技巧，还是建议看一虾吧！</p>

<h2 id="结束">结束</h2>

<p>明明这么简单的东西，看不懂的建议把电脑砸了，然后去报读幼儿园。</p>

<p>复制粘贴我文章的抄袭狗没鸡鸡！</p>
</div>