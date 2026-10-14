# Can video game data reveal patterns associated with higher commercial sales?

## Project Overview
The project is focused on creating and analysing a dataset of games which was published from August 2025 - August 2026; Specifically on what factors patterns drove higher commercial sales, I will compare and evaluate and finally conclude what drives success due to the findings I have encountered within the past year.

### The workflow will be the following:

RAWG API
     → 
🐍 Python
     → 
CSV
     → 
📊 Excel
     → 
🗄️ SQL
     → 
🐍 Python analysis
     → 
📈 Tableau


## 01 - How the Data was Gathered
The aim is to gather as much data as I can in terms of games as it would be more time consuming if I handpicked each 90+ games 

<img width="470" height="414" alt="image" src="https://github.com/user-attachments/assets/cf69b9f3-845a-4249-b190-10d5f927293d" />

I started first by scraping information from RAWG which I then (in python) dug through the ‘results’ which showcased  the playtime, name, rating, id, owned, beaten and more but the main aim is to grasp information I can compare which in the end I found was the rating, platform and genre.



→ View full Python notebook



I wanted the information I found to be transferred into excel so I can add more data efficiently so I I used my for loop, printing the following games as a list so I can separate it as commas in excel

<img width="429" height="291.5" alt="Screenshot 2026-09-09 131837" src="https://github.com/user-attachments/assets/f2424e2d-f595-4c4d-848b-51a38d813208" />

as it only extracted 41 games I had to manually research for the rest of the games. 
The sources I looked for games will be at the bottom of this page


## 02 - Cleaning the Data
### Old Data
<img width="554" height="517" alt="image" src="https://github.com/user-attachments/assets/b7be138f-e807-4ed3-a62c-fa7f6e5f2df8" /> 
‎

‎ 

### New Data
<img width="962" height="442" alt="image" src="https://github.com/user-attachments/assets/ba7c082a-bfee-4e9d-8d68-eb6044a9de1d" />

I added Copies sold, Revenue and release date in the new data for more comparinsons and insights within my table. What I noticed was that within Column 3/ Genres, they were way to broad so I would normally go into either [steam](https://store.steampowered.com/) to look at the genres and [Metacritic](https://www.metacritic.com/) for the ratings and Platforms for the other remaining games which I manually inputted. the games platforms in the old data was very stiff and broad such as indie when the game genre was more of a Rhythm game such as  Rhythm Doctor 

→ View cleaned dataset


## 03 - SQL Analysis
The Goal here is to Answer the question in form of SQL, underneath is the following which helped me calculate  how I figured out the question (bru idk)



Before hand I noticed there were alot of anomalies when checking 
```sql
SELECT Distinct "Genre" from "AllGames"
```
I had to clean and replace typos before engaging within my queries

## Q1: How does commercial performance differ between Indie, AA and AAA games? 

 
My hope is to 
Compare Indie, AA and AA by its copies sold, revenue and rating and see what drove
```sql
--MEDIAN OF COPIES SOLD AAA

With "AllGames" AS (SELECT *
, Row_number() OVER(Order by "Copies Sold" ASC) as "CopiesASC"
, Row_number() OVER(Order by "Copies Sold" DESC) as "CopiesDESC"
FROM "AllGames"

 Where "Game Type" = 'AAA'
 
)
SELECT * FROM "AllGames"
WHERE abs("CopiesASC" - "CopiesDESC") <= 1
ORDER BY "Copies Sold"




--MEDIAN OF REVENUE  AAA

With "AllGames" AS (SELECT *
, Row_number() OVER(Order by "Revenue" ASC) as "RevenueASC"
, Row_number() OVER(Order by "Revenue" DESC) as "RevenueDESC"
FROM "AllGames"

 Where "Game Type" = 'AAA'
 
)
SELECT * FROM "AllGames"
WHERE abs("RevenueASC" - "RevenueDESC") <= 1
ORDER BY "Revenue"

```


| Game | Rating | Genre | Copies Sold | Revenue | The Cost | Game Type | Release Date | Platform | 
|---|---|---|---|---|---|---|---|---|
| Sonic Crossworlds | 4.65 | Racing | 1200000 | 32444500 |  64.99  |  AAA  | 2025-09-25 | PS4, PS5, Xbox, Switch 1, Switch 2, PC |




### Q2: Which genres sell the most copies?  
The aim was to compare the total sales or average/median sales for each genre. 


```sql

SELECT 
MAX ("Genre") as "Genre",
COUNT("Genre") as "TotalGameGenre",
SUM("Revenue") as "Total_Revenue",
Avg("Revenue") as "Average"
from "AllGames"
Group by "Genre"

```
<details>
<summary>View All Genres</summary>
     
| Genre | TopGameGenre | Total_Revenue | Average |
|---|---:|---:|---:|
| Sports | 3 | 13,710,780 | 4,570,260.00 |
| Party | 1 | 4,999,000 | 4,999,000.00 |
| Rhythm | 3 | 19,493,142 | 6,497,714.00 |
| Survival | 3 | 53,121,782 | 17,707,260.67 |
| Hack and Slash | 2 | 751,844,050 | 375,922,025.00 |
| Roguelike | 2 | 92,895,000 | 46,447,500.00 |
| Sandbox | 1 | 1,999,600 | 1,999,600.00 |
| Fighting | 1 | 8,028,540 | 8,028,540.00 |
| Horror | 6 | 139,027,234.88 | 23,171,205.81 |
| Racing | 3 | 201,594,500 | 67,198,166.67 |
| Management | 1 | 46,161,000 | 46,161,000.00 |
| Shooter | 6 | 305,807,694 | 50,967,949.00 |
| Action | 13 | 716,277,682 | 55,098,283.23 |
| Card | 1 | 115,000,000 | 115,000,000.00 |
| Visual Novel | 1 | 5,700,000 | 5,700,000.00 |
| Tower Defence | 1 | 449,100 | 449,100.00 |
| Soulslike | 1 | 33,990,000 | 33,990,000.00 |
| RPG | 5 | 148,348,080 | 29,669,616.00 |
| Adventure | 17 | 1,309,030,100 | 77,001,770.59 |
| Puzzle | 1 | 42,639 | 42,639.00 |
| Storytelling | 1 | 93,227 | 93,227.00 |
| Rhythm | 1 | 7,000,000 | 7,000,000.00 |
| Strategy | 3 | 115,250,000 | 38,416,666.67 |
| Platformer | 5 | 492,050,039 | 98,410,007.80 |
| Simulation | 9 | 50,100,114,403 | 5,566,679,378.11 |
| Casual | 8 | 170,043,150 | 21,255,393.75 |

</details>



### Q3: Does a game's rating relate to its commercial performance? 

```sql

-- Getting Rating, Copies Sold and Rev

SELECT 
"Rating",
"Game Type",
"Copies Sold",
"Revenue"
From "AllGames"
Order by "Rating" DESC


-- Grouping Top 10 Ratings 
CREATE TABLE "Rating_Info" AS (
Select "Rating", "Group_Number", "Game Type", "Revenue", "Copies Sold",
Sum("Copies Sold") OVER(PARTITION BY "Group_Number" ) AS "Rate_Copies",
Sum("Revenue") OVER(PARTITION BY "Group_Number" ) AS "Rate_Rev"

FROM

(SELECT "Rating", "Copies Sold", "Revenue", "Game Type", NTILE(10) OVER(ORDER BY "Rating" DESC) AS "Group_Number" FROM "AllGames")
LIMIT 10

```
<details>
<summary>View Table Query</summary>

| Rating | Rating_Group | Game_Type | Revenue | Copies_Sold | Avg_Group_Rating | Total_Group_Revenue |
|---:|---:|---|---:|---:|---:|---:|
| 4.90 | 1 | Indie | 26,495,000 | 5,300 | 1,434,100 | 133,552,651 |
| 4.85 | 1 | Indie | 129,492 | 500,000 | 1,434,100 | 133,552,651 |
| 4.83 | 1 | Indie | 2,900,000 | 89,400 | 1,434,100 | 133,552,651 |
| 4.80 | 1 | Indie | 9,995,000 | 117,000 | 1,434,100 | 133,552,651 |
| 4.80 | 1 | Indie | 28,900 | 3,400 | 1,434,100 | 133,552,651 |
| 4.80 | 1 | AAA | 89,982,000 | 146,000 | 1,434,100 | 133,552,651 |
| 4.80 | 1 | Indie | 881,580 | 42,000 | 1,434,100 | 133,552,651 |
| 4.75 | 1 | Indie | 42,639 | 400,000 | 1,434,100 | 133,552,651 |
| 4.70 | 1 | Indie | 449,100 | 25,000 | 1,434,100 | 133,552,651 |
| 4.70 | 1 | Indie | 2,648,940 | 106,000 | 1,434,100 | 133,552,651 |

</details>


### Q4: Does game price affect how many copies are sold? 
Querying whether there is a relationship between game price and copies sold?

```sql

SELECT 
"Rating",
"Genre",
"Revenue",
"Copies Sold"
FROM "AllGames"
ORDER BY "Rating" DESC

```


<details>
<summary>View all 99 games</summary>
     
| Rating | Genre | Revenue | Copies_Sold |
|---:|---|---:|---:|
| 4.90 | Casual | 26,495,000 | 5,300 |
| 4.85 | Rhythm | 129,492 | 500,000 |
| 4.83 | Adventure | 2,900,000 | 89,400 |
| 4.80 | Action | 9,995,000 | 117,000 |
| 4.80 | Horror | 28,900 | 3,400 |
| 4.80 | RPG | 89,982,000 | 146,000 |
| 4.80 | RPG | 881,580 | 42,000 |
| 4.75 | Puzzle | 42,639 | 400,000 |
| 4.70 | Tower Defence | 449,100 | 25,000 |
| 4.70 | Simulation | 2,648,940 | 106,000 |
| 4.70 | Management | 46,161,000 | 152,000 |
| 4.65 | Hack and Slash | 1,994,050 | 95,000 |
| 4.65 | Racing | 32,444,500 | 1,200,000 |
| 4.60 | Rhythm | 3,373,650 | 135,000 |
| 4.55 | Sports | 3,646,480 | 850,000 |
| 4.50 | Simulation | 5,148,000 | 1,200,000 |
| 4.50 | Platformer | 125,625,000 | 7,500,000 |
| 4.50 | Simulation | 1,307,673 | 1,100,000 |
| 4.50 | Simulation | 50,000,000,000 | 5,000,000 |
| 4.50 | Platformer | 70,000,000 | 2,000,000 |
| 4.45 | Adventure | 13,747,500 | 40,000 |
| 4.45 | Casual | 3,400,000 | 6,900,000 |
| 4.45 | Simulation | 49,283,000 | 35,000 |
| 4.44 | Casual | 665,000 | 288,000 |
| 4.43 | Action | 200,000,000 | 7,000,000 |
| 4.42 | Action | 200,000,000 | 4,000,000 |
| 4.40 | Strategy | 79,000,000 | 3,000,000 |
| 4.40 | Storytelling | 93,227 | 240,000 |
| 4.40 | RPG | 45,487,000 | 500,000 |
| 4.40 | Survival | 176,882 | 11,800 |
| 4.40 | Action | 24,895,850 | 500,000 |
| 4.40 | Platformer | 83,944 | 5,600 |
| 4.39 | Strategy | 3,250,000 | 1,500,000 |
| 4.37 | Adventure | 45,000,000 | 2,500,000 |
| 4.36 | Simulation | 1,400,000 | 300,000 |
| 4.35 | Roguelike | 89,400,000 | 3,700,000 |
| 4.35 | Action | 2,631,330 | 500,000 |
| 4.35 | Sports | 1,189,300 | 70,000 |
| 4.33 | Racing | 92,463,000 | 6,400,000 |
| 4.33 | Adventure | 383,936,000 | 24,300 |
| 4.30 | Shooter | 50,344 | 5,600 |
| 4.30 | Rhythm | 7,000,000 | 680,000 |
| 4.30 | Racing | 76,687,000 | 1,900,000 |
| 4.30 | Rhythm | 15,990,000 | 1,000,000 |
| 4.29 | Action | 16,600,000 | 1,500,000 |
| 4.27 | RPG | 11,700,000 | 537,000 |
| 4.25 | Adventure | 83,000,000 | 1,500,000 |
| 4.25 | Platformer | 296,322,000 | 7,800,000 |
| 4.25 | Adventure | 89,985,000 | 46,000 |
| 4.25 | Horror | 5,900,000 | 294,600 |
| 4.25 | Survival | 22,944,900 | 4,700,000 |
| 4.20 | Action | 31,395 | 250,000 |
| 4.20 | Hack and Slash | 749,850,000 | 1,300,000 |
| 4.19 | Visual Novel | 5,700,000 | 543,400 |
| 4.18 | Action | 231,000,000 | 3,300,000 |
| 4.15 | Action | 2,800,000 | 134,000 |
| 4.15 | Adventure | 336,432,700 | 1,000,000 |
| 4.15 | Shooter | 88,000,000 | 20,000,000 |
| 4.14 | Action | 18,100,000 | 500,000 |
| 4.14 | Casual | 2,200,000 | 200,000 |
| 4.14 | Casual | 2,600,000 | 550,000 |
| 4.12 | Adventure | 374,000 | 17,635 |
| 4.11 | Card | 115,000,000 | 5,300,000 |
| 4.11 | Horror | 10,000,000 | 888,000 |
| 4.07 | Adventure | 11,700,000 | 537,000 |
| 4.06 | Adventure | 215,000,000 | 3,500,000 |
| 4.06 | Adventure | 2,300,000 | 57,900 |
| 4.05 | Survival | 30,000,000 | 1,800,000 |
| 4.05 | Simulation | 35,994,000 | 6,730,000 |
| 4.03 | Adventure | 2,000,000 | 138,000 |
| 4.00 | Adventure | 6,745,000 | 157,300 |
| 4.00 | Casual | 27,600,000 | 4,100,000 |
| 4.00 | Adventure | 36,850,000 | 40,000 |
| 4.00 | Strategy | 33,000,000 | 664,800 |
| 4.00 | Adventure | 34,850,000 | 119,000 |
| 4.00 | Action | 7,076,927 | 1,500,000 |
| 4.00 | Simulation | 3,558,100 | 500,000 |
| 3.99 | Shooter | 97,485,000 | 1,000,000 |
| 3.97 | Adventure | 43,990,000 | 600,000 |
| 3.90 | Shooter | 7,917,600 | 415,000 |
| 3.90 | Shooter | 112,081,000 | 1,000,000 |
| 3.90 | Soulslike | 33,990,000 | 510,000 |
| 3.87 | Shooter | 273,750 | 1,300,000 |
| 3.85 | Casual | 29,095,150 | 9,100 |
| 3.75 | Roguelike | 3,495,000 | 16,000 |
| 3.70 | Sports | 8,875,000 | 550,000 |
| 3.70 | Party | 4,999,000 | 6,100 |
| 3.60 | Horror | 560,684.88 | 26,712 |
| 3.50 | Simulation | 774,690 | 10,800 |
| 3.50 | Horror | 384,650 | 35,000 |
| 3.40 | Platformer | 19,095 | 1,140 |
| 3.25 | Action | 228,640 | 90,000 |
| 3.20 | Sandbox | 1,999,600 | 31,000 |
| 3.20 | Action | 2,918,540 | 100,000 |
| 2.80 | Horror | 122,153,000 | 32,700 |
| 2.70 | Casual | 77,988,000 | 146,000 |
| 2.65 | Adventure | 219,900 | 10,000 |
| 2.40 | RPG | 297,500 | 15,000,000 |
| 2.35 | Fighting | 8,028,540 | 485,000 |

</details>



### Q5: Does a game's release period relate to its commercial performance? 

Querying if any months influence growth in games and what month is the most selling (is there any trends?)

```sql

Select 

EXTRACT(month from "Release Date") as Month,
SUM("Revenue") AS "Total Revenue",
SUM("Copies Sold") AS "Total Copies",
COUNT("Game Type") AS "Number_Games"

FROM "AllGames"
Group by Month 
ORDER BY MONTH ASC


```



| Rating_Group | Total_Revenue | Total_Copies_Sold | Game_Count |
|---:|---:|---:|---:|
| 1 | 76,575,520 | 809,300 | 5 |
| 2 | 270,849,753 | 11,362,000 | 8 |
| 3 | 50,630,246,927 | 13,409,600 | 12 |
| 4 | 96,959,700 | 10,226,100 | 6 |
| 5 | 686,130,175 | 19,928,535 | 19 |
| 7 | 230,990,000 | 4,500,000 | 2 |
| 8 | 767,328,775 | 12,742,900 | 10 |
| 9 | 406,170,589 | 19,663,740 | 11 |
| 10 | 464,319,723.88 | 51,030,112 | 11 |
| 11 | 1,085,207,630 | 5,910,900 | 8 |
| 12 | 137,291,950 | 3,762,400 | 7 |



→ View SQL Queries


## 04 —FINDINGS
Q1: How does commercial performance differ between Indie, AA and AAA games?

<img width="1173" height="783" alt="Screenshot 2026-10-12 125031" src="https://github.com/user-attachments/assets/e904e837-567d-4048-8c27-3a3a9b1a6dc8" />



Indie games generally have smaller team and budgets, AA games Occupy a mid budget postion while AAA games involve larger teams and higher investment.

AAA games account for 74% of total copies sold followed by AA at 18% and indie at 8% however the limited number of AA titles may affect the reliability of comparinsions. Using the median is important because a small number of blockbuster games can inflate the average sales which can distort comparinsons, comparing the median of copies sold provides a clerer insight to the typical performance across all game type. This helps determine  whether AAAs dominance in total sales is reflected in the performance of individual games or driven by a few exceptionally successful releases.


QUESTION 2

<img width="996" height="794" alt="image" src="https://github.com/user-attachments/assets/3f3bc226-2343-4687-9325-719687fa7bbb" />


Shooters, Action and Platformers Lead commercial sales, This suggests that these genres attract a strong consumer demand. Established franchises such as Battlefield and Metroid may benefit from loyal fanbases and brand recognition, encouraging repeat purchases 

<img width="1532" height="598" alt="image" src="https://github.com/user-attachments/assets/4c707056-783e-4020-abb3-3d69092f8fb7" />

Looking deeper, Card games are recorded as the highest average sales at 5.3 million copies; however this figure reflects just one game making it less representative of the genre overall. Platformers provide a more balanced insight with sales across AAA, AA and indie titles. This suggests that comercial oppurtunites exist across different development budgets making Platformers a potentially attractive genre for smaller studios seeking to compete without AAA-level investment

QUESTION 3

<img width="993" height="799" alt="image" src="https://github.com/user-attachments/assets/10cba4fb-7b2c-45b5-be3a-31695543a2dc" />

The games in the High-Mid rating range is recorded as the highest total sales, peaking at approxmiately 320 million copies, while the highest rated games generated considerably fewer sales; This suggests that higher ratings do not necessarily translate to higher sales, although positively rated games may still benefit from strong consumer confidence and purchasing interest.



Q4: Does game price affect how many copies are sold? 

<img width="979" height="788" alt="Screenshot 2026-10-12 115607" src="https://github.com/user-attachments/assets/bf628279-165d-448e-86fd-91a39e803a9c" />


The following Scatterplot follows the relationship between copies sold and the cost of the games. The results suggest that the relationship between cost and commercial sales varies across categories offering insights into investment oppurtunity and potential risks. 

AAA games show a postivie relationship between cost and copies sold, with some titles achieving exceptionally high sales however high investment does not guarentee comercial success in comparison to indie games where they show a gradual increase with some lower cost titles achieve sales as high or higher than some AAA games. This highlights the fact that smaller budget games can reach substantial audiences without requiring a same level of investment in comparinson to AAA titles. In contrast AA games display a negative trend suggesting that higher costs associated with lower sales within this dataset although further investigation is needed to establish  whether this pattern is meaningful.

These findings highlight potential investment oppurtunities across different categories. Publishers could balance AAA titles with lower cost indie projects as that is substantial for a wider audience, particually to players who are more price concious and may be less willing to purchase expensive releases. Investing in a broader range of afforable games could help not only expand your audience but generate more copies in the long run.

QUESTION 5

<img width="992" height="801" alt="image" src="https://github.com/user-attachments/assets/17d77242-bd55-4775-914a-bb89a1baa897" />

The findings suggest that release timing may be associated with commercial performance although patterns vary by game types.                                                                                                                                                                                                                                                                   Across the whole dataset, May and September show the most promising sales while October is recorded as the highest total sales, largely driven by one of the best selling AAA titles during this year which makes October a outlier rather than a reliable indicater of the the best release month. AAA titles performed strongly thoughout much of the year, AA titles peaked during May and Indie titles recorded their strongest sales in the later month represented within the data.                                                                                                                                                                                                                                                                                                Overall, May and September appear to be promising release windows. However due to seeing the rise in copies due to a best selling AAA game during October, Release timing alone cannot fully determine the commercial success such as factors such as Marketing, game quality and franchise recognition. A larger data set would determine whether these seasonal patters are consistent.
