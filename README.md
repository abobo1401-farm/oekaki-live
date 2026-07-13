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


## v0.1.2 修正
- 管理画面から絵を消したあと、新しく描いた線がOBSへ反映されなくなる問題を修正
- OBSが描画のたびに画面全体を作り直していた処理を廃止
- 参加者情報と描画データを別々に監視して、リアルタイム表示を安定化


## v0.1.3 軽量化
- 約50msごとに線をまとめてFirebaseへ送信
- スマホ側は通信を待たずローカル描画
- 自分の描画データの二重描画を防止
- OBSは旧形式と新しいまとめ描画形式の両方に対応


## v0.1.4 全消し同期修正
- 全消し時に clearVersion を更新し、OBSへ確実に消去命令を送信
- 全消し直前の未送信描画データを破棄
- 個別全消し・全員全消しの同期を強化


## v0.1.5 同期・4人描画最適化
- 描画パケットへ clearVersion を付与し、全消し前の遅延パケットをOBS側で破棄
- clearVersionを先に更新してから描画データを削除する順序へ変更
- OBS描画をrequestAnimationFrameで1フレーム単位にまとめ、60fps表示を維持しやすく改善
- 管理画面が描画データ更新のたびに全体再描画していた処理を廃止
- 管理画面は参加者ID・名前だけを個別監視し、4人同時描画時の通信・DOM負荷を軽減
