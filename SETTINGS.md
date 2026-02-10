# GitHubリポジトリ設定ガイド

## 公開リポジトリで編集権限を制限する方法

このドキュメントでは、GitHubリポジトリを一般公開しながら、リポジトリ作成者のみが編集できるように設定する方法を説明します。

## 1. リポジトリの公開設定

### Settings → General → Danger Zone

1. GitHubリポジトリのSettingsページを開く
2. 一番下の「Danger Zone」セクションまでスクロール
3. 「Change repository visibility」をクリック
4. 「Make public」を選択
5. リポジトリ名を入力して確認

**注意**: プライベートリポジトリをパブリックにすると、すべてのコードと履歴が一般公開されます。機密情報が含まれていないか必ず確認してください。

## 2. コラボレーター設定

### Settings → Collaborators and teams

デフォルトでは、パブリックリポジトリは以下の設定になっています：

- **リポジトリオーナー（作成者）**: すべての権限（読み取り、書き込み、管理）
- **一般ユーザー**: 読み取り専用（クローン、閲覧可能）

### 編集権限を制限するには

パブリックリポジトリでは、以下の操作により編集権限をオーナーのみに制限できます：

1. **コラボレーターを追加しない**
   - Settings → Collaborators にコラボレーターを追加しない
   - これにより、オーナーのみが直接編集できます

2. **ブランチ保護ルールの設定**（オプション）
   - Settings → Branches → Add rule
   - `main`または`master`ブランチに保護ルールを設定
   - "Require pull request reviews before merging"を有効化
   - "Restrict who can push to matching branches"を有効化してオーナーのみを指定

## 3. その他の推奨設定

### Pull Request設定

Settings → General → Pull Requests:

- ☑ Allow merge commits
- ☑ Allow squash merging
- ☑ Allow rebase merging
- ☑ Always suggest updating pull request branches
- ☑ Automatically delete head branches

### Issues設定

Settings → General → Features:

- ☑ Issues（外部からのフィードバックを受け取るため）
- ☐ Projects（必要に応じて）
- ☐ Wiki（必要に応じて）

## 4. アクセス権限の種類

GitHubのリポジトリには以下のアクセスレベルがあります：

| 権限レベル | 説明 |
|-----------|------|
| Read | コードの閲覧、クローン、Issueの作成が可能 |
| Triage | Readに加え、Issueとプルリクエストの管理が可能 |
| Write | Triageに加え、コードのプッシュが可能 |
| Maintain | Writeに加え、一部の設定変更が可能 |
| Admin | すべての権限（設定変更、削除など） |

パブリックリポジトリで何も設定しない場合：
- **オーナー**: Admin権限
- **一般ユーザー**: Read権限（フォークしてPull Requestは可能）

## 5. コントリビューションの受け付け方

編集権限を制限していても、以下の方法でコントリビューションを受け付けることができます：

1. **Fork & Pull Request**
   - 外部ユーザーはリポジトリをフォーク
   - フォークしたリポジトリで変更を加える
   - オリジナルリポジトリにPull Requestを作成
   - オーナーがレビュー・承認してマージ

2. **Issues**
   - バグ報告や機能提案をIssueとして受け付け
   - オーナーが内容を確認して対応

## 6. セキュリティ設定

Settings → Security & analysis:

- ☑ Dependency graph
- ☑ Dependabot alerts
- ☑ Dependabot security updates

これらを有効にすることで、セキュリティの脆弱性を自動検出できます。

## まとめ

公開リポジトリで編集権限をオーナーのみに制限するには：

✅ リポジトリをPublicに設定
✅ コラボレーターを追加しない
✅ ブランチ保護ルールを設定（オプション）
✅ Issuesを有効にしてフィードバックを受け付ける

この設定により、コードを一般公開しながら品質管理を維持できます。
