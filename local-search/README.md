# local-search

愛知県MVPの地域・ジャンル検索サイトです。店舗情報は自社IDを持ちつつ、Google Place IDを外部正規IDとして保存する方針です。

## 起動

```bash
npm start
```

URL:

```text
http://127.0.0.1:4173/
```

## 店舗データ方針

店舗DBは次の役割分担にします。

- 自社ID: サイト内URL、重複統合、編集履歴の基準
- Google Place ID: 店舗の正規化、住所、営業時間、営業状態、地図の基準
- 自社ジャンル: アダルトショップ、ネットカフェ、ゲームセンター、カラオケ、サウナなどの分類
- Hotpepper: 予約・クーポン
- 楽天: 関連商品・通販
- ValueCommerce: 予約リンクの中継

## Google Places 同期

`data/place-seeds.json` に検索クエリを入れ、Google Places APIで候補を取得します。

```bash
set GOOGLE_PLACES_API_KEY=YOUR_KEY
npm run sync:places
```

出力:

```text
data/google-places-candidates.json
```

候補を確認してから `data/shops.json` に採用します。Place IDは保存できますが、古くなる可能性があるため定期的に更新します。

## 重要

Googleの業種分類だけでは、アダルトショップなどの細かい分類は弱いことがあります。そのため、Google Place IDで店舗を識別し、自社ジャンルで分類します。
