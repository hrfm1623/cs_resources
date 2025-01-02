# CS Resources

このリポジトリは、静的リソース（画像、CSS、JS など）を管理し、Google Cloud Storage と自動的に同期するためのリポジトリです。

## 機能

- GitHub リポジトリと Google Cloud Storage の自動同期
- ファイルの追加、更新、削除の自動反映
- `images/origin` ディレクトリの同期除外

## セットアップ

### 1. Google Cloud Storage の設定

1. [Google Cloud Console](https://console.cloud.google.com/)でプロジェクトを作成または選択
2. Cloud Storage バケット `cs_resources` を作成
3. サービスアカウントの作成：
   - IAM → サービスアカウント → 新しいサービスアカウント
   - 役割: Storage 管理者
   - JSON キーをダウンロード

## 使用方法

1. ファイルの追加/更新：
   ```bash
   git add .
   git commit -m "Add new resources"
   git push origin main
   ```
2. ファイルの削除：
   ```bash
   git rm path/to/file
   git commit -m "Remove resource"
   git push origin main
   ```

プッシュ後、GitHub Actions が自動的に変更を Google Cloud Storage に同期します。

## 除外設定

以下のファイル/ディレクトリは同期から除外されます：

- `images/origin/`
- `.git/`
- `.github/`
- `node_modules/`
- その他`.gitignore`に記載されたパス

## 注意事項

- `images/origin/` ディレクトリは同期されません（オリジナルファイルの保管用）
- 大容量ファイルのアップロードには時間がかかる場合があります
- バケット内のファイルは自動的に上書きされます
