DROP TABLE IF EXISTS users;
DROP TABLE IF EXISTS televisions_wallbrackets;
DROP TABLE IF EXISTS televisions;
DROP TABLE IF EXISTS remote_controllers;
DROP TABLE IF EXISTS ci_modules;
DROP TABLE IF EXISTS wallbrackets;


CREATE TABLE users (
	-- ipv id serial primary key gebruik ik de SQL standaard.
	-- https://stackoverflow.com/questions/55300370/postgresql-serial-vs-identity
	id int GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
	username varchar(255),
	password varchar(255)
);

CREATE TABLE remote_controllers (
	id int GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
	name varchar(255) NOT NULL UNIQUE,
	brand varchar(255) NOT NULL,
	price decimal NOT NULL,
	current_stock int,
	sold int,
	compatible_with varchar(255),
	battery_type varchar(255)
);

-- in het klassediagram staan bij ciModules en wallbrackets geen 'compatibleWith' opties

CREATE TABLE ci_modules (
	id int GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
	name varchar(255) NOT NULL UNIQUE,
	brand varchar(255) NOT NULL,
	price decimal,
	current_stock int,
	sold int
);

CREATE TABLE wallbrackets (
	id int GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
	name varchar(255) NOT NULL UNIQUE,
	brand varchar(255) NOT NULL,
	price decimal,
	current_stock int,
	sold int,
	adjustable boolean
);

CREATE TABLE televisions (
	id int GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
	name varchar(255) NOT NULL UNIQUE,
	brand varchar(255) NOT NULL,
	price decimal,
	current_stock int,
	sold int,
	type varchar(255),
	refresh_rate decimal,
	screentype varchar(255),
	remote_id int,
	cimodule_id int,
	CONSTRAINT fk_remote FOREIGN KEY (remote_id) REFERENCES remote_controllers(id),
	CONSTRAINT fk_cimodule FOREIGN KEY (cimodule_id) REFERENCES ci_modules(id)
);

CREATE TABLE televisions_wallbrackets(
	television_id int,
	wallbracket_id int,
	CONSTRAINT fk_television FOREIGN KEY (television_id) REFERENCES televisions(id),
	CONSTRAINT fk_wallbracket FOREIGN KEY (wallbracket_id) REFERENCES wallbrackets(id)
);

INSERT INTO remote_controllers(name, brand, price, current_stock, sold, compatible_with, battery_type)
VALUES ('URC4910', 'Samsung', 29.99, 13, 5, 'Samsung', 'AAA'),
	('URC4913', 'Philips', 38, 10, 2, 'Philips', 'AAA'),
	('URC7935', 'One for All', 38, 15, 7, 'Universeel', 'AAA');

INSERT INTO ci_modules(name, brand, price, current_stock, sold)
VALUES ('Quantis CI+ 1.3', 'Quantis', 69.95, 25, 5),
	('Smit CI+ 1.3', 'SMiT', 61, 20, 3);

INSERT INTO wallbrackets(name, brand, price, current_stock, sold, adjustable)
VALUES('BlueBuilt draaibaar 48" - 75"', 'BlueBuilt', 104.99, 25, 5, true),
	('BlueBuilt vast 50" - 75"', 'BlueBuilt', 57.99, 20, 2, false);

INSERT INTO televisions(name, brand, price, current_stock, sold, type, screentype, remote_id, cimodule_id)
VALUES('OLED55CS6LA', 'LG', 1199, 15, 5, 'S', 'OLED', 3, 1),
	('OLED65S95B', 'Samsung', 2069, 10, 3, 'M', 'OLED', 1, 1),
	('QLED50Q64B', 'Philips', 799, 5, 4, 'S', 'QLED', 2, 2);

INSERT INTO televisions_wallbrackets(television_id, wallbracket_id)
VALUES(1,1),
	(2,1),
	(3,2);

INSERT INTO users(username, password)
VALUES ('user1', 'laksdjifwo1'),
	('admin', 'ljksoiwwea2');

-- SELECT * FROM televisions;

select CONCAT(t.name, ' van ', t.brand, ' heeft een ci-module van ', c.brand,
			  ' en een afstandsbediening van ', r.brand)
from televisions t
join ci_modules c on c.id = t.cimodule_id
join remote_controllers r on r.id = t.remote_id;