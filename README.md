# sql
CREATE SCHEMA `shop2` ;
use shop2;

drop table product;
create table product (
	id int not null primary key auto_increment,
    article_number varchar(128) not null
);

--
create table order_products (
    product_id int not null,
    order_id int not null,
    `count` int not null
);
drop table order_products;

--
create table `order` (
	id int not null primary key auto_increment,
    user_name varchar(128) not null,
    phone varchar(32) not null
);

SELECT * FROM product;
SELECT * FROM order_products;
SELECT * FROM `order`;
SELECT * FROM brand;
SELECT * FROM product_type;

truncate product;
ALTER TABLE product AUTO_INCREMENT = 3;
delete from product where id > 3;

insert into product (article_number, brand_id) values ('qweasdzxc', 1);
insert into product (article_number, brand_id) values ('123456789', 2);
insert into product (article_number, brand_id) values ('poi;lk/.,', 2);

-- add additional columns to product
alter table product add column product_type_id int not null;
alter table product add column price decimal(10,2) not null;
-- end

-- add data to added columns
update product
	set brand_id = 2
    where id = 3;
    
update product
	set product_type_id = 1, price = 190
    where id = 1;
-- end

insert into `order` (user_name, phone) values ('bench', '555-555-555');
insert into `order` (user_name, phone) values ('nuni', '42-42-42');

-- Added foreign keys
ALTER TABLE `shop2`.`order_products` 
ADD INDEX `fk_order_products_product_idx` (`product_id` ASC),
ADD INDEX `fk_order_product_order_idx` (`order_id` ASC);
ALTER TABLE `shop2`.`order_products` 
ADD CONSTRAINT `fk_order_products_product`
  FOREIGN KEY (`product_id`)
  REFERENCES `shop2`.`product` (`id`)
  ON DELETE cascade
  ON UPDATE cascade,
ADD CONSTRAINT `fk_order_product_order`
  FOREIGN KEY (`order_id`)
  REFERENCES `shop2`.`order` (`id`)
  ON DELETE cascade
  ON UPDATE cascade;
-- -------------------

-- Add primary keys for order_products
ALTER TABLE `shop2`.`order_products` 
ADD PRIMARY KEY (`product_id`, `order_id`);
-- 

insert into order_products (product_id, order_id, `count`) values (1, 1, 4);
insert into order_products (product_id, order_id, `count`) values (1, 2, 5);
insert into order_products (product_id, order_id, `count`) values (2, 2, 6);


-- additional tables

create table brand(
	id int not null primary key auto_increment,
    brand_name varchar(128) not null
);

create table product_type(
	id int not null primary key auto_increment,
    product_type_name varchar(128) not null,
    discount int not null
);

insert into brand (brand_name) values ('Nike');
insert into brand (brand_name) values ('Adidas');
insert into brand (brand_name) values ('Reebok');
insert into brand (brand_name) values ('Jhordan');


insert into product_type (product_type_name, discount) values('t-short', 5);
insert into product_type (product_type_name, discount) values('socks', 5);
insert into product_type (product_type_name, discount) values('cross', 5);
insert into product_type (product_type_name, discount) values('run cross', 5);


alter table product add column brand_id int not null;

--
ALTER TABLE `shop2`.`product` 
ADD INDEX `fk_product_brand_idx` (`brand_id` ASC),
ADD INDEX `fk_product_product_type_idx` (`product_type_id` ASC);
ALTER TABLE `shop2`.`product` 
ADD CONSTRAINT `fk_product_brand`
  FOREIGN KEY (`brand_id`)
  REFERENCES `shop2`.`brand` (`id`)
  ON DELETE CASCADE
  ON UPDATE CASCADE,
ADD CONSTRAINT `fk_product_product_type`
  FOREIGN KEY (`product_type_id`)
  REFERENCES `shop2`.`product_type` (`id`)
  ON DELETE CASCADE
  ON UPDATE CASCADE;

--

select * from product
	inner join brand on brand_id = brand.id;
    
select * from product
	 join brand on brand_id = brand.id;

