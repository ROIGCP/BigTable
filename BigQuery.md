# How to query BigTable from BigQuery

Requires:
    BigQuery Console 

Example SQL Statement to created external table\

Replace:\
    `BQDATASET.BQTABLE` with desired BigQuery dataset.table\
    `PROJECTNAME` with the project containing the Bigtable instance\
    `INSTANCENAME` with the Bigtable instance\
    `TABLENAME` with the Bigtable table name
    
    `CREATE or REPLACE EXTERNAL TABLE BQDATASET.BQTABLE
    OPTIONS (
    format = 'CLOUD_BIGTABLE',
    uris = ['https://googleapis.com/bigtable/projects/PROJECTNAME/instances/INSTANCENAME/tables/TABLENAME'],
    bigtable_options = 
    """{}"""
    );`

Table will now appear in the BigQuery Dataset as an external table.
