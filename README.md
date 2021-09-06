# YYYYMMDD-GYYMMDD
I had to do this once. Now you don't have to.


``` SQL
WITH [years] AS (
          SELECT '19120729' AS [YMD]
    UNION SELECT '19120829' AS [YMD]
    UNION SELECT '19261214' AS [YMD]
    UNION SELECT '19261230' AS [YMD]
    UNION SELECT '19890107' AS [YMD]
    UNION SELECT '19890108' AS [YMD]
    UNION SELECT '19990101' AS [YMD]
    UNION SELECT '20190101' AS [YMD]
    UNION SELECT '20190501' AS [YMD]
    UNION SELECT '20210906' AS [YMD]
)
SELECT
    [YMD],
    CASE 
        -- Concat(G, YY, MMDD)
        --  1868:明治
        --  1912:大正
        --  1926:昭和
        --  1989:平成
        --  2019:令和
        --  There will be more and this will eventually be out of date.
        WHEN [YMD] <= '19120729' THEN CONCAT(1, RIGHT(CONCAT(0, PARSE(LEFT([YMD], 4) AS Int) - 1867), 2), RIGHT([YMD], 4)) 
        WHEN [YMD] <= '19261224' THEN CONCAT(2, RIGHT(CONCAT(0, PARSE(LEFT([YMD], 4) AS Int) - 1911), 2), RIGHT([YMD], 4)) 
        WHEN [YMD] <= '19890107' THEN CONCAT(3, RIGHT(CONCAT(0, PARSE(LEFT([YMD], 4) AS Int) - 1925), 2), RIGHT([YMD], 4)) 
        WHEN [YMD] <= '20190430' THEN CONCAT(4, RIGHT(CONCAT(0, PARSE(LEFT([YMD], 4) AS Int) - 1988), 2), RIGHT([YMD], 4)) 
        ELSE                          CONCAT(5, RIGHT(CONCAT(0, PARSE(LEFT([YMD], 4) AS Int) - 2018), 2), RIGHT([YMD], 4)) 
    END AS [GYMD]
FROM [years]
```

# Contributing
Feel free to add other languages or improve this abomination of SQL. 
There has to be at least 4 of us who has run into this need in the real world.
