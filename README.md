# Netflix_PowerBI
Netflix TV Shows &amp; Movies Analysis by Country and Ratings

-- Show movies and tv-shows distribution

SELECT
    COUNT(type = 'TV Show' OR NULL) as TV_ShowsCount,
    COUNT(type = 'Movie' OR NULL) as MoviesCount,
    (COUNT(type = 'TV Show' OR NULL) * 100.0) / (COUNT(*)) as TV_ShowsPercentage,
    (COUNT(type = 'Movie' OR NULL) * 100.0) / (COUNT(*)) as MoviesPercentage
FROM
    Netflix;

-- Show top 5 movie countries on Netflix

SELECT
  type,
  Country,
    COUNT(Country) as CountryCount
FROM Netflix
WHERE type LIKE '%movie%'
GROUP BY type, Country
ORDER BY CountryCount DESC
LIMIT 5;

-- Show top 5 tv-shows countries on Netflix

SELECT
  type,
  Country,
  COUNT(Country) as CountryCount
FROM Netflix
WHERE type LIKE '%tv%'
GROUP BY type, Country
ORDER BY CountryCount DESC
LIMIT 5;


-- Show Country distribution of TVShows and Movies

SELECT
  Country,
    COUNT(COUNTRY) as "TV Shows & Movies Count",
    (COUNT(Country)/(SELECT COUNT(*) FROM NETFLIX)*100) as PerCountryPercentage
FROM NETFLIX
GROUP BY Country
ORDER BY "TV Shows & Movies Count" DESC;

-- Display 

SELECT
    Country,
    rating,
    (COUNT(rating) / (SELECT COUNT(*) FROM Netflix WHERE Country = n.Country) * 100) AS Rating
FROM Netflix n
GROUP BY Country, rating;
