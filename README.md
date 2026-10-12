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

### Q1: How does commercial performance differ between Indie, AA and AAA games? 

 
My hope is to 
Compare Indie, AA and AA by its copies sold, revenue and rating and see what drove

<img width="638" height="680" alt="image" src="https://github.com/user-attachments/assets/fd0c8bd5-57d1-4333-9e91-3040d02b4af5" />



### Q2: Which genres sell the most copies?  
The aim was to compare the total sales or average/median sales for each genre. 



<img width="342" height="236" alt="image" src="https://github.com/user-attachments/assets/7a3b3bd5-8d2c-458f-9b55-c708386f30d3" />




### Q3: Does a game's rating relate to its commercial performance? 
Rating → Copies Sold + Revenue 

<img width="616" height="699" alt="image" src="https://github.com/user-attachments/assets/09d743ad-6d16-4e8a-8843-4b110e5898d6" />




### Q4: Does game price affect how many copies are sold? 
Querying whether there is a relationship between game price and copies sold?

<img width="227" height="194" alt="image" src="https://github.com/user-attachments/assets/e58616dc-2c90-47ff-89c5-6238e149f1b6" />





### Q5: Does a game's release period relate to its commercial performance? 

Querying if any months influence growth in games and what month is the most selling (is there any trends?)

<img width="418" height="296" alt="image" src="https://github.com/user-attachments/assets/168ea63c-29f3-49d1-9cb5-f54e942f7851" />


→ View SQL Queries


## 04 —FINDINGS
Q1: How does commercial performance differ between Indie, AA and AAA games?

<img width="1173" height="783" alt="Screenshot 2026-10-12 125031" src="https://github.com/user-attachments/assets/e904e837-567d-4048-8c27-3a3a9b1a6dc8" />



Indie games generally have smaller team and budgets, AA games Occupy a mid budget postion while AAA games involve larger teams and higher investment.

AAA games account for 74% of total copies sold followed by AA at 18% and indie at 8% however the limited number of AA titles may affect the reliability of comparinsions. Using the median is important because a small number of blockbuster games can inflate the average sales a which can distort comparinsons, comparing the median of copies sold provides a clerer insight to the typical performance across all game type. This helps determine  whether AAAs dominance in total sales is reflected in the performance of individual games or driven by a few exceptionally successful releases.


QUESTION 2

<img width="996" height="794" alt="image" src="https://github.com/user-attachments/assets/3f3bc226-2343-4687-9325-719687fa7bbb" />


Shooters, Action and Platformers Lead commercial sales, This suggests that these genres attract a strong consumer demand. Established franchises such as Battlefield and Metroid may benefit from loyal fanbases and brand recognition, encouraging repeat purchases 

QUESTION 3

<img width="993" height="799" alt="image" src="https://github.com/user-attachments/assets/10cba4fb-7b2c-45b5-be3a-31695543a2dc" />

The games in the High-Mid rating range is recorded the highest total sales, peaking at approxmiately 320 million copies, while the highest rated games generated considerably ferwer sales; This suggests that higher ratings do not necessarily translate to higher sales, although positively rated games may still benefit from strong consumer confidence and purchasing interest.



Q4: Does game price affect how many copies are sold? 

<img width="979" height="788" alt="Screenshot 2026-10-12 115607" src="https://github.com/user-attachments/assets/bf628279-165d-448e-86fd-91a39e803a9c" />


The following Scatterplot follows the relationship between copies sold and the cost of the games. The results suggest that the relationship between cost and commercial sales varies across categories offering insights into investment oppurtunity and potential risks. 

AAA games show a postivie relationship between  cost and copies sold , with some titles achieveing exceptionally high sales however high investment does not guarentee comercial success in comparison to indie games where they show a gradual increase with some lower cost titles achieve sales as high or higher than some AAA games. This highlights the fact that smaller budget games can reach substantial audiences without requiring a same level of investment in comparinson to AAA titles. In contrast AA games display a negative trend suggesting that higher costs associated with lower sales within this dataset although further investigation is needed to establish  whether this pattern is meaningful.

These findings highlight potential investment oppurtunities across different categories. Publishers could balance AAA titles with lower cost indie projects as that is substantial for a wider audience, particually to players who are more price concious and may be less willing to purchase expensive releases. Investing in a broader range of afforable games could help not only expand your audience but generate more copies in the long run.

QUESTION 5

<img width="992" height="801" alt="image" src="https://github.com/user-attachments/assets/17d77242-bd55-4775-914a-bb89a1baa897" />

The findings suggest that release timing may be associated with commercial performance although patterns vary by game types.                                                                                                                                                                                                                                                                   Across the whole dataset, May and September show the most proising sales while October is recorded as the highest total sales, largely driven by one of the best selling AAA titles during this year which makes October a outlier rather than a reliable indicater of the the best release month. AAA titles performed strongly thoughout much of the year, AA titles peaked during May and Indie titles recorded their stongest sales in the later month represented within the data.                                                                                                                                                                                                                                                                                                Overall, May and September appear to be promising release windows. However due to seeing the rise in copies due to a best selling AAA game during October, Release timing alone cannot fully determine the commercial success such as factors such as MArketing, game quality and franchise recognition. A larger data set would determine whther these seasonal patters are consistent.
