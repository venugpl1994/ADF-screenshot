In pipeline parameter we are fetching data from sql database which contain numerous table. The use of pipeline parameter here is during runtime we can dynamically
assign database from which we wanted to fetch data and copy it to ADLS .
The following step we need to build to  migrate data from AZure SQL Database to ADLS 
1) Create mission100db database 
2)Create missionsqldb Linked sevice which is used to establish connection with mission100db
3)Create SQL_Generic_DS which establish link with missionsqldb Linkedservice and pass parameter schemaName,databaseName,tableName for makinng SQL_Generic_DS generic.
4) Create copy activity having source and sink:-
    source- connect with SQL_Generic_DS
    sink- connect with ADLS CSV_DS having folderpath-dynamic content (global-parameter-pipeline)
    And outside copyAtivity parameter - entityName
5)ADLS_CSV connected with AzuredataLakestorage1 Linkedservice where parameter is folderpath and give filepath- @dataset().folderpath()
6)Create AzureDataLakestorage1 Linkedservice which is connected with storage100mission ADLS 

TO create any ADF general pipeline the general method is :

Azure SQL DB->>>>>missionsqldb Linkedservice->>>>>SQL_GENERIC_DS->>>>>>>Copy Activity->>>>>>>>ADLS_CSV_DS->>>>>>>AzureDataLakestorage1 Linkedservice->>>Storage account
