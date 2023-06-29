# 吃上免费的午餐(GPT)

在github上，有一个高达41.6K star的项目，叫[gpt4free]([GitHub - xtekky/gpt4free: The official gpt4free repository | various collection of powerful language models](https://github.com/xtekky/gpt4free))。项目正如其名称一样简单： 免费使用GPT。它的原理，就是借助市场上免费的GPT（比如Bing、Poe）等，做的一层反向代理。

借助此项目，我们可以完全做一套自己API，实现自己的API Server，然后开发和使用OPEN AI的各种模型。关于这个，我们晚点再说，因为有更简单、易用的方式，有人已经帮我们搭建好了API代理，且具有充足的免费使用额度 FOXGPT。

FOXGPT的官网已经宕了很久了，不知道是不是为了避风头，但是其根据地discord还是保持联络的状态。因此，通过以下几个步骤，就可以轻松拿到代理的API KEY

1. 注册discord账号；
2. 点击邀请链接，加入foxgpt：[邀请链接](https://discord.gg/YBuHTWeD)
3. 在群组中，找到verify频道，点击认证
4. 认证后，右侧出现全部的频道，点击bot，并输入`/key`获取密钥

![iShot_2023-06-28_21.26.18.png](https://pic-bed-1302552283.cos.ap-guangzhou.myqcloud.com/blog/iShot_2023-06-28_21.26.18.png)

这样，你就获取了一份`fg`开头的密钥，与open ai 的使用方式一致，无论是使用open ai的api还是直接使用相关应用，只需要将`base_url`替换为代理地址，这里是`https://api.hypere.app/`

最后，安装Chrome插件，ChatGPT Sidebar，并在设置中填写上面获得的密钥和代理URL:

![image-20230629122741981](https://pic-bed-1302552283.cos.ap-guangzhou.myqcloud.com/image-20230629122741981.png)

这样，就获取了一份免费、高效的GPT助手，基本可以无限制的使用助手，并且在配置中，添加自己的日常需要的Prompt。

### 日常开发常用Prompt

1. Interface 生成器 可以快速、高效的从各类接口或文档中提取Prompt

```
你是一个Typescript的Interface生成器，可以根据所给描述或者JSON，生成该结构的Interface。请以markdown形式返回给我
```

2. LessCode 属性提取 可以从组件的文档中，快速提取组件的属性配置，用于在Lesscode中集成组件

```
将标个内容提取，并将其输出为Json。 参数列的值为Json的key, value为一个object。object包含4个key: type、val、tips分别对应类型、默认值和说明。请以Markdown形式，仅返回Json。
```