# Wattravels Event_Sphere

#### Wattravels Project Overview

Data analytics project designed to deliver deep insights into global events across continents and countries. It leverages event data to uncover trends, optimize strategies, and drive decision-making for event planning and management.

![Wattravel View](https://github.com/user-attachments/assets/46df4b2e-5dd5-4834-b18d-17705606e917)

### Project Question

- Identifies total profit generated by events across continents
- Evaluates profit by continent for events marked as 'Completed
- Highlights countries with the highest profits from completed events
- Analyzes the total PHQ attendance across continents to identify regions with the highest engagement
- Most Frequently Hosted Event Categories

#### Data Analysis

My SQL Server query/code

```sql
-- Query 1.1: Continent profit from all events (highest to lowest) without 'Other'
SELECT 
    CASE 
        WHEN Country IN ('France', 'Germany', 'Spain', 'Poland', 'Sweden') THEN 'Europe'
        WHEN Country IN ('USA', 'Canada', 'Mexico') THEN 'North America'
        WHEN Country IN ('China', 'Japan', 'India') THEN 'Asia'
        WHEN Country IN ('South Africa', 'Nigeria', 'Egypt') THEN 'Africa'
        WHEN Country IN ('Australia', 'New Zealand') THEN 'Oceania'
        WHEN Country IN ('Brazil', 'Argentina', 'Chile') THEN 'South America'
    END AS Continent,
    SUM([Event Total Spend]) AS Total_Profit
FROM 
    dbo.event_data
WHERE 
    Country IN (
        'France', 'Germany', 'Spain', 'Poland', 'Sweden',
        'USA', 'Canada', 'Mexico',
        'China', 'Japan', 'India',
        'South Africa', 'Nigeria', 'Egypt',
        'Australia', 'New Zealand',
        'Brazil', 'Argentina', 'Chile'
    )
GROUP BY 
    CASE 
        WHEN Country IN ('France', 'Germany', 'Spain', 'Poland', 'Sweden') THEN 'Europe'
        WHEN Country IN ('USA', 'Canada', 'Mexico') THEN 'North America'
        WHEN Country IN ('China', 'Japan', 'India') THEN 'Asia'
        WHEN Country IN ('South Africa', 'Nigeria', 'Egypt') THEN 'Africa'
        WHEN Country IN ('Australia', 'New Zealand') THEN 'Oceania'
        WHEN Country IN ('Brazil', 'Argentina', 'Chile') THEN 'South America'
    END
ORDER BY 
    Total_Profit DESC;
```

```sql
-- Query 1.2: Continent profit from completed events (highest to lowest)
SELECT 
    CASE 
        WHEN Country IN ('France', 'Germany', 'Spain', 'Poland', 'Sweden') THEN 'Europe'
        WHEN Country IN ('USA', 'Canada', 'Mexico') THEN 'North America'
        WHEN Country IN ('China', 'Japan', 'India') THEN 'Asia'
        WHEN Country IN ('South Africa', 'Nigeria', 'Egypt') THEN 'Africa'
        WHEN Country IN ('Australia', 'New Zealand') THEN 'Oceania'
        WHEN Country IN ('Brazil', 'Argentina', 'Chile') THEN 'South America'
    END AS Continent,
    SUM([Event Total Spend]) AS Total_Profit
FROM 
    dbo.event_data
WHERE 
    [Event status] = 'Completed' 
    AND Country IN (
        'France', 'Germany', 'Spain', 'Poland', 'Sweden',
        'USA', 'Canada', 'Mexico',
        'China', 'Japan', 'India',
        'South Africa', 'Nigeria', 'Egypt',
        'Australia', 'New Zealand',
        'Brazil', 'Argentina', 'Chile'
    )
GROUP BY 
    CASE 
        WHEN Country IN ('France', 'Germany', 'Spain', 'Poland', 'Sweden') THEN 'Europe'
        WHEN Country IN ('USA', 'Canada', 'Mexico') THEN 'North America'
        WHEN Country IN ('China', 'Japan', 'India') THEN 'Asia'
        WHEN Country IN ('South Africa', 'Nigeria', 'Egypt') THEN 'Africa'
        WHEN Country IN ('Australia', 'New Zealand') THEN 'Oceania'
        WHEN Country IN ('Brazil', 'Argentina', 'Chile') THEN 'South America'
    END
ORDER BY 
    Total_Profit DESC;
```

```sql
-- Query 1.3: Country profit from all events (highest to lowest)
SELECT 
    Country,
    SUM([Event Total Spend]) AS Total_Profit
FROM 
    dbo.event_data
GROUP BY 
    Country
ORDER BY 
    Total_Profit DESC;
```

```sql
-- Query 1.4: Country profit from completed events (highest to lowest)
SELECT 
    Country,
    SUM([Event Total Spend]) AS Total_Profit
FROM 
    dbo.event_data
WHERE 
    [Event status] = 'Completed'
GROUP BY 
    Country
ORDER BY 
    Total_Profit DESC;
```

```sql
-- Query 2.1: Continents with the highest PHQ attendance (highest to lowest)
SELECT 
    CASE 
        WHEN Country IN ('France', 'Germany', 'Spain', 'Poland', 'Sweden') THEN 'Europe'
        WHEN Country IN ('USA', 'Canada', 'Mexico') THEN 'North America'
        WHEN Country IN ('China', 'Japan', 'India') THEN 'Asia'
        WHEN Country IN ('South Africa', 'Nigeria', 'Egypt') THEN 'Africa'
        WHEN Country IN ('Australia', 'New Zealand') THEN 'Oceania'
        WHEN Country IN ('Brazil', 'Argentina', 'Chile') THEN 'South America'
    END AS Continent,
    SUM([PHQ Attendance]) AS Total_PHQ_Attendance
FROM 
    dbo.event_data
WHERE 
    [PHQ Attendance] IS NOT NULL -- Ensures only rows with attendance data
    AND Country IN (
        'France', 'Germany', 'Spain', 'Poland', 'Sweden',
        'USA', 'Canada', 'Mexico',
        'China', 'Japan', 'India',
        'South Africa', 'Nigeria', 'Egypt',
        'Australia', 'New Zealand',
        'Brazil', 'Argentina', 'Chile'
    ) -- Only include valid countries mapped to continents
GROUP BY 
    CASE 
        WHEN Country IN ('France', 'Germany', 'Spain', 'Poland', 'Sweden') THEN 'Europe'
        WHEN Country IN ('USA', 'Canada', 'Mexico') THEN 'North America'
        WHEN Country IN ('China', 'Japan', 'India') THEN 'Asia'
        WHEN Country IN ('South Africa', 'Nigeria', 'Egypt') THEN 'Africa'
        WHEN Country IN ('Australia', 'New Zealand') THEN 'Oceania'
        WHEN Country IN ('Brazil', 'Argentina', 'Chile') THEN 'South America'
    END
ORDER BY 
    Total_PHQ_Attendance DESC;
```
