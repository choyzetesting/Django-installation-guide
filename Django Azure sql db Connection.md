
<h1>**Connecting Django to Azure SQL Database**</h1>

Django is a powerful web framework used for building web applications. Azure SQL Database is a cloud-based relational database service provided by Microsoft. This documentation provides step-by-step instructions on how to connect Django to an Azure SQL database.

**Step 1: Install required packages**

You will need to install the following packages to connect Django to Azure SQL:

-   `pyodbc` - Python library for connecting to ODBC databases
-   `django-pyodbc-azure` - Django library for connecting to Azure SQL databases using pyodbc

You can install these packages using pip:

    pip install pyodbc django-pyodbc-azure

**Step 2: Configure database settings**

In your Django project's `settings.py` file, add the following database settings:

    DATABASES = {
        'default': {
            'ENGINE': 'sql_server.pyodbc',
            'NAME': '<database_name>',
            'USER': '<database_user>',
            'PASSWORD': '<database_password>',
            'HOST': '<database_server_name>.database.windows.net',
            'PORT': '1433',
            'OPTIONS': {
                'driver': 'ODBC Driver 17 for SQL Server',
            },
        },
    }

Replace the placeholders with the appropriate values:

-   `<database_name>` - Name of the Azure SQL database
-   `<database_user>` - Username for accessing the database
-   `<database_password>` - Password for accessing the database
-   `<database_server_name>` - Name of the Azure SQL database server. It's one in the format somthingchoyze.database.windows.net. I hope you got the deal.


What is what I guess is easily understood 
Please Get access to Azure database from Steffan or Me(Akshay).Also we need to add your Ip from which you are trying to access the databse. It's a firewall thing you need to have access to enter into databse firewall.

**Step 3: Configure ODBC driver**

You will need to install and configure the ODBC driver for connecting to Azure SQL. Follow these steps:

1.  Download and install the ODBC Driver for SQL Server from Microsoft's website: [https://docs.microsoft.com/en-us/sql/connect/odbc/download-odbc-driver-for-sql-server](https://docs.microsoft.com/en-us/sql/connect/odbc/download-odbc-driver-for-sql-server)
    
This is the most error prone step as there many versions of odbc driver are available and you need to install what you mentioned in the  settings.py
 file in django.
for example - `'driver': 'ODBC Driver 17 for SQL Serve`r' this line the version of odbc.

**Step 4: Test connection**

You can test the connection to the Azure SQL database by running the Django shell and executing a query:

    python manage.py dbshell
    
    # Run a sample query
    SELECT * FROM <table_name>;
If everything right you As soon as you hit first dbshell command you will be able to db shell activated in your command line.
Exit it using \q or \quit or control+z or whtever works for you.

**Step 5: Run migrations**

You can now run the migrations to create the required database tables:

    python manage.py migrate
**Step 6: Generate Django models**

Django provides a `inspectdb` management command that generates models by introspecting an existing database. Run the following command in your terminal to generate models for the tables in your Azure SQL database:

    python manage.py inspectdb > models.py

This command will generate a file named `models.py` that contains the model definitions for the tables in your database.
OK! Cheers That's a lot for your first time.But I hope i made it easy for you.

**Step 7: Include models in your Django project**

Add the generated `models.py` file to your Django project. You can place it in the same directory as your `models.py` file or create a new file and include it in your `INSTALLED_APPS` setting in your project's `settings.py` file.

    INSTALLED_APPS = [
        # ...
        'myapp',
        'myotherapp',
        'app_with_models_generated_from_azure_sql',
        # ...
    ]

Step 7 is really not needed but if we have lot of apps in future inside our django architecture we you know the deal of django flow.

**Conclusion**

In this documentation, we have seen how to connect Django to an Azure SQL database using pyodbc and django-pyodbc-azure libraries. Follow these steps to establish a connection and start building your Django web application with Azure SQL.
