# LAMP2

PHP開発環境を提供する。
## 使い方
1. `UID`を外部から設定するため`.env`を作成する。
    ```
    # MacOS の場合
    UID=33

    # Windows10 WSL2 の場合
    UID=1000
    ```
1. `composer build`を実行
1. 生成された`image`を自身のプロジェクトに組み込んで使う。
    - `example`のような`docker-compose.yml`を作ればいい。
    - 設定を変えたい場合は、`vhosts`を差し替えればいい。
