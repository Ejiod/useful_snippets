# useful_snippets
Database Migration Script Documentation

This script demonstrates how to migrate data from one database to another. It uses the pyodbc and pandas libraries to interact with the databases.

##Dependencies

    pyodbc
    pandas

You can install them using pip:

pip install pyodbc pandas

Overview

The script follows these steps:

    Connect to the source and target databases
    For each table in the source database
        Read the table data into a DataFrame
        Create a table in the target database and insert the data
        Create a view of the source table in the source database
        If the table was successfully created in the target database and the view was successfully created in the source database, delete the table from the source database

## Code Breakdown
Connecting to the Databases

The script connects to the source and target databases using pyodbc.connect(). The connections are established using DSNs, which should be configured in your ODBC data sources.
Reading Table Data into a DataFrame

The script reads the data from each table in the source database into a DataFrame using pd.read_sql(). The DataFrame holds the data in memory while it is being migrated.

## Creating a Table and Inserting Data

The create_table_and_insert_data() function creates a new table in the target database and inserts the data from the DataFrame. The function infers the Teradata data type for each column in the DataFrame and uses these types to create the table. Once the table is created, the function iterates over the rows in the DataFrame, inserting each row into the table.
Creating a View in the Source Database

The create_view() function creates a view of the source table in the source database. This view remains in the source database after the table is deleted, providing a reference to the table's structure and content.
Checking if a Table or View Exists

The table_exists() and view_exists() functions are used to check if a table or view exists in a database. These functions execute a SELECT statement on the table or view and return True if the statement executes successfully and False if it raises an exception.
Deleting a Table from the Source Database

The delete_table() function deletes a table from the source database. This function is called after the table has been successfully migrated to the target database and a view of the table has been created in the source database.
Migrating Each Table

The script iterates over each row in migration_df, which defines the source and target databases and tables for the migration. For each row, the script reads the source table into a DataFrame, creates a table in the target database and inserts the data, creates a view in the source database, and deletes the source table.
Usage

Replace 'YourSourceDSN', 'YourUsername', and 'YourPassword' in the pyodbc.connect() calls with your source and target database DSNs, usernames, and passwords.

Replace the values in migration_df with your source and target databases and tables.

Run the script to migrate the tables from the source to the target databases.
