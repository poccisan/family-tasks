# Firebase セットアップ手順

## 1. Firebaseプロジェクトを作成

1. https://console.firebase.google.com にアクセス
2. 「プロジェクトを作成」をクリック
3. プロジェクト名を入力（例：`family-tasks`）
4. Googleアナリティクスは「無効」で OK → 「プロジェクトを作成」

## 2. Firestoreデータベースを有効化

1. 左メニューの「Firestore Database」をクリック
2. 「データベースの作成」をクリック
3. モードは「テストモード」を選択（後で変更可能）
4. ロケーションは `asia-northeast1`（東京）を選択 → 「完了」

## 3. ウェブアプリを登録してコードを取得

1. プロジェクトのトップページで「</>」（ウェブ）アイコンをクリック
2. アプリのニックネームを入力（例：`family-tasks-web`）
3. 「アプリを登録」をクリック
4. 表示される `firebaseConfig` の内容をコピー

## 4. index.html に貼り付け

`index.html` の以下の部分を、コピーした値に書き換えてください：

```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",          // ← 実際の値
  authDomain: "your-app.firebaseapp.com",
  projectId: "your-app",
  storageBucket: "your-app.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

## 5. 家族で共有する方法

- `index.html` をそのままブラウザで開く（`file://` で動作）
- または GitHub Pages / Firebase Hosting にデプロイして URL で共有
- 全員が同じ URL を開けば、タスクがリアルタイムで同期されます

## Firestoreのセキュリティルール（後で設定推奨）

Firestore の「ルール」タブで以下を設定すると安全になります：

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true; // テスト用（後で制限を追加）
    }
  }
}
```
