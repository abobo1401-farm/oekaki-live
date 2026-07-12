# oekaki-live Version 0.1

## ファイル
- index.html：参加者ページ
- admin.html：管理ページ
- obs.html：OBS表示
- style.css
- firebase-config.js

## URL例
- 参加者：`https://あなたのURL/index.html?room=abo-room`
- 管理：`https://あなたのURL/admin.html?room=abo-room`
- OBS：`https://あなたのURL/obs.html?room=abo-room`

## Firebaseルール
現在の `drawingRooms` 用ルールをそのまま使えます。

```json
{
  "rules": {
    "drawingRooms": {
      "$room": {
        ".read": true,
        ".write": true
      }
    }
  }
}
```

## Version 0.1
- 名前・お題を入力して参加
- 空き枠へ自動参加
- 最大4人
- OBSへリアルタイム表示
- 管理画面で1・2・4人切替
- 参加者削除
- 個別・全体の全消し
- 部屋リセット


## v0.1.1 修正
- 参加ページからお題入力を削除
- 参加ボタンが反応しない問題を修正
- 古いスマホでも参加者IDを生成できるよう改善
