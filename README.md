# PyToolkit

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