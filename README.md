# PyToolkit

## バージョニング

### バージョン番号の形式

このプロジェクトでは以下の形式でバージョン番号を付与します：

```
vYYYY.MM.DD.XX
```

- `v`: 固定の接頭辞
- `YYYY`: 年（4桁）
- `MM`: 月（2桁、01-12）
- `DD`: 日（2桁、01-31）
- `XX`: 同日中の更新番号（2桁、01から開始）

### バージョン番号の例

```bash
v2025.07.12.01  # 2025年7月12日の最初のリリース
v2025.07.12.02  # 2025年7月12日の2回目のリリース
v2025.07.13.01  # 2025年7月13日の最初のリリース
```

### バージョンタグの作成

```bash
# 新しいバージョンタグを作成
git tag -a v2025.07.12.01 -m "機能追加: Option型の実装"
git push origin v2025.07.12.01

# 同日中の2回目の更新
git tag -a v2025.07.12.02 -m "バグ修正: Result型のエラーハンドリング"
git push origin v2025.07.12.02
```

## インストール方法

### GitHubから直接インストール

#### 最新版（mainブランチ）
```bash
pip install git+https://github.com/username/pytoolkit.git
```

#### 特定のブランチを指定
```bash
pip install git+https://github.com/username/pytoolkit.git@develop
pip install git+https://github.com/username/pytoolkit.git@feature-branch
```

#### 特定のタグを指定
```bash
pip install git+https://github.com/username/pytoolkit.git@v1.0.0
pip install git+https://github.com/username/pytoolkit.git@v2.1.0
```

#### uvを使用する場合
```bash
uv add git+https://github.com/username/pytoolkit.git
uv add git+https://github.com/username/pytoolkit.git@develop
uv add git+https://github.com/username/pytoolkit.git@v1.0.0
```

### 注意事項
- プライベートリポジトリの場合は、適切な認証が必要です
- SSHキーが設定されている場合は、`git+ssh://` を使用することも可能です
- リポジトリのURLは実際のものに置き換えてください

## サブモジュールの管理

### サブモジュールの追加
```bash
git submodule add <リポジトリURL> <サブモジュール名>
```

例：
```bash
git submodule add https://github.com/username/async-worker.git async-worker
git submodule add https://github.com/username/meta2package.git meta2package
```

### サブモジュールの確認
```bash
# サブモジュールの状態確認
git submodule status

# サブモジュールの詳細確認
git submodule

# .gitmodulesファイルの確認
cat .gitmodules
```

### サブモジュールの更新
```bash
# 特定のサブモジュールを更新
git submodule update --remote <サブモジュール名>

# 全てのサブモジュールを更新
git submodule update --remote

# サブモジュールの初期化と更新
git submodule update --init --recursive
```

### サブモジュールの削除
```bash
# サブモジュールの削除（段階的に実行）
git submodule deinit <サブモジュール名>
git rm <サブモジュール名>
rm -rf .git/modules/<サブモジュール名>
```

例：
```bash
git submodule deinit async-worker
git rm async-worker
rm -rf .git/modules/async-worker
```

### クローン時のサブモジュール取得
```bash
# サブモジュールを含めてクローン
git clone --recurse-submodules <リポジトリURL>

# 既存のクローンにサブモジュールを取得
git submodule update --init --recursive
```

## タグの管理

### タグの追加
```bash
# 軽量タグ（タグ名のみ）
git tag <タグ名>

# 注釈付きタグ（推奨）
git tag -a <タグ名> -m "タグの説明"

# 特定のコミットにタグを追加
git tag -a <タグ名> <コミットハッシュ> -m "タグの説明"
```

例：
```bash
git tag -a v1.0.0 -m "Initial release"
git tag -a v1.1.0 -m "Bug fixes and improvements"
git tag -a v2.0.0 879ce3a -m "Major update with breaking changes"
```

### タグの確認
```bash
# 全てのタグを表示
git tag

# パターンでタグを検索
git tag -l "v1.*"

# タグの詳細情報を表示
git show <タグ名>

# リモートのタグを確認
git ls-remote --tags origin

# リモートのタグを取得してローカルに反映
git fetch --tags

# リモートとローカルのタグを比較
git tag -l | sort
git ls-remote --tags origin | awk '{print $2}' | sed 's/refs\/tags\///' | sort
```

### タグのリモートへの送信
```bash
# 特定のタグを送信
git push origin <タグ名>

# 全てのタグを送信
git push origin --tags

# 注釈付きタグのみを送信
git push origin --follow-tags
```

### タグの削除
```bash
# ローカルのタグを削除
git tag -d <タグ名>

# リモートのタグを削除
git push origin --delete <タグ名>

# または
git push origin :<タグ名>
```

例：
```bash
# ローカルとリモートの両方からタグを削除
git tag -d v1.0.0
git push origin --delete v1.0.0
```