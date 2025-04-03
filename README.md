# github_cdn
代码功能说明
GitHub文件代理功能：

当访问非根路径时，会代理请求到GitHub的raw文件服务
支持两种访问方式：
直接使用完整GitHub路径（如 /https://raw.githubusercontent.com/user/repo/branch/file）
使用环境变量配置的默认仓库（通过 GH_NAME, GH_REPO, GH_BRANCH）
根路径访问：

访问根路径 / 时，返回一个伪装成nginx的欢迎页面
这可以增加Worker的隐蔽性
环境变量配置：

GH_NAME: GitHub用户名
GH_REPO: 仓库名
GH_BRANCH: 分支名（可选）
这些变量可以在Worker的设置中配置
使用示例
假设Worker地址是 https://my-worker.example.com：

直接访问仓库文件：

https://my-worker.example.com/user/repo/branch/file.txt
使用完整GitHub路径：

https://my-worker.example.com/https://raw.githubusercontent.com/user/repo/branch/file.txt
如果配置了环境变量：

GH_NAME = “user”
GH_REPO = “repo”
GH_BRANCH = “branch”
那么可以直接访问：

https://my-worker.example.com/file.txt
这个简化版去掉了所有token相关的逻辑，只支持访问公开的GitHub仓库文件。
