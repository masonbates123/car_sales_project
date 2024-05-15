# Car Sales Analysis

### Table of Contents

- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Tools](#tools)
- [Questions](#questions)
- [Data Analysis](#data-analysis)
- [Results](#results)
- [Limitations](#limitations)

### Project Overview

This project analyzes trends and characteristics of car sales over the past few decades. Some questions that are answered include which cars are the most popular and when do people typically purchase cars.

### Data source

The dataset used for this project is the "car_sales.csv" file in Kaggle which contains information such year, make, model, body, transmission, purchase date, and more.
[Download here](https://www.kaggle.com/datasets/syedanwarafridi/vehicle-sales-data)
### Tools

- R - Data Visualization
- Excel
- SQL Server - Data Analysis

### Questions

- What are the best selling make and models?
- What are the most popular body types
- How has the average selling price changed over time?
- Which transmission type is more expensive: automatic or manual?
- Over time, what has been the most popular months to buy a car?

### Data Analysis

- Question 1

```sql
select make,model,count(model) as total
      from sales
      group by make,model
      order by total desc
      limit 5;
```
- Question 2

```sql
select body,count(body) as total
                        from (select upper(body) as body
                              from sales) t1
                        group by body
                        order by total desc
                        limit 10;
```

- Question 3

```sql
select year,avg(sellingprice) as AVG
                     from sales
                     where year >= 2000
                     group by year;
```

![image](https://github.com/masonbates123/projects/assets/169870845/77fe537c-9d8e-47ad-8217-40470be2b68c)


- Question 4

```sql
select transmission, avg(sellingprice) as AVG
                   from sales
                   where transmission in ('automatic','manual')
                   group by transmission;
```

- Question 5

  ```sql
  with months as (select year, substr(saledate,5,3) as month
               from sales)

  with month_freqs as (select year,month, 
        row_number() over (partition by year order by count(month) desc) freq
        from months
        group by year,month)

  select year,month
         from month_freqs
         where freq = (select max(freq) as freq
         from month_freqs
         group by year);

### Results

1. The most popular car in the dataset is the Nissan Altima. Out of the top 5, Ford has 3 vehicles: the F-150, Fusion, and Escape.
2. Sedans are by far the most popular body type, as it has nearly a one hundred thousand more sales than the next most popular body type, SUVs.
3. The average selling price has increased greatly over time, reaching to $20,090.20 by the middle of the 2010s.
4. On average, automatic transmissions are more expensive than manual transmissions. The difference is a little over $2000.
5. Since the early 1980s, the most popular month to buy a car in has almost exclusively been January or February.

### Limitations

The last year in the dataset is 2015, so current trends may be slightly different than the findings in this project.


 

