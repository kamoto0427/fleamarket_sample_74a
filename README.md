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
- has_many: products
- has_many: comments, dependent: :destroy
- has_many: likes, dependent: :destroy
- has_many: favorites, dependent: :destroy




## itemsテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|explain|text|null: false|
|state_id|references|null: false, foreign_key: true|
|price|integer|null: false|
|seller_id|references|null: false, foreign_key: true|
|buyer_id|references|
|resarvavation_email|references|null: false|
|category_id|references|null: false, foreign_key: true|
|shipping_burden_id|references|null: false, foreign_key: true|
|shipping_day_id|references|null: false, foreign_key: true|
|prefecture_id|references|null: false, foreign_key: true|
|brand_id|references|null: false, foreign_key: true|
|size_id|references|null: false, foreign_key: true|

### Association
- has_many: images, dependent: :destroy
- has_many: comments, dependent: :destroy
- has_many: likes, dependent: :destroy
- has_many: favorites, dependent: :destroy
- belongs_to: seller, class_name: 'user', :foreign_key => 'seller_id'
- belongs_to: buyer, class_name: 'user', :foreign_key => 'buyer_id'
- belongs_to: category
- belongs_to: bland
- belongs_to_active_hash: state
- belongs_to_active_hash: shipping_burden
- belongs_to_active_hash: shipping_day
- belongs_to_active_hash: size
- belongs_to_active_hash: prefecture



## addressesテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|references|null: false, foreign_key: true|
|first_name|string|null: false|
|last_name|string|null: false|
|first_name_kana|string|null: false|
|last_name_kana|string|null: false|
|postal_code|integer|null: false|
|prefecture_id|references|null: false, foreign_key: true|
|city|string|null: false|
|block|string|null: false|
|building|string|
|phone_numeber|string|

### Association
- belongs_to: user
- belongs_to_active_hash: prefecture




## credit_card
|column|type|options|
|:-:|:-:|:-:|
|token|string|null:false
|user|references|null: false, foreign_key: true

### Association
- belongs_to: user



## imagesテーブル
|Column|Type|Options|
|------|----|-------|
|photo|text|null: false|
|items|references|null: false, foreing_key: true|

### Association
- belongs_to: item



## categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|ancestry|string|null: false|

### Association
- has_many: items



## shipping_daysテーブル
|Column|Type|Options|
|------|----|-------|
|shipping_day|string|null: false|

### Association
- has_many: items


## sizeテーブル
|Column|Type|Options|
|------|----|-------|
|size_id|string|null:false|

### Association
- has_many: items


### commentsテーブル
|Column|Type|Options|
|------|----|-------|
|comment|text|null: false|
|user_id|references|null: false, foreing_key: true|
|item_id|references|null: false, foreing_key: true|

### Association
- belongs_to: item
- belongs_to: user



## likesテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|references|null: false, foreing_key: true|
|item_id|references|null: false, foreing_key: true|

### Association
- belongs_to: item
- belongs_to: user



## favoritesテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|references|null: false, foreing_key: true|
|item_id|references|null: false, foreing_key: true|

### Association
- belongs_to: item
- belongs_to: user



## sns_authentcationsテーブル
|Column|Type|Options|
|------|----|-------|
|provider|string|null: false|
|uid|string|null: false, unique: true|
|user_id|string|null: false, foreing_key: true|

### Association
- belongs_to: user




