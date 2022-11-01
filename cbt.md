# `cbt` command line examples
Replace BIGTABLEINSTANCE with your Bigtable Instance Name\
Replace TABLENAME with your Bigtable Table Name\
Full reference: https://cloud.google.com/bigtable/docs/cbt-reference\

Sample CSV format\
NOTES: key column does NOT get a name\
the leading, between and trailing , in the header rows are important!\
  `,columnfamily,,,\
  ,column1name,column2name,column3name\
  key,column1,column2,column3`
  
Sample CSV file (save as `sample.csv`/also available as sample.csv in this git repository)\
`,columnfamily1,,columnfamily2,`\
`,column1,column2,column3,column4`\
`KEYAAA,ABC,111,Elmhurst,Illinois`\
`KEYABC,ABC,123,Chicago,Illinois`\
`KEYDEF,DEF,456,Butte,Montana`\
`KEYXYZ,XYZ,789,Seattle,Washington`\
`KEYZZZ,ZZZ,999,Portland,Oregon`

Import into cbt\
`cbt -instance BIGTABLEINSTANCE import TABLENAME sample.csv`

Query Table for a specific key (lookup)\
`cbt -instance BIGTABLEINSTANCE lookup TABLENAME "KEYABC"`

Query Table for a range of keys (read)\
`cbt -instance BIGTABLEINSTANCE read TABLENAME start="KEYABC" end="KEYXYZ"`

