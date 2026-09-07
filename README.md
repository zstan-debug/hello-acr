# hello-acr

最小练习：个人版 ACR 自动构建。成功标准是个人版仓库里能 `docker pull` 到这次构建的 tag。

不要绑公司 `museflow-server` / `museflow-vue`，也不要把镜像推进 `museflow-registry.cn-shanghai.cr.aliyuncs.com`。

## 1. 单独建一个 Git 仓库

把本目录三个文件放进一个**新的空仓库**（个人 Codeup 或个人 GitHub 均可），默认分支用 `main`。不要塞进 MuseFlow 现有仓库。

## 2. 控制台用个人版实例

1. 打开 [容器镜像服务](https://cr.console.aliyun.com)
2. 地域选你方便的，例如华东2（上海）
3. 实例选 **个人版**（默认实例），不要进企业版 `museflow-registry`
4. 创建一个命名空间、一个镜像仓库（例如 `practice` / `hello-acr`）
5. 代码源绑上一步那个 Git 仓库；开启「代码变更时自动构建」

## 3. 一条构建规则

| 项 | 建议 |
| --- | --- |
| 类型 | Branch |
| 分支 | `main` |
| Dockerfile 目录 | `/` |
| 镜像版本 | 用 git 短 SHA，或再加一个 `latest` 当指针 |

保存后往 `main` 推一次提交（或点「立即构建」）。

## 4. 怎样算成功

构建完成后，在本机 Docker Desktop：

```bash
docker login registry.cn-shanghai.aliyuncs.com
docker pull registry.cn-shanghai.aliyuncs.com/<命名空间>/hello-acr:<tag>
```

地域若不是上海，把域名里的 `cn-shanghai` 换成控制台显示的地域。能 pull 下来即成功。不要部署 MuseFlow，也不要跑 `museflow-deploy.sh`。
