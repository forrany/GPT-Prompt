# 让AI助手更加丝滑、顺手

GPT可以渗透在各个领域，不同的人群、不同的工作对于如何利用GPT会有差异。在这里想分享下，作为一个前端开发者，如何打造工作流程中的得力AI助手。

借助强大Chrome插件，优秀的AI助手已经被实现，且体验相当的丝滑

比如在使用搜索引擎时，利用AI帮你总结你的问题，对于一些编程领域的一些指令、命令等问题有着非常好的效果。除此之外，对于网页中所有内容，都可以让AI帮我们进行解释、总结、归纳、翻译等等。

体验是很好的，但问题是它不免费，或者免费的往往有各种各样的限制：

![image-20230630160301176](https://pic-bed-1302552283.cos.ap-guangzhou.myqcloud.com/image-20230630160301176.png)

如果不能很好的解决这个点，似乎很难让“助手”为所有人所用，毕竟大部分都还是习惯“白嫖”
## 吃上免费的午餐(GPT)

在github上，有一个高达41.6K star的项目，[xtekky/gpt4free](https://github.com/xtekky/gpt4free)。项目正如其名称一样简单： 免费使用GPT。它的原理，就是借助市场上免费的GPT（比如Bing、Poe）等，做的一层反向代理。

借助此项目，我们可以完全做一套自己API，实现自己的API Server，然后开发和使用OPEN AI的各种模型。关于这个，我们晚点再说，因为有更简单、易用的方式，有人已经帮我们搭建好了API代理，且具有充足的免费使用额度 FOXGPT。

FOXGPT的官网已经宕了很久了，不知道是不是为了避风头，但是其根据地discord还是保持联络的状态。因此，通过以下几个步骤，就可以轻松拿到代理的API KEY

1. 注册discord账号；
2. 点击邀请链接，加入foxgpt：[邀请链接](https://discord.gg/YBuHTWeD)
3. 在群组中，找到verify频道，点击认证

在左侧verify频道，进入后点击输入验证码，即可完成认证
![企业微信截图_43d7c9b8-8afd-4e58-8bf0-79bd654fba1f](https://pic-bed-1302552283.cos.ap-guangzhou.myqcloud.com/%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_43d7c9b8-8afd-4e58-8bf0-79bd654fba1f.png)

4. 认证后，右侧出现全部的频道，点击bot，并输入`/key`获取密钥

![iShot_2023-06-28_21.26.18.png](https://pic-bed-1302552283.cos.ap-guangzhou.myqcloud.com/blog/iShot_2023-06-28_21.26.18.png)

这样，你就获取了一份`fg`开头的密钥，与open ai 的使用方式一致，无论是使用open ai的api还是直接使用相关应用，只需要将`base_url`替换为代理地址，这里是`https://api.hypere.app`


## 工具加持打造丝滑体验

### 浏览器插件 + Free API = 免费的丝滑体验

安装Chrome插件，ChatGPT Sidebar，并在设置中填写上面获得的密钥和代理URL:

![image-20230629122741981](https://pic-bed-1302552283.cos.ap-guangzhou.myqcloud.com/image-20230629122741981.png)

这样，就获取了一份免费、高效的GPT助手，基本可以无限制的使用助手，并且在配置中，添加自己的日常需要的Prompt。

#### 日常开发常用Prompt

1. Interface 生成器 可以快速、高效的从各类接口或文档中提取Prompt

```
你是一个Typescript的Interface生成器，可以根据所给描述或者JSON，生成该结构的Interface。请以markdown形式返回给我
```

2. LessCode 属性提取 可以从组件的文档中，快速提取组件的属性配置，用于在Lesscode中集成组件

```
将标个内容提取，并将其输出为Json。 参数列的值为Json的key, value为一个object。object包含4个key: type、val、tips分别对应类型、默认值和说明。请以Markdown形式，仅返回Json。
```

### ChatGPT-next-web + 面具 多场景、多助手

开源项目[ChatGPT-Next-Web](https://github.com/Yidadaa/ChatGPT-Next-Web)支持更丰富的预设词，且可自行设置代理，对于不同场景下的应用，有着更好的支持。

这里建议，fork该仓库后，直接点击"Deploy"在Vecel中在线部署，一方面免费在Vecel中部署使用，另一方面通过环境变量的方式注入key和baseurl可以让你随时随地打开页面进行使用，而不用一在不同的电脑使用，都要重新输入一次key, [部署教程](https://github.com/Yidadaa/ChatGPT-Next-Web/blob/main/README_CN.md#%E5%BC%80%E5%A7%8B%E4%BD%BF%E7%94%A8)

如果嫌麻烦，可以使用我部署的服务，只需要填入API Key即可开始使用， [在线地址](https://chat-gpt-next-web-rho-bice-34.vercel.app/)

只需要在设置中，填写相应的key即可(**注：接口地址不要动，我已经在部署时通过环境变量打入。**)


![image-20230630155155392](https://pic-bed-1302552283.cos.ap-guangzhou.myqcloud.com/image-20230630155155392.png)

> 注意：目前测试fotgpt的base-url(https://api.hypere.app/)无法直接在此app中修改，只能通过环境变量注入，否则会报错。

### Prompt推荐

在仓库中，提供了一些我个人日常工作中常用的Prompt，对于前端的开发场景中，还是比较友好的。我自己常用的Prompt在本仓库的.json文件，可以直接在app上导入使用。
![image-20230630155828929](https://pic-bed-1302552283.cos.ap-guangzhou.myqcloud.com/image-20230630155828929.png)
