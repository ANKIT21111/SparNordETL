# SparNordETL
Spar Nord Bank is a Danish Bank which is trying to observe the withdrawal behavior and the corresponding dependent factors to optimally manage the refill frequency. It has published dataset on (https://www.kaggle.com/datasets/sparnord/danish-atm-transactions) Kaggle .
## Dataset featuring: 
This data set contains various types of transactional data as well as the weather data at the time of the transaction, such as:
Transaction Date and Time: Year, month, day, weekday, hour
1. Status of the ATM: Active or inactive
2. Details of the ATM: ATM ID, manufacturer name along with location details such as longitude, latitude, street name, street number and zip code
3. The weather of the area near the ATM during the transaction: Location of measurement such as longitude, latitude, city name along with the type of weather, temperature, pressure, wind speed, cloud and so on
4. Transaction details: Card type, currency, transaction/service type, transaction amount and error message (if any)
## TARGET DIMENSIONAL MODEL:
For this project Spar Nord needs there warehouse to be designed in provided target dimensional model as follows:
![image](https://github.com/ANKIT21111/SparNordETL/assets/52655857/ce97647e-f5f8-4053-a6b7-3c795a0a03c7)
1. ATM dimension - This dimension will have the data related to the various ATMs present in the dataset along with the ATM number(ATM ID in the original dataset), ATM manufacturer and a reference to the ATM location and is very important for solving analytical queries related where ATM data will be used.
2. Location dimension - This is a very important dimension containing all the location data including location name, street name, street number, zip code and even the latitude and longitude. This information will be very important for solving problems related to the particular location at which a transaction took place and can help banks in things like pinpointing locations where ATMs where demand is higher as compared to other locations. Combined with weather data in the transaction table, this can be used to further do analysis such as how weather affects the demand at ATMs at a particular location.
3. Date dimension - This is another very important dimension which is almost always present where data such as transactional data is being dealt with. This dimension includes fields such as the full date and time timestamp, year, month, day, hour as well as the weekday for a transaction. This all can help in analysing the transaction behaviour with respect to the time at which the transaction took place and also how the transaction activity varies between weekdays and weekends.
4. Card type dimension - This dimension has the information about the particular card type with which a particular transaction took place. This can help in performing analysis on how the number of transactions varies with respect to each different card type.
5. Transaction fact - This is the actual fact table for the data set which contains all of the numerical data such as the currency of the transaction, service, transaction amount, message code and text as well as weather info such as description, weather id etc.
## SCHEMA FOR ATM_DATA TARGET DIMENSIONAL MODEL:
1 .DIM_LOCATION Column Name Data Type location_id INT location VARCHAR(50) streetname VARCHAR(255) street_number INT zipcode INT lat DECIMAL(10,3) lon DECIMAL(10,3) PRIMARY KEY location_id

2. DIM_ATM Column Name Data Type Comments/Foreign Key atm_id INT atm_number VARCHAR(20) atm_manufacturer VARCHAR(50) atm_location_id INT PRIMARY KEY atm_id FOREIGN KEY atm_location_id REFERENCES DIM_LOCATION (location_id) 

3. DIM_DATE Column Name Data Type date_id INT full_date_time TIMESTAMP year INT month VARCHAR(20) day INT hour INT weekday VARCHAR(20) PRIMARY KEY date_id 

4. DIM_CARD_TYPE Column Name Data Type card_type_id INT card_type VARCHAR(30) PRIMARY KEY card_type_id 

5. FACT_ATM_TRANS Column Name Data Type Comments/Foreign Key trans_id BIGINT atm_id INT weather_loc_id INT date_id INT card_type_id INT atm_status VARCHAR(20) currency VARCHAR(10) service VARCHAR(20) transaction_amount INT message_code VARCHAR(255) message_text VARCHAR(255) rain_3h DECIMAL(10,3) clouds_all INT weather_id INT weather_main VARCHAR(50) weather_description VARCHAR(255) PRIMARY KEY trans_id FOREIGN KEY weather_loc_id REFERENCES DIM_LOCATION (location_id) atm_id REFERENCES DIM_ATM (atm_id) date_id REFERENCES DIM_DATE (date_id) card_type_id REFERENCES DIM_CARD_TYPE (card_type_id)
