# ChatGPT-Next-Web

## 这是什么
这是一键免费部署你的私人 ChatGPT 网页应用的项目，你可以在这里看到一个[示例](https://chatgpt-next-web.vercel.app/)。

## 在线部署
+ 准备好你的 OpenAI API Key;
+ 打开 https://github.com/Yidadaa/ChatGPT-Next-Web
+ 点击右侧按钮开始部署： Deploy with Vercel，直接使用 Github 账号登录即可，记得在环境变量页填入 API Key 和页面访问密码 CODE；
+ 部署完毕后，即可开始使用；
+ （可选）绑定自定义域名：Vercel 分配的域名 DNS 在某些区域被污染了，绑定自定义域名即可直连。
  
```{note}
CODE （可选）访问密码，可选，可以使用逗号隔开多个密码。

```

```{warning}
如果不填写此项，则任何人都可以直接使用你部署后的网站，可能会导致你的 token 被急速消耗完毕，建议填写此选项。
```

## 容器部署 (Docker)
```注意：docker 版本在大多数时间都会落后最新的版本 1 到 2 天，所以部署后会持续出现“存在更新”的提示，属于正常现象。```

```
docker pull yidadaa/chatgpt-next-web

docker run -d -p 3000:3000 \
   -e OPENAI_API_KEY="sk-xxxx" \
   -e CODE="页面访问密码" \
   yidadaa/chatgpt-next-web
```
你也可以指定 proxy：
```
docker run -d -p 3000:3000 \
   -e OPENAI_API_KEY="sk-xxxx" \
   -e CODE="页面访问密码" \
   --net=host \
   -e PROXY_URL="http://127.0.0.1:7890" \
   yidadaa/chatgpt-next-web
   ```

## 本地部署
在控制台运行下方命令：
``
bash <(curl -s https://raw.githubusercontent.com/Yidadaa/ChatGPT-Next-Web/main/scripts/setup.sh)
``