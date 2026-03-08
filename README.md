# Power BI Sales Dashboard — Awesome Chocolates

![Dashboard Preview](screenshots/dashboard-overview.png)

## Overview

This project demonstrates a basic end-to-end analytics workflow using **MySQL and Power BI**.
A MySQL database (`awesome chocolates`) was connected to Power BI to build a dynamic sales dashboard with calculated measures and parameterized queries.

The dashboard allows users to **dynamically filter the dataset by Product ID (PID)** using a parameter, automatically updating all visuals and metrics.



## Tech Stack

* **Power BI Desktop**
* **MySQL**
* **Power Query (M language)**
* **SQL**



## Dataset

The project uses the **Awesome Chocolates** sample database.

Tables used:

* `sales`
* `people`
* `geo`
* `products`



## Features

### Database Integration

* Connected a **MySQL database** to Power BI.
* Imported sales data into the Power BI data model.


### Data Modeling

Created the following **DAX measures** in the `Sales` table:

* **Total Sales**
* **Total Boxes**
* **Shipment Count**
* **Low Box Shipments**
* **LBS %**

These measures were used across dashboard visualizations.



### Dashboard Visualizations

The Power BI dashboard includes:

* KPI cards for:

  * Total Sales
  * Total Boxes
  * Shipment Count
  * Low Box Shipments
* **Sales Trend** visualization - Line Chart
* **Sales by Geography** visualization - Bar Chart
* **People table** for sales personnel insights - Table



### Dynamic Query Parameterization

A key feature of the dashboard is **dynamic filtering using Power Query parameters**.

Steps implemented:

1. Created a **Power Query parameter** named `Product Code`.
2. Modified the MySQL query using `Value.NativeQuery()` to dynamically filter sales by Product ID (PID).
3. Applied the parameterized query to the dataset.
4. Updating the parameter automatically refreshes the dashboard visuals.

Example Power Query implementation:

```m
let
    Source = MySQL.Database("localhost:3306", "awesome chocolates"),
    Result = Value.NativeQuery(
        Source,
        "select * from sales where PID = @pid",
        [pid = #"Product Code"]
    )
in
    Result
```

Changing the parameter value (e.g., `P04`, `P05`, `P06`) dynamically updates all dashboard visuals.



### Dynamic Dashboard Title

The dashboard title was made dynamic by including the **selected Product ID (PID)**, allowing users to easily identify which product is currently being analyzed.

<br/>

## Example Use Case

A user can change the **Product Code parameter** and instantly view:

* Sales trends for that product
* Shipment statistics
* Geographic distribution of sales
* Performance metrics

This allows quick analysis of individual products without modifying the dataset manually.



## Repository Contents

```
/powerbi
    awesome_chocolates_dashboard.pbix

/screenshots
    dashboard_overview.png

README.md
```



## What I Learned

* Connecting **Power BI to MySQL databases**
* Writing **native SQL queries inside Power Query**
* Creating **dynamic parameters in Power BI**
* Building **interactive dashboards**
* Creating **DAX measures for KPIs**



## Future Improvements

* Add slicers for geography and salesperson
* Implement time-based analysis (YoY / MoM trends)
* Deploy dashboard using **Power BI Service**
* Automate refresh using scheduled refresh



## Author

Data analytics learning project built while exploring **Power BI and SQL integration**.
