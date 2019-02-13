# Database
CREATE TABLE Customer(
CustomerID int, 
CustomerName varchar(30), 
CustomerAddress varchar(40),
CustomerCity varchar(20), 
CustomerState varchar(3), 
CustomerPostalCode varchar(15), 
CustomerEmail varchar(40), 
CustomerUserName varchar(20),
CustomerPassowrd varchar(20),
PRIMARY KEY (CustomerID)
);


INSERT INTO Customer VALUES (1, 'Contemporary Casuals', '1355 S Hines Blvd', 'Gainesville', 'FL', '32601-2871', null, null, null);
INSERT INTO Customer VALUES (2, 'Value Furnitures', '15145 S.W. 17th St.', 'Plano', 'TX', '75094-7734', null, null, null);
INSERT INTO Customer VALUES (3, 'Home Furnishings', '1900 Allard Ave', 'Albany', 'NY', '12209-1125', 'homefurnishings?@gmail.com', 'CUSTOMER1','CUSTOMER1#');
INSERT INTO Customer VALUES (4, 'Eastern Furniture', '1925 Beltline Rd.', 'Carteret', 'NJ', '07008-3188', null, null, null);
INSERT INTO Customer VALUES (5, 'Impressions', '5585 Westcott Ct.', 'Sacramento', 'CA', '94206-4056', null, null, null);
INSERT INTO Customer VALUES (6, 'Furniture Gallery', '325 Flatiron Dr.', 'Boulder', 'CO', '80514-4432', null, null, null);
INSERT INTO Customer VALUES (7, 'New Furniture', 'Palace Ave', 'Farmington', 'NM', null, null, null, null);
INSERT INTO Customer VALUES (8, 'Dunkins Furniture', '7700 Main St', 'Syracuse', 'NY', '31590', null, null, null); 
INSERT INTO Customer VALUES (9, 'A Carpet', '434 Abe Dr', 'Rome', 'NY', '13440', null, null, null);
INSERT INTO Customer VALUES (12, 'Flanigan Furniture', 'Snow Flake Rd', 'Ft Walton Beach', 'FL', '32548', null, null, null);
INSERT INTO Customer VALUES (13, 'Ikards', '1011 S. Main St', 'Las Cruces', 'NM', '88001', null, null, null); 
INSERT INTO Customer VALUES (14, 'Wild Bills', 'Four Horse Rd', 'Oak Brook', 'Il', '60522', null, null, null); 
INSERT INTO Customer VALUES (15, 'Janet''s Collection', 'Janet Lane', 'Virginia Beach', 'VA', '10012', null, null, null);
INSERT INTO Customer VALUES (16, 'ABC Furniture Co.', '152 Geramino Drive', 'Rome', 'NY', '13440', null, null, null);

CREATE TABLE Territory(
TerritoryID int, 
TerritoryName varchar(15),
PRIMARY KEY (TerritoryID)
);

CREATE TABLE SalesPerson(
SalespersonID int, 
SalespersonName varchar(20),
SalespersonPhone varchar(20), 
SalespersonEmail varchar(30),
SalespersonUserName varchar(20),
SalespersonPassword varchar(20),
TerritoryID int, 
FOREIGN KEY (TerritoryID) REFERENCES Territory(TerritoryID)
);

CREATE TABLE DoesBusinessIn(
CustomerID int,
TerritoryID int NOT NULL UNIQUE, 
PRIMARY KEY (CustomerID),
FOREIGN KEY (CustomerID) REFERENCES Customer(CustomerID),
FOREIGN KEY (TerritoryID) REFERENCES Territory(TerritoryID)
);

CREATE TABLE ProductLine(
ProductLineID int, 
ProductLineName varchar(20),
PRIMARY KEY (ProductLineID)
);


CREATE TABLE Product(
ProductID int, 
ProductName varchar(20), 
ProductFinish varchar(20), 
ProductStandardPrice varchar(20), 
ProductLineID int, 
Photo clob,
PRIMARY KEY (ProductID),
FOREIGN KEY (ProductLineID) REFERENCES ProductLine(ProductLineID)
);

CREATE TABLE Orders(
OrderID int,
OrderDate date,
CustomerID int,
PRIMARY KEY (OrderID), 
FOREIGN KEY (CustomerID) REFERENCES Customer(CustomerID)
);

CREATE TABLE OrderLine(
OrderID int, 
ProductID int, 
OrderedQuantity int, 
SalePrice decimal(38,2),
PRIMARY KEY (OrderID),
FOREIGN KEY (OrderID) REFERENCES Orders(OrderID), 
FOREIGN KEY (ProductID) REFERENCES Product(ProductID)
);


CREATE TABLE PriceUpdate(
PriceUpdateID int, 
DateChanged date, 
OldPrice decimal(38,2), 
NewPrice decimal(38,2),
PRIMARY KEY (PriceUpdateID)
);
