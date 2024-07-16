## Zadanie

Wykonaj poniższy skrypt na bazie `LibraryDatabase`, zapoznaj się z dodanymi wierszami, a następnie wykonaj zadania.

### Skrypt




```sql
BEGIN TRAN


-- Genres
INSERT INTO [dbo].[Genres] ([Name])
VALUES
('Fiction'),
('Science Fiction'), 
('Romance'),
('Mystery'),
('Thriller'),
('Horror'),
('Adventure'),
('Coming-of-Age'),
('Biography'),
('Memoir'),
('Autobiography'),
('Poetry'),
('Drama'),
('Comedy'),
('Action'),
('Crime'),
('Classic Fiction'),
('Children''s'),
('Young Adult');


-- Addresses
INSERT INTO [dbo].[Addresses] ([City], [Street], [HouseNumber], [Country])
VALUES
('Paris', 'Champs-Élysées', '789', 'France'),
('Tokyo', 'Shibuya', '1011', 'Japan'),
('Sydney', 'George Street', '1213', 'Australia'),
('Berlin', 'Alexanderplatz', '1415', 'Germany'),
('Moscow', 'Red Square', '1617', 'Russia'),
('Rome', 'Via Condotti', '1819', 'Italy'),
('Beijing', 'Wangfujing', '2021', 'China'),
('Dubai', 'Sheikh Zayed Road', '2223', 'UAE'),
('Toronto', 'Yonge Street', '2425', 'Canada'),
('Mexico City', 'Paseo de la Reforma', '2627', 'Mexico'),
('Cairo', 'Tahrir Square', '2829', 'Egypt'),
('Rio de Janeiro', 'Copacabana', '3031', 'Brazil'),
('Bangkok', 'Sukhumvit Road', '3233', 'Thailand'),
('Mumbai', 'Marine Drive', '3435', 'India'),
('Cape Town', 'Long Street', '3637', 'South Africa'),
('Madrid', 'Gran Vía', '3839', 'Spain'),
('Seoul', 'Myeongdong', '4041', 'South Korea'),
('Oslo', 'Karl Johans gate', '4243', 'Norway');

-- Authors
INSERT INTO [dbo].[Authors] ([FirstName], [LastName], [BirthDate], [Country])
VALUES
('John', 'Smith', '1980-05-15', 'USA'),
('Emma', 'Johnson', '1975-08-20', 'UK'),
('Jean', 'Dupont', '1983-03-10', 'France'),
('Kenji', 'Tanaka', '1972-11-28', 'Japan'),
('Olivia', 'Brown', '1988-02-07', 'Australia'),
('Luis', 'Garcia', '1977-06-22', 'Spain'),
('Anna', 'Müller', '1985-09-12', 'Germany'),
('Ivan', 'Popov', '1979-04-18', 'Russia'),
('Marco', 'Rossi', '1981-12-30', 'Italy'),
('Mohammed', 'Ali', '1974-10-05', 'Egypt'),
('Sara', 'Kim', '1986-07-01', 'South Korea'),
('Andreas', 'Johansen', '1970-09-29', 'Norway'),
('Chen', 'Li', '1973-01-25', 'China'),
('Maria', 'Santos', '1984-03-19', 'Brazil'),
('Juan', 'Lopez', '1976-11-14', 'Mexico'),
('Raj', 'Patel', '1982-08-11', 'India'),
('Yuki', 'Tanaka', '1971-05-08', 'Japan'),
('Ahmed', 'Khalid', '1987-06-03', 'UAE'),
('Emily', 'White', '1978-12-17', 'Canada'),
('Thomas', 'Andersen', '1989-04-26', 'Denmark');

-- Books
INSERT INTO [dbo].[Books] ([Title], [Description], [PublicationDate], [ISBN], [AuthorId], [GenreId])
VALUES
('The Great Gatsby', 'A classic American novel', '1925-04-10', '9780743273565', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'John' AND [LastName] = 'Smith'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Fiction')),
('Pride and Prejudice', 'A romantic novel by Jane Austen', '1813-01-28', '9780141439518', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'Emma' AND [LastName] = 'Johnson'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Romance')),
('Les Misérables', 'Victor Hugo''s masterpiece', '1862-03-15', '9780140444308', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'Jean' AND [LastName] = 'Dupont'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Drama')),
('Norwegian Wood', 'A novel by Haruki Murakami', '1987-08-04', '9780099543793', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'Kenji' AND [LastName] = 'Tanaka'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Fiction')),
('1984', 'A dystopian novel by George Orwell', '1949-06-08', '9780451524935', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'George' AND [LastName] = 'Orwell'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Fiction')),
('To Kill a Mockingbird', 'A novel by Harper Lee', '1960-07-11', '9780061120084', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'Harper' AND [LastName] = 'Lee'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Fiction')),
('The Catcher in the Rye', 'A novel by J.D. Salinger', '1951-07-16', '9780316769488', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'J.D.' AND [LastName] = 'Salinger'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Coming-of-Age')),
('The Lord of the Rings', 'A high fantasy novel by J.R.R. Tolkien', '1954-07-29', '9780544003415', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'J.R.R.' AND [LastName] = 'Tolkien'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Drama')),
('The Hobbit', 'A fantasy novel by J.R.R. Tolkien', '1937-09-21', '9780261102217', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'J.R.R.' AND [LastName] = 'Tolkien'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Fantasy')),
('Moby-Dick', 'A novel by Herman Melville', '1851-10-18', '9781853260087', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'Herman' AND [LastName] = 'Melville'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Adventure')),
('The Great Expectations', 'A novel by Charles Dickens', '1861-08-01', '9780141439566', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'Charles' AND [LastName] = 'Dickens'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Classic Fiction')),
('The Chronicles of Narnia', 'A series of high fantasy novels by C.S. Lewis', '1950-10-16', '9780007323128', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'C.S.' AND [LastName] = 'Lewis'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Fantasy')),
('Gone with the Wind', 'A novel by Margaret Mitchell', '1936-06-30', '9781416548942', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'Margaret' AND [LastName] = 'Mitchell'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Fiction')),
('The Da Vinci Code', 'A mystery thriller novel by Dan Brown', '2003-03-18', '9780385504201', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'Dan' AND [LastName] = 'Brown'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Mystery')),
('The Alchemist', 'A novel by Paulo Coelho', '1988-01-01', '9780061122415', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'Paulo' AND [LastName] = 'Coelho'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Adventure')),
('The Hunger Games', 'A dystopian novel by Suzanne Collins', '2008-09-14', '9780439023481', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'Suzanne' AND [LastName] = 'Collins'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Science Fiction')),
('The Girl with the Dragon Tattoo', 'A psychological thriller novel by Stieg Larsson', '2005-08-01', '9780307269751', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'Stieg' AND [LastName] = 'Larsson'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Mystery')),
('The Road', 'A post-apocalyptic novel by Cormac McCarthy', '2006-09-26', '9780307387899', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'Cormac' AND [LastName] = 'McCarthy'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Drama')),
('The Fault in Our Stars', 'A romance novel by John Green', '2012-01-10', '9780525478812', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'John' AND [LastName] = 'Green'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Romance')),
('The Shining', 'A horror novel by Stephen King', '1977-01-28', '9780385121675', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'Stephen' AND [LastName] = 'King'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Horror')),
('The Secret Garden', 'A children''s novel by Frances Hodgson Burnett', '1911-10-01', '9780141321066', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'Frances' AND [LastName] = 'Burnett'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Children''s')),
('The Picture of Dorian Gray', 'A philosophical novel by Oscar Wilde', '1890-07-01', '9780141439573', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'Oscar' AND [LastName] = 'Wilde'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Classic Fiction')),
('Alice''s Adventures in Wonderland', 'A fantasy novel by Lewis Carroll', '1865-11-26', '9780141439764', (SELECT [AuthorId] FROM [dbo].[Authors] WHERE [FirstName] = 'Lewis' AND [LastName] = 'Carroll'), (SELECT [GenreId] FROM [dbo].[Genres] WHERE [Name] = 'Fantasy'));


-- Copies
INSERT INTO [dbo].[Copies] ([Condition], [BookId])
VALUES
('Good', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'Harry Potter and the Philosopher''s Stone')),
('Fair', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Hobbit')),
('Excellent', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Great Gatsby')),
('Good', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'Moby-Dick')),
('Fair', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = '1984')),
('Good', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'To Kill a Mockingbird')),
('Fair', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Catcher in the Rye')),
('Excellent', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Lord of the Rings')),
('Excellent', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'Pride and Prejudice')),
('Good', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'Les Misérables')),
('Fair', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'Norwegian Wood')),
('Good', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Great Gatsby')),
('Good', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'Harry Potter and the Philosopher''s Stone')),
('Fair', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'Harry Potter and the Philosopher''s Stone')),
('Excellent', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Hobbit')),
('Good', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Hobbit')),
('Fair', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Hobbit')),
('Excellent', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Great Gatsby')),
('Good', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'Moby-Dick')),
('Fair', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = '1984')),
('Good', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'To Kill a Mockingbird')),
('Fair', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'To Kill a Mockingbird')),
('Excellent', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Catcher in the Rye')),
('Excellent', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Lord of the Rings')),
('Excellent', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'Pride and Prejudice')),
('Good', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'Les Misérables')),
('Fair', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'Norwegian Wood')),
('Good', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Great Gatsby')),
('Fair', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Great Gatsby')),
('Good', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Secret Garden')),
('Good', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Picture of Dorian Gray')),
('Fair', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Picture of Dorian Gray')),
('Excellent', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Chronicles of Narnia')),
('Good', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'Gone with the Wind')),
('Fair', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'Gone with the Wind')),
('Good', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Da Vinci Code')),
('Good', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Alchemist')),
('Excellent', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Hunger Games')),
('Good', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Girl with the Dragon Tattoo')),
('Excellent', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Road')),
('Excellent', (SELECT [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Fault in Our Stars'));


-- Users
INSERT INTO [dbo].[Users] ([Name], [Surname], [Email], [PhoneNumber], [AddressId])
VALUES
('Alice', 'Johnson', 'alice@example.com', '123-456-7890', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'New York')),
('Bob', 'Smith', 'bob@example.com', '987-654-3210', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'London')),
('Charlie', 'Williams', 'charlie@example.com', '111-222-3333', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Paris')),
('David', 'Brown', 'david@example.com', '444-555-6666', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Tokyo')),
('Emma', 'Jones', 'emma@example.com', '777-888-9999', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Sydney')),
('Fiona', 'Taylor', 'fiona@example.com', '999-888-7777', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Berlin')),
('George', 'Anderson', 'george@example.com', '666-555-4444', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Moscow')),
('Hannah', 'Martinez', 'hannah@example.com', '333-222-1111', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Rome')),
('Isaac', 'Garcia', 'isaac@example.com', '000-999-8888', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Beijing')),
('Jack', 'Rodriguez', 'jack@example.com', '111-000-7777', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Dubai')),
('Karen', 'Hernandez', 'karen@example.com', '222-111-6666', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Toronto')),
('Liam', 'Lopez', 'liam@example.com', '333-444-5555', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Mexico City')),
('Mia', 'Gonzalez', 'mia@example.com', '666-777-8888', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Cairo')),
('Noah', 'Perez', 'noah@example.com', '999-888-7777', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Rio de Janeiro')),
('Olivia', 'Torres', 'olivia@example.com', '000-111-2222', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Bangkok')),
('Peter', 'Sanchez', 'peter@example.com', '444-555-6666', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Mumbai')),
('Quinn', 'Ramirez', 'quinn@example.com', '777-888-9999', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Cape Town')),
('Rachel', 'Rivera', 'rachel@example.com', '123-456-7890', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Madrid')),
('Samuel', 'Smith', 'samuel@example.com', '987-654-3210', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Seoul')),
('Taylor', 'Baker', 'taylor@example.com', '111-222-3333', (SELECT [AddressId] FROM [dbo].[Addresses] WHERE [City] = 'Oslo'));


-- Loans
INSERT INTO [dbo].[Loans] ([UserId], [CopyId], [LoanDate], [ReturnDate])
VALUES
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] WHERE [BookId] = (SELECT TOP 1 [BookId] FROM [dbo].[Books] WHERE [Title] = 'Harry Potter and the Philosopher''s Stone') ORDER BY NEWID()), '2000-04-01 10:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] WHERE [BookId] = (SELECT TOP 1 [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Hobbit') ORDER BY NEWID()), '2020-04-02 11:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] WHERE [BookId] = (SELECT TOP 1 [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Great Gatsby') ORDER BY NEWID()), '2004-04-03 12:00:00', '2024-04-21 12:00:00'), 
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] WHERE [BookId] = (SELECT TOP 1 [BookId] FROM [dbo].[Books] WHERE [Title] = 'Moby-Dick') ORDER BY NEWID()), '2003-04-04 13:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] WHERE [BookId] = (SELECT TOP 1 [BookId] FROM [dbo].[Books] WHERE [Title] = '1984') ORDER BY NEWID()), '2024-04-05 14:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] WHERE [BookId] = (SELECT TOP 1 [BookId] FROM [dbo].[Books] WHERE [Title] = 'To Kill a Mockingbird') ORDER BY NEWID()), '2024-04-06 15:00:00', '2024-04-22 10:00:00'), 
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] WHERE [BookId] = (SELECT TOP 1 [BookId] FROM [dbo].[Books] WHERE [Title] = 'Les Misérables') ORDER BY NEWID()), '2024-04-07 16:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] WHERE [BookId] = (SELECT TOP 1 [BookId] FROM [dbo].[Books] WHERE [Title] = 'Norwegian Wood') ORDER BY NEWID()), '2024-04-08 17:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] WHERE [BookId] = (SELECT TOP 1 [BookId] FROM [dbo].[Books] WHERE [Title] = '1984') ORDER BY NEWID()), '2024-04-09 18:00:00', '2024-04-23 11:00:00'), 
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] WHERE [BookId] = (SELECT TOP 1 [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Catcher in the Rye') ORDER BY NEWID()), '2024-04-10 19:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] WHERE [BookId] = (SELECT TOP 1 [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Lord of the Rings') ORDER BY NEWID()), '2024-04-11 20:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] WHERE [BookId] = (SELECT TOP 1 [BookId] FROM [dbo].[Books] WHERE [Title] = 'Pride and Prejudice') ORDER BY NEWID()), '2024-04-12 21:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] WHERE [BookId] = (SELECT TOP 1 [BookId] FROM [dbo].[Books] WHERE [Title] = '1984') ORDER BY NEWID()), '2024-04-13 22:00:00', '2024-04-24 12:00:00'), 
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] WHERE [BookId] = (SELECT TOP 1 [BookId] FROM [dbo].[Books] WHERE [Title] = 'Les Misérables') ORDER BY NEWID()), '2024-04-14 23:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] WHERE [BookId] = (SELECT TOP 1 [BookId] FROM [dbo].[Books] WHERE [Title] = 'To Kill a Mockingbird') ORDER BY NEWID()), '2024-04-15 10:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] WHERE [BookId] = (SELECT TOP 1 [BookId] FROM [dbo].[Books] WHERE [Title] = 'The Great Gatsby') ORDER BY NEWID()), '2024-04-16 11:00:00', '2024-04-25 13:00:00'),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-04-17 12:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-04-18 13:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-04-19 14:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-04-20 15:00:00', '2024-05-05 10:00:00'), 
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-04-21 16:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-04-22 17:00:00', '2024-05-06 11:00:00'), 
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-04-23 18:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-04-24 19:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-04-25 20:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-04-26 21:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-04-27 22:00:00', '2024-05-07 12:00:00'), 
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-04-28 23:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-04-29 10:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-04-30 11:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-05-01 12:00:00', '2024-05-08 13:00:00'), 
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-05-02 13:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-05-03 14:00:00', '2024-05-09 14:00:00'), 
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-05-04 15:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-05-05 16:00:00', NULL),
((SELECT TOP 1 [UserId] FROM [dbo].[Users] ORDER BY NEWID()), (SELECT TOP 1 [CopyId] FROM [dbo].[Copies] ORDER BY NEWID()), '2024-05-06 17:00:00', '2024-05-10 15:00:00'); 

COMMIT TRAN
```

## Zadanie - `UPDATE`

1. Zmień stan wszystkich kopii książek, wydanych przed 1990 rokiem, na `Bad`


```sql
SELECT CopyId, Condition
FROM Copies c
JOIN Books b on b.BookId = c.BookId
WHERE b.PublicationDate < '1990-01-01'

UPDATE Copies
SET Condition = 'Bad'
WHERE BookId IN (SELECT BookId
                FROM Books b
                WHERE b.PublicationDate < '1990-01-01')

SELECT CopyId, Condition
FROM Copies c
JOIN Books b on b.BookId = c.BookId
WHERE b.PublicationDate < '1990-01-01'
```

2. Zmień gatunek książki 'The Hobbit' na 'Drama'


```sql
SELECT *
FROM Books
WHERE Title = 'The Hobbit'

UPDATE Books
SET GenreId = (SELECT GenreId FROM Genres WHERE Name = 'Drama')
WHERE Title = 'The Hobbit'

SELECT *
FROM Books
WHERE Title = 'The Hobbit'
```


(1 row affected)



(1 row affected)



(1 row affected)



Total execution time: 00:00:00.010





<table><tr><th>BookId</th><th>Title</th><th>Description</th><th>PublicationDate</th><th>ISBN</th><th>AuthorId</th><th>GenreId</th></tr><tr><td>465</td><td>The Hobbit</td><td>A fantasy novel by J.R.R. Tolkien</td><td>1937-09-21</td><td>9780261102217</td><td>NULL</td><td>1</td></tr></table>






<table><tr><th>BookId</th><th>Title</th><th>Description</th><th>PublicationDate</th><th>ISBN</th><th>AuthorId</th><th>GenreId</th></tr><tr><td>465</td><td>The Hobbit</td><td>A fantasy novel by J.R.R. Tolkien</td><td>1937-09-21</td><td>9780261102217</td><td>NULL</td><td>455</td></tr></table>



3. Zmień wartość `HouseNumber` na `99`, dla adresu użytkownika, który wypożyczył najwięcej książek.




```sql
-- ROZWIĄZANIE

UPDATE Addresses
SET HouseNumber = '99'
WHERE AddressId = (
    SELECT AddressId
    FROM Users
    WHERE UserId = (
            SELECT TOP 1 UserId
            FROM Loans
            GROUP BY UserId
            ORDER BY COUNT(*) DESC))


```


(1 row affected)



Total execution time: 00:00:00.003


## Zadanie - `DELETE`

1. Usuń kopie książek, których stan jest '`Fair`'



```sql
-- ROZWIĄZANIE

DELETE FROM Loans
WHERE CopyId IN (SELECT CopyId
                FROM Copies
                WHERE Condition = 'Fair')

DELETE FROM Copies
WHERE Condition = 'Fair'
```


(1 row affected)



(1 row affected)



Total execution time: 00:00:00.005


2. Usuń informacje o wypożyczeniach książek, które były wypożyczone przed '`2005`' rokiem i do tej pory nie zostały zwrócone


```sql
-- ROZWIĄZANIE

SELECT *
FROM Loans
WHERE LoanDate < '2005-01-01' AND ReturnDate IS NULL

DELETE FROM Loans
WHERE LoanDate < '2005-01-01' AND ReturnDate IS NULL

SELECT *
FROM Loans
WHERE LoanDate < '2005-01-01' AND ReturnDate IS NULL
```


(2 rows affected)



(2 rows affected)



(0 rows affected)



Total execution time: 00:00:00.004





<table><tr><th>LoanId</th><th>UserId</th><th>CopyId</th><th>LoanDate</th><th>ReturnDate</th></tr><tr><td>104</td><td>240</td><td>1</td><td>2000-04-01 10:00:00.0000000</td><td>NULL</td></tr><tr><td>107</td><td>231</td><td>596</td><td>2003-04-04 13:00:00.0000000</td><td>NULL</td></tr></table>






<table><tr><th>LoanId</th><th>UserId</th><th>CopyId</th><th>LoanDate</th><th>ReturnDate</th></tr></table>



3. Usuń gatunek `Mystery` i powiązane z nim książki


```sql
-- ROZWIĄZANIE

SELECT GenreId -- 446
FROM Genres
WHERE Name = 'Mystery'

DELETE FROM Loans
WHERE CopyId IN (
    SELECT CopyId
    FROM Copies
    WHERE BookId IN (
        SELECT BookId
        FROM Books
        WHERE GenreId = 446
    )

)

DELETE FROM Copies
WHERE BookId IN (
    SELECT BookId
    FROM Books
    WHERE GenreId = 446
)

DELETE FROM Books
WHERE GenreId = 446

DELETE FROM Genres
WHERE GenreId = 446
```


(1 row affected)



(2 rows affected)



(2 rows affected)



(2 rows affected)



(1 row affected)



Total execution time: 00:00:00.011





<table><tr><th>GenreId</th></tr><tr><td>446</td></tr></table>



4. Usuń z bazy użytkownika `Bob Smith` i powiązane z nim informacje


```sql
-- ROZWIĄZANIE

SELECT *
FROM Users
WHERE Name = 'Bob' AND Surname = 'Smith'

-- 225

DELETE FROM Addresses
WHERE AddressId = (SELECT AddressId FROM Users WHERE UserId = 225)

DELETE FROM Loans
WHERE UserId = 225

DELETE FROM Users
WHERE UserId = 225
```


(1 row affected)



The statement has been terminated.



(2 rows affected)



(1 row affected)



Total execution time: 00:00:00.007





<table><tr><th>UserId</th><th>Name</th><th>Surname</th><th>Email</th><th>PhoneNumber</th><th>AddressId</th></tr><tr><td>225</td><td>Bob</td><td>Smith</td><td>bob@example.com</td><td>987-654-3210</td><td>2</td></tr></table>




