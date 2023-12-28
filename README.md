# Practice_Linq
## ПОСТАНОВКА ЗАВДАННЯ
1.	Клонуватирепозиторій:https://github.com/IlonaShevchenko/Practice_Linq.git
- У проєкті є частковий код:
-	опис класу FootballGame, який описує футбольний матч (FootballGame.сs);
-	у файлі Program.cs вже реалізований метод ReadFromFileJson(), який десеріалізаціє json-файл (data/results_2010.json) у колекцію List;
-	також у файлі Program.cs повністю реалізований метод Main().

Склонований проєкт має запускатися і виводити на екран тестове значення 13049 (це кількість всіх матчів збірних, які були проведені з 2010 року включно).

2.	Необхідно реалізувати методи Query1(), Query2(), …, Query10(), шаблони цих методів наявні в проєкті. Завдання (запити для реалізації) див. у вигляді коментарів до кожного методу.

3.	Крім запиту у кожному методі має бути реалізований вивід на екран результатів запиту (приклад оформлення виводу див. файл output.txt).

4.	Для проєкту має бути створений власний локальний і віддалений репозиторії. Після реалізації кожного методу QueryN() необхідно робити коміт, вказуючи номер N реалізованого запиту.

5.	Оформити Readme.md файл.

## РЕЗУЛЬТАТ ВИКОНАННЯ РОБОТИ

***Запит 1:*** Вивести всі матчі, які відбулися в Україні у 2012 році.
        
        static void Query1(List<FootballGame> games)
        {
            //Query 1: Вивести всі матчі, які відбулися в Україні у 2012 році.

            var selectedGames = games.Where(game => game.Country == "Ukraine" && game.Date.Year == 2012); // Корегуємо запит !!!


            // Перевірка
            Console.WriteLine("\n======================== QUERY 1 ========================");

            foreach (var game in selectedGames)
            {
                Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
            }
            // див. приклад як має бути виведено:


        }

 ![image](https://github.com/JuliaSylenok/Practice_2_Sylenok/assets/149322465/24015c90-0793-49af-92b5-7afbb8271b57)

Рисунок 1 – Результат виконання запиту 1 та його порівняння з даними в файлі output.txt

***Запит 2:*** Вивести Friendly матчі збірної Італії, які вона провела з 2020 року.



        static void Query2(List<FootballGame> games)
        {
            //Query 2: Вивести Friendly матчі збірної Італії, які вона провела з 2020 року.  

            var selectedGames = games.Where(game =>
                game.Tournament == "Friendly" &&
                game.Home_team == "Italy" &&
                game.Date.Year >= 2020 ||
                game.Tournament == "Friendly" &&
                game.Away_team == "Italy" &&
                game.Date.Year >= 2020);

            // Перевірка
            Console.WriteLine("\n======================== QUERY 2 ========================");
            foreach (var game in selectedGames)
            {
                Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
            }
            // див. приклад як має бути виведено:


        }
        
![image](https://github.com/JuliaSylenok/Practice_2_Sylenok/assets/149322465/79b64336-a242-41b1-8535-cc82f49e3adc)
Рисунок 2 – Результат виконання запиту 2 та його порівняння з даними в файлі output.txt

***Запит 3:*** Вивести всі домашні матчі збірної Франції за 2021 рік, де вона зіграла у нічию.

Якщо вважати за нічию рівну кількість очок у обох командах то запит формується так: 

        static void Query3(List<FootballGame> games)
        {
            //Query 3: Вивести всі домашні матчі збірної Франції за 2021 рік, де вона зіграла у нічию.

            var selectedGames = games.Where(game => game.Home_team == "France" && game.Date.Year == 2021 && game.Home_score == game.Away_score);

            // Перевірка
            Console.WriteLine("\n======================== QUERY 3 ========================");
            foreach (var game in selectedGames)
            {
                Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
            }
            // див. приклад як має бути виведено:
        }

Результат такого запиту показано на рисунку 3.

 ![image](https://github.com/JuliaSylenok/Practice_2_Sylenok/assets/149322465/0bc417f8-03ea-42e3-95bd-d6c7c30b5560)

Рисунок 3 – Результат запиту


Якщо вважати за нічию тільки значення очок 1 – 1, то запит формується наступним чином:

        static void Query3(List<FootballGame> games)
        {
            // Query 3: Вивести всі домашні матчі збірної Франції за 2021 рік, де вона зіграла у нічию.

            var selectedGames = games
                .Where(game => game.Home_team == "France" &&
                               game.Date.Year == 2021 &&
                               game.Home_score == 1 &&
                               game.Away_score == 1);

            // Перевірка
            Console.WriteLine("\n======================== QUERY 3 ========================");
            foreach (var game in selectedGames)
            {
                Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
            }
            // див. приклад як має бути виведено:
        }

 ![image](https://github.com/JuliaSylenok/Practice_2_Sylenok/assets/149322465/4185548f-7735-42b8-b476-155d08cc3e58)

Рисунок 4 – Результат виконання запиту 3 якщо нічия лише 1-1 

***Запит 4:*** Вивести всі матчі збірної Германії з 2018 року по 2020 рік (включно), в яких вона на виїзді програла.

        static void Query4(List<FootballGame> games)
        {
            //Query 4: Вивести всі матчі збірної Германії з 2018 року по 2020 рік (включно), в яких вона на виїзді програла.

            var selectedGames = games.Where(game => game.Date.Year >= 2018 && game.Date.Year <= 2020 && game.Away_team == "Germany" && game.Away_score < game.Home_score);

            // Перевірка
            Console.WriteLine("\n======================== QUERY 4 ========================");
            foreach (var game in selectedGames)
            {
                Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
            }
            // див. приклад як має бути виведено:
        }

 ![image](https://github.com/JuliaSylenok/Practice_2_Sylenok/assets/149322465/3220f79d-9d3b-4017-9256-a298e8440465)

Рисунок 5 – Результат виконання запиту 4 та його порівняння з даними в файлі output.txt

***Запит 5:*** Вивести всі кваліфікаційні матчі (UEFA Euro qualification), які відбулися у Києві чи у Харкові, а також за умови перемоги української збірної.

        static void Query5(List<FootballGame> games)
        {
            //Query 5: Вивести всі кваліфікаційні матчі (UEFA Euro qualification), які відбулися у Києві чи у Харкові, а також за умови перемоги української збірної.


            var selectedGames = games
                            .Where(game => (game.Tournament == "UEFA Euro qualification") &&
                                           (game.City == "Kyiv" || game.City == "Kharkiv") &&
                                           (game.Home_team == "Ukraine" && game.Home_score > game.Away_score))
                            .Select(game => $"{game.Date:dd.MM.yyyy} Ukraine - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
            // Перевірка
            Console.WriteLine("\n======================== QUERY 5 ========================");
            foreach (var game in selectedGames)
            {
                Console.WriteLine(game);
            }
            // див. приклад як має бути виведено:
        }

 ![image](https://github.com/JuliaSylenok/Practice_2_Sylenok/assets/149322465/ce09f1a4-c965-4d8a-926a-9d966c62b47a)

Рисунок 6 – Результат виконання запиту 5 та його порівняння з даними в файлі output.txt

***Запит 6:*** Вивести всі матчі останнього чемпіоната світу з футболу (FIFA World Cup), починаючи з чвертьфіналів (тобто останні 8 матчів).
Матчі мають відображатися від фіналу до чвертьфіналів (тобто у зворотній послідовності).

        static void Query6(List<FootballGame> games)
        {
            //Query 6: Вивести всі матчі останнього чемпіоната світу з футболу (FIFA World Cup), починаючи з чвертьфіналів (тобто останні 8 матчів).
            //Матчі мають відображатися від фіналу до чвертьфіналів (тобто у зворотній послідовності).

            var selectedGames = games.Where(game => game.Tournament == "FIFA World Cup").OrderByDescending(game => game.Date).Take(8);

            // Перевірка
            Console.WriteLine("\n======================== QUERY 6 ========================");
            foreach (var game in selectedGames)
            {
                Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
            }            // див. приклад як має бути виведено:
        }

 ![image](https://github.com/JuliaSylenok/Practice_2_Sylenok/assets/149322465/1152fb68-885d-4b94-925b-2750a06dce82)

Рисунок 7 – Результат виконання запиту 6 та його порівняння з даними в файлі output.txt

***Запит 7:*** Вивести перший матч у 2023 році, в якому збірна України виграла.

        static void Query7(List<FootballGame> games)
        {
            //Query 7: Вивести перший матч у 2023 році, в якому збірна України виграла.
             var selectedGame = games.Where(game => game.Date.Year == 2023 &&(game.Home_team == "Ukraine" || game.Away_team == "Ukraine") &&(game.Home_team == "Ukraine" && game.Home_score > game.Away_score ||game.Away_team == "Ukraine" && game.Away_score > game.Home_score)).FirstOrDefault();

            // Перевірка
            Console.WriteLine("\n======================== QUERY 7 ========================");
            if (selectedGame != null)
            {
                Console.WriteLine($"{selectedGame.Date:dd.MM.yyyy} {selectedGame.Home_team} - {selectedGame.Away_team}, Score: {selectedGame.Home_score} - {selectedGame.Away_score}, Country: {selectedGame.Country}");
            }
            // див. приклад як має бути виведено:
        }


 ![image](https://github.com/JuliaSylenok/Practice_2_Sylenok/assets/149322465/11559303-fcbd-4182-93bd-e034becbdd98)

Рисунок 8 – Результат виконання запиту 7 та його порівняння з даними в файлі output.txt

***Запит 8:*** Перетворити всі матчі Євро-2012 (UEFA Euro), які відбулися в Україні, на матчі з наступними властивостями:
MatchYear - рік матчу, Team1 - назва приймаючої команди, Team2 - назва гостьової команди, Goals - сума всіх голів за матч

        static void Query8(List<FootballGame> games)
        {
            //Query 8: Перетворити всі матчі Євро-2012 (UEFA Euro), які відбулися в Україні, на матчі з наступними властивостями:
            // MatchYear - рік матчу, Team1 - назва приймаючої команди, Team2 - назва гостьової команди, Goals - сума всіх голів за матч

            var selectedGames = games.Where(game => game.Tournament == "UEFA Euro" && game.Country == "Ukraine").Select(game => new
            {
                 MatchYear = game.Date.Year,
                 Team1 = game.Home_team,
                 Team2 = game.Away_team,
                 Goals = game.Home_score + game.Away_score
            });

            // Перевірка
            Console.WriteLine("\n======================== QUERY 8 ========================");
            foreach (var game in selectedGames)
            {
                Console.WriteLine($"{game.MatchYear} {game.Team1} - {game.Team2}, Goals: {game.Goals}");
            }
            // див. приклад як має бути виведено:
        }

 ![image](https://github.com/JuliaSylenok/Practice_2_Sylenok/assets/149322465/8fbe525f-c101-4d82-8a21-fbd1082d09eb)

Рисунок 9 – Результат виконання запиту 8 та його порівняння з даними в файлі output.txt

***Запит 9:*** Перетворити всі матчі UEFA Nations League у 2023 році на матчі з наступними властивостями:
MatchYear - рік матчу, Game - назви обох команд через дефіс (першою - Home_team), Result - результат для першої команди (Win, Loss, Draw)

        static void Query9(List<FootballGame> games)
        {
            //Query 9: Перетворити всі матчі UEFA Nations League у 2023 році на матчі з наступними властивостями:
            // MatchYear - рік матчу, Game - назви обох команд через дефіс (першою - Home_team), Result - результат для першої команди (Win, Loss, Draw)

            var selectedGames = games.Where(game => game.Tournament == "UEFA Nations League" && game.Date.Year == 2023).Select(game => new
            {
                MatchYear = game.Date.Year,
                Game = $"{game.Home_team}-{game.Away_team}",
                Result = game.Home_score > game.Away_score ? "Win" : (game.Home_score < game.Away_score ? "Loss" : "Draw")
            });

            // Перевірка
            Console.WriteLine("\n======================== QUERY 9 ========================");
            foreach (var game in selectedGames)
            {
                Console.WriteLine($"{game.MatchYear} {game.Game}, Result for team1: {game.Result}");
            }
            // див. приклад як має бути виведено:
        }

 ![image](https://github.com/JuliaSylenok/Practice_2_Sylenok/assets/149322465/b21d7e76-ab40-4b9e-b0aa-84d429040a54)

Рисунок 10 – Результат виконання запиту 9 та його порівняння з даними в файлі output.txt

***Запит 10:*** Вивести з 5-го по 10-тий (включно) матчі Gold Cup, які відбулися у липні 2023 р.

        static void Query10(List<FootballGame> games)
        {
            //Query 10: Вивести з 5-го по 10-тий (включно) матчі Gold Cup, які відбулися у липні 2023 р.

            var selectedGames = games.Where(game => game.Tournament == "Gold Cup" && game.Date.Year == 2023 && game.Date.Month == 7).Skip(4) .Take(6);

            // Перевірка
            Console.WriteLine("\n======================== QUERY 10 ========================");
            foreach (var game in selectedGames)
            {
                Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
            }
            // див. приклад як має бути виведено:
        }

 ![image](https://github.com/JuliaSylenok/Practice_2_Sylenok/assets/149322465/fea7a524-1baf-4e84-ad34-f232b98b7329)

Рисунок 11 – Результат виконання запиту 10 та його порівняння з даними в файлі output.txt

