
# README

# テーブル設計

## user テーブル
| Column                  | Type      | Options                   |
|-------------------------|-----------|---------------------------|
| email                   | string    | null: false  unique: true |
| encrypted_password      | string    | null: false               |
| nickname                | string    | null: false               |
| gender                  | integer   | null: false               | 
| first_language          | integer   | null: false               |
| birthday                | date      | null: false               |
| occupation              | integer   | null: false               |
| second_language_level   | integer   | null: false               |

### Association
- has_many :likes
- has_many :like_users, through: :likes, source: :my_like_user
- has_many :reverse_of_likes, class_name: "Like", foreign_key: "my_like_user"
- has_many :liked_users, through: :reverse_of_likes, source: :user
- has_many :user_communities
- has_many :communities, through: :user_communities
- has_many :matching_room_users
- has_many :matching_rooms, through: :matching_room_users
- has_many :messages
- has_one  :profile



## like テーブル
| Column          |  Type      | Options                                                 |
|-----------------|------------|---------------------------------------------------------|
| user            | references | null: false, foreign_key: true                          |
| my_like_user    | references | null: false, foreign_key: true { to_table: :users }     |

### Association
- belongs_to :user
- belongs_to :my_like_user, class_name: "User"

| Column          |  Type      | Options                             |
|-----------------|------------|-------------------------------------|
| user            | references | null: false, foreign_key: true      |
| my_like_user    | references | null: false, foreign_key: true      |

### Association
- belongs_to :user




## message テーブル
| Column           | Type       | Option                              |
|------------------|------------|-------------------------------------|
| user             | references | null: false, foreign_key: true      |
| text             | string     | null: false                         |
| matching_room    | references | null: false, foreign_key: true      | 
| matching_room    | integer    | null: false                         | 

### Association 
- belongs_to :user
- belongs_to :matching_room



## community テーブル
| Column                 | Type       | Options           |
|------------------------|------------|-------------------|
| community_name         | string     | null: false       |
| second_language_level  | integer    | null: false       |
| introduction           | text       | null: false       |

### Association 
- has_many :user_communities
- has_many :users, through: :user_communities



## user_community テーブル (中間)
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

### Association 
- has_many :matching_room_users
- has_many :users, through: :matching_room_users
- has_many :messages



## matching_room_user テーブル
| user           | references | null: false, foreign_key: true  |
| matching_room  | references | null: false, foreign_key: true  |

### Association 
- has_many :users, through: :matching_room_users
- has_many :messages



## matching_room_user テーブル (中間)
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
| introduction   | text       | null: false                     |

### Association 
- belongs_to :user



