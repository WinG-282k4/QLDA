erDiagram
USERS {
INT user_id PK
VARCHAR(50) username UNIQUE NOT NULL
VARCHAR(100) email UNIQUE NOT NULL
VARCHAR(255) password NOT NULL
VARCHAR(255) avatar
TIMESTAMP created_at
}

    GAMES {
        INT game_id PK
        INT player1_id FK
        INT player2_id FK
        INT winner_id FK
        VARCHAR room_code
        ENUM status NOT NULL
        TIMESTAMP created_at
    }

    MOVES {
        INT move_id PK
        INT game_id FK
        INT player_id FK
        INT move_order
        INT position_x NOT NULL
        INT position_y NOT NULL
        INT used_skill_id FK
        TIMESTAMP created_at
    }

    LEADERBOARD {
        INT rank_id PK
        INT user_id FK
        INT total_games
        INT wins
        INT losses
        FLOAT win_rate
        TIMESTAMP last_updated
    }

    SKILLS {
        INT skill_id PK
        VARCHAR(50) name NOT NULL
        TEXT description NOT NULL
        VARCHAR(255) unlock_condition NOT NULL
        TIMESTAMP created_at
    }

    USER_SKILLS {
        INT user_id FK
        INT skill_id FK
        TIMESTAMP unlocked_at
        BOOLEAN is_active DEFAULT FALSE
    }

    SKINS {
        INT skin_id PK
        VARCHAR(50) name NOT NULL
        VARCHAR(255) image_url NOT NULL
        INT price
        TIMESTAMP created_at
    }

    USER_SKINS {
        INT user_id FK
        INT skin_id FK
        TIMESTAMP unlocked_at
        BOOLEAN is_active DEFAULT FALSE
    }

    USERS ||--o{ GAMES : "chơi"
    LEADERBOARD ||--o{ USERS : "thuộc về"
    USERS ||--o{ USER_SKILLS : "mở khóa"
    USERS ||--o{ USER_SKINS : "sở hữu"
    GAMES ||--o{ MOVES : "có"
    MOVES ||--|| SKILLS : "sử dụng"
    SKILLS ||--o{ USER_SKILLS : "được sở hữu"
    SKINS ||--o{ USER_SKINS : "được sử dụng"
