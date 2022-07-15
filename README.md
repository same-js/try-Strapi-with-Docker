# strapi 
Headless CMS である strapi を色々な方法で起動してみる。

次の3つのディレクトリがある。

## strapi-strapi 

「[strapi/strapi](https://hub.docker.com/r/strapi/strapi)」という公式イメージを使用して起動する。

Docker Image が strapi のインストールまで面倒を見てくれるが、v3にしか対応していない。

最初は before ディレクトリのように docker-compose.yml だけを入れた状態にしておく。
その状態で以下の操作をおこなっていくと、 最終的に after ディレクトリの状態になる。

### Docker起動
```bash
$ cd strapi-strapi/Docker
$ docker compose pull
$ docker compose up
```

```
strapi_1  | Using strapi 3.6.8
strapi_1  | No project found at /srv/app. Creating a new strapi project
strapi_1  | Creating a project from the database CLI arguments.
strapi_1  | Creating a new Strapi application at /srv/app.
strapi_1  | Creating files.
strapi_1  | - Installing dependencies:
```

まで表示された後、しばらく（10分ぐらい）待たされる。特にログは更新されないので、エラーで止まったかと勘違いするが、辛抱強く待つこと。

下記のように表示されれば、インストール成功。

```
strapi_1  | Dependencies installed successfully.
strapi_1  | 
strapi_1  | Your application was created at /srv/app.
strapi_1  | 
strapi_1  | Available commands in your project:
strapi_1  | 
strapi_1  |   yarn develop
strapi_1  |   Start Strapi in watch mode.
strapi_1  | 
strapi_1  |   yarn start
strapi_1  |   Start Strapi without watch mode.
strapi_1  | 
strapi_1  |   yarn build
strapi_1  |   Build Strapi admin panel.
strapi_1  | 
strapi_1  |   yarn strapi
strapi_1  |   Display all available commands.
strapi_1  | 
strapi_1  | You can start by doing:
strapi_1  | 
strapi_1  |   cd /srv/app
strapi_1  |   yarn develop
strapi_1  | 
strapi_1  | Starting your app...
strapi_1  | Building your admin UI with development configuration ...
strapi_1  | ℹ Compiling Webpack
```

もうしばらく待つ。

```
strapi_1  |  Project information
strapi_1  | 
strapi_1  | ┌────────────────────┬──────────────────────────────────────────────────┐
strapi_1  | │ Time               │ Fri Jul 15 2022 11:59:22 GMT+0000 (Coordinated … │
strapi_1  | │ Launched in        │ 29549 ms                                         │
strapi_1  | │ Environment        │ development                                      │
strapi_1  | │ Process PID        │ 329                                              │
strapi_1  | │ Version            │ 3.6.8 (node v14.16.0)                            │
strapi_1  | │ Edition            │ Community                                        │
strapi_1  | └────────────────────┴──────────────────────────────────────────────────┘
strapi_1  | 
strapi_1  |  Actions available
strapi_1  | 
strapi_1  | One more thing...
strapi_1  | Create your first administrator 💻 by going to the administration panel at:
strapi_1  | 
strapi_1  | ┌─────────────────────────────┐
strapi_1  | │ http://localhost:1337/admin │
strapi_1  | └─────────────────────────────┘
```

`http://localhost:1337/admin` とログに表示されれば、完全に起動OK。このURLでstrapi管理画面にログインできるようになる。

data ディレクトリに は MySQLの実データが置かれるので、ここはGit管理対象外とする。（`.gitignore` を置く）



## strapi-base

「[strapi/base](https://hub.docker.com/r/strapi/base)」という公式イメージを使用して起動する。
インストール自体は CLI で行う必要があり、イメージが面倒をみるのはローカル環境での起動のみ。

