# 総合オンラインストレージサービス DECO検証環境

[総合オンラインストレージサービス DECO](https://www.deco-project.org/)をDockerで動作させて検証してみる環境です。
おまけ的にDockerイメージができます。

## 使い方
### ビルド
```
docker-compose build
```

### シークレットキー生成
```
docker-compose run --rm web rake secret

```

### 設定を生成 
SECRET_KEY_BASEに上記で生成したキーをセット

```.env.production
SECRET_KEY_BASE=
DECO_DATABASE_PASSWORD=password
RAILS_ENV=production
```

### 起動
```
docker-compose up -d
```


### DBデータ準備
```
docker-compose run --rm web rails db:migrate RAILS_ENV=production
docker-compose run --rm web rake db:seed RAILS_ENV=production
```

## アクセス方法
* [サイト](http://localhost:8888/)
* [管理サイト](http://localhost:8889/sys_top)
* [](http://localhost:8889/)
