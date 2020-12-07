## DB一覧

|  No  | テーブルID        | テーブル名             | 想定件数 | 備考                                         |
| :--: | :---------------- | ---------------------- | -------- | -------------------------------------------- |
|  1   | [TTPJM001](#jump) | 顧客マスタ             | 100      | 自動配送サービスを利用するユーザー情報を管理 |
|  2   | TTPJM002          | 配送元マスタ           | 50       | 自動配送サービスを利用する配送元情報を管理   |
|  3   | TTPJM003          | 配送先マスタ           | 50       | 自動配送サービスを利用する配送先情報を管理   |
|  4   | TTPJM004          | 車体マスタ             | 500      | 車体毎の情報を管理                           |
|  5   | TTPJM005          | サービス時間管理マスタ | 2000     | 車体毎の稼働時間を管理                       |
|  6   | TTPJM006          | 汎用コードマスタ       | 100      | 汎用のステータス内容、区分内容などを管理     |
|  7   | TTPJD001          | 配送依頼               | 500      | 配送依頼を管理                               |
|  8   | TTPJD002          | 車体配送状況           | 5000     | 配送依頼の状況履歴を管理                     |
|  9   | TTPJD003          | 車体位置履歴           | 50000    | 車体毎の位置履歴を管理                       |

## DBレイアウト一覧

#### <span id="jump">TTPJM001 ユーザーマスタ</span>

|  No  | カラム名     | カラムID         |    型    | 桁数 |  PK  | IDX1 | IDX2 | IDX3 | default | not null | 備考 |
| :--: | :----------- | :--------------- | :------: | :--: | :--: | :--: | :--: | :--: | :-----: | :------: | :--- |
|  1   | ID           | id               |   int    |  11  |  〇  |      |      |      |         |          |      |
|  2   | password     | パスワード       | varchar  | 128  |      |      |      |      |         |    〇    |      |
|  ３  | last_login   | 最後ログイン日時 | datetime |      |      |      |      |      |         |          |      |
|  4   | is_superuser | 管理員フラグ     | tinyint  |  1   |      |      |      |      |         |    〇    |      |
|  5   | username     | ユーザーID       | varchar  | 150  |      |  1   |      |      |         |    〇    |      |
|  6   | first_name   | ファーストネーム | varchar  | 150  |      |      |      |      |         |    〇    |      |
|  7   | last_name    | ラストネーム     | varchar  | 150  |      |      |      |      |         |    〇    |      |
|  8   | email        | 電子メール       | varchar  | 254  |      |      |      |      |         |    〇    |      |
|  9   | is_staff     | 権限             | tinyint  |  1   |      |      |      |      |         |    〇    |      |
|  10  | is_active    | アクティブ       | tinyint  |  1   |      |      |      |      |         |    〇    |      |
|  11  | date_joined  | 登録日時         | datetime |      |      |      |      |      |         |    〇    |      |

------

#### TTPJM002 配送元マスタ

|  No  | カラム名  | カラムID       |   型    | 桁数  |  PK  | IDX1 | IDX2 | IDX3 | default | not null | 備考         |
| :--: | :-------- | :------------- | :-----: | :---: | :--: | :--: | :--: | :--: | :-----: | :------: | :----------- |
|  1   | code      | 配送コード     | varchar |  10   |      |  1   |      |      |         |    〇    |              |
|  2   | name      | 配送名称       | varchar |  50   |      |      |      |      |         |    〇    |              |
|  3   | address   | アドレス       | varchar |  100  |      |      |      |      |         |          |              |
|  4   | email     | メールアドレス | varchar |  100  |      |      |      |      |         |          | カンマ区切り |
|  5   | tel       | TEL            | varchar |  20   |      |      |      |      |         |          |              |
|  6   | longitude | 経度           | decimal | (8,5) |      |      |      |      |         |          |              |
|  7   | latitude  | 緯度           | decimal | (8,5) |      |      |      |      |         |          |              |

------

#### TTPJM003 配送先マスタ

|  No  | カラム名  | カラムID       |   型    | 桁数  |  PK  | IDX1 | IDX2 | IDX3 | default | not null | 備考         |
| :--: | :-------- | :------------- | :-----: | :---: | :--: | :--: | :--: | :--: | :-----: | :------: | :----------- |
|  1   | code      | 配送コード     | varchar |  10   |      |  1   |      |      |         |    〇    |              |
|  2   | name      | 配送名称       | varchar |  50   |      |      |      |      |         |    〇    |              |
|  3   | address   | アドレス       | varchar |  100  |      |      |      |      |         |          |              |
|  4   | email     | メールアドレス | varchar |  100  |      |      |      |      |         |          | カンマ区切り |
|  5   | tel       | TEL            | varchar |  20   |      |      |      |      |         |          |              |
|  6   | longitude | 経度           | decimal | (8,5) |      |      |      |      |         |          |              |
|  7   | latitude  | 緯度           | decimal | (8,5) |      |      |      |      |         |          |              |

------

#### TTPJM004 車体マスタ

|  No  | カラム名      | カラムID                 |   型    | 桁数 |  PK  | IDX1 | IDX2 | IDX3 | default | not null | 備考 |
| :--: | :------------ | :----------------------- | :-----: | :--: | :--: | :--: | :--: | :--: | :-----: | :------: | :--- |
|  1   | car_id        | 車体ID                   | varchar |  5   |      |  1   |      |      |         |    〇    |      |
|  2   | locker_no     | ロッカーNo               | varchar |  2   |      |  2   |      |      |         |    〇    |      |
|  3   | locker_size   | ロッカー規格             | tinyint |  1   |      |      |      |      |         |    〇    |      |
|  4   | locker_status | ロッカー利用状況(配送ID) | varchar |  15  |      |      |      |      |         |          |      |

------

#### TTPJM005 サービス時間管理マスタ

|  No  | カラム名           | カラムID         |   型    | 桁数 |  PK  | IDX1 | IDX2 | IDX3 | default | not null | 備考 |
| :--: | :----------------- | :--------------- | :-----: | :--: | :--: | :--: | :--: | :--: | :-----: | :------: | :--- |
|  1   | car_id             | 車体ID           | varchar |  5   |      |      |      |      |         |    〇    |      |
|  2   | date               | 日付             |  date   |      |      |      |      |      |         |    〇    |      |
|  3   | service_start_time | サービス開始時刻 |  time   |      |      |      |      |      |         |          |      |
|  4   | service_end_time   | サービス終了時刻 |  time   |      |      |      |      |      |         |          |      |
|  5   | return_start_time  | 基地帰還開始時刻 |  time   |      |      |      |      |      |         |          |      |
|  6   | return_end_time    | 基地帰還終了時刻 |  time   |      |      |      |      |      |         |          |      |

------

#### TTPJM006 汎用コードマスタ

|  No  | カラム名 | カラムID |   型    | 桁数 |  PK  | IDX1 | IDX2 | IDX3 | default | not null | 備考                                           |
| :--: | :------- | :------- | :-----: | :--: | :--: | :--: | :--: | :--: | :-----: | :------: | :--------------------------------------------- |
|  1   | kbn      | 区分     | varchar |  2   |      |  1   |      |      |         |    〇    | 1:配送ステータス<br/>2:配送状況<br/>3:稼働内容 |
|  2   | code     | コード   | varchar |  10  |      |  2   |      |      |         |    〇    |                                                |
|  3   | content  | 内容     | varchar | 100  |      |      |      |      |         |    〇    |                                                |

------

#### TTPJD001 配送依頼

|  No  | カラム名                | カラムID       |    型    | 桁数  |  PK  | IDX1 | IDX2 | IDX3 | default | not null | 備考                                              |
| :--: | :---------------------- | :------------- | :------: | :---: | :--: | :--: | :--: | :--: | :-----: | :------: | :------------------------------------------------ |
|  1   | delivery_code           | 配送コード     | varchar  |  10   |      |  1   |      |      |         |    〇    |                                                   |
|  2   | delivery_id             | 配送ID         | varchar  |  15   |      |  2   |      |      |         |    〇    |                                                   |
|  3   | company_code_from       | 配送元コード   | varchar  |  10   |      |      |      |      |         |    〇    |                                                   |
|  4   | company_address_from    | 配送元アドレス | varchar  |  100  |      |      |      |      |         |          |                                                   |
|  5   | company_email_from      | 配送元メール   | varchar  |  100  |      |      |      |      |         |          | カンマ区切り                                      |
|  6   | tel_from                | 配送元TEL      | varchar  |  20   |      |      |      |      |         |          |                                                   |
|  7   | longitude_from          | 配送元経度     | decimal  | (8,5) |      |      |      |      |         |          |                                                   |
|  8   | latitude_from           | 配送元緯度     | decimal  | (8,5) |      |      |      |      |         |          |                                                   |
|  9   | company_code_to         | 配送先コード   | varchar  |  10   |      |      |      |      |         |    〇    |                                                   |
|  10  | company_address_to      | 配送先アドレス | varchar  |  100  |      |      |      |      |         |          |                                                   |
|  11  | company_email_to        | 配送先メール   | varchar  |  100  |      |      |      |      |         |          | カンマ区切り                                      |
|  12  | tel_to                  | 配送先TEL      | varchar  |  20   |      |      |      |      |         |          |                                                   |
|  13  | longitude_to            | 配送先経度     | decimal  | (8,5) |      |      |      |      |         |          |                                                   |
|  14  | latitude_to             | 配送先緯度     | decimal  | (8,5) |      |      |      |      |         |          |                                                   |
|  15  | car_id                  | 配送車ID       | varchar  |   5   |      |      |  1   |      |         |          |                                                   |
|  16  | locker_no               | ロッカーNo     | varchar  |   2   |      |      |  2   |      |         |          |                                                   |
|  17  | estimated_collect_date  | 予定集荷日時   | datetime |       |      |      |      |      |         |          |                                                   |
|  18  | estimated_delivery_date | 予定受取日時   | datetime |       |      |      |      |      |         |          |                                                   |
|  19  | status_code             | 配送ステータス | varchar  |   1   |      |      |      |      |         |          | 1:集荷中<br/>2:配送中<br/>3:配送完了<br/>4:未配送 |
|  20  | insert_user             | 登録者         | varchar  |  10   |      |      |      |      |         |          |                                                   |
|  21  | insert_date             | 登録日         | datetime |       |      |      |      |      |         |          |                                                   |
|  22  | update_user             | 更新者         | varchar  |  10   |      |      |      |      |         |          |                                                   |
|  23  | update_date             | 更新日         | datetime |       |      |      |      |      |         |          |                                                   |
|  24  | receipt_user            | 受取者         | varchar  |  10   |      |      |      |      |         |          |                                                   |
|  25  | receipt_date            | 受取日         | datetime |       |      |      |      |      |         |          |                                                   |

------

#### TTPJD002 車体配送状況

|  No  | カラム名      | カラムID       |    型    | 桁数 |  PK  | IDX1 | IDX2 | IDX3 | default | not null | 備考                                                         |
| :--: | :------------ | :------------- | :------: | :--: | :--: | :--: | :--: | :--: | :-----: | :------: | :----------------------------------------------------------- |
|  1   | delivery_code | 配送コード     | varchar  |  10  |      |      |      |      |         |    〇    |                                                              |
|  2   | delivery_id   | 配送ID         | varchar  |  15  |      |      |      |      |         |    〇    |                                                              |
|  3   | car_id        | 車体ID         | varchar  |  5   |      |      |      |      |         |    〇    |                                                              |
|  4   | status        | 配送状況       | varchar  |  1   |      |      |      |      |         |          | 1:配送依頼受付<br/>2:集荷のため移動中<br/>3:{0}株式会社　到着<br/>4:集荷のため停車中<br/>5:ロッカー開錠<br/>6:ロッカー開錠中<br/>7:ロッカー施錠<br/>8:発車準備 |
|  5   | work_content  | 稼働内容       | varchar  |  2   |      |      |      |      |         |          | 1:電源ON<br/>2:発車準備<br/>3:集荷に向けて移動開始<br/>4:移動<br/>5:(割込)集荷に向けて移動開始<br/>6:移動中<br/>7:集荷場所到着<br/>8:集荷<br/>9:集荷完了<br/>10:発車準備<br/>11:集荷に向けて移動開始 |
|  6   | address_from  | 目的地(配送元) | varchar  | 100  |      |      |      |      |         |          |                                                              |
|  7   | address_to    | 目的地(配送先) | varchar  | 100  |      |      |      |      |         |          |                                                              |
|  8   | upd_date      | 更新日時       | datetime |      |      |      |      |      |         |    〇    |                                                              |
|  9   | remark        | 備考           | varchar  | 200  |      |      |      |      |         |          |                                                              |

------

#### TTPJD003 車体位置履歴

|  No  | カラム名  | カラムID |   型    | 桁数  |  PK  | IDX1 | IDX2 | IDX3 | default | not null | 備考 |
| :--: | :-------- | :------- | :-----: | :---: | :--: | :--: | :--: | :--: | :-----: | :------: | :--- |
|  1   | car_id    | 車体ID   | varchar |   5   |      |      |      |      |         |    〇    |      |
|  2   | longitude | 経度     | decimal | (8,5) |      |      |      |      |         |    〇    |      |
|  3   | latitude  | 緯度     | decimal | (8,5) |      |      |      |      |         |    〇    |      |