该命令行工具提供了简化生成 **shell 命令、代码片段、文档**,消除了对外部资源(如 Google 搜索)的需求,支持 Linux、macOS、Windows 和兼容所有主要 Shells 如 PowerShell、CMD、Bash、Zsh 等。

https://github.com/TheR1D/shell_gpt/assets/16740832/9197283c-db6a-4b46-bfea-3eb776dd9093

## 安装

```shell
pip install shell-gpt
```

默认情况下,ShellGPT 使用 OpenAI 的 API 和 GPT-4 模型。您需要一个 API 密钥,您可以生成一个 [这里](https://beta.openai.com/account/api-keys).您将被提示获取您的密钥,然后将被存储在 `~/.config/shell_gpt/.sgptrc。 OpenAI API 不是免费的,请参阅 [OpenAI 定价](https://openai.com/pricing)以获取更多信息。

> [!TIP]
> 要使用本地模型,你需要运行自己的LLM后端服务器,如 [Ollama](https://github.com/ollama/ollama). 要与Ollama设置ShellGPT,请遵循这个全面的 [指南](https://github.com/TheR1D/shell_gpt/wiki/Ollama)。
> 
> **❗️请注意,ShellGPT 未针对本地模型优化,可能无法按预期工作。

## 使用

**ShellGPT**旨在快速分析和检索信息,可用于从技术配置到一般知识的简单请求。

```shell
sgpt "What is the fibonacci sequence"
# -> The Fibonacci sequence is a series of numbers where each number ...
```

ShellGPT 接受 stdin 和命令行参数的提示,无论您是否喜欢通过终端输入或将其直接指定为参数,‘sgpt’ 都会让你被覆盖,例如,您可以轻松地基于 diff 生成 git commit 消息:

```shell
git diff | sgpt "Generate git commit message, for my changes"
# -> Added main feature details into README.md
```

例如,我们可以使用它快速分析日志,识别错误,并获得可能的解决方案的建议:

```shell
docker logs -n 20 my_app | sgpt "check logs, find errors, provide possible solutions"
```

```text
Error Detected: Connection timeout at line 7.
Possible Solution: Check network connectivity and firewall settings.
Error Detected: Memory allocation failed at line 12.
Possible Solution: Consider increasing memory allocation or optimizing application memory usage.
```

您还可以使用各种重定向操作器来传输输入:

```shell
sgpt "summarise" < document.txt
# -> The document discusses the impact...
sgpt << EOF
What is the best way to lear Golang?
Provide simple hello world example.
EOF
# -> The best way to learn Golang...
sgpt <<< "What is the best way to learn shell redirects?"
# -> The best way to learn shell redirects is through...
```

### Shell 命令

你有没有发现自己忘记了常见的 shell 命令,例如“查找”,并需要在线搜索语法?使用“--shell”或“shortcut-s”选项,您可以直接在终端快速生成和执行您需要的命令。

```shell
sgpt --shell "find all json files in current folder"
# -> find . -type f -name "*.json"
# -> [E]xecute, [D]escribe, [A]bort: e
```

Shell GPT 知道您正在使用的操作系统,它会为您所拥有的特定系统提供 shell 命令,例如,如果您要求“sgpt”更新您的系统,它会返回基于您的操作系统的命令。
```shell
sgpt -s "update my system"
# -> sudo softwareupdate -i -a
# -> [E]xecute, [D]escribe, [A]bort: e
```


