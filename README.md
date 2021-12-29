##### ※ VsCode(エディターの拡張機能)と併用する際の注意点
Prettierとリンターの自動フォーマット機能の競合を防ぐ必要があるので、リンターの拡張機能(EsLint、stylelint-plus)のみ有効にする。

# 必要なパッケージのインストール
prettier、eslint、stylelint本体と併せて、以下のパッケージをインストールする。
#### PrettierとESLintの連携
- **eslint-plugin-prettier**
  - Prettier のチェックを同時に実行
- **eslint-config-prettier**
  - Prettier と競合するルールを無効化

#### PrettierとStyleLintの連携
- **stylelint-prettier**
  - Prettier のチェックを同時に実行
- **stylelint-config-standard**
  - 一般的なCSSのコーディング規約集
- **stylelint-config-prettier**
  - Prettier と競合するルールを無効化
- **stylelint-order**
  - CSSプロパティをABC順に並べる

> ⚠️ **Warning** <br/>
> stylelint-plus と stylelint-config-prettier のバージョンによっては、ファイル保存時に「Undefined rule unicode-bom」エラーが発生する。stylelint-config-prettier のバージョンを変更するなどして対応する必要がある。

# Git と連携するために必要なツール
- **husky**
  - git hooks を package.json から設定するためのツール。git から lint-staged を呼び出すために使用する。  
- **lint-staged**
  - ステージングしたファイルに対してコマンドを実行するためのツール。設定したリンターがコミット時に実行される。

```json:package.json
{
  ...省略
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "*.css": "stylelint",
    "*.js": "eslint"
  },
  "devDependencies": {
    "eslint": "^7.17.0",
    "eslint-config-prettier": "^7.1.0",
    "eslint-plugin-prettier": "^3.3.1",
    "husky": "^4.3.7",
    "lint-staged": "^10.5.3",
    "prettier": "^2.2.1",
    "stylelint": "^13.8.0",
    "stylelint-config-prettier": "7.0.0",
    "stylelint-config-standard": "^20.0.0",
    "stylelint-order": "^4.1.0",
    "stylelint-prettier": "^1.1.2"
  }
}
```
