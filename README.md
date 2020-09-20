# README

## usersテーブル

|Column|Type|Options|
|------|----|-------|
|nickname|string|null: false|
|email|string|null: false,unique: true|
|password|string|null: false|
|first_name|string|null: false|
|last_name|string|null: false|
|first_name_kana|string|null: false|
|last_name_kana|string|null: false|
|birthday|date|null: false|

### Association
- has_one: address, dependent: :destroy
- has_one: credit_card, dependent: :destroy
- has_one: sns_authentication, dependent: :destroy
- has_many: items
- has_many: comments, dependent: :destroy

## addressesテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|references||
|destination_first_name|string|null: false|
|destination_last_name|string|null: false|
|destination_first_name_kana|string|null: false|
|destination_last_name_kana|string|null: false|
|postal_code|integer|null: false|
|prefecture_id|references|null: false|
|city|string|null: false|
|block|string|null: false|
|building|string||
|phone_numeber|string||

### Association
- belongs_to: user, optional: true
- belongs_to_active_hash :prefecture

## itemsテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|explain|text|null: false|
|category_id|references|null: false, foreign_key: true|
|brand|text||
|state_id|references|null: false|
|shipping_burden_id|references|null: false|
|prefecture_id|references|null: false|
|shipping_day_id|references|null: false|
|price|integer|null: false|
|seller_id|references|null: false, foreign_key: { to_table: :users }|
|buyer_id|references|foreign_key: { to_table: :users }|

### Association
- belongs_to :seller, class_name: "User"
- has_many: images, dependent: :destroy
- belongs_to: category
- has_many: comments, dependent: :destroy
- belongs_to: brand
- belongs_to_active_hash :state
- belongs_to_active_hash :shipping_burden
- belongs_to_active_hash :shipping_day
- belongs_to_active_hash :prefecture

## imagesテーブル
|Column|Type|Options|
|------|----|-------|
|items|references|foreing_key: true|
|src|string||

### Association
- belongs_to: item

## categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|ancestry|string||

### Association
- has_ancestry
- has_many: items

## commentsテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|references|null: false, foreing_key: true|
|item_id|references|null: false, foreing_key: true|
|text|text|null: false|

### Association
- belongs_to: item
- belongs_to: user

## credit_card
|column|type|options|
|------|----|-------|
|user_id|references|null:false, foreign_key: true|
|card_id|string|null:false|
|customer_id|string|null:false|

### Association
- belongs_to: user

## sns_authentcationsテーブル
|Column|Type|Options|
|------|----|-------|
|provider|string||
|uid|string||
|user_id|references|foreing_key: true|

### Association
- belongs_to: user, optional: true




