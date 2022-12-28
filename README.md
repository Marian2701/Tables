# Tables
Для того чтобы запустить проект, вам потребуется установить Docker, на ваш компьютер. 

Ниже приведены статьи, для установки Docker, под разные операционные системы:

1) Mac OS: https://docs.docker.com/desktop/install/mac-install/
2) Ubuntu : https://docs.docker.com/engine/install/ubuntu/

После установки Docker, вам потребуется docker-compose, рекомендации по его установки вы найдете здесь: https://docker-docs.netlify.app/compose/install/

Необходимые действия по подготовке вашего компьютера выполнены.

Для запуска проекта зайдите в скаченную директорию при помощи CLI.

Запустите проект при помощи команды : docker-compose up -d
Если на вашем  компьютере отсутсвуют необходимые образы, начнется их скачивание.
После скачивания образов, проект запустится.

Для проверки работоспособности, в браузере откройте: http://localhost:5001

Для остановки запущенного проекта, в CLI введите команду: docker-compose down

Шаг 1:
Справочник 1: TILE_COMPANY  - Компания по производству плиток.

Колонки:

TC_ID        SERIAL PRIMARY KEY,

TC_NAME      VARCHAR(40) NOT NULL,

TC_DATE      DATE        NOT NULL,

TC_INCOME    NUMERIC(10, 2),

TC_STAFF     INT,

TC_COMMENT   VARCHAR(150),

TC_IS_ENABLE INT DEFAULT (1)

Справочник 2: TILES  - Плитка.

Колонки:

TIL_ID        SERIAL PRIMARY KEY,

TIL_NAME      VARCHAR(40) NOT NULL,

TIL_SIZE      INT         NOT NULL,

TIL_PRICE     NUMERIC(10, 2),

TIL_DATE      DATE        NOT NULL,

TC_REFID      INT,

TIL_COMMENT   VARCHAR(150),

TIL_IS_ENABLE INT DEFAULT (1)

Шаг2:

1) Postgresql

2) CREATE TABLE TILE_COMPANY
(
    TC_ID        SERIAL PRIMARY KEY,
    
    TC_NAME      VARCHAR(40) NOT NULL,
    
    TC_DATE      DATE        NOT NULL,
    
    TC_INCOME    NUMERIC(10, 2),
    
    TC_STAFF     INT,
    
    TC_COMMENT   VARCHAR(150),
    
    TC_IS_ENABLE INT DEFAULT (1)
    
);


comment on column TILE_COMPANY.TC_ID is 'Tile Company ID';

comment on column TILE_COMPANY.TC_NAME is 'Tile Company name';

comment on column TILE_COMPANY.TC_DATE is 'Tile Company creation date';

comment on column TILE_COMPANY.TC_INCOME is 'Tile Company income';

comment on column TILE_COMPANY.TC_STAFF is 'Tile Company staff amount';

comment on column TILE_COMPANY.TC_COMMENT is 'Comment about Tile Company';

comment on column TILE_COMPANY.TC_IS_ENABLE is 'Tile Company enabling';

INSERT INTO TILE_COMPANY (TC_NAME,TC_DATE,TC_INCOME,TC_STAFF,TC_COMMENT) VALUES ('Ceramin',to_date('1999-1-1' ,'YYYY-MM-DD'),7000000.05,500,'Belarusian Tile factory');

INSERT INTO TILE_COMPANY (TC_NAME,TC_DATE,TC_INCOME,TC_STAFF,TC_COMMENT) VALUES ('Maryan Tile LTD',to_date('2001-10-02' ,'YYYY-MM-DD'),100.05,1,'Maryan Tile work');

CREATE TABLE TILES
(
    TIL_ID        SERIAL PRIMARY KEY,
    
    TIL_NAME      VARCHAR(40) NOT NULL,
    
    TIL_SIZE      INT         NOT NULL,
    
    TIL_PRICE     NUMERIC(10, 2),
    
    TIL_DATE      DATE        NOT NULL,
    
    TC_REFID      INT,
    
    TIL_COMMENT   VARCHAR(150),
    
    CONSTRAINT TILES_TC_REFID_F_KEY FOREIGN KEY (TC_REFID) REFERENCES TILE_COMPANY (TC_ID),
    
    TIL_IS_ENABLE INT DEFAULT (1)
    
);

INSERT INTO TILES (TIL_NAME,TIL_SIZE,TIL_PRICE,TIL_DATE,TC_REFID,TIL_COMMENT) VALUES ('Spain sabor',50,45.67,to_date('1847-04-21' ,'YYYY-MM-DD'),1,'Old Tile from Davinchi');

INSERT INTO TILES (TIL_NAME,TIL_SIZE,TIL_PRICE,TIL_DATE,TC_REFID,TIL_COMMENT) VALUES ('Farnce sabor',12,100.67,to_date('1647-03-17' ,'YYYY-MM-DD'),1,'Old Tile from Gigo');

INSERT INTO TILES (TIL_NAME,TIL_SIZE,TIL_PRICE,TIL_DATE,TC_REFID,TIL_COMMENT) VALUES ('Kitchen',30,35.98,to_date('2022-12-12' ,'YYYY-MM-DD'),2,'Tile To Kleck');

INSERT INTO TILES (TIL_NAME,TIL_SIZE,TIL_PRICE,TIL_DATE,TC_REFID,TIL_COMMENT) VALUES ('Bathroom',5,5.00,to_date('2019-06-03' ,'YYYY-MM-DD'),2,'Tile to Dzerzinsk');

comment on column TILES.TIL_ID is 'Tiles ID';

comment on column TILES.TIL_NAME is 'Tiles name';

comment on column TILES.TIL_SIZE is 'Tiles size';

comment on column TILES.TIL_PRICE is 'Tiles price';

comment on column TILES.TIL_DATE is 'Tiles creation date';

comment on column TILES.TC_REFID is 'Tiles Company name';

comment on column TILES.TIL_COMMENT is 'Comment about Tile';

comment on column TILES.TIL_IS_ENABLE is 'Tiles enabling';

А также **изображение_1**, **изображение_2** и **изображение_3**

Шаг 3:
1) Python flask, Postgresql
