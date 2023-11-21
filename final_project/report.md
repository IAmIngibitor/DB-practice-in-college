## Приложение: потоковый сервис музыки
### Схема баз данных
![music_service](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/bdfebcc7-4f8a-4081-88e7-32f7184355f6)
### SQL
#### CREATE TABLES
```sql
DROP SCHEMA public cascade;
CREATE SCHEMA public;

-- CREATE TABLES

CREATE TABLE users
(
    id bigint PRIMARY KEY,
    nickname varchar(32) NOT NULL,
    email varchar NOT NULL,
    vip_subscriber boolean NOT NULL DEFAULT false
);

CREATE TABLE authors
(
    id bigint PRIMARY KEY,
    user_id bigint NOT NULL,
    nickname varchar(32) NOT NULL,
	FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE music_genre
(
    id bigint PRIMARY KEY,
    title varchar NOT NULL
);

CREATE TABLE author_genres
(
    id bigint PRIMARY KEY,
    author_id bigint NOT NULL,
    genre_id bigint NOT NULL,
	FOREIGN KEY (author_id) REFERENCES authors(id),
	FOREIGN KEY (genre_id) REFERENCES music_genre(id)
);

CREATE TABLE music_list
(
    id bigint PRIMARY KEY,
    title varchar NOT NULL,
    genre_id bigint NOT NULL,
    author_id bigint NOT NULL,
	FOREIGN KEY (author_id) REFERENCES authors(id),
	FOREIGN KEY (genre_id) REFERENCES music_genre(id)
);

CREATE TABLE favorites_music
(
    id bigint PRIMARY KEY,
    user_id bigint NOT NULL,
    song_id bigint NOT NULL,
	FOREIGN KEY (user_id) REFERENCES users(id),
	FOREIGN KEY (song_id) REFERENCES music_list(id)
);

CREATE TABLE playlists
(
    id bigint PRIMARY KEY,
    title varchar NOT NULL,
    user_id bigint NOT NULL,
	FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE playlist_music
(
    id bigint PRIMARY KEY,
    playlist_id bigint NOT NULL,
    song_id bigint NOT NULL,
	FOREIGN KEY (playlist_id) REFERENCES playlists(id),
	FOREIGN KEY (song_id) REFERENCES music_list(id)
);

CREATE TABLE author_auditions (
	author_id bigint NOT NULL,
	auditions bigint NOT NULL DEFAULT 0,
	FOREIGN KEY (author_id) REFERENCES authors(id)
);
```
#### INSERTS VALUES
```sql
-- INSERTS

-- USERS
INSERT INTO users VALUES (1, 'Кирилл', 'slkdjg@mail.ru', true);
INSERT INTO users VALUES (2, 'Антон', 'hhdfgs@mail.ru');
INSERT INTO users VALUES (3, 'Максим', 'sfhksdfg@mail.ru');
INSERT INTO users VALUES (4, 'Иван', 'efgdghd@mail.ru', true);
INSERT INTO users VALUES (5, 'afgs', 'edskdg@mail.ru');
INSERT INTO users VALUES (6, 'Кириajgfjлл', 'amsdfa@mail.ru');
INSERT INTO users VALUES (7, 'gsfdhssd', 'fgjgts@mail.ru');
INSERT INTO users VALUES (8, 'Киdfgdfhdрилл', 'fsgasdef@mail.ru', true);
INSERT INTO users VALUES (9, 'sgjhsgh', 'afjhfdjgmfg@mail.ru', true);
INSERT INTO users VALUES (10, 'dsfsdgn', 'kjdghsf@mail.ru');
INSERT INTO users VALUES (11, 'asdfsxfv', 'sggkhjr@mail.ru', true);
INSERT INTO users VALUES (12, 'sdfgdjnbrd', 'sdfbvgftg@mail.ru');

-- AUTHORS
INSERT INTO authors VALUES (1, 2, 'Антон');
INSERT INTO authors VALUES (2, 4, 'Иван');
INSERT INTO authors VALUES (3, 6, 'Кириajgfjлл');
INSERT INTO authors VALUES (4, 7, 'gsfdhssd');
INSERT INTO authors VALUES (5, 10, 'dsfsdgn');
INSERT INTO authors VALUES (6, 11, 'asdfsxfv');

-- MUSIC GENRE
INSERT INTO music_genre VALUES (1, 'Рок');
INSERT INTO music_genre VALUES (2, 'Фонк');
INSERT INTO music_genre VALUES (3, 'Реп');
INSERT INTO music_genre VALUES (4, 'Поп');

-- AUTHOR GENRES
INSERT INTO author_genres VALUES (1, 1, 4);
INSERT INTO author_genres VALUES (2, 2, 3);
INSERT INTO author_genres VALUES (3, 3, 1);
INSERT INTO author_genres VALUES (4, 4, 2);
INSERT INTO author_genres VALUES (5, 5, 2);
INSERT INTO author_genres VALUES (6, 6, 2);

-- MUSIC LIST
INSERT INTO music_list VALUES (1, 'ksjldhfls', 2, 4);
INSERT INTO music_list VALUES (2, 'asfdjags', 2, 4);
INSERT INTO music_list VALUES (3, 'ggrtgde', 2, 4);
INSERT INTO music_list VALUES (4, 'ukdsfgasdf', 2, 4);
INSERT INTO music_list VALUES (5, 'jkhsfdgsx', 2, 5);
INSERT INTO music_list VALUES (6, 'qawrsvdrf', 2, 5);
INSERT INTO music_list VALUES (7, 'dfgdf', 2, 6);
INSERT INTO music_list VALUES (8, 'fghjghnbcv', 2, 6);
INSERT INTO music_list VALUES (9, 'swefas', 2, 6);
INSERT INTO music_list VALUES (10, 'tscdvr', 1, 3);
INSERT INTO music_list VALUES (11, 'fthfgv', 1, 3);
INSERT INTO music_list VALUES (12, 'ggffgfs', 3, 2);
INSERT INTO music_list VALUES (13, 'efsdf', 3, 2);
INSERT INTO music_list VALUES (14, 'hfgjserf', 3, 2);
INSERT INTO music_list VALUES (15, 'wxcdvcf', 3, 2);
INSERT INTO music_list VALUES (16, 'fgdsfdxz', 3, 2);
INSERT INTO music_list VALUES (17, 'xczvrgdf', 4, 1);
INSERT INTO music_list VALUES (18, 'efsdfhg', 4, 1);
INSERT INTO music_list VALUES (19, 'gdfhdfgsa', 4, 1);
INSERT INTO music_list VALUES (20, 'tjfghsdg', 4, 1);

-- FAVORITES MUSIC
INSERT INTO favorites_music VALUES (1, 1, 2);
INSERT INTO favorites_music VALUES (2, 1, 5);
INSERT INTO favorites_music VALUES (3, 1, 8);
INSERT INTO favorites_music VALUES (4, 2, 1);
INSERT INTO favorites_music VALUES (5, 2, 2);
INSERT INTO favorites_music VALUES (6, 2, 5);
INSERT INTO favorites_music VALUES (7, 2, 9);
INSERT INTO favorites_music VALUES (8, 2, 12);
INSERT INTO favorites_music VALUES (9, 2, 15);
INSERT INTO favorites_music VALUES (10, 3, 1);
INSERT INTO favorites_music VALUES (11, 3, 2);
INSERT INTO favorites_music VALUES (12, 4, 4);
INSERT INTO favorites_music VALUES (13, 4, 7);
INSERT INTO favorites_music VALUES (14, 4, 9);
INSERT INTO favorites_music VALUES (15, 4, 16);
INSERT INTO favorites_music VALUES (16, 4, 20);
INSERT INTO favorites_music VALUES (17, 5, 2);
INSERT INTO favorites_music VALUES (18, 5, 6);
INSERT INTO favorites_music VALUES (19, 5, 8);
INSERT INTO favorites_music VALUES (20, 5, 9);
INSERT INTO favorites_music VALUES (21, 5, 15);
INSERT INTO favorites_music VALUES (22, 5, 18);
INSERT INTO favorites_music VALUES (23, 5, 19);
INSERT INTO favorites_music VALUES (24, 6, 3);
INSERT INTO favorites_music VALUES (25, 6, 10);
INSERT INTO favorites_music VALUES (26, 6, 11);
INSERT INTO favorites_music VALUES (27, 7, 1);
INSERT INTO favorites_music VALUES (28, 7, 2);
INSERT INTO favorites_music VALUES (29, 8, 4);
INSERT INTO favorites_music VALUES (30, 8, 7);
INSERT INTO favorites_music VALUES (31, 8, 9);
INSERT INTO favorites_music VALUES (32, 9, 16);
INSERT INTO favorites_music VALUES (33, 11, 1);
INSERT INTO favorites_music VALUES (34, 11, 2);
INSERT INTO favorites_music VALUES (35, 11, 6);
INSERT INTO favorites_music VALUES (36, 11, 8);
INSERT INTO favorites_music VALUES (37, 11, 9);

-- PLAYLISTS
INSERT INTO playlists VALUES (1, 'shdeufghs', 2);
INSERT INTO playlists VALUES (2, 'ytdyse', 2);
INSERT INTO playlists VALUES (3, 'oiujasd', 4);
INSERT INTO playlists VALUES (4, 'uydgwed', 5);
INSERT INTO playlists VALUES (5, 'isudyhiwu3e', 5);
INSERT INTO playlists VALUES (6, 'iuhyew', 6);
INSERT INTO playlists VALUES (7, 'iuysgdfi', 8);
INSERT INTO playlists VALUES (8, 'dxfwee', 9);
INSERT INTO playlists VALUES (9, 'serhdw', 11);

-- PLAYLIST MUSIC
INSERT INTO playlist_music VALUES (1, 1, 1);
INSERT INTO playlist_music VALUES (2, 1, 2);
INSERT INTO playlist_music VALUES (3, 1, 5);
INSERT INTO playlist_music VALUES (4, 2, 9);
INSERT INTO playlist_music VALUES (5, 2, 12);
INSERT INTO playlist_music VALUES (6, 2, 15);
INSERT INTO playlist_music VALUES (7, 3, 4);
INSERT INTO playlist_music VALUES (8, 3, 7);
INSERT INTO playlist_music VALUES (9, 3, 9);
INSERT INTO playlist_music VALUES (10, 3, 16);
INSERT INTO playlist_music VALUES (11, 3, 20);
INSERT INTO playlist_music VALUES (12, 4, 2);
INSERT INTO playlist_music VALUES (13, 4, 6);
INSERT INTO playlist_music VALUES (14, 4, 9);
INSERT INTO playlist_music VALUES (15, 4, 18);
INSERT INTO playlist_music VALUES (16, 5, 8);
INSERT INTO playlist_music VALUES (17, 5, 9);
INSERT INTO playlist_music VALUES (18, 5, 15);
INSERT INTO playlist_music VALUES (19, 5, 19);
INSERT INTO playlist_music VALUES (20, 6, 10);
INSERT INTO playlist_music VALUES (21, 6, 11);
INSERT INTO playlist_music VALUES (22, 7, 1);
INSERT INTO playlist_music VALUES (23, 7, 2);
INSERT INTO playlist_music VALUES (24, 8, 16);
INSERT INTO playlist_music VALUES (25, 9, 1);
INSERT INTO playlist_music VALUES (26, 1, 2);
INSERT INTO playlist_music VALUES (27, 1, 8);
INSERT INTO playlist_music VALUES (28, 1, 9);
```
#### CREATE VIEWS
```sql
-- VIEWS

DROP VIEW IF EXISTS v_music_info;
CREATE VIEW v_music_info AS 
	SELECT ml.id AS music_id, ml.title AS music_title, mg.title AS music_genre, ath.nickname AS author_nickname FROM music_list ml
	JOIN music_genre mg ON mg.id = ml.genre_id
	JOIN authors ath ON ath.id = ml.author_id;

DROP VIEW IF EXISTS v_playlists_info;
CREATE VIEW v_playlists_info AS 
	SELECT pls.id AS playlist_id, pls.title AS playlist_title, ml.title AS song_title FROM playlists pls
	JOIN playlist_music pm ON pm.playlist_id = pls.id
	JOIN music_list ml ON ml.id = pm.song_id;
	
DROP VIEW IF EXISTS v_favorite_music_info;
CREATE VIEW v_favorite_music_info AS 
	SELECT us.id AS user_id, us.nickname AS user_nickname, ml.title AS song_title FROM users us
	JOIN favorites_music fvm ON fvm.user_id = us.id
	JOIN music_list ml ON ml.id = fvm.song_id;

DROP VIEW IF EXISTS v_playlists_song_popularity;
CREATE VIEW v_playlists_song_popularity AS 
	SELECT ml.title AS song_title, COUNT(*) FILTER (WHERE pm.song_id = ml.id) AS added_to_playlists FROM music_list ml
	JOIN playlist_music pm ON pm.song_id = ml.id
	GROUP BY 1
	ORDER BY 2 DESC;

DROP VIEW IF EXISTS v_favorites_song_popularity;
CREATE VIEW v_favorites_song_popularity AS 
	SELECT ml.title AS song_title, COUNT(*) FILTER (WHERE fvm.song_id = ml.id) AS added_to_favorites FROM music_list ml
	JOIN favorites_music fvm ON fvm.song_id = ml.id
	GROUP BY 1
	ORDER BY 2 DESC;

-- MATERIALISED VIEWS

DROP MATERIALIZED VIEW IF EXISTS mv_music_info;
CREATE MATERIALIZED VIEW mv_music_info AS 
	SELECT ml.id AS music_id, ml.title AS music_title, mg.title AS music_genre, ath.nickname AS author_nickname FROM music_list ml
	JOIN music_genre mg ON mg.id = ml.genre_id
	JOIN authors ath ON ath.id = ml.author_id;

DROP MATERIALIZED VIEW IF EXISTS mv_vip_subscribers;
CREATE MATERIALIZED VIEW mv_vip_subscribers AS 
	SELECT * FROM users
	WHERE vip_subscriber = 'true'
```
#### SELECTS
```sql
WITH tmp_song_top AS (
	SELECT ml.title AS song_title, COUNT(*) FILTER (WHERE fvm.song_id = ml.id) AS added_to_favorites, ml.author_id FROM music_list ml
	JOIN favorites_music fvm ON fvm.song_id = ml.id
	GROUP BY 1, 3
	ORDER BY 2
), tmp_author_top AS (
	SELECT ath.id AS author_id, ath.nickname AS author_nickname, COUNT(*) FILTER (WHERE ml.author_id = ath.id AND fvm.song_id = ml.id) AS songs_in_favorites FROM authors ath
	JOIN music_list ml ON ml.author_id = ath.id
	JOIN favorites_music fvm ON fvm.song_id = ml.id
	GROUP BY 1, 2
	ORDER BY 3 DESC
), tmp_author_songs AS (
	SELECT tat.author_nickname, tst.song_title, tst.added_to_favorites  FROM tmp_author_top tat
	JOIN tmp_song_top tst ON tst.author_id = tat.author_id
), tmp_limit_3 AS (
	SELECT * FROM (SELECT tas.author_nickname, tas.song_title, row_number() over(partition by tas.author_nickname order by tas.added_to_favorites DESC) as rn FROM tmp_author_songs tas) ath_song
	WHERE rn < 4
)

SELECT author_nickname, song_title FROM tmp_limit_3;
```
#### TRIGGERS
```sql
-- TRIGGERS

-- insert new row in author_auditions table after insert in author table

CREATE OR REPLACE FUNCTION fnc_after_new_author_inserts(ath_id bigint = 0) RETURNS trigger AS $$trg_after_new_author_insert$$
INSERT INTO author_auditions (author_id)
SELECT NEW.*;
RETURN NULL;
END;
$$trg_after_new_author_insert$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_after_new_author_insert AFTER INSERT ON authors
	FOR EACH ROW EXECUTE FUNCTION fnc_after_new_author_inserts();
	
-- update auditions column from the corresponding author after insert his song in favorites

CREATE OR REPLACE FUNCTION fnc_after_insert_in_favorites_inserts(ath_id bigint = 0) RETURNS TRIGGER AS $$trg_after_insert_in_favorites_insert$$
UPDATE author_auditions
SET = auditions = auditions + 1
WHERE author_auditions.author_id = ath_id
SELECT OLD.*;
RETURN NULL;
END;
$$trg_after_new_author_insert$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_after_new_author_insert AFTER INSERT ON favorites_music
	FOR EACH ROW EXECUTE FUNCTION fnc_after_insert_in_favorites_inserts(author.id)
```
