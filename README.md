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