# GitHubのプライベートリポジトリで共同開発（チーム開発）

GitHubのプライベートリポジトリで共同開発（チーム開発）を行うための設定方法と手順を解説します。<br>
主な作業は「リポジトリ作成」「メンバー招待」「クローン・開発」「プルリクエスト（PR）」のフローで行います。

## 1. 前提条件
- メンバー全員がGitHubアカウントを持っていること。
- プロジェクトの管理者がプライベートリポジトリを作成済みであること。 

## 2. 共同開発者の招待手順（管理者側）
プライベートリポジトリは、明示的に許可されたユーザーのみがアクセスできます。<br>

1. GitHub上で、対象のプライベートリポジトリに移動ます。
2. 上部メニューの「Settings」タブをクリックします。3. 左サイドバーの「Access」セクションにある「Collaborators」を選択します。
4. 必要に応じてGitHubのパスワードを再入力します。
5. 「Add people」ボタンをクリックします。
6. 招待したい人の「GitHubユーザー名」「メールアドレス」を入力し、候補から選択します。
7. 「Add [ユーザー名] to this repository」をクリックして招待を送信します。 

## 3. 招待の承認（共同開発者側）
招待されたメンバーにメール、またはGitHubの通知（右上のベルマーク）で招待が届きます。

1. 通知を開き、「View invitation」をクリックします。
2. リポジトリページが表示されるので、「Accept invitation」をクリックして参加します。 

## 4. 共同開発の流れ（チーム開発の手順）
招待が完了したら、以下の手順で開発を進めます。

1. リポジトリのクローン (ローカルへの取得)
招待されたメンバーは、GitHubからリポジトリをローカル環境にダウンロードします。 

    **[bash]**
    ```bash
    git clone <リポジトリのURL>
    ```

2. ブランチの作成 (作業用)
mainやmasterブランチに直接pushせず、機能ごとにブランチを作成して開発します。

    **[bash]**
    ```bash
    git checkout -b <作業ブランチ名>
    ```

3. コードの変更とコミット
ファイルを作成・変更し、ローカルにコミットします。 

    **[bash]**
    ```bash
    git add .
    git commit -m "修正内容"
    ```

4. プッシュ (リモートへ反映)
作成したブランチをGitHubへアップロードします。 
 
    **[bash]**
    ```bash
    git push origin <作業ブランチ名>
    ```

5. プルリクエスト (PR) の作成
    1. GitHubの該当リポジトリ画面へ行くと、pushしたブランチに「Compare & pull request」という黄色いボタンが表示されます。
    2. 内容（変更点）を記入し、「Create pull request」をクリックします。 

6. レビューとマージ

    他のメンバーがコードを確認し、問題がなければ「Merge pull request」ボタンをクリックし、mainブランチに統合します。 

## 5. 重要な設定・ベストプラクティス
<dl>
<dt><b>ブランチ保護ルール (Branch Protection Rules):</b></dt>
<dd>
mainブランチへの直接pushを禁止し、必ずプルリクエストを経由するように設定します。<br>
詳細は<a href="#pull-request-settings">プルリクエスト設定</a>を参照してください。
これにより、レビューなしのコード混入を防げます。
<dd>
<dd>
※GitHubの個人用無料プライベートリポジトリでもこの機能は利用可能です。
</dd>
<br>
<dt><b>権限の管理:</b></dt>
<dd>
「Settings」>「Collaborators」で、メンバーの権限（Read, Write, Admin）を確認・設定します。
</dd>
<br>
<dt><b>コミットメッセージの統一:</b></dt>
<dd>
「Fix:」や「Add:」など、チーム内でコミットメッセージのプレフィックスを決めると見やすくなります。
</dd>
<br>
</dl>
これで、安全にプライベートリポジトリで共同開発を始めることができます。

---
## <a id="pull-request-settings"></a>**【参考】プルリクエスト設定**
GitHubでmainブランチへの直接pushを禁止し、**プルリクエスト**を必須にするには、
- リポジトリの「Settings」>「Branches」>「Branch protection rules」でルールを追加します。
- 「Require a pull request before merging」にチェックを入れ、保護対象にmainを指定し保存することで、直接プッシュがブロックされ、安全なレビュープロセスが強制されます。

### **具体的な設定手順**
1. GitHubリポジトリ画面を開く
    ``` 
    対象となるリポジトリのページへ移動します。
    ``` 

2. Settings (設定) へ移動
    ``` 
    上部メニューの「Settings」タブをクリックします。
    ``` 
3. Branches (ブランチ) を選択
    ``` 
    左側メニューの「Code and automation」内にある「Branches」を選択します。
    ``` 
4. Add rule (ルール追加) をクリック
    ``` 
    「Branch protection rules」セクションにある「Add rule」ボタンをクリックします。
    ``` 
5. ブランチパターンを指定
    ``` 
    「Branch name pattern」に main (または master など保護したいブランチ名) を入力します。
    ```
6. 保護ルールを有効化
    ``` 
    1. Require a pull request before merging:
        プルリクエスト（PR）を必須にする。
    2. Require approvals:
        マージ前に承認（Approve）を必須にする（推奨）。
    3. Dismiss stale pull request approvals when new commits are pushed:
        新しいコミットがプッシュされたら、既存の承認を無効にする（推奨）。
    4. Block force pushes:
        強制プッシュ（push -f）を禁止する。
    5. Do not allow bypassing the above settings:
        管理者を含め全員にこのルールを適用する（必要に応じて）。
    ``` 
7. 保存

        「Create」または「Save changes」をクリックします。 

これで、mainブランチへ直接プッシュしようとするとエラーとなり、必ずプルリクエストを作成し、レビューを経る必要が生じます。