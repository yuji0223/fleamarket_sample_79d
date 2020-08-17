# 接続先情報
http://54.248.161.97
#### BASIC認証 ID/Pass
- ID: fleamarket_sample_79d
- Pass: teamD
#### テスト用アカウント等
- 購入者用
  - メールアドレス: buyer@gmail.com
  - パスワード: buyer1234
- 購入用カード情報
  - 番号：4242424242424242
  - 期限：01/22
  - セキュリティコード：123
- 出品者用
  - メールアドレス: seller@gmail.com
  - パスワード: seller1234


# アプリ概要
フリーマーケットのアプリケーションを作成しました。
実際にあるサイトを確認しながら、DB設計、要件定義、UI/UX設計に至るまで全て自分たちで実装しました。毎日3回のデイリースクラムを実施し、進捗状況や実装方針の確認などを行いました。1週間に1度のスプリントミーティングにより、達成できた箇所や反省点の振り返りを行い、次回スプリントレビューまでの目標を再設定することにより、開発スピードを上げてきました。

## 開発体制
- 開発期間：7/21〜8/12 (約4週間)
- 1日あたりの平均作業時間：約9時間
- 人数：5人
- アジャイル型開発（スクラム）
- Trelloによるタスク管理
## 開発環境
Ruby/Ruby on Rails/Haml/Scss/JavaScript/jQuery/MySQL/Github/AWS/
Visual Studio Code

## 開発担当箇所
- DB設計
- ユーザー新規登録・ログイン機能及び機能
- ユーザーマイページ
- 商品詳細ページ
- 購入完了ページ
- コメント機能
### 詳細は下記URLにございます
https://docs.google.com/document/d/14gmy6us1uIIRUORE2EAOOv1NnWHJQXevhiWWxnVQCA0/

# DB設計

## usersテーブル
|Column|Type|Options|
|------|----|-------|
|family_name|string|null: false|
|first_name|string|null: false|
|family_name_kana|string|null: false|
|first_name_kana|string|null: false|
|nickname|string|null: false|
|email|string|null:false, unique: true|
|password|string|null: false|
|birth_day|string|null: false|

### Association
- has_many :items, dependent: :destroy
- has_one :address, dependent: :destroy
- has_one :card, dependent: :destroy


## addressesテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|references|null: false, foreign_key: true|
|family_name|string|null: false|
|first_name|string|null: false|
|family_name_kana|string|null: false|
|first_name_kana|string|null: false|
|postal_code|string|null: false|
|prefecture_id|integer|null: false|
|city|string|null: false|
|block|string|null: false|
|building|string||
|phone_number|string||

### Association
- belongs_to :user


## itemsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|description|text|null: false|
|condition(enum)|integer|null: false|
|price|integer|null: false|
|category_id|references|null: false, foreign_key: true|
|shipping_cost|integer|null: false|
|prefecture_id|integer|null: false|
|shipping_day|integer|null: false|
|seller_id|references|null: false, foreign_key: true|
|buyer_id|references|foreign_key :true|
|size|integer||

### Association
- belongs_to :user
- belongs_to :category
- has_many :images, dependent: :destroy
- has_many :comments, dependent: :destroy


## commentsテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|references|null: false, foreign_key: true|
|item_id|references|null: false, foreign_key: true|
|comment|string||
|delete_check|integer|default: 0|

### Association
- belongs_to :user
- belongs_to :item


## imagesテーブル
|Column|Type|Options|
|------|----|-------|
|image|string|null: false|
|item_id|references|null: false, foreign_key: true|

### Association
- belongs_to :item


## categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|ancestry|string||

### Association
- has_many :items


## cardsテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|references|null: false, foreign_key: true|
|customer_id|string|null: false|
|card_id|string|null: false|

### Association
- belongs_to :user
