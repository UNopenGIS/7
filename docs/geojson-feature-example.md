# GeoJSON Feature の正しいフォーマット

## 問題

単なる geometry オブジェクトは、valid な GeoJSON Feature ではありません。

### 不正な例（Geometry のみ）

```json
{
  "type": "MultiPolygon",
  "coordinates": [
    [
      [
        [-13.257, 8.4558],
        [-13.238, 8.4558],
        [-13.238, 8.4709],
        [-13.257, 8.4709],
        [-13.257, 8.4558]
      ]
    ]
  ]
}
```

これは GeoJSON Geometry オブジェクトですが、GeoJSON Feature ではありません。

## 解決方法

Geometry を valid な GeoJSON Feature にラップします。

### 正しい例（Feature でラップ）

```json
{
  "type": "Feature",
  "geometry": {
    "type": "MultiPolygon",
    "coordinates": [
      [
        [
          [-13.257, 8.4558],
          [-13.238, 8.4558],
          [-13.238, 8.4709],
          [-13.257, 8.4709],
          [-13.257, 8.4558]
        ]
      ]
    ]
  },
  "properties": {}
}
```

## GeoJSON Feature の必須要素

RFC 7946 に基づく GeoJSON Feature には、以下の3つのメンバーが必要です：

1. **`type`**: `"Feature"` である必要があります
2. **`geometry`**: geometry オブジェクト（または `null`）
3. **`properties`**: プロパティを格納するオブジェクト（空でも可）

オプションで `id` メンバーを含めることもできます。

## 参考文献

- [RFC 7946 - The GeoJSON Format](https://datatracker.ietf.org/doc/html/rfc7946)
- [GeoJSON Specification](https://geojson.org/)
