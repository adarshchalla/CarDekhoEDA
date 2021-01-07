# CarDekhoEDA
Web Scraping (Data Mining) with EDA Project

1)	Problem Statement

Analysis of data of Used Cars from https://cardekho.com/

Domain : Website has Used Car Sales data
Related websites : cars24.com, carwale.com, cartrade.com
Reason for choosing cardekho.com : 
i.	Provided more number of features for web scraping
ii.	Website allows for web scraping without any denial of 404 error
iii.	Data can be scrapped using wide range of filters available in it

2)	Data Collection
BeautifulSoup was used to collect the data scrapped from the website. While scraping itself, few variables were handled and cleaned as per the requirement. 
The for loop is run on the url by considering different filters from the above cell.
Since the data is huge if the cities (12 cities) are considered on whole, they were chosen individually in different notebooks to extract the data from the cities individually.

Later, they were put into a data frame (df)

Number of rows and columns in the data frame: 12954 rows and 11 columns

Column names in the raw file of scraped data : 
a)	carname = name of the car along with year of registration and brand-variant
b)	city - place where car being sold['ahmedabad','bangalore','chennai','delhi-ncr','gurgaon','hyderabad','jaipur','kolkata','mumbai','new-delhi','noida','pune']
c)	car_price = price of the car quoted
d)	body_type=['sedan','Hatchback','SUV','Luxury','MUV','Minivan','Convertible','Coupe','Hybrid','Wagon','super-luxury','hybrid']
e)	tranmission= ['manual','automatic']
f)	seller_type= ['dealer','individual']
g)	owner_type= ['unregistered','first-owner','second-owner','third-owner-or-more']
h)	color= ['White','Silver','Red','Blue','Black','Brown','Orange','Green','violet','Yellow','Gold','Other']
i)	Year = data taken from the car name using regex
j)	Fuel_type = Fuel used, km_run and locality of the car sold



3)	Data Understanding and Cleaning

Regex Usage to clean data :
The column Fuel_type had to be further cleaned to extract the needed values of km_driven, fuel_used and locality into separate columns. Similarly, column CarName had to be further cleaned and processed to extract Brand column in the data frame. Both these requirements were fulfilled using regex.

Duplicate Data: The cities new-delhi,Gurgaon,Noida and Delhi-NCR had same data mentioned across all the cities. Hence deleted 3 cities out of the above four. Only data pertaining to Delhi-NCR were retained.

Junk Data: The column owner_type had four options : first,second, third & more and unregistered.
Unregistered Car meant its New Car, where the problem statement deals with Used Cars. Hence, we had to delete all data pertaining to this junk unregistered value in owner_type column.

After cleaning and removing (duplicate & junk) data and also modifying the columns, the following are the properties of the table derived:

Rows: 9027
Columns: 13

 



4)	Converting the cleaned and usable data into csv file
 
5)	Data Investigation & Analysis
 
Conclusion :
The average km_driven of the cars put on sale is 56632 km
The average price of the car is 11.02 Lakhs
The minimum price of car sold is 37000 thousand

i)	Univariate Analysis
1)	The count of cars according to brands.
 

 

Conclusion
Maruti cars were present the most in non-luxury variants 
Hyundai were second 
Surprisingly, Mercedes and BMW were also sold comparatively to other brands.
2)	The range of kilometres driven of the cars that were being sold
 

 
Conclusion 
The range of kilometers is from 30000 to 70000 , rest of all are outliers

(3)	Cars sorted as per city with delhi-ncr having the highest no. of cars and jaipur the least.
 
 
Conclusion
Cities like kolkata , chennai , hyderabad, ahmedabad and jaipur may be relying on public transport whereas the metros like delhi mumbai and bangalore and pune are more towards own-transport

(4)	Registration year-wise cars sale
 
 
  

 Conclusion 
   2017 registration year cars saw the highest number of sales. which is periodically declining towards 2020
ii)	Bivariate Analysis 
(1)	Minimum, max and mean of the car price according to the body type
 

 

Conclusion
The costliest ones are the super luxury cars and minimum are hatch-back and minivan types.
Luxury and wagon types have costs in mid-range.

(2)	Car Price for a given type of owner 

 
 
Conclusion :

As it is obvious, first owner cars costs higher followed by second and third owner cars

iii)	Multivariate Analysis
(1)	Correlation (via heatmap) between car_price, Year and Km_driven columns
 
 


Conclusion
The older the car the more is the no. of km_driven 
The more the number of km_driven lower is the price.
More than age of the car , it is the km_driven that decides the price of the car. 

(2)	Car statistics (price, km-driven) for a given owner-type as per the fuel used
Code :
pd.pivot_table(index =['Fuel_used', 'owner_type'],data=df, aggfunc={'km_driven': np.mean,'car_price': [min,max,np.mean]}).round()
 

(3)	Car price and km driven as per transmission type
 
 
Conclusion : The cost of automatic cars is thrice the cost of manual cars.

6)	Client Requirement

(1)	The statistics of car_price and km_driven as per the brand
Code: 
pd.pivot_table(data, index =['Brand'], aggfunc={'km_driven': [min , max, np.mean],'car_price': [min , max, np.mean, np.median],'Year': np.mean})
 
Conclusion : For the brand maruti- the minimum and maximum car price is 45000 and 11.85 lakh respectively with an average of 4.86 lakhs and for the same brand maruti - the minimum km_driven is 1000 and maximum is 12 lakh kms and an average of 53800 kms

(2)	The cars sold according to color
 
 
Conclusion : White cars are the maximum to be sold followed by silver and black where as rare colors of violet , gold , yellow , etc are the least to be sold
(3)	The cars available in a particular city according to color
 
 
Conclusion : white cars are most sold cars across the city
(4)	The number of cars sold for different owner types based on whether the seller is a dealer or individual
 
 
Conclusion : People are preferring to sell the car via dealers
(5)	The average price of cars being sold for a given owner_type and seller type
 
 
Conclusion : First owner cars sold by a dealer are costly whereas third owner cars sold by individually cost the least. For a customer who is willing to sell a car, irrespective of the owner-type, its preferable that he sells it via a dealer
(6)	Statistical analysis for the most sold car maruthi
 
 
Conclusion : Manual maruthi cars are used to the maximum extent than automatic cars.
The older the better , manual cars have overtook automatic cars in terms of usage
(7)	Brands sold according to transmission type
 
 
Conclusion : The luxury cars like mercedes and bmw are mostly having automatic transmission. Audi car has the least manual cars for sale
(8)	Average rate of cars being sold according to the year
 
 
                    
Conclusion : The average rates of car are steadily increasing in the modern times
(9)	Preferred brands sold in cities

 

 
Conclusion : Maruti was sold the highest in all the cities except for chennai and kolkata where the hyundai was sold the highest
(10)	The average car rates for a given brand according to owner type
 
 
Conclusion : The average rates of car are steadily increasing in the modern times
(11)	Depiction of car brands, sold the maximum according to cities
 
 
Conclusion : Maruti is the highest sold brand followed by Hyundai across cities


Submitted By : 
Adarsh Challa
Sandhya CSR 

