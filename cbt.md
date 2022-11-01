# `cbt` command line examples
Replace BIGTABLEINSTANCE with your Bigtable Instance Name\
Replace TABLENAME with your Bigtable Table Name\
Full reference: https://cloud.google.com/bigtable/docs/cbt-reference\

Sample CSV format\
NOTES: key column does NOT get a name\
the leading, between and trailing , in the header rows are important!\
  `,columnfamily,,,`\
  `,column1name,column2name,column3name`\
  `key,column1,column2,column3`
  
Sample CSV file (save as `sample.csv`/also available as sample.csv in this git repository)\
`,columnfamily1,,columnfamily2,`\
`,column1,column2,column3,column4`\
`KEYAAA,ABC,111,New York,New York`\
`KEYABC,ABC,123,Chicago,Illinois`\
`KEYDEF,DEF,456,Butte,Montana`\
`KEYXYZ,XYZ,789,Seattle,Washington`\
`KEYZZZ,ZZZ,999,Portland,Oregon`

Create table\
`cbt -instance BIGTABLEINSTANCE createtable TABLENAME families=columnfamily1,columnfamily2`

Import into table (uses sample.csv above)\
`cbt -instance BIGTABLEINSTANCE import TABLENAME sample.csv`

Count rows (count)\
`cbt -instance BIGTABLEINSTANCE count TABLENAME`

List tables (ls)\
`cbt -instance BIGTABLEINSTANCE ls`

List column family(s) in a table (ls TABLENAME)\
`cbt -instance BIGTABLEINSTANCE ls TABLENAME`

Query Table for a specific key (lookup)\
`cbt -instance BIGTABLEINSTANCE lookup TABLENAME "KEYABC"`

Query Table for a range of keys (read)\
`cbt -instance BIGTABLEINSTANCE read TABLENAME start="KEYABC" end="KEYXYZ"`

Set value of a cell (write)\
`cbt -instance BIGTABLEINSTANCE set TABLENAME "KEYABC" columnfamily2:column3="Elmhurst"`

Create a row (if key does not exist) (write)\
`cbt -instance BIGTABLEINSTANCE set TABLENAME "KEYMNO" columnfamily1:column1="MNO"` columnfamily1:column2="567"` columnfamily1:column1="San Francisco" columnfamily2:column4="California"`

Delete a row (deleterow)\
`cbt -instance BIGTABLEINSTANCE deleterow TABLENAME "KEYMNO"`

Delete all rows (deleteallrows)\
`cbt -instance BIGTABLEINSTANCE deleteallrows TABLENAME`

Delete table (deletetable)\
`cbt -instance BIGTABLEINSTANCE deletetable TABLENAME`
