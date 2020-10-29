# wp_starter_with_docker

WordPress開発用のdocker-compose設定ファイルです。

## Dockerをいれます

[DockerDesktop](https://www.docker.com/get-started)

## 起動

このリポジトリをcloneしDockerでdocker-compose

```
cd 任意のディレクトリ
git clone https://github.com/technotework/wp_starter_with_docker.git .
docker-compose up -d
```

以下に接続してWordPressをセットアップ

```
localhost:8080
```

## docker-compose

docker-composeで以下が起動します。

- db  mySQLイメージ
- wordpress WordPressイメージ
- web
  - phpイメージに以下を追加してBuildするDockerFile
    - Node.js
    - git
    - composer
      - phpcs
      - wp-coding-standards

WP用サーバーの、wordpressイメージ内 /var/www/html/wp-content を
開発環境用である、webイメージにマウントして共有しています。

VSCodeのリモートエクスプローラーなどで "web" のコンテナを開きます。
/var/www/html/wp-content/themes/　がテーマフォルダなので、

```
mkdir /var/www/html/wp-content/themes/myTheme
```
などをつくって、VSCodeで開き、myTheme以下をgit管理してテーマ開発に使います。

また、プラグインやメディアなどは下記ディレクトリなので、別途バージョン管理するのもいいと思います。

```
cd /var/www/html/wp-content/
```

## PHPCSとWP規約

PHPCSの場所

```
which phpcs
/root/.composer/vendor/bin/phpcs
```

WPコーディング規約の場所

```
/root/.composer/vendor/wp-coding-standards/wpcs
```

PHPCS用VSCodeエクステンションはいろいろあるが
[wongjn.php-sniffer](https://marketplace.visualstudio.com/items?itemName=wongjn.php-sniffer)を使った。
PHP Sniffer: Auto Detect をチェック。 PHP Sniffer: Standard にWordPressを設定。
いちおう自動で探してくれるっぽい。

VSCodeの設定のJSONのPHPCSのところ

```
{
    "phpSniffer.autoDetect": true,
    "phpSniffer.run": "onType",
    "phpSniffer.standard": "WordPress",
    "[php]": {
        "editor.defaultFormatter": "wongjn.php-sniffer"
    }
}
```
