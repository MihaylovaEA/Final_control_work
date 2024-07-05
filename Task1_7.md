Михайлова Е.А.
19.04.2024
5275(или 5276)

1. Использование команды cat в Linux
   - Создать два текстовых файла: "Pets"(Домашние животные) и "Pack animals"(вьючные животные), используя команду `cat` в терминале Linux. В первом файле перечислить собак, кошек и хомяков. Во втором — лошадей, верблюдов и ослов.
   - Объединить содержимое этих двух файлов в один и просмотреть его содержимое.
   - Переименовать получившийся файл в "Human Friends"

_*Пример конечного вывода после команды “ls” :*_

_Desktop Documents Downloads  HumanFriends.txt  Music  PackAnimals.txt  Pets.txt  Pictures  Videos_

2. Работа с директориями в Linux
   - Создать новую директорию и переместить туда файл "Human Friends".

   ![alt text](image1_2.png)

3. Работа с MySQL в Linux. “Установить MySQL на вашу вычислительную машину ”
   - Подключить дополнительный репозиторий MySQL и установить один из пакетов из этого репозитория.

sudo wget https://dev.mysql.com/get/mysql-apt-config_0.8.23-1_all.deb

sudo dpkg -i mysql-apt-config_0.8.23-1_all.deb

sudo apt-get update

sudo apt-get install mysql-server




4. Управление deb-пакетами
   - Установить и затем удалить deb-пакет, используя команду `dpkg`.

sudo wget https://download.docker.com/linux/ubuntu/dists/jammy/pool/stable/amd64/docker-ce-cli_20.10.13~3-0~ubuntu-jammy_amd64.deb

sudo dpkg -i docker-ce-cli_20.10.133-0ubuntu-jammy_amd64.deb

sudo dpkg -r docker-ce-cli


5. История команд в терминале Ubuntu
   - Сохранить и выложить историю ваших терминальных команд в Ubuntu.
В формате: Файла с ФИО, датой сдачи, номером группы(или потока)

6. Диаграмма классов
   - Создать диаграмму классов с родительским классом "Животные", и двумя подклассами: "Pets" и "Pack animals".

    В составы классов, которых в случае Pets войдут классы: собаки, кошки, хомяки, а в класс Pack animals войдут: Лошади, верблюды и ослы).
Каждый тип животных будет характеризоваться (например, имена, даты рождения, выполняемые команды и т.д)
Диаграмму можно нарисовать в любом редакторе, такими как Lucidchart, Draw.io, Microsoft Visio и других.

Task1_6_Diagram.png

![alt text](<Uml Diagram.png>)

7. Работа с MySQL (Задача выполняется в случае успешного выполнения задачи “Работа с MySQL в Linux. “Установить MySQL на вашу машину”

    7.1. После создания диаграммы классов в 6 пункте, в 7 пункте база данных "Human Friends" должна быть структурирована в соответствии с этой диаграммой. Например, можно создать таблицы, которые будут соответствовать классам "Pets" и "Pack animals", и в этих таблицах будут поля, которые характеризуют каждый тип животных (например, имена, даты рождения, выполняемые команды и т.д.). 

    7.2.   - В ранее подключенном MySQL создать базу данных с названием "Human Friends".

    DROP DATABASE IF EXISTS Human_friends;
    CREATE DATABASE Human_friends;

    - Создать таблицы, соответствующие иерархии из вашей диаграммы классов.

   DROP TABLE IF EXISTS commands;
   CREATE TABLE commands
   (
       id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
       name varchar(30),
       description varchar(255)
   );

   DROP TABLE IF EXISTS animals_group;
   CREATE TABLE animals_group
   (
       id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
       name varchar(30)
   );

   DROP TABLE IF EXISTS animal_genius;
   CREATE TABLE animal_genius
   (
       id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
       name varchar(30),
       group_id INT,
       FOREIGN KEY (group_id) REFERENCES animals_group (id)
       ON DELETE CASCADE ON UPDATE CASCADE
   );

   DROP TABLE IF EXISTS nursery_animal;
   CREATE TABLE nursery_animal
   (
       id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
       name varchar(30),
       birth_date DATE,
       genius_id INT,
       FOREIGN KEY (genius_id) REFERENCES animal_genius  (id)
       ON DELETE CASCADE ON UPDATE CASCADE
   );

   DROP TABLE IF EXISTS animal_commands;
   CREATE TABLE animal_commands
   (
       animal_id INT NOT NULL,
       command_id INT NOT NULL,

       PRIMARY KEY (animal_id, command_id),
       FOREIGN KEY (animal_id) REFERENCES nursery_animal (id)
        ON DELETE CASCADE ON UPDATE CASCADE,
         FOREIGN KEY (command_id) REFERENCES commands (id)
         ON DELETE CASCADE  ON UPDATE CASCADE
   );

   - Заполнить таблицы данными о животных, их командах и датами рождения.

   INSERT INTO commands(name)
   VALUES
	 ('Sit'),
	 ('Stay'),
	 ('Fetch'),
	 ('Pounce'),
	 ('Hide'),
	 ('Roll'),
	 ('Paw'),
	 ('Bark'),
	 ('Scratch'),
	 ('Spin'),
	 ('Meow'),
	 ('Jump'),
	 ('Trot'),
	 ('Canter'),
	 ('Gallop'),
	 ('Walk'),
	 ('Carry Load'),
	 ('Bray'),
	 ('Kick'),
	 ('Run');

   INSERT INTO animals_group (name)
   VALUES
	 ('Pets'),
	 ('PackAnimals');

   INSERT INTO animal_genius (name, group_id)
   VALUES
	 ('Cat', 2),
	 ('Dog', 2),
	 ('Hamster', 2),
	 ('Horse', 1),
	 ('Camel', 1),
	 ('Donkey', 1);

   INSERT INTO nursery_animal (name, birth_date, genius_id)
   VALUES
	 ('Fido', '2020-01-01', 2),
	 ('Whiskers', '2019-05-15', 1),
	 ('Hammy', '2021-03-10', 3),
	 ('Buddy', '2018-12-10', 2),
	 ('Smudge', '2020-02-20', 1),
	 ('Peanut', '2021-08-01', 3),
	 ('Bella', '2019-11-11', 2),
	 ('Oliver', '2020-06-30', 1),
	 ('Thunder', '2015-07-21', 4),
	 ('Sandy', '2016-11-03', 5),
	 ('Eeyore', '2017-09-18', 6),
	 ('Storm', '2014-05-05', 4),
	 ('Dune', '2018-12-12', 5),
	 ('Burro', '2019-01-23', 6),
	 ('Blaze', '2016-02-29', 4),
	 ('Sahara', '2015-08-14', 5);

   INSERT INTO animal_commands (animal_id, command_id)
   VALUES
	 (1, 1), (1, 2), (1, 3), 
	 (2, 1), (2, 4),
	 (3, 6), (3, 5), 
	 (4, 1), (4, 7), (4, 8), 
	 (5, 1), (5, 4), (5, 9), 
	 (6, 6), (6, 10),  
	 (7, 1), (7, 2), (7, 6), 
	 (8, 11), (8, 9), (8, 12), 
	 (9, 13), (9, 14), (9, 15), 
	 (10, 16), (10, 17), 181), 
	 (12, 13), (12, 14), 
	 (13, 16), (13, 1), 
	 (14, 16), (14, 18), (14, 19), 
	 (15, 13), (15, 12), (15, 15), 
	 (16, 16), (16, 20);

- Удалить записи о верблюдах и объединить таблицы лошадей и ослов.

   DELETE FROM nursery_animal WHERE genius_id = 5;

   CREATE TABLE horse_donkey AS
   SELECT * from nursery_animal WHERE genius_id = 4
   UNION
   SELECT * from nursery_animal WHERE genius_id = 5;

- Создать новую таблицу для животных в возрасте от 1 до 3 лет и вычислить их возраст с точностью до месяца.

   CREATE TABLE young_animals  
   SELECT id, name, birth_date, 
   datediff(curdate(),birth_date)  DIV 31as age, genius_id from nursery_animal 
   WHERE date_add(birth_date, INTERVAL 1 YEAR) < curdate() 
   AND date_add(birth_date, INTERVAL 3 YEAR) > curdate();

- Объединить все созданные таблицы в одну, сохраняя информацию о принадлежности к исходным таблицам.

   SELECT id, name, birth_date, genius_id FROM horse_donkey
   UNION
   SELECT id, name, birth_date, genius_id FROM young_animals;

[Задания 8-10] (https://github.com/MihaylovaEA/Final_control_work/tree/main/src)
