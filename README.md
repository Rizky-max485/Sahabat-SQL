# Sahabat-SQL

CREATE TABLE `pengguna` (
	`user_id` INTEGER,
	`nama` VARCHAR(255) NOT NULL,
	`email` VARCHAR(255) NOT NULL UNIQUE,
	`password` VARCHAR(255) NOT NULL,
	`member` BOOLEAN DEFAULT FALSE,
	`join_date` DATETIME,
	PRIMARY KEY(`user_id`)
);


CREATE TABLE `Artis` (
	`artis_id` INTEGER,
	`nama` VARCHAR(255),
	PRIMARY KEY(`artis_id`)
);


CREATE TABLE `Album` (
	`album_id` INTEGER,
	`judul` VARCHAR(255),
	`artis_id` INTEGER,
	`rilis_date` DATE,
	PRIMARY KEY(`album_id`),
    FOREIGN KEY (artis_id) REFERENCES Artis(artis_id)
);


CREATE TABLE `Lagu` (
	`lagu_id` INTEGER,
	`judul` VARCHAR(255),
	`durasi` INTEGER,
	`album_id` INTEGER,
	`play_count` INTEGER DEFAULT 0,
	PRIMARY KEY(`lagu_id`),
    FOREIGN KEY (album_id) REFERENCES Album(album_id)
);


CREATE TABLE `Playlist` (
	`playlist_id` INTEGER,
	`user_id` INTEGER,
	`playlist_nama` VARCHAR(255),
	`playlist_dibuat` DATETIME,
	PRIMARY KEY(`playlist_id`),
    FOREIGN KEY (user_id) REFERENCES Pengguna(user_id)
);


CREATE TABLE `Playlist_Lagu` (
	`playlist_id` INTEGER,
	`lagu_id` INTEGER,
	PRIMARY KEY(`playlist_id`, `lagu_id`),
    FOREIGN KEY (playlist_id) REFERENCES Playlist(playlist_id),
    FOREIGN KEY (lagu_id) REFERENCES Lagu(lagu_id)
);


CREATE TABLE `riwayat_lagu` (
	`riwayat_id` INTEGER,
	`user_id` INTEGER,
	`lagu_id` INTEGER,
	`play_lagu` DATETIME,
	PRIMARY KEY(`riwayat_id`),
    FOREIGN KEY (user_id) REFERENCES Pengguna(user_id),
    FOREIGN KEY (lagu_id) REFERENCES Lagu(lagu_id)
);


CREATE TABLE `Transaksi` (
	`transaksi_id` INTEGER,
	`user_id` INTEGER,
	`saldo` DECIMAL,
	`transaksi_date` DATETIME,
	`status` VARCHAR(255),
	PRIMARY KEY(`transaksi_id`),
    FOREIGN KEY (user_id) REFERENCES Pengguna(user_id)
);
