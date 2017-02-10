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
    - MySql Data Entity : `MySql.Data.Entity` . After install this, new files should be added under our project directories on **references**'s folder. This directories exist under solution explorer. These two files are `MySQL.Data` and `MySQL.Data.Entity.EF6`.
    
  - Using NuGet Package Manager Searching Window. To open, right click our project name under `solution explorer menu`, and choose `Manage NuGet Package`. New windows will open and do searching for these below pacakge inside search Box :
    - Entity Framework(v6.1.3 - at the time of writing), and
    - MySql.Data.Entity(v6.9.9 - at the time of writing)
