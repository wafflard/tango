# 単語カード

公開URL: https://wafflard.github.io/tango/

英検準1級 単熟語EX（1〜1000）とターゲット1200（1〜1700）の単語カード。
ログインすると学習記録が Firebase（プロジェクト `tango-card-803c5`）に保存され、どの端末でも同じ記録が使える。

## ファイル
- `index.html` … 単語カード本体（単語データもこの中）
- `firestore.rules` … Firestore のセキュリティルール（Firebase コンソールの Firestore →「ルール」に貼り付けて公開する）
- `manifest.webmanifest`・アイコン … ホーム画面に追加したときの名前とアイコン

## 管理のしかた（Firebase コンソール）
- **招待コード**：Firestore の `config/invite` ドキュメントの `code` フィールド。変えると以後の新規登録はそのコードが必要になる（登録済みの生徒には影響しない）。
- **講師の追加**：講師もアプリから普通に登録し、Authentication の一覧でその人の「ユーザー UID」をコピー → Firestore に `admins/{UID}` ドキュメントを作る（フィールドは何でもよい）。アプリに「講師用：進み具合」が出るようになる。
- **パスワードを忘れた生徒**：
  1. Authentication の一覧で `{ID}@tango.example.com` のユーザーを削除
  2. Firestore の `accounts/{ID}` を開き、`reset` を `true` に変更
  3. 生徒にアプリの「新規作成」から同じID・新しいパスワード・招待コードで登録してもらう（記録は引き継がれる）
