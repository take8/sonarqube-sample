# SonarQube Sample

SonarQubeをお手軽に試してみたかったので作りました。

## 参考サイト

- [DockerでSonarQubeを入れる！](https://qiita.com/takao-takass/items/5d54768ad0d315d3dad4)
- [Alpine Linuxのパッケージ管理システムapkについて理解を深める](https://blog.kasei-san.com/entry/2020/08/25/084430)
- [今更だけどSonarQubeをDockerで動かす](https://qiita.com/ProjectEuropa/items/b9df95e3190b22aaa69f)

## Get started

`./repositories` 配下に解析したいリポジトリをクローンする。

```sh
docker compose build
docker compose up -d
```

### 接続

`http://{ip_address}:9001/`

ログイン: `admin` / `admin`

右上の "Add Project" を押して画面の指示に従う。

```sh
# コンテナに接続
docker exec -it -u root sonar2 bash

apk add wget unzip vim git
# JS, TSの解析は以下も必要
apk add nodejs npm

# sonar-scanner のダウンロード、解凍
wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.6.2.2472-linux.zip
unzip sonar-scanner-cli-4.6.2.2472-linux.zip

# .bashrc を編集
vim ~/.bashrc
```

`.bashrc` に以下を追記

```sh
export PATH="$PATH:/opt/sonarqube/sonar-scanner-4.6.2.2472-linux/bin"
```

```sh
# 再読み込み
source ~/.bashrc
```

### コード解析の実行

SonarQubeの管理画面で"Add Project"して進む画面に以下のようなコマンドが表示されるので、それを実行する。

```sh
sonar-scanner \
  -Dsonar.projectKey={projcet_name} \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://{ip_address}:9001 \
  -Dsonar.login={token}
```
