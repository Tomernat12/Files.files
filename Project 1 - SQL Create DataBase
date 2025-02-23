-- SQL * FIRST PROJECT 
--- TABLE DESIGN & CREATION ABOUT ALCOHOLIC DRINKS 

USE master;
GO

CREATE DATABASE Economy;
GO

USE Economy;
GO

CREATE TABLE Sectors (
    sector_id INT IDENTITY PRIMARY KEY,
    sector_name VARCHAR(255) NOT NULL,
    sector_description VARCHAR(255),
    number_of_companies INT);
GO

CREATE TABLE Countries (
    country_id INT IDENTITY PRIMARY KEY,
    country_name VARCHAR(255) NOT NULL,
    GDP MONEY,
    population INT,
    currency VARCHAR(50));
GO

CREATE TABLE Companies (
    company_id INT IDENTITY PRIMARY KEY,
    company_name VARCHAR(255) NOT NULL,
    ticker_symbol VARCHAR(10),
    market_cap MONEY,
    sector_id INT,
    country_id INT,
    FOREIGN KEY (sector_id) REFERENCES Sectors(sector_id),
    FOREIGN KEY (country_id) REFERENCES Countries(country_id));
GO

CREATE TABLE CEOs (
    ceo_id INT IDENTITY PRIMARY KEY,
    ceo_name VARCHAR(255) NOT NULL,
    age INT,
    net_worth MONEY,
    company_id INT,
    FOREIGN KEY (company_id) REFERENCES Companies(company_id));
GO

CREATE TABLE Leaders (
    leader_id INT IDENTITY PRIMARY KEY,
    leader_name VARCHAR(255) NOT NULL,
    country_id INT,
    net_worth MONEY,
    term_start DATE,
    term_end DATE,
    FOREIGN KEY (country_id) REFERENCES Countries(country_id));
GO

INSERT INTO Countries (country_name, GDP, population, currency)
VALUES
('United States', 25000000.00, 331000000, 'USD'),
('China', 17400000.00, 1444216107, 'CNY'),
('Japan', 4900000.00, 125584838, 'JPY'),
('Germany', 4000000.00, 83166711, 'EUR'),
('India', 3100000.00, 1393409038, 'INR'),
('United Kingdom', 3100000.00, 68207114, 'GBP'),
('France', 2900000.00, 67391582, 'EUR'),
('Italy', 2100000.00, 60262770, 'EUR'),
('Canada', 2000000.00, 37742154, 'CAD'),
('Russia', 1700000.00, 145912025, 'RUB'),
('South Korea', 1800000.00, 51329899, 'KRW'),
('Australia', 1400000.00, 25687041, 'AUD'),
('Brazil', 2100000.00, 212559417, 'BRL'),
('Spain', 1400000.00, 46719142, 'EUR'),
('Mexico', 1200000.00, 128933395, 'MXN'),
('Indonesia', 1100000.00, 273523615, 'IDR'),
('Netherlands', 900000.00, 17134872, 'EUR'),
('Saudi Arabia', 800000.00, 34813867, 'SAR'),
('Turkey', 700000.00, 84339067, 'TRY'),
('South Africa', 400000.00, 59308690, 'ZAR'),
('Senegal', 100000.00, 16925000, 'XOF'),
('Iran', 500000.00, 83992949, 'IRR'),
('Romania', 600000.00, 19237691, 'RON'),
('Poland', 600000.00, 38386000, 'PLN'),
('Ukraine', 600000.00, 43733762, 'UAH');
GO

INSERT INTO Sectors (sector_name, sector_description, number_of_companies)
VALUES
('Information Technology', 'Companies that deal with technology and software', 74),
('Health Care', 'Companies in the health care and pharmaceutical industries', 63),
('Financials', 'Banks, investment firms, and insurance companies', 58),
('Consumer Discretionary', 'Companies that sell non-essential goods and services', 57),
('Communication Services', 'Companies that provide communication and media services', 25),
('Industrials', 'Companies involved in manufacturing and infrastructure', 68),
('Consumer Staples', 'Companies that provide essential products', 34),
('Energy', 'Companies involved in oil, gas, and other energy resources', 26),
('Materials', 'Companies in raw materials production and distribution', 28),
('Utilities', 'Companies that provide essential public services', 16),
('Real Estate', 'Companies involved in the real estate sector', 29),
('Healthcare Equipment and Services', 'Companies involved in medical supplies and healthcare services', 30),
('Automobiles', 'Companies manufacturing automobiles and parts', 15),
('Retailing', 'Companies involved in the sale of goods and services', 19),
('Technology Hardware & Equipment', 'Manufacturers of electronic equipment', 22),
('Semiconductors', 'Companies that produce semiconductor materials and equipment', 19),
('Transportation', 'Companies that provide transport services', 17),
('Banking', 'Commercial and investment banks', 29),
('Insurance', 'Companies providing insurance services', 14),
('Aerospace & Defense', 'Companies involved in defense and aerospace production', 11),
('Pharmaceuticals', 'Companies that produce drugs and pharmaceuticals', 18),
('Food & Staples Retailing', 'Companies in the food and beverage retail market', 20),
('Homebuilders', 'Companies involved in the construction of residential homes', 9),
('Leisure Products', 'Companies in the entertainment and leisure industries', 8),
('Insurance Brokers', 'Companies that provide brokerage services in insurance', 5);
GO


INSERT INTO Companies (company_name, ticker_symbol, market_cap, sector_id, country_id) 
VALUES
('Apple', 'AAPL', 2200000000000.00, 1, 1),
('Microsoft', 'MSFT', 1800000000000.00, 1, 1),
('Amazon', 'AMZN', 1600000000000.00, 4, 1),
('Tesla', 'TSLA', 800000000000.00, 8, 1),
('Meta', 'META', 800000000000.00, 5, 1),
('NVIDIA', 'NVDA', 600000000000.00, 1, 1),
('Berkshire Hathaway', 'BRK.A', 700000000000.00, 3, 1),
('Alphabet', 'GOOG', 1800000000000.00, 1, 1),
('Johnson & Johnson', 'JNJ', 500000000000.00, 2, 1),
('Walmart', 'WMT', 400000000000.00, 4, 1),
('Visa', 'V', 400000000000.00, 3, 1),
('Procter & Gamble', 'PG', 350000000000.00, 2, 1),
('Home Depot', 'HD', 350000000000.00, 4, 1),
('Coca-Cola', 'KO', 250000000000.00, 2, 1),
('Pfizer', 'PFE', 250000000000.00, 2, 1),
('Chevron', 'CVX', 250000000000.00, 8, 1),
('ExxonMobil', 'XOM', 300000000000.00, 8, 1),
('JPMorgan Chase', 'JPM', 450000000000.00, 3, 1),
('UnitedHealth', 'UNH', 500000000000.00, 2, 1),
('AbbVie', 'ABBV', 250000000000.00, 2, 1),
('Mastercard', 'MA', 350000000000.00, 3, 1),
('Intel', 'INTC', 200000000000.00, 1, 1),
('Nike', 'NKE', 250000000000.00, 4, 1),
('Disney', 'DIS', 200000000000.00, 4, 1),
('McDonalds', 'MCD', 200000000000.00, 4, 1);
GO

INSERT INTO CEOs (ceo_name, age, net_worth, company_id) 
VALUES
('Tim Cook', 63, 100000000000.00, 1),      
('Satya Nadella', 52, 150000000000.00, 2), 
('Andy Jassy', 53, 130000000000.00, 3),    
('Elon Musk', 52, 250000000000.00, 4),     
('Mark Zuckerberg', 40, 90000000000.00, 5),
('Jensen Huang', 61, 25000000000.00, 6),   
('Warren Buffett', 93, 90000000000.00, 7), 
('Sundar Pichai', 51, 120000000000.00, 8), 
('Alex Gorsky', 61, 15000000000.00, 9),    
('Doug McMillon', 55, 20000000000.00, 10), 
('Alfred Kelly', 61, 35000000000.00, 11),  
('David Taylor', 64, 70000000000.00, 12),  
('Craig Menear', 63, 35000000000.00, 13),  
('James Quincey', 56, 40000000000.00, 14), 
('Albert Bourla', 61, 20000000000.00, 15), 
('Mike Wirth', 63, 30000000000.00, 16),    
('Darren Woods', 57, 25000000000.00, 17),  
('Jamie Dimon', 67, 180000000000.00, 18),  
('Andrew Witty', 60, 30000000000.00, 19),  
('Richard Gonzalez', 68, 70000000000.00, 20),
('Michael Miebach', 57, 50000000000.00, 21), 
('Pat Gelsinger', 60, 40000000000.00, 22), 
('Elliott Hill', 61, 50000000000.00, 23),  
('Bob Chapek', 62, 80000000000.00, 24),    
('Chris Kempczinski', 54, 10000000000.00, 25);
GO

INSERT INTO Leaders (leader_name, country_id, net_worth, term_start, term_end)
VALUES
('Joe Biden', 1, 900000000, '2021-01-20', '2025-01-20'),      
('Xi Jinping', 2, 1100000000, '2013-03-14', '2028-03-14'),    
('Fumio Kishida', 3, 50000000, '2021-10-04', '2025-10-04'),   
('Olaf Scholz', 4, 10000000, '2021-12-08', '2025-12-08'),     
('Narendra Modi', 5, 2000000, '2014-05-26', '2024-05-26'),    
('Rishi Sunak', 6, 90000000, '2022-10-25', '2026-10-25'),    
('Emmanuel Macron', 7, 15000000, '2017-05-14', '2027-05-14'),  
('Giuseppe Conte', 8, 1000000, '2018-06-01', '2022-10-13'),   
('Justin Trudeau', 9, 10000000, '2015-11-04', '2025-11-04'),  
('Vladimir Putin', 10, 7000000000, '2012-05-07', '2026-05-07'),
('Moon Jae-in', 11, 50000000, '2017-05-10', '2022-05-09'),    
('Anthony Albanese', 12, 4000000, '2022-05-23', '2026-05-23'),
('Jair Bolsonaro', 13, 10000000, '2019-01-01', '2023-12-31'), 
('Pedro Sánchez', 14, 5000000, '2018-06-02', '2025-06-02'),   
('Andrés Manuel López Obrador', 15, 1000000, '2018-12-01', '2024-12-01'),
('Joko Widodo', 16, 1000000, '2014-10-20', '2024-10-20'),    
('Mark Rutte', 17, 4000000, '2010-10-14', '2026-10-14'),     
('Mohammed bin Salman', 18, 1700000000, '2017-06-21', '2026-06-21'),
('Recep Tayyip Erdoğan', 19, 50000000, '2014-08-28', '2026-08-28'), 
('Cyril Ramaphosa', 20, 450000000, '2018-02-15', '2026-02-15'),
('Macky Sall', 21, 10000000, '2012-04-02', '2025-04-02'),    
('Ali Khamenei', 22, 2000000000, '1989-06-04', '2025-06-04'),
('Klaus Iohannis', 23, 2000000, '2014-12-21', '2025-12-21'), 
('Andrzej Duda', 24, 1000000, '2015-08-06', '2025-08-06'),   
('Vladimir Zelensky', 25, 600000, '2019-05-20', '2025-05-20');

