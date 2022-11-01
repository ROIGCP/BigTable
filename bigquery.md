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

Using sample from cbt.md file loaded (see https://github.com/ROIGCP/BigTable/blob/main/cbt.md for demo)
NOTE: all values are binary encoded  - use cast(column as STRING))

select rowkey from BQDATASET.BQTABLE limit 1\
(Results viewed as JSON)\
`[{
  "rowkey": "S0VZQUFB"
}]`

select cast(rowkey as string) as rowkey from BQDATASET.BQTABLE limit 1
`[{
  "rowkey": "KEYAAA"
}]`

select * from BQDATASET.BQTABLE limit 1
`[{
  "rowkey": "S0VZQUFB",
  "columnfamily1": {
    "column": [{
      "name": "column1",
      "cell": [{
        "timestamp": "2022-11-01 15:00:35.333000 UTC",
        "value": "QUJD"
      }]
    }, {
      "name": "column2",
      "cell": [{
        "timestamp": "2022-11-01 15:00:35.333000 UTC",
        "value": "MTEx"
      }]
    }]
  },
  "columnfamily2": {
    "column": [{
      "name": "column3",
      "cell": [{
        "timestamp": "2022-11-01 15:03:02.868000 UTC",
        "value": "RWxtaHVyc3Q\u003d"
      }, {
        "timestamp": "2022-11-01 15:00:35.333000 UTC",
        "value": "TmV3IFlvcms\u003d"
      }]
    }, {
      "name": "column4",
      "cell": [{
        "timestamp": "2022-11-01 15:00:35.333000 UTC",
        "value": "TmV3IFlvcms\u003d"
      }]
    }]
  }
}]`
