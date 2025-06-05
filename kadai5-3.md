## 外部APIの呼び出しのミニレポート
### Q3-1. 郵便番号APIについて説明せよ。
* エンドポイントと機能
* https://zipcloud.ibsnet.co.jp/api/search
* 日本の郵便番号API「zipcloud」は、郵便番号を入力することで対応する住所（都道府県・市区町村・町域）を取得できる無料API
* リクエストとレスポンスのフォーマット
* 【リクエスト例】（郵便番号：1000001）
* sql GET https://zipcloud.ibsnet.co.jp/api/search?zipcode=1000001
* 【レスポンス例（JSON）】
* json {
  "message": null,
  "results": [
    {
      "zipcode": "1000001",
      "prefcode": "13",
      "address1": "東京都",
      "address2": "千代田区",
      "address3": "千代田",
      "kana1": "ﾄｳｷｮｳﾄ",
      "kana2": "ﾁﾖﾀﾞｸ",
      "kana3": "ﾁﾖﾀﾞ"
    }
  ],
  "status": 200
}
### Q3-2. 各自で調査したAPIについて説明せよ。
* APIの名称と参照URL
* 名称：Open-Meteo Weather API
* 参照URL：天気予報API：https://open-meteo.com/en/docs
  　　　　 ジオコーディングAPI：https://open-meteo.com/en/docs/geocoding-api
* エンドポイントと機能
* ジオコーディングAPI（都市名→緯度・経度を取得）
bash https://geocoding-api.open-meteo.com/v1/search
機能：都市名や地名から緯度・経度などの位置情報を検索できる。
*天気予報API（緯度・経度→天気データ）
bash https://api.open-meteo.com/v1/forecast
機能：指定した位置の天気予報を取得できる。日別、時刻別の温度や降水量などに対応。
パラメータで取得する天気要素を柔軟に指定可能。
* リクエストとレスポンスのフォーマット
* ジオコーディングAPI
【リクエスト例】
pgsql GET https://geocoding-api.open-meteo.com/v1/search?name=Tokyo&count=1
【レスポンス例（JSON）】
json
{
  "results": [
    {
      "name": "Tokyo",
      "latitude": 35.682839,
      "longitude": 139.759455,
      "country": "Japan"
    }
  ]
}
◆ 天気予報API
【リクエスト例】
bash GET https://api.open-meteo.com/v1/forecast?latitude=35.682839&longitude=139.759455&daily=temperature_2m_max,temperature_2m_min&timezone=auto
【レスポンス例（JSON）】
json
{
  "daily": {
    "time": ["2025-06-05", "2025-06-06", "..."],
    "temperature_2m_max": [28.3, 29.1, "..."],
    "temperature_2m_min": [20.5, 21.0, "..."]
  }
}
### Q3-3. 感想
* 今回の課題で苦労したこと
* WeAPIの扱い
* 演習を通して理解できたこと
* APIの活用方法
* Web APIの利便性や課題など
* Web APIは外部の情報を活用できる点でとても便利なものだと感じた。
