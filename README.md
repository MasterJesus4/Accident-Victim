# Accident-Victim
Exploratory Data Analysis In SQL

## Project Overview
To investigate and analyze accidents, focusing on the victims and level of impact to identify trends, patterns and insights that can inform prevention and mitigation strategies. Under thhis project, i asked about about eight(8) questions to arrive at my conclusion.

## Data Source
The data source was obtained from government databases, including :
- National Highway Traffic Safety administration(NHTSA)
- Occupational Safety Health Administration (OSHA)
- National Institute For Occupational Safety And Health (NIOSH)

  ## Objectives
  The objective for this project are as follows :
  - Analyze the data on accidents to identify trends, patterns, and correlation between variables such as :
  - Number of victims
  - Number of injuries
  - Type of accident and impact
  - Identify the most common  causes of accidents and their corresponding impact
  - Determine the relationship between variables such as: left hand or right hand and point of impact, etc

    ## Tools
    SQL was used to analyze the data and the following questions were asked to arrive at a meaningful conclusion:

     How many accidents have occurred in urban areas versus rural areas?
  
    SELECT
		
     [Area],
		
     COUNT([AccidentIndex]) AS 'Total Accident'
		
    FROM 
		
   [Project Portfolio].dbo.accident

    GROUP BY 

  		[Area];

2. Which day of the week has the highest number of accidents?
 
 SELECT 

 [Day],
	
 COUNT([AccidentIndex]) 'Total Accident'

FROM 

 [Project Portfolio].dbo.accident

GROUP BY 

 [Day]

ORDER BY 

 Total Accident' DESC;

3. What is the average age of vehicles involved in accidents based on type?

SELECT 

 [VehicleType], 

 COUNT([AccidentIndex]) AS 'Total Accident', 
	
 AVG([AgeVehicle]) AS 'Average Age'

FROM 

 [Project Portfolio].dbo.accident
 
WHERE 

 [AgeVehicle] IS NOT NULL

GROUP BY 

 [VehicleType]

ORDER BY 

 'Total Accident' DESC;

4.  Can we identify any trends in accidents based on the age of vehicles involved?
	
 SELECT Age_group,
	
 COUNT([AccidentIndex]) AS 'Total Accident',
	
 AVG([AgeVehicle]) AS 'Average Year'

FROM (

 SELECT
	
  [AccidentIndex],
	
  [AgeVehicle],
	
  CASE
	
   WHEN [AgeVehicle] BETWEEN 0 AND 5 THEN 'New'
		
   WHEN [AgeVehicle] BETWEEN 6 AND 10 THEN 'Regular'
		
   ELSE 'Old'
		
  END AS Age_group
	
 FROM [Portfolio Project].dbo.vehicle
)
AS SubQuery

GROUP BY 

 Age_group

5.  Are there any specific weather conditions that contribute to severe accidents?

   NOTE: Declare is used to call each severity.
 
 Severity can be fatal,serious and slight. You can change your declare at each point
	
   Declare @Severity Varchar(100)
		
   SET @Severity = 'serious'

			SELECT 
	
    [WeatherConditions],
		
    COUNT([Severity]) AS Total_Accident
		
   FROM 
		
    [Portfolio Project].dbo.accident
		
   WHERE Severity =  @Severity
		
   GROUP BY 
		
    [WeatherConditions]
		
   ORDER BY 
		
    Total_Accident DESC;

6.  Do accidents often involve impacts on the left-hand side of vehicles?

   SELECT 

	[LeftHand], 

   COUNT([AccidentIndex]) AS 'Total Accident'
		
  FROM 
	
   [Portfolio Project].dbo.vehicle
		
   WHERE
		
   [LeftHand] IS NOT NULL
		
  GROUP BY 
	
   [LeftHand]

7.  Are there any relationships between journey purposes and the severity of accidents?
	
  Select V.[JourneyPurpose], COUNT( A.[Severity]) AS Total_Accident,
	
 CASE 
	
 WHEN COUNT( A.[Severity]) BETWEEN 0 AND 1000 THEN 'Low'
	
 WHEN COUNT( A.[Severity]) BETWEEN 1000 AND 2000 THEN 'Mild'
	
 WHEN COUNT( A.[Severity]) BETWEEN 2000 AND 3000 THEN 'Serious'
	
   ELSE 'Very high'
	 
   END AS 'Level'

FROM [Portfolio Project].dbo.accident AS A

JOIN [Portfolio Project].dbo.vehicle AS V

ON A.AccidentIndex = V.AccidentIndex

GROUP BY  V.[JourneyPurpose]

ORDER BY 2 DESC

8.  Calculate the average age of vehicles involved in accidents , considering Day light and point of impact:
	
  SELECT 
	
   AVG(V.[AgeVehicle]) AS Average,
		
  A.[LightConditions],
	
  V.[PointImpact]
	
   FROM 
		
   [Portfolio Project].dbo.accident AS A
		
   JOIN [Portfolio Project].dbo.vehicle AS V
		
   ON A.AccidentIndex = V.AccidentIndex
		
    WHERE [PointImpact] = 'Nearside' AND [LightConditions] = 'Daylight'
		
   GROUP BY V.[PointImpact], A.[LightConditions]




  
  
