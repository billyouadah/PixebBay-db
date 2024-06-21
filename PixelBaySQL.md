# Projet SQL PixelBay : Création et gestion d'une base de données pour une boutique de jeux vidéo en ligne


### Mission 1 : Création de la base de données

CREATE DATABASE PixelBayDB : Création de la base de données PixelBayDB


### Mission 2 : Création de la table des produits
Création d'une table de products avec définitions de types attendus (éventuellement nombre de caractères)

USE PixelBayDB
CREATE TABLE products (
    products_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    price DECIMAL,
    category VARCHAR(100),
    in_stock BOOLEAN,
);


### Mission 3 : Insertion de produits

INSERT INTO products (name, price, category , in_stock) VALUES
('Final Fantasy XV', 59.99, 'RPG', 'true'),
('Super Mario Odyssey', 49.99, 'Aventure', 'true'),
('FIFA 2024', 69.99, 'Sport', 'false'),
USE PixelBaydb;

+++

INSERT INTO products (name, price, category, in_stock) VALUES
('Geometry Wars', 39.99, 'Space', true),
('Tekken', 49.99, 'Fight', true),
('Skate 3', 69.99, 'Sport', false);

D'abord il faut préciser les attributs qui seront incérés et ensuite on "injecte" les bonnes valeurs (dans le type adapté)

### Mission 4 : Création et gestion des utilisateurs

CREATE TABLE users (
    users_id INT AUTO_INCREMENT PRIMARY KEY,
    email VARCHAR(255) UNIQUE,
    name VARCHAR(255),
    password VARCHAR(255)
);

++- Ajoutez des exemples d'utilisateurs.

INSERT INTO users (email, name, password) VALUES
('jeanmarc@free.fr', 'Jean Marc', 'oputrjuike4'),
('marietutu@gmail.com', 'Marie Tutu', 'jupfrporte7'),
('remifrancois@gmail.com', 'Remi François', 'kopkopmo2');
('francoisremi@gmail.com', 'François Remi', 'kopkopmo4');

Nouvelle table avec les mêmes commandes que précédement 
### Mission 5 : Requêtes de sélection

- Sélectionnez tous les jeux de la catégorie "RPG".

SELECT * FROM products WHERE category = 'RPG';


- Trouvez tous les produits en stock.

SELECT * FROM products WHERE in_stock = true;

SELECT permet de selectionner les données d'une table (ici products) qui font partie de la catégorie RPG

### Mission 6 : Mises à jour des données

- Mettez à jour le prix de "Super Mario Odyssey" à 44.99.

UPDATE products SET price = 44.99 WHERE name = 'Super Mario Odyssey';


- Changez le statut de "en_stock" pour "FIFA 2024" à true.

UPDATE products SET in_stock = true WHERE name = 'FIFA 2024';

Set permet d'envoyer une nouvelle valeur dans un attribut

### Mission 7 : Fonctions avancées

- Calculez le prix moyen des produits dans chaque catégorie.

SELECT AVG(price) AS avg_price_rpg FROM products WHERE category = 'RPG';
SELECT AVG(price) AS avg_price_adventure FROM products WHERE category = 'Adventure';
SELECT AVG(price) AS avg_price_sport FROM products WHERE category = 'Sport';
SELECT AVG(price) AS avg_price_fight FROM products WHERE category = 'Fight';


- Sélectionnez le produit le plus cher et le moins cher.

SELECT 
    MAX(price) AS prix_le_plus_cher,
    MIN(price) AS prix_le_moins_cher
FROM products;

### Mission 8 : Gestion des commandes

CREATE TABLE orders (
    orders_id INT AUTO_INCREMENT PRIMARY KEY,
    users_id INT,
    FOREIGN KEY (users_id) REFERENCES users(users_id),
    date DATETIME,
    status VARCHAR(100)
);

- Insérez des exemples de commandes.


INSERT INTO orders (users_id, date, status) VALUES
(1, '2024-04-17 10:00:00', 'En cours'),
(2, '2024-04-16 14:30:00', 'Expédiée'),
(3, '2024-04-15 09:45:00', 'En cours');


### Mission 9 : Jointures
 CREATE TABLE orders_products (
      orders_id INT,
      products_id INT,
      FOREIGN KEY (orders_id) REFERENCES ORDERS(orders_id) ON DELETE CASCADE ON UPDATE CASCADE,
      FOREIGN KEY (products_id) REFERENCES PRODUCTS(products_id) ON DELETE CASCADE ON UPDATE CASCADE
  );
- Affichez toutes les commandes avec les informations des utilisateurs.

SELECT o.orders_id, o.date, o.status, u.email, u.name
FROM orders o
JOIN users u ON o.users_id = u.users_id;

- Montrez les détails de tous les produits commandés par chaque utilisateur.

### Mission 10 : Suppression de données


MAJ du 21 juin : j'avais un souci avec les décimales de mes prix produit. j'ai modifié le champ price avec cette requête : 

ALTER TABLE products MODIFY price DECIMAL(10, 2);

Ensuite pour vérifier que ça fontionnait, j'ai rajouté un produit : 

INSERT INTO products (name, price, category, in_stock) VALUES ('Skate 4', 69.99, 'Sport', false);
