# Porsche Sales Data Quality

### Columns Data Map

| Column | Required | Description | Examples raw values|
|--------|----------|-------------|--------------------|
|sale_id|yes| Unique sales record ID|1, 2, 86| 
|sale_date|yes|Raw sales date|`2024-02-30 `, ` April 31st, 2024`,`2027.10.01`, `05-27-27`, `03/07/2027`|
|customer_name|yes|Customer Name|`SOPHIA Miller`,`Isabella Garcia`|
|porsche_model|yes|Porsche Model|`911 Turbo S`,`Taycan Turbo`|
|model_year|yes|Porsche model year|`2022`,`twenty twenty four`,`two thousand twenty one`,`20-23`|
|sale_price|yes|Raw Sales Price|`$79,500.00`,`235000 USD`,`USD $96,300`,`$121k`,`91.300 dollars`,`eighty two thousand USD`|
|vehicle_mileage|yes|Raw vehicle mileage|`9,800 miles`,`1.200 mi`,`Miles: 6,400`,`KM 18,900`,`19,250 mi.`,`fifteen thousand miles`|
|payment_method|yes|Raw Payment Method|`bank_transfer`,`credit`,`Credit card`,`Leasing`,`finance`,`CASH`,`bank wire`|
|city|yes|City|`boston`,`austin`,`san antonio`|
|state|yes|state name or abbreviation|`Texas`,`TX`,`GA`|
|salesperson|yes|Salesperson Name|`kevin`,`AMANDA scott`,`nancy reed`|
|delivery_status|yes|Raw Delivery Status|`delivered`,`DELIVERED`,`in Transit`,`Pending`|


 ### Output of Processed Data Columns

|Column Input|Column Output|Format Column Output|
|------------|-------------|--------------------|
|sale_id|sale_id_processed|`integer`|
|sale_date|sale_date_processed|`YYYY-MM-DD`|
|customer_name|customer_name_processed|`Title Case Customer Name`|
|porsche_model|porsche_model_processed|`Canonical Porsche Model`|
|model_year|model_year_processed|`YYYY`|
|sale_price|sale_price_processed|`Value in USD with two decimal places`|
|vehicle_mileage|vehicle_mileage_processed|`Integer Miles`|
|payment_method|payment_method_processed|`Controlled Label`|
|city|city_processed|`Title Case City`|
|state|state_processed|`USPS  with two letter code`|
|salesperson|salesperson_processed|`Title Case Sales Person`|
|delivery_status|delivery_status_processed|`Controlled Label`|

### Rules for processing and handling column data

#### Dates
Normalize to a `YYYY-MM-DD`.

Examples: 

* `April 31st, 2024` -> `2024-04-31` 
* `September 17, 2024` -> `2024-09-17`
* `22/05/2024` -> `2024-05-22`
* `2025.07.07` -> `2025-07-07`
* `2025-09-31` -> `2025-09-31`

#### Customer Name
Normalize to a Title Case.

Example:

* `SOPHIA Miller` -> `Sophia Miller`

#### Porsche Models
Normalize to a Canonical Porsche Model. 

Example:

* `718 Boxster` -> `718 Boxster`
* `718 Boxster GTS` -> `718 Boxster GTS`
* `718 Cayman` ->  `718 Cayman`
* `718 Cayman GT4 RS` - > `718 Cayman GT4 RS`

#### Model Year
Normalize to a `YYYY`.

Example:

* `20-21` -> `2021`
* `twenty twenty three` -> `2023`
* `20 24` ->`2024`
* `2026` ->`2026`

#### Sales Price
Normalize to a decimal USD amount without symbols.

Examples:

* `$79,500.00` -> `79500.00`
* `235000 USD` -> `235000.00`
* `USD 112.750` -> `112750.00`
* `68.900 dollars` -> `68900.00`
* `$121k`-> `121000.00`
* `95,000 dollars` -> `95000.00`
* `188k USD` -> `188000.00`
* `eighty two thousand USD` -> `82000.00`

#### Vehicle Mileage
Normalize to a integer miles. 

if a value explicity KM, convert the value using `1 km = 0.621371 miles`, rounded to the nearest integer.
if a value explicity `new` ou `new car` convert to 0.

Examples:

* `9,800 miles` -> `9800`
* `1.200 mi` -> `1200`
* `Miles: 6,400` -> `6400`
* `zero miles` -> `0`
* `14.500 miles` -> `14500`
* `KM 18,900` -> `11744`
* `twelve thousand miles` -> `12000`
* `new` -> `0`
* `new car` -> `0`

#### Payment Method
Normalize the controlled label to one of:

- `ACH Payment`
- `Bank Transfer`
- `Wire Transfer`
- `Cash`
- `Credit Card`
- `Crypto`
- `Debit Card`
- `Financing`
- `Leasing`

The result of processing will be one of this values.

#### City
Normalize city names to title case and preserve known punctuation such as `St. Louis`

#### State
Normalize US states to USPS two-letter codes. Convert both names and abbreviations, case-insensitively.

Examples:

* `California` -> `CA`
* `california` -> `CA`
* `ca` -> `CA`
* `New York` -> `NY`

#### Sales Person
Normalize Sales Person to Title Case like `AMANDA scott` to `Amanda Scott`.


#### Delivery Status
Normalize the controlled label to one of:

* `Delivered`
* `In Transit`
* `Pending`
* `Cancelled`
* `Pending Aproval`
* `Shipped`
* `Awaiting Delivery`
* `Awaiting Pickup`
* `Pending  Review`
* `Awaiting Review`

The result of processing will be one of this values.

### Quality Checks

After normalization, verify:

- No original columns were removed.
- Sanitized columns appear immediately after their source columns.
- Dates are ISO format or `INVALID`.
- State values are two-letter USPS codes or `INVALID`.
- Mileage is integer miles.
- Price is numeric with two decimals.
- No new blank values are introduced in sanitized columns; use `INVALID` or normalized defaults instead.

## Invalid handling

Use `INVALID` when a value cannot be processed safely. Never leave a sanitized field blank.
