# SonarQube Sample

SonarQubeをお手軽に試してみたかったので作りました。

## 参考サイト

- [DockerでSonarQubeを入れる！](https://qiita.com/takao-takass/items/5d54768ad0d315d3dad4)
- [Alpine Linuxのパッケージ管理システムapkについて理解を深める](https://blog.kasei-san.com/entry/2020/08/25/084430)
- [今更だけどSonarQubeをDockerで動かす](https://qiita.com/ProjectEuropa/items/b9df95e3190b22aaa69f)
- [Install Sonar Scanner in Alpine](https://gist.github.com/henrist/302eeb29233ed45e8d2a119386fd394d)

## Get started

1. `./repositories` 配下に解析したいリポジトリをクローンする。
2. 以下を実行する。

```sh
docker compose build
docker compose up -d
```

### 接続

`http://{ip_address}:9001/`

ログイン: `admin` / `admin`

右上の "Add Project" を押して画面の指示に従う。

### コード解析の実行

```sh
# コンテナに接続
docker compose exec sonarqube bash

# 解析したいリポジトリのルートへ移動
cd repositories/xxxx
```

SonarQubeの管理画面で"Add Project"して進む画面に以下のようなコマンドが表示されるので、それを実行する。

```sh
sonar-scanner \
  -Dsonar.projectKey={projcet_name} \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://{ip_address}:9001 \
  -Dsonar.login={token}
```
