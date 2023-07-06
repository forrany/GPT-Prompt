## 最新进展

很可惜，近期本仓库所使用的FOXGPT的API不太稳定，会出现宕机，无法请求的问题。因此，为了能维持日常使用，这里不再依赖单一的API，而是提供更多的备用选项，以此来避免当某个免费API宕机而无法使用的问题。

目前主要有两个渠道：

- FoxGPT： 基本无限制，完全没有任何使用压力，但是2023年7月份后开始不太稳定，偶尔宕机；
- ChatAnyWhereAPI：免费的API限制为120次/Hour, 但是个人的日常使用应该是完全没问题，相对稳定，且支持GPT Slide（下文会介绍该插件）拉取Model接口。

FoxGPT及其API获取方法下文会详细介绍，这里主要更新下其备用借口ChatAnyWhere API的方法。

### 备用接口
备用接口仓库在这里：[GPT-API-FREE](https://github.com/chatanywhere/GPT_API_free)。 

快速使用方法：

1. [点击获取免费Key](https://api.chatanywhere.cn/v1/oauth/free/github/render)
2. 在使用的App或者插件中修改base-url为以下其中之一（App的使用会在下文详细介绍

​	转发Host1: https://api.chatanywhere.cn (国外服务器使用)

​	转发Host2: https://api.chatanywhere.com.cn (国内中转，延时更低，推荐)

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

![image-20230630194337286](https://pic-bed-1302552283.cos.ap-guangzhou.myqcloud.com/image-20230630194337286.png)

这样，就获取了一份免费、高效的GPT助手，基本可以无限制的使用助手，并且在配置中，添加自己的日常需要的Prompt。



#### 使用最新模型: gpt-3.5-16k-0613

foxgpt提供的转发接口，仅代理了官方的`/v1/chat`接口，获取模型列表的接口`/v1/model`并没有做映射，因此，在首次填入API Key和URL时，会报错（如下图），但是报错并不影响侧栏的使用，默认使用的模型是`gpt-3.5-turbo`。

<img src="https://pic-bed-1302552283.cos.ap-guangzhou.myqcloud.com/image-20230702002152382.png" alt="image-20230702002152382" style="zoom: 33%;" />



但是，fotgpt的免费API是支持最新的`gpt-3.5-turbo-16k-0613`的，相比于`gpt-3.5-turbo`,不仅提高了context上限，也更节省token。所以，为了能够使用最新的模型，需要在拉取列表的时候，对返回数据进行一下修改，只要能选上`gpt-3.5-turbo-16k-0613`模型，以后就可以一直使用了。

因为接口无法调通，这里介绍使用抓包替换Response的方法实现来实现模型的切换。



1. 模型列表数据

模型列表数据已经命名为[model-list.json](https://github.com/forrany/GPT-Prompt/blob/master/model-list.json),并放在了仓库的同名文件中。

2. 抓包软件

这里Mac推荐使用Charles软件抓包、替换返回数据； Windows可以使用Fiddler。

3. Charles替换response示例

Charles和Fiddler是非常优秀的抓包软件，使用教程这里不再赘述。这里以Charles抓包作为示例，开始抓包后，找到`https://api.hypere.app`的`/v1/models`接口，右键点击`Map Local...`，并在弹出的窗口中，将其替换步骤一下载的`model-list.json`，如下图

![image-20230702003712772](https://pic-bed-1302552283.cos.ap-guangzhou.myqcloud.com/image-20230702003712772.png)

4. 替换后，再次返回插件设置，并点击更新按钮，成功获得模型列表，并选择最新的模型，然后 Just Enjoy It！



![image-20230702003912306](https://pic-bed-1302552283.cos.ap-guangzhou.myqcloud.com/image-20230702003912306.png)



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