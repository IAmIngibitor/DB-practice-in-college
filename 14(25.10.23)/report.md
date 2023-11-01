## Приложение: потоковый сервис музыки
### Схема баз данных
![diagram drawio (1) drawio (3)](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/7bc19af2-e87f-4363-96e7-3aa3af40d526)
### SQL
```sql
DROP SCHEMA public cascade;
CREATE SCHEMA public;

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
    email varchar NOT NULL,
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

INSERT INTO users VALUES (1, 'Кирилл', 'slkdjg@mail.ru', true);
INSERT INTO users VALUES (2, 'Антон', 'hhdfgs@mail.ru');
INSERT INTO users VALUES (3, 'Максим', 'sfhksdfg@mail.ru');
INSERT INTO users VALUES (4, 'Иван', 'efgdghd@mail.ru', true);
INSERT INTO users VALUES (5, 'afgs', 'edskdg@mail.ru');
INSERT INTO users VALUES (6, 'Кириajgfjлл', 'amsdfa@mail.ru');
INSERT INTO users VALUES (7, 'gsfdhssd', 'fgjgts@mail.ru');
INSERT INTO users VALUES (8, 'Киdfgdfhdрилл', 'fsgasdef@mail.ru', true);
```



