# Setup Description

# Require Installer
Download all the required installer

1) Connector/Net is a fully-managed ADO.NET driver for MySQL
 - https://dev.mysql.com/downloads/connector/net/
 
2) MySQL for Visual Studio provides access to MySQL objects and data using Microsoft Visual Studio.
 - https://dev.mysql.com/downloads/windows/visualstudio/
 
3) Visual Studio Community Edition 2015(Free)
 - https://www.visualstudio.com/downloads/
 
 
# Create New MVC(C#) Project
Before these step were configured, create new MVC project. 

1) **File > New > Project**. 

2) From left panel chose **Web**, and chose **ASP.NET Web Application(.NET Framework)** from right pane. At the time of writing was using .NET Framework 4.5.2. 

3) Change **Name** and click *OK*

4) New window open(select a template)

5) Select **MVC** template at left panel

6) Click **Change Authentication** button at right panel

7) And finally choose **No Authentication**, and press OK.

8) Last, press OK again.

9) These above step may or may not change in future version.

# Manage NuGet Dependencies
Once the project successfully finished installed, we need to install 2 dependencies installer into our project. Since this project was planed to use `Entity Framework` and `MySQL`, then we need install these two :

1) For this tutorial, we install EF6. Open nuget package manager. We have 2 options for NuGet package installation as follow :
  - Using Package Manager Console. Find **Tools > NuGet Package Manager > Package Manager Console**. After clicking on this, new panel will showing up at the buttom of application, from the console we can install directly package using command. Install these 2 package for our project.
    - Entity Framework : `Install-Package EntityFramework`
    - MySql Data Entity : `Install-Package MySql.Data.Entity` . After install this, new files should be added under our project directories on **references**'s folder. This directories exist under solution explorer. These two files are `MySQL.Data` and `MySQL.Data.Entity.EF6`.
    
  - Using NuGet Package Manager Searching Window. To open, right click our project name under `solution explorer menu`, and choose `Manage NuGet Package`. New windows will open and do searching for these below pacakge inside search Box :
    - Entity Framework(v6.1.3 - at the time of writing), and
    - MySql.Data.Entity(v6.9.9 - at the time of writing)
    
# Manage Web.config with our mysql connection and entity framework
Open `web.config` file located under our project. You may find this file under `solution explorer` panel. Copy and paste this setting into `web.config` before closing tag `</configuration>`.

```xml
<entityFramework>
    <defaultConnectionFactory type="System.Data.Entity.Infrastructure.LocalDbConnectionFactory, EntityFramework">
      <parameters>
        <parameter value="mssqllocaldb" />
      </parameters>
    </defaultConnectionFactory>
    <providers>
      <provider invariantName="System.Data.SqlClient" type="System.Data.Entity.SqlServer.SqlProviderServices, EntityFramework.SqlServer" />
    <provider invariantName="MySql.Data.MySqlClient" type="MySql.Data.MySqlClient.MySqlProviderServices, MySql.Data.Entity.EF6, Version=6.9.9.0, Culture=neutral, PublicKeyToken=c5687fc88969c44d"></provider></providers>
  `</entityFramework>
<system.data>
    <DbProviderFactories>
      <remove invariant="MySql.Data.MySqlClient" />
      <add name="MySQL Data Provider" invariant="MySql.Data.MySqlClient" description=".Net Framework Data Provider for MySQL" type="MySql.Data.MySqlClient.MySqlClientFactory, MySql.Data, Version=6.9.9.0, Culture=neutral, PublicKeyToken=c5687fc88969c44d" />
    </DbProviderFactories>
  </system.data>
```
# Adding database connection
From server explored, find `Data Connection` and right click add connection. You can create MysqlData source from this window.

# Adding ADO.NET Entity Data Model
For querying from/to MySQL database, we need to use `DbContext` class for our DAL(Data Access Layer) to communicate with our POJO(Plain Object) that having fields that react with our database's fields.

1) Under solution explored, right click on our project's name. Choose **Add > New Item**

2) New window open. Choose **Data** at left pane, and choose **ADO.NET Entity Data Model** at right pane. And give that a name, this name should react with our table's name in database.

3) Click ok, and choose **Code First from Database**

4) Press next, choose connection we set earlier, and press `Next`

5) Select table for our entity context, and click `Finish`

6) This will aoutomatically added connection string on `web.config`, if dont, copy and paste below code inside `web.config` before closing tag `</configuration>` :

```xml
<configuration>
...
  <connectionStrings>
    <add name="localhostJer" connectionString="server=localhost;user id=root;database=test" providerName="MySql.Data.MySqlClient" />       </connectionStrings>
....
</configuration>
```


