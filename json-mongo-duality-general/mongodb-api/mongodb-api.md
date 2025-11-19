# MongoDB Plug-and-Play - Full MongoDB compatibility to work with JSON Collections and Duality Views

## Introduction

JSON collections - JSON Collection Tables and JSON Collection Views like Duality Views - store JSON documents alongside some metadata , making them fully MongoDB compatible out-of-the box. Through the MongoDB API, part of Oracle REST Data Services (ORDS), you can use any MongoDB tool, utility, or SDK to work with these collections.

This lab walks you through the steps to install MongoDB Shell and Command Line Database Tools to interaction with our JSON collection through the MongoDB API. 

Estimated Time: 15 minutes

### Objectives

In this lab, you will:

* Install MongoDB Shell and MongoDB Command Line Database Tools on your local machine
* Alternatively, you can install MongoDB Compass (GUI)
* Set up your PATH to point to the MongoDB Shell and MongoDB Command Line Database Tools executable
* Load more data through the Database API for MongoDB
* Use MongoDB Shell to interact with Oracle AI Database

### Prerequisites

- An Oracle Autonomous AI Database or any Oracle AI Database. Note that if you don't use Oracle Autonomous AI Database, you have to manually install and configure Oracle Rest Data Services (ORDS) to use the MongoDB API used in this lab.
- You have successfully completed Lab 2, JSON Collections, and Lab 3, Duality Views. We will rely on the JSON Collections and Duality Views that were created in these labs in this module.

## Task 1: Install MongoDB Shell and MongoDB Command Line Database Tools

This section walks you through the installation of the MongoDB Shell and MongoDB Command Line Database Tools on your own machine. Instructions are provided for Mac OS X and Windows machines. Installation on a Linux machine will be similar to the Mac instructions, but obviously will require a different download file.

**NOTE**: MongoDB Shell and MongoDB Command Line Database Tools are tools provided by MongoDB Inc. Oracle is not associated with MongoDB Inc, and has no control over the software. These instructions are provided simply to help you learn about MongoDB Shell and MongoDB Command Line Database Tools. Links may change without notice.

Check the official MongoDB download website for latest versions and instructions, e.g.:

https://www.mongodb.com/try/download/shell

https://www.mongodb.com/try/download/database-tools

https://www.mongodb.com/try/download/compass

### Objectives

In this section, you will:

* Install MongoDB Shell and MongoDB Command Line Database Tools on your local machine
* Optionally, you can install MongoDB Compass (GUI)
* Set up your PATH to point to the MongoDB Shell and MongoDB Command Line Database Tools executable

### Prerequisites

- A Mac OS X machine (Intel or Apple hardware) or a Windows PC.
- Access to the command prompt / terminal

### 1: (Mac only) Determine the type of hardware

1. If you know already whether your Mac uses Intel or Apple Silicon you can skip this step. Otherwise:

    Click on the Apple menu in the top left-hand corner of your screen and go to "About this Mac". 

    !["about this mac" menu item](./images/about-this-mac.png " ")

    That will open a "details" panel. Intel Mac will show a line with *Processor:* and the name of an Intel processor. Apple Silicon Macs will show a line saying *Chip* and a line such as "Apple M1 Pro".

    ![processor details](./images/about-mac-details.png " ")

### 2: Open a command prompt or terminal window

1. On a Mac:

    Open the Launchpad icon in the Dock (or press Command-space) and start typing "terminal" in the search box. Press enter to start terminal.

    ![open terminal in launchpad](./images/terminal.png " ")

2.  On a Windows PC:

    Press "Run" (Windows-R) and type "cmd.exe". Press enter or click "OK".

    ![open command prompt](./images/cmd-exe.png " ")

3.  Create and enter a suitable directory. We'll create a directory 'mongosh' under the default home directory, but you can choose to create it elsewhere. For **Mac or Windows**, enter the following commands:

    ```
    <copy>
    mkdir mongosh
    cd mongosh
    </copy>
    ```

### 3: Download and expand the installer files

On both Mac and Windows, you can use the built-in 'curl' command to access a URL and download a file from it. The URL to use will vary according to the machine involved.

**Note: If you encounter any issues with the download or the version listed here, then please visit https://www.mongodb.com/try/download/shell or https://www.mongodb.com/try/download/database-tools to download the most recent shell for your operating system. All subssequent instructions continue to be the same.**

Copy **ONE** of the following *curl* commands and paste it to the command or terminal window:

1. For **Mac with Intel processor**:

    Download MongoDB Shell:

    ```bash
    <copy>
    curl https://downloads.mongodb.com/compass/mongosh-2.5.9-darwin-x64.zip -o mongosh.zip
    </copy>
    ```

    Download Command Line Database Tools:

    ```bash
    <copy>
    curl https://fastdl.mongodb.org/tools/db/mongodb-database-tools-macos-x86_64-100.13.0.zip -o mongodbtools.zip
    </copy>
    ```

2. For **Mac with Apple chip**:

    Download MongoDB Shell:

    ```bash
    <copy>
    curl https://downloads.mongodb.com/compass/mongosh-2.5.9-darwin-arm64.zip -o mongosh.zip
    </copy>
    ```

    Download Command Line Database Tools:

    ```bash
    <copy>
    curl https://fastdl.mongodb.org/tools/db/mongodb-database-tools-macos-arm64-100.13.0.zip -o mongodbtools.zip
    </copy>
    ```

3. For **Windows**:

    Download MongoDB Shell:

    ```bash
    <copy>
    curl https://downloads.mongodb.com/compass/mongosh-2.5.9-win32-x64.zip -o mongosh.zip
    </copy>
    ```

    Download Command Line Database Tools:

    ```bash
    <copy>
    curl https://fastdl.mongodb.org/tools/db/mongodb-database-tools-windows-x86_64-100.13.0.zip -o mongodbtools.zip
    </copy>
    ```

4. The previous step will have downloaded a zip file called mongosh.zip and mongodbtools.zip, which we need to expand.

    On **Mac or Windows**, run the following command:

    ```bash
    <copy>
    mkdir -p mongosh | tar -xvf mongosh.zip -C mongosh --strip-components=1
    </copy>
    ```

    ```bash
    <copy>
    mkdir -p mongodbtools | tar -xvf mongodbtools.zip -C mongodbtools --strip-components=1
    </copy>
    ```

    **Notes**: tar is a built-in command in Windows 11 and recent Windows 10 builds. If for any reason it is not available, you will need to expand the zip file using Windows Explorer. On Mac, you could use the command 'unzip mongosh.zip' to the same effect.

### 4: Set the PATH to include the mongosh executable

1. On **Mac** (Intel or Apple silicon) run the following command to set your path variable to include the location of the **mongosh** and **mongoimport** executable.

    ```bash
    <copy>
    export PATH=[path to]/mongosh/bin:[path to]/mongodbtools/bin:$PATH
    </copy>
    ```

    If that fails, you'll have to set your path manually to include the 'bin' directories from the zip files you just downloaded. If you close and reopen your terminal window, you will need to re-run this command. Alternatively, you can always navigate to the directory where you have extracted the software and run the shell with the relative path.

2. On **Windows** you can use the following command, assuming you created the 'mongosh' directory in your home directory. If you created it elsewhere, you'll need to edit the path command appropriately.

    ```
    <copy>
    set path=[path to]\mongosh\bin\:[path to]\mongodbtools\bin\:%PATH%
    </copy>
    ```

3. Keep the command or terminal window open for later use. If you close it and need to reopen it, you will need to set the PATH again according to the instructions above.

MongoDB Shell is now set up on your PC or Mac.

### 5: Alternatively, you can install MongoDB Compass, the GUI for MongoDB

1. Identify the appropriate MongoDB Compass download for your local machine on https://www.mongodb.com/docs/compass/install/?operating-system=linux&package-type=.deb#std-label-download-install, download and install it. MongoDB Compass offers you both a graphical user interface, as well as a built-in MongoDB shell.

This step is optional, so it is not described in more detail here, although the installation itself is intuitive and self-describing.

## Task 2: Use MongoDB API to interact with Oracle AI Database

With our JSON Collection and Duality Views created in the Oracle AI Database, we can use MongoDB APIs to interact with these collections as if we were interacting with a MongoDB Database. In this section, we will use native MongoDB tools and connect to the Oracle AI Database with a MongoDB connection string -- which was configured as a part of the Oracle REST Data Service (ORDS) configuration. From there, we can interact with MongoDB tools or SQL Developer Web interchangeably to access our data.

### Objectives

In this section, you will:

* Explore all MongoDB compatible JSON Collections - JSON Collection Tables and Duality Views - in your database
* Load data into both JSON Collections and Duality Views using MongoDB tools and utilities
* Use MongoDB Shell to interact with your JSON Collections and experience DML operations and what it means for JSON Collections and Duality Views

### Explore your JSON Collections

1. Add a JSON Collection View

    Oracle allows you to define read-only JSON Collection Views. JSON Collection Views can become arbitrarily complex, and the only requirement is to have a single-column SELECT list, returning a JSON Object. The common use case is to expose some relational reference data to the MongoDB tool that is a shared enterprise-wide. 
    
    We can quickly create such a JSON Collection View on a V$ View using **SQL worksheet in Database Actions or your preferred SQL client tool**:

    ```
    <copy>
    create or replace json collection view myversion as
    select json {*} from v$version;

    select json_serialize(data pretty) from myversion;
    </copy>
    ```
    ![JSON Collection View](./images/json-collection-view.png " ")

    **Note**: It is not necessary to have an '_id' field in a JSON Collection View, although it is normally recommended to define such a field. JSON Collection Views are read only.In our simple example with a collection with one document we omit this column.


2. JSON Collections, both tables and views, are automatically compatible with any MongoDB tool, utility, and SDK. You can identify such objects in the database with the **\*\_JSON_COLLECTIONS** family of views. 

    ```
    <copy>
    select * from user_json_collections;
    </copy>
    ```
    ![JSON Collections](./images/json-collections.png " ")

    You'll see that we have our JSON Collection Table movies, three Duality Views, and our newly created (read-only) JSON Collection View. All of these collections can be queried and modified using MongoDB tools.

    Let us look at those with MongoDB tools now.

### Interact with native JSON Collections in the Oracle AI Database using MongoDB API


1. First, you must set the URI to the MongoDB API running in ORDS on your machine. 

    **Your Autonomous AI Database should be configured with an enabled MongoDB API, ready for you to go. If you don't see the MongoDB API enabled in your environment, then let's enable it quickly.** 
    
    You need to do two things:

    1. Enable Access Control Lists (ACLs)

        Due to security precautions, the MongoDB API is not enabled to the public out of the box, but requires some conscious control access. To enable ACLs, go to the details page of your Autonomous AI Database and select to edit the access control lists.

        ![Set ACL](./images/set-acl.png " ")

        Choose an ACL that enables the machine where you have installed the MongoDB tools to access the database. For demonstration purposes, the most pragmatic way to do this is to set the CIDR block to 0.0.0.0/0 which allows full access from the Internet. **This is for demonstration purposes only and never meant for production environment or systems with sensitive data.**

        ![Set CIDR block](./images/set-cidr-block.png " ")

        Save your changes and go back to the detail page of your Autonomous AI Database.        

    2. If the MongoDB API is successfully enabled, it will show you the URI to copy.

    ![Copy MongoDB URI](./images/newmonogoapi.png " ")

    The MongoDB API URI looks like this:

    ```bash
    <copy>
    mongodb://[user:password@][ADB Instance name].adb.[region].oraclecloudapps.com:27017/[user]?authMechanism=PLAIN&authSource=$external&ssl=true&retryWrites=false&loadBalanced=true
    </copy>
    ```


    Let's create an environment variable called *URI* which contains the MongoDB URI including the user and password information.

    On Mac or Linux, issue the following command in your shell to set the environment variable. If you close the shell, you need to set this variable again.

    ```bash
    $ <copy>
    export URI='[user:password@][ADB Instance name].adb.[region].oraclecloudapps.com:27017/[user]?authMechanism=PLAIN&authSource=$external&ssl=true&retryWrites=false&loadBalanced=true'
    </copy>
    ```

    Example:

    ```
    export URI='mongodb://admin:*redacted*@ATP3834*redacted*.adb.us-ashburn-1.oraclecloudapps.com:27017/admin?authMechanism=PLAIN&authSource=$external&tls=true&retryWrites=false&loadBalanced=true'
    ```

    On Windows systems, issue the following command in your shell to set the environment variable. If you close the shell, you need to set this variable again.

    ```bash
    $ <copy>
    set URI="[user:password@][ADB Instance name].adb.[region].oraclecloudapps.com:27017/[user]?authMechanism=PLAIN&authSource=$external&ssl=true&retryWrites=false&loadBalanced=true"
    </copy>
    ```

    > **_NOTE:_** Please make sure you replace both the user and password. Also, keep in mind that the **[user]** tag needs to be updated in two places.

    <if type="sandbox">

    In your LiveLabs Sandbox environment, the user is `admin`. You can find the password for the user on the **View Login Info** 

    ![ADB Admin password in the LiveLabs Sandbox](./images/adb-admin-password.png " ")


    </if>


   You might need to escape some characters as well.



    | Special Character |   !   |   #   |   $   |   %   |   &   |   '   |   (   |   )   |   *   |   +   |
    | ----------------- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
    | Replace with      |  %21  |  %23  |  %24  |  %25  |  %26  |  %27  |  %28  |  %29  |  %2A  |  %2B  |
    {: title="Special characters and their replacements 1"}

    | Special Character |   ,   |   /   |   :   |   ;   |   =   |   ?   |   @   |   [   |   ]   |
    | ----------------- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
    | Replace with      |  %2C  |  %2F  |  %3A  |  %3B  |  %3D  |  %3F  |  %40  |  %5B  |  %5D  |
    {: title="Special characters and their replacements 2"}

     Please check [this link](https://docs.oracle.com/en/cloud/paas/autonomous-database/serverless/adbsb/mongo-using-oracle-database-api-mongodb.html#GUID-44088366-81BF-4090-A5CF-09E56BB2ACAB) to learn more about Using MongoDB API in the Oracle AI Database.


2. Let's use the first MongoDB utility - mongoimport - to populate our database with data exported from a MongoDB in ndjson (newline delimited JSON) format. You will use a document from Object Storage to seed the data in your **movie** collection.

    On Linux and Mac systems, issue the following command in your shell to use mongoimport and your URI the environment variable. If you closed the shell, you need to set the URI variable again or specify the connect string directly in the command.

    ```
    $ <copy>curl -s https://objectstorage.us-ashburn-1.oraclecloud.com/n/c4u04/b/moviestream_gold/o/movie/movies.json | mongoimport --collection movies --drop --uri $URI
    </copy>
    ```

    On Windows systems, issue the following command in your shell to use mongoimport and your URI the environment variable. If you closed the shell, you need to set the URI variable again or specify the connect string directly in the command.

    ```
    $ <copy>curl -s https://objectstorage.us-ashburn-1.oraclecloud.com/n/c4u04/b/moviestream_gold/o/movie/movies.json | mongoimport --collection movies --drop --uri %URI%
    </copy>
    ```
    ![Populate the database](./images/populate-mongo-db.png " ")

3. Now with the URI set, we can connect to MongoDB Shell. Run the command below to connect.

    On Mac and Linux systems:

    ```
    $ <copy>mongosh $URI</copy>
    ```
    
    On Windows systems:

    ```
    $ <copy>mongosh %URI%</copy>
    ```
    ![Connect to the Mongo Shell](./images/mongo-shell.png " ")

4. Within the MongoDB Shell, you can begin running commands to interact with the data in your database as if you were using a Mongo Database. Let us first examine the JSON collections we have:

    ```
    admin> <copy>show collections</copy>
    </copy>
    ```
    ![Available JSON collections](./images/mongo-collections.png " ")

    If you ran Lab 2 and Lab 3 as suggested, you will see the same JSON Collections we had seen in the database earlier in this section.


5. To show the **movie** collection we created and the count of documents we imported, run the following commands.

    ```
    admin> <copy>db.movies.countDocuments()
    </copy>
    ```
    ![Query result for count](./images/mongo-count.png " ")

6. You can also query for specific documents. Run this query to find the document with title "Zootopia."

    ```
    admin> <copy>db.movies.find( {"title": "Zootopia"} )
    </copy>
    ```
    ![Query result for Zootopia](./images/mongo-zootopia.png " ")

7. Now query for all movies made after 2020.

    ```
    admin> <copy>db.movies.find ( { "year": {"$gt": 2020} } )
    </copy>
    ```
    ![Query result for after 2020](./images/mongo-2020.png " ")

    There's only one movie in our library that was released after 2020.

8. You can do the same for your JSON Collection Views, both the read-only View and our Duality Views

    ```
    admin> <copy>db.MYVERSION.findOne()
    </copy>
    ```
    ![JSON Collection View](./images/mongo-myversion.png " ")

    ```
    admin> <copy>db.SCHEDULEV.findOne()
    </copy>
    ```
    ![JSON Collection View](./images/mongo-schedulev.png " ")

9. If you happen to have installed Mongo Compass, this is how the Duality View would look like in MongoDB's GUI:

    ![JSON Duality View in Compass](./images/mongo-compass.png " ")

    We have briefly glanced at all our JSON Collections using mongosh. Let's now actually work with the data.


## Task 3: Interact interchangeably with MongoDB API and SQL Developer Web

Let's take some time to demonstrate the interactivity between the Oracle and MongoDB tools we have installed on our machine to see the different APIs working against the same data set.

1. Use the MongoDB Shell to insert 2 documents to our movie collection.

    ```
    admin> <copy>db.movies.insertMany( [{
    "title": "Love Everywhere",
    "summary": "Plucky Brit falls in love with American actress",
    "year": 2023,
    "genre": "Romance"
    }
    ,
    {
    "title": "SuperAction Mars",
    "summary": "A modern day action thriller",
    "year": 2023,
    "genre": [
        "Action",
        "Sci-Fi"
    ],
    "cast": [
        "Arnold Schwarzenegger",
        "Tom Cruise"
    ]
    } ])
    </copy>
    ```
    ![Mongo inserts two docs](./images/mongo-insert.png " ")

2. Now check for movies again that were released after 2020 and you will see these two movies popping up as well:

    ```
    admin> <copy>db.movies.find ( { "year": {"$gt": 2020} } )
    </copy>
    ```
    ![New result for after 2020](./images/mongo-2020-new.png " ")

3. Oops. We made a mistake with SuperAction Mars, it has the wrong year. Let's quickly update what we just entered. 

    In mongosh, look at the movie again. This also helps us to ensure that we can use the filter to update exactly one document.

    ```
    <copy>db.movies.find({ "title": "SuperAction Mars" })
    </copy>
    ```

    ![Find SuperAction Mars in Mongo](./images/mongo-find-superaction-mars.png " ")

    Ok, we are ready to update the single movie. (In real applications you would probably use "_id", the unique identifier of the document)

    ```
    <copy>db.movies.updateOne({ "title": "SuperAction Mars" },{$set: {"year": 2025}})
    </copy>
    ```
    Done. You can see that we had one matched document that we updated.

    ![Update SuperAction Mars in Mongo](./images/mongo-update-superaction-mars.png " ")


4. Let's go back to the JSON IDE in Database Actions and see that we really updated the document in the Oracle AI Database. When you have selected the collection **movies**, which is most likely the only one you are having, use the following filter to look at SuperAction Mars 

    ```
    <copy>{ "title": "SuperAction Mars" }
    </copy>
    ```

    Indeed, the record was properly updated.

	![New result for after 2020 edit](./images/json-ide-find-superaction-mars-after-update.png)

5. We are now updating a shared nested JSON Object in our JSON Duality View. Unlike JSON Collections where data is duplicated in any document that shares the same content, we update the content of our Duality View in ONE place, and all JSON Collections (Duality Views) that share the JSON Object will be magically and automatically updated, too.

    Look at the speaker collection. 

    ```
    <copy>db.SPEAKERV.find()
    </copy>
    ```
	![Speakers](./images/speakers.png)

    There is a speaker named *Beda*, who will be replaced with *Julian*. Unfortunately Beda is busy and is currently not available as speaker.
    ```
    <copy>db.SPEAKERV.updateOne({_id:1}, {$set: {name: "Julian"}})
    db.SPEAKERV.find({ _id: 1})
    </copy>
    ```
	![Speakers](./images/update-speaker.png)

    With the groundbreaking architecture of JSON Duality Views and the denormalized storage of shared data, we not only updated the **SPEAKERV** collection, but also automatically updated the schedule of all attendess, represented through collection **SCHEDULEV**.

    ```
    <copy>db.SCHEDULEV.find()
    </copy>
    ```
	![Schedules](./images/schedules.png)

## Task 4: Supporting Flexible JSON APIs: MongoDB API aggregate function

In Task 2, you loaded a denormalized JSON collection, **movies** to your Oracle Database. In Lab 3, you leveraged JSON Duality Views to expose your data as normalized relational structures while still supporting flexible JSON APIs. This means you can benefit from data consistency and referential integrity — core "normalized" database benefits — without losing the hierarchically modeling capability of JSON. Oracle Database introduced native support for the MongoDB API aggregate function in Oracle Database 26ai. Let's quickly show this capability on the **movies** database.

1. Use the MongoDB Shell aggregate function. This will return the rank list of actors/actresses with the highest box office gross of movies that have received at least one award.

    ```bash
    <copy>db.movies.aggregate([
    // First Stage
    { $match: {
       awards: { $exists: true, $ne: [] },
       gross: { $ne: null }
    }},
    { $project: {
      _id: 0,
      gross: 1,
      awards: 1,
      cast: 1
}},
// Second Stage
{ $unwind: "$cast" },
// Third Stage
{ $group: {
  _id: "$cast",
  averageGross: { $avg: "$gross" }
}},
// Fourth Stage
{ $sort: { averageGross: -1 } }
]);
    </copy>
    ```
    ![Terminal aggregate command](./images/terminal-mongosh-aggregate.png)

2. View the results, type `it` for more documents
![Terminal aggregate command](./images/terminal-aggregate-results.png)

## Task 5: Normalize the movies database

Let's work our way from a JSON collection back to a normalized database to realize the efficiencies of relational tables.  A normalized database enhances data integrity and minimizes redundancy by organizing data into related tables, whereas a JSON non-relational collection offers schema flexibility and scalability, making it suitable for handling unstructured or semi-structured data. With Oracle 26ai, you get the best of both worlds. Let's normalize parts of the **movies** database by focusing on the movie, crew, and awards.

![Normalized Tables of movies db](./images/normalized-tables.png)

Start in your database actions SQL view you were previously working in, if you're not there, take the following step:

![Get back to sql](./images/go-to-sql-dev-db.png)

1. Create the **MOVIE** table and populate it. In a new **worksheet** run the following as a `SQL Script` (F5):
    ```
    <copy>
    CREATE TABLE movie (
    movie_id NUMBER PRIMARY KEY,
    title VARCHAR2(255) NOT NULL,
    year NUMBER,
    sku VARCHAR2(50),
    list_price NUMBER(10,2),
    runtime VARCHAR2(20),
    gross NUMBER,
    budget NUMBER,
    opening_date DATE,
    summary CLOB,
    image_url VARCHAR2(400),
    main_subject VARCHAR2(100),
    wiki_article VARCHAR2(200),
    views NUMBER
    -- Add other columns as desired
    );
    </copy>
    ```
    ```
    <copy>
    MERGE INTO award a
    USING (
    SELECT DISTINCT
    UPPER(TRIM(val)) AS award_name_norm,
    TRIM(val) AS award_name
    FROM (
    -- Awards array
    SELECT jt_aw.val
    FROM movies m
    CROSS APPLY JSON_TABLE(
    m.data FORMAT JSON, '$.awards[*]' COLUMNS(val VARCHAR2(4000) PATH '$')) jt_aw

    UNION ALL

    SELECT jt_nm.val FROM movies m CROSS APPLY JSON_TABLE( m.data FORMAT JSON, '$.nominations[*]' COLUMNS ( val VARCHAR2(4000) PATH '$' ) ) jt_nm
    )
    WHERE val IS NOT NULL
    ) s
    ON (a.award_name_norm = s.award_name_norm)
    WHEN NOT MATCHED THEN INSERT (award_name) VALUES (s.award_name);
    </copy>
    ```
2. Create the **CREW** table and populate it. In a new **worksheet** run the following as a `SQL Script` (F5):
    ```
    <copy>
    CREATE TABLE crew (
    crew_id NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    name VARCHAR2(200) NOT NULL
    );
    </copy>
    ```
    ```
    <copy>
    INSERT INTO crew (name)
    SELECT DISTINCT jt.member_name
    FROM movies mj
    CROSS APPLY JSON_TABLE(
    mj.data FORMAT JSON,
    '$.crew[*]'
    COLUMNS (
        job VARCHAR2(100) PATH '$.job',
        NESTED PATH '$.names[*]'
        COLUMNS (
            member_name VARCHAR2(200) PATH '$'
        )
    )
    ) jt
    WHERE jt.member_name IS NOT NULL
    AND NOT EXISTS (
        SELECT 1 FROM crew WHERE name = jt.member_name
    );
    </copy>
    ```
3. Create the **AWARD** table and populate it. In a new **worksheet** run the following as a `SQL Script` (F5):
    ```
    <copy>
    CREATE TABLE award (
     award_id NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
     award_name VARCHAR2(400) NOT NULL,
     award_name_norm VARCHAR2(400) GENERATED ALWAYS AS (UPPER(TRIM(award_name))) VIRTUAL,
     CONSTRAINT uq_award_name UNIQUE (award_name_norm)
    );
    </copy>
    ```
    ```
    <copy>
    MERGE INTO award a
    USING (
    SELECT DISTINCT
    UPPER(TRIM(val)) AS award_name_norm,
    TRIM(val) AS award_name
    FROM (
    -- Awards array
    SELECT jt_aw.val
    FROM movies m
    CROSS APPLY JSON_TABLE(
    m.data FORMAT JSON, '$.awards[*]' COLUMNS(val VARCHAR2(4000) PATH '$')) jt_aw

    UNION ALL

    SELECT jt_nm.val FROM movies m CROSS APPLY JSON_TABLE( m.data FORMAT JSON, '$.nominations[*]' COLUMNS ( val VARCHAR2(4000) PATH '$' ) ) jt_nm )
    WHERE val IS NOT NULL ) s
    ON (a.award_name_norm = s.award_name_norm)
    WHEN NOT MATCHED THEN INSERT (award_name) VALUES (s.award_name);
    </copy>
    ```
4. Create a junction table, the **MOVIE\_CREW\_LINK** table and populate it. In a new **worksheet** run the following as a `SQL Script` (F5):
    ```
    <copy>
    CREATE TABLE movie_crew_link (
    movie_crew_id NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    movie_id NUMBER REFERENCES movie(movie_id),
    crew_id NUMBER REFERENCES crew(crew_id),
    job VARCHAR2(100) NOT NULL,
    -- Unique so same crew/job/movie not duplicated
    UNIQUE (movie_id, crew_id, job)
    );
    </copy>
    ```
    ```
    <copy>
    INSERT INTO movie_crew_link (movie_id, crew_id, job)
    SELECT DISTINCT
    m2.movie_id,
    c.crew_id,
    jt.job
    FROM movies mj
    CROSS APPLY JSON_TABLE(
    mj.data FORMAT JSON,
    '$'
    COLUMNS ( movie_id NUMBER PATH '$.movie_id' )
    ) m2
    CROSS APPLY JSON_TABLE(
    mj.data FORMAT JSON,
    '$.crew[*]'
    COLUMNS (
        job VARCHAR2(100) PATH '$.job',
        NESTED PATH '$.names[*]'
        COLUMNS (
            member_name VARCHAR2(200) PATH '$'
        )
    )
    ) jt
    JOIN crew c ON c.name = jt.member_name
    WHERE jt.member_name IS NOT NULL
    AND NOT EXISTS (
    SELECT 1 FROM movie_crew_link mc
    WHERE mc.movie_id = m2.movie_id
        AND mc.crew_id = c.crew_id
        AND mc.job = jt.job
    );
    </copy>
    ```
5. Create a junction table, the **MOVIE_AWARD** table and populate it. In a new **worksheet** run the following as a `SQL Script` (F5):
    ```
    <copy>
    CREATE TABLE movie_award (
    movie_award_id NUMBER GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    movie_id NUMBER REFERENCES movie(movie_id),
    award_id NUMBER REFERENCES award(award_id),
    result VARCHAR2(10) CHECK (result IN ('nominated','won')),
    UNIQUE (movie_id, award_id, result)
    );
    </copy>
    ```
    ```
    <copy>
    INSERT INTO movie_award (movie_id, award_id, result)
SELECT DISTINCT
    m.movie_id,
    a.award_id,
    'nominated' AS result
FROM
    movies mj
    CROSS APPLY JSON_TABLE(
        mj.data FORMAT JSON,
        '$'
        COLUMNS (
            movie_id NUMBER PATH '$.movie_id'
        )
    ) m
    CROSS APPLY JSON_TABLE(
        mj.data FORMAT JSON,
        '$.nominations[*]'
        COLUMNS (
            award_name VARCHAR2(400) PATH '$'
        )
    ) n
    JOIN award a ON UPPER(TRIM(a.award_name)) = UPPER(TRIM(n.award_name))
    WHERE NOT EXISTS (
        SELECT 1
        FROM movies mj2
            CROSS APPLY JSON_TABLE(
                mj2.data FORMAT JSON,
                '$'
                COLUMNS (
                    movie_id NUMBER PATH '$.movie_id'
                )
            ) m2
            CROSS APPLY JSON_TABLE(
                mj2.data FORMAT JSON,
                '$.awards[*]'
                COLUMNS (
                    award_name VARCHAR2(400) PATH '$'
                )
            ) w
            JOIN award a2 ON UPPER(TRIM(a2.award_name)) = UPPER(TRIM(w.award_name))
        WHERE m2.movie_id = m.movie_id
        AND a2.award_id = a.award_id
    )
    AND NOT EXISTS (
        SELECT 1 FROM movie_award
        WHERE movie_id = m.movie_id
        AND award_id = a.award_id
        AND result = 'nominated'
    );
    </copy>
    ```

## Task 6: Create a Duality View from the normalized tables

If data integrity, consistency, and flexibility are paramount, and the system involves frequent updates, starting with normalized tables and creating views for simplified access may be the best approach. Let's create a JSON duality view from the tables in Task 5.

1. In a new **worksheet** run the following as a `SQL Script` (F5):
    ```
    <copy>
    create JSON DUALITY VIEW movie_crew_awards AS
    crew @insert @update @delete
    {
        _id   : crew_id,
        name  : name,
        work   : movie_crew_link @insert @update @delete
        [ { movie_id : movie_id,
            crew_id  : crew_id,
            job : job,
            movie_title : movie @insert @update @delete
            [{ movie_id : movie_id,
                title    : title
            }],
            awards : movie_award @link (from: movie_id to: movie_id)
            [{ movie_id : movie_id,
            award_id : award_id,
            award_name : award @insert @update @delete
            [ { award_id : award_id,
                award_name : award_name_norm}],
            result : result
            }]
        }
        ]
    };
    </copy>
    ```

    For additional information on creating JSON Duality Views using GraphQL, visit:

    [Creating JSON Duality Views](https://docs.oracle.com/en/database/oracle/oracle-database/26/jsnvu/creating-car-racing-duality-views-using-graphql.html)

## Task 7: Mongosh aggregate the JSON Duality View

When you execute MongoDB commands against a JSON-relational duality view in Oracle Database, these commands are translated into SQL operations that interact with the underlying relational tables. Executing MongoDB commands against a JSON-relational duality view in Oracle Database allows developers to use familiar MongoDB tools while benefiting from Oracle's robust relational database features.

1. Return to your terminal or console. Ensure you are logged in as administrator, if not you may need to use the "`mongosh <MongoDB API string>`" again.

    ![I'm still logged into my database](./images/still-logged-in.png)

2. Enter the following command while logged into the database:

    ```
    <copy>
    db.movie_crew_awards.aggregate([
    // Stage 1: deconstruct the 'work' array field
    { $unwind: "$work" },
    // Stage 2: include only those where the 'job' field in 'work' is 'screenwriter'
    { $match: { "work.job": "screenwriter" } },
    // Stage 3: Deconstruct the 'awards' to output a document for each award
    { $unwind: "$work.awards" },
    // Stage 4: Group documents by 'name' and count the total number
    { $group: { _id: "$name", total_awards: { $sum: 1 } } },
    // Stage 5: Sort the results in descending order
    { $sort: { total_awards: -1 } }
    ]);
    </copy>
    ```
    ![Run aggregate on json duality view](./images/aggregate-json-view.png)

## Task 8: SQL query the normalized tables

For read-heavy operations, especially complex aggregations, using SQL queries on relational tables is generally more performant. For write operations, using duality views can simplify development by allowing updates in a JSON format, with Oracle handling the synchronization to relational tables.

1. In your database actions SQL view you were previously working in, Enter the following in a new **worksheet** and run the following as a `SQL Script` (F5):

    ```
    <copy>
    SELECT
        c.name,
        COUNT(ma.award_id) AS total_awards
    FROM
        -- Start with the 'crew' table
        crew c
        -- Join with 'movie_crew_link' to associate crew members with movies
        JOIN movie_crew_link mcl ON c.crew_id = mcl.crew_id
        -- Join with 'movie_award' to associate movies with their awards
        JOIN movie_award ma ON mcl.movie_id = ma.movie_id
    WHERE
        -- Filter to include only those with the job title 'screenwriter'
        mcl.job = 'screenwriter'
    GROUP BY
        -- Group the results by crew member's name
        c.name
    ORDER BY
        -- Sort the results in descending order based on the total number of awards
        total_awards DESC;
    </copy>
    ```
    ![All Results SQL Query](./images/all-results-sql-query.png)

That was a quick run-through of using JSON Collections with the MongoDB compatible API in Oracle AI Database. Oracle 26ai and its MongoDB API capabilities empower developers to build applications using familiar MongoDB tools and commands, while leveraging Oracle's robust performance, scalability, and enterprise-grade features.

## Learn More

* [JSON Relational Duality: The Revolutionary Convergence of Document, Object, and Relational Models](https://blogs.oracle.com/database/post/json-relational-duality-app-dev)
* [JSON Duality View documentation](https://docs.oracle.com/en/database/oracle/oracle-database/23/jsnvu/overview-json-relational-duality-views.html#)
* [Oracle AI Database API for MongoDB](https://blogs.oracle.com/database/post/mongodb-api)

## Acknowledgements

* **Authors** - Hermann Baer
* **Contributors** -  Beda Hammerschmidt
- **Last Updated By/Date** - Eileen Beck, November 2025
