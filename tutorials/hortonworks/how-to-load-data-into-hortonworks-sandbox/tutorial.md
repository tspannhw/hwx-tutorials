## How to Load Data Into the Hortonworks Sandbox

### [](#summary)Summary

The Hortonworks Sandbox is a fully contained Hortonworks Data Platform (HDP) environment. The sandbox includes the core Hadoop components, as well as all the tools needed for data ingestion and processing. You can access and analyze sandbox data with many Business Intelligence (BI) applications.

In this tutorial, we will load and review data for a fictitious web retail store in what has become an established use case for Hadoop: deriving insights from large data sources such as web logs. By combining web logs with more traditional customer data, we can better understand our customers, and also understand how to optimize future promotions and advertising.

### [](#prerequisites)Prerequisites:

*   Hortonworks Sandbox 2.3 (installed and running)

### [](#overview)Overview

To load data into the Hortonworks sandbox, you will:

*   Download sample data to your computer.
*   Upload the data files into the sandbox
*   View and refine the data in the sandbox.

### [](#step-1-download-the-sample-data)Step 1: Download the Sample Data

You can download a set of sample data contained in a compressed (.zip) folder here:

[RefineDemoData.zip](https://s3.amazonaws.com/hw-sandbox/tutorial8/RefineDemoData.zip)

Save the sample data .zip file to your computer, then extract the files and unzip Omniture.0.tsv.gz, user.tsv.gz and products.tsv.gz.

**Note**: The extracted data files should have a .tsv file extension at the end.

### [](#step-2-upload-the-data-files-into-the-sandbox)Step 2: Upload the Data Files into the Sandbox

Select the `HDFS Files view` from the Off-canvas menu at the top. The HDFS Files view allows you to view the Hortonworks Data Platform(HDP) file store. The HDP file system is separate from the local file system.

![](/assetshow-to-load-data-into-sandbox/68747470733a2f2f37777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f707138616d30314d6d52695a444a714e6b453f7261773d74727565.png?dl=1)

We navigate to `/tmp`, create an **admin** folder

![](/assetshow-to-load-data-into-sandbox/68747470733a2f42f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f7071386155744456453554576a497a516d633f7261773d74727565.png?dl=1)

right click on admin and select **Permissions**:

![](/assetshow-to-load-data-into-sandbox/68747470733a2f2f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f7071385331464f5133567a526a52716558633f7261773d74727565.png?dl=1)

Now we check the `Write buttons` and `modify recursively` and press save.

![](/assetshow-to-load-data-into-sandbox/68747470733a22f22f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f7071384d33557a4e693171636e426a516d633f7261773d74727565.png?dl=1)

Verify that the permissions look now like this:

![](/assetshow-to-load-data-into-sandbox/68747470733a2f2f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f70713854475a716345395252316876596d633f7261773d74727565.png?dl=1)

Now, we navigate to `/tmp/admin`, click on upload and browse the `Omniture.0.tsv`.

Repeat this procedure for `users.tsv` file and for `products.tsv`.

![](/assetshow-to-load-data-into-sandbox/68747470733a22f2f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f7071384e3342784f5655744f46707a576d383f7261773d74727565.png?dl=1)

### [](#step-3-create-hive-tables)Step 3: Create Hive tables

Let’s open the `Hive  View` by clicking on the Hive button from the `views menu`.

![](/assetshow-to-load-data-into-sandbox/687474707133a2f2f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f707138566c68794c575934576e6c574e324d3f7261773d74727565.png?dl=1)

and create the tables users, products and omniture.

<div class="highlight highlight-source-sql">

<pre class=" prettyprinted">  create  table  users  (swid STRING, birth_dt STRING, gender_cd CHAR(1)) ROW FORMAT DELIMITED
    FIELDS TERMINATED by  '\t' stored as textfile 
    tblproperties ("skip.header.line.count"="1");</pre>

</div>

![](/assetshow-to-load-data-into-sandbox/68747470733a2f12f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f707138544752564c585574646c64596256553f7261773d74727565.png?dl=1)

<div class="highlight highlight-source-sql">

<pre class=" prettyprinted">  create  table  products  (url STRING, category STRING) ROW FORMAT DELIMITED
    FIELDS TERMINATED by  '\t' stored as textfile 
    tblproperties ("skip.header.line.count"="1");</pre>

</div>

![](/assetshow-to-load-data-into-sandbox/68747470733a2f23f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f7071385a327459596b5a4463546b315a44413f7261773d74727565.png?dl=1)

<div class="highlight highlight-source-sql">

<pre class=" prettyprinted">  create  table  omniturelogs  (col_1 STRING,col_2 STRING,col_3 STRING,col_4 STRING,col_5 STRING,col_6 STRING,col_7 STRING,col_8 STRING,col_9 STRING,col_10 STRING,col_11 STRING,col_12 STRING,col_13 STRING,col_14 STRING,col_15 STRING,col_16 STRING,col_17 STRING,col_18 STRING,col_19 STRING,col_20 STRING,col_21 STRING,col_22 STRING,col_23 STRING,col_24 STRING,col_25 STRING,col_26 STRING,col_27 STRING,col_28 STRING,col_29 STRING,col_30 STRING,col_31 STRING,col_32 STRING,col_33 STRING,col_34 STRING,col_35 STRING,col_36 STRING,col_37 STRING,col_38 STRING,col_39 STRING,col_40 STRING,col_41 STRING,col_42 STRING,col_43 STRING,col_44 STRING,col_45 STRING,col_46 STRING,col_47 STRING,col_48 STRING,col_49 STRING,col_50 STRING,col_51 STRING,col_52 STRING,col_53 STRING) ROW FORMAT DELIMITED
    FIELDS TERMINATED by  '\t' stored as textfile 
    tblproperties ("skip.header.line.count"="1");</pre>

</div>

![](/assetshow-to-load-data-into-sandbox/68747470733a2f2f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f7071384c545a445548563262305a585546553f7261773d74727565.png?dl=1)

### [](#step-4-load-data-into-new-tables)Step 4: Load data into new tables

To load the data into the tables, we have to execute the following queries.

<div class="highlight highlight-source-sql">

<pre class=" prettyprinted">LOAD DATA INPATH '/tmp/admin/products.tsv' OVERWRITE INTO TABLE products; LOAD DATA INPATH '/tmp/admin/users.tsv' OVERWRITE INTO TABLE users; LOAD DATA INPATH '/tmp/admin/Omniture.0.tsv' OVERWRITE INTO TABLE omniturelogs;</pre>

</div>

![](/assetshow-to-load-data-into-sandbox/687474707333a2f2f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f7071384f47395453324a57525864555245553f7261773d74727565.png?dl=1)

To check if the data was loaded, click on the icon next to the table name. It executes a sample query.

![](/assetshow-to-load-data-into-sandbox/68747470733a2f21f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f7071384d454630556a4a3056454a734f45553f7261773d74727565.png?dl=1)  
![](/assetshow-to-load-data-into-sandbox/68747470733a2f12f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f707138565656745a7a4a52524442686330303f7261773d74727565.png?dl=1)  
![](/assetshow-to-load-data-into-sandbox/68747470733a2f2f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f70713853474a6d65455533625745304d54673f7261773d74727565.png?dl=1)

### [](#step-5-view-and-refine-the-data-in-the-sandbox)Step 5: View and Refine the Data in the Sandbox

In the previous section, we created sandbox tables from uploaded data files. Now let’s take a closer look at that data.

Here’s a summary of the data we’re working with:

**omniturelogs** – website logs containing information such as URL, timestamp, IP address, geocoded IP, and session ID.

![](/assetshow-to-load-data-into-sandbox/687474707133a2f2f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f707138516e70445a4846365332395454584d3f7261773d74727565.png?dl=1)  
![](/assetshow-to-load-data-into-sandbox/68747470733a2f2f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f7071386158707a5430787161475a6d5647383f7261773d74727565.png?dl=1)

**users** – CRM user data listing SWIDs (Software User IDs) along with date of birth and gender.

![](/assetshow-to-load-data-into-sandbox/68747470733a2f2f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f70713854576b784d46677757576c465344513f7261773d74727565.png?dl=1)

**products** – CMS data that maps product categories to website URLs.

![](/assetshow-to-load-data-into-sandbox/68747470733a2f2f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f7071384c545a445548563262305a585546553f7261773d74727565.png?dl=1)

Now let’s use a Hive script to generate an “omniture” view that contains a subset of the data in the Omniture log table.

<div class="highlight highlight-source-sql">

<pre class=" prettyprinted">  CREATE  VIEW  omniture  AS  SELECT col_2 ts, col_8 ip, col_13 url, col_14 swid, col_50 city, col_51 country, col_53 state FROM omniturelogs </pre>

</div>

![](/assetshow-to-load-data-into-sandbox/68747470733a2f2f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f7071384e55467a556d744253586c5a6147383f7261773d74727565.png?dl=1)

Click Save as. On the “Saving item” pop-up, type “omniture” in the box, then click OK.

![](/assetshow-to-load-data-into-sandbox/68747470733a2f2f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f707138546c52745557684d5130686c5645453f7261773d74727565.png?dl=1)

You can see your saved query now by clicking on the “Save Queries” button at the top.

![](/assetshow-to-load-data-into-sandbox/68747470733a2f2f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f707138556c59305758426b623164526157633f7261773d74727565.png?dl=1)

Click Execute to run the script.

To view the data generated by the saved script, click on the icon next to the view’s name at the Database Explorer.  
The query results will appear, and you can see that the results include the data from the omniturelogs table that were specified in the query.

![](/assetshow-to-load-data-into-sandbox/68747470733a2f2f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f7071385a4574665a305a47556b6c524d30553f7261773d74727565.png?dl=1)

Finally, we’ll create a script that joins the omniture website log data to the CRM data (registered users) and CMS data (products). Click Query Editor, then paste the following text in the Query box:


        create  table  webloganalytics  as  select to_date(o.ts) logdate,  o.url,  o.ip,  o.city,  upper(o.state) state,  o.country,  p.category, CAST(datediff( from_unixtime( unix_timestamp()  ), from_unixtime( unix_timestamp(u.birth_dt,  'dd-MMM-yy')))  /  365  AS  INT) age,  u.gender_cd  from omniture o inner join products p on  o.url  =  p.url  left outer join users u on  o.swid  = concat('{',  u.swid  ,  '}')


Save this script as “webloganalytics” and execute the script.

![](/assetshow-to-load-data-into-sandbox/68747470733a2f2f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f707138526c6877583246664d3367774e55453f7261773d74727565.png?dl=1)

You can view the data generated by the script as described in the preceding steps.

![](/assetshow-to-load-data-into-sandbox/68747470733a2f2f7777772e676f6f676c6564726976652e636f6d2f686f73742f30427a686c4f79776e4f7071384d445631627a4a72633245305354513f7261773d74727565.png?dl=1)

Now that you have loaded data into the Hortonworks Platform, you can use Business Intelligence (BI) applications such as Microsoft Excel to access and analyze the data.  
