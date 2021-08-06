# README

## user テーブル
| Column                  | Type      | Options                   |
|-------------------------|-----------|---------------------------|
| email                   | string    | null: false  unique: true |
| encrypted_password      | string    | null: false               |
| nickname                | string    | null: false               |
| sex                     | integer   | null: false               | 
| first_language          | integer   | null: false               |
| birthday                | date      | null: false               |
| occupation              | integer   | null: false               |
| second_language_level   | integer   | null: false               |

### Association
- has_many :like
- has_many :community, through:user_community
- has_many :matching_room, through:matching_room_user
- has_many :message
- has_one  :profile



## like テーブル
| Column          |  Type      | Options                             |
|-----------------|------------|-------------------------------------|
| user            | references | null: false, foreign_key: true      |
| my_like_user    | integer    | null: false                         |

### Association
- belongs_to :user



## message テーブル
| Column           | Type       | Option                              |
|------------------|------------|-------------------------------------|
| user             | references | null: false, foreign_key: true      |
| text             | string     | null: false                         |
| matching_room    | integer    | null: false                         | 

### Association 
- belongs_to :user
- belongs_to :matching_room



## community テーブル
| Column                 | Type       | Options           |
|------------------------|------------|-------------------|
| community_name         | string     | null: false       |
| second_language_level  | integer    | null: false       |
| introduction           | string     | null: false       |

### Association 
- has_many :user, through:user_community



## user_community テーブル
| Column       | Type       | Options                         |
|--------------|------------|---------------------------------|
| user         | references | null: false, foreign_key: true  |
| community    | references | null: false, foreign_key: true  |

### Association 
- belongs_to :user
- belongs_to :community



## matching_room テーブル
| Column         | Type       | Options                         |
|----------------|------------|---------------------------------|
| user           | references | null: false, foreign_key: true  |
| matching_room  | references | null: false, foreign_key: true  |

### Association 
- has_many :user, through:matching_room_user
- has_many :message



## matching_room_user テーブル
| Column         | Type       | Options                         |
|----------------|------------|---------------------------------|
| user           | references | null: false, foreign_key: true  |
| matching_room  | references | null: false, foreign_key: true  |

### Association 
- belongs_to :user
- belongs_to :matching_room



## profile テーブル
| Column         | Type       | Options                         |
|----------------|------------|---------------------------------|
| user           | references | null: false, foreign_key: true  |

### Association 
- belongs_to :user
