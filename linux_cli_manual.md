### Shell Script

Current environment
```
export -p
```

Set 755 for all directories
```
find . -type d -exec chmod 755 {} \;
```
Set 644 for all files
```
find . -type f -exec chmod 644 {} \;
```
Find files with specific extension and remove those
```
find . -type f \( -iname \*.class \) -exec rm {} \;
```

Append multiple files (e.g. sample*.txt)
```
for f in sample*.txt
do
    tr -d ',' < $f >> new_file.txt
done
```

Remove all newline carriage
```
tr -d '\n' < $1 > $2
```

Select fields from text file (assuming delimter is :)
```
cut -d : -f 1,5 <txt_file>
```
or
```
awk -F: -v 'OFS=,' '{ print $1, $5 }' <txt_file>
awk 'BEGIN { FS = ":" ; OFS = "," }
    { print $1, $5 }' mypasswd.txt
```

Swap fields
```
# You love me
echo "I love you" | sed -f love_cmd_script
# I love you
echo "You love me" | sed -f love_cmd_script
```

SQL like merge data
```
# remove comments
sed '/^#/d;' quota.dat | sort > quota.sorted
sed '/^#/d;' sales.dat | sort > sales.sorted

# join
join quota.sorted sales.sorted

# remove tmp files
rm quota.sorted
rm sales.sorted
```

Count word frequency
```
tr -cs A-Za-z\' '\n' |
    # change lower case
    tr A-Z a-z |
    # count unique words
    sort |
    uniq -c |
    # sort by frequency (col 1 then col 2)
    sort -k1,1nr -k2 |
    sed ${1:-25}q |
    # show nicely in 4 columns
    pr -c4 -w80 -t
```

Solving puzzles
```
FILES="
    /usr/share/dict/american-english
      "
pattern="$1"

egrep -h -i "$pattern" $FILES 2> /dev/null | sort -u -f
```

Get sub-directories
```
find /usr/share -type d
```

Finding files
```
locate <files>
which <files>
```

### AWS CLI
Download from s3
```
aws s3api get-object --bucket <bucket-name> --key <file-name> <out-file-name>
```

### wget Download 
Download using wildcards
```
wget -r --no-parent -A 'bar.*.tar.gz' http://url/dir/

```

### EC2
connect ssh command
```
ssh -i <pem-file> <instance-user-name>@<instance-public-name>
```
for amazon linux,use ec2-user as username

### Mongodb startup

To start mongo daemon and mongo client
```
mongod.exe --dbpath "d:\test\mongoDir
mongo
```
select database
```
use foobar
```
Install python package
```
pip3 install pymongo --user
```
###### Admin Commands
```
shell: show dbs
javascript: db.getMongo().getDBs()
```

```
shell: show collections
javascript: db.getCollectionNames()
```

```
shell: use db
javascrpt: db.getSisterDB("foo")
```

###### Mongo Commands
* select database
```
use local
```

* insert document to collection called blog
```
db.blog.insert(doc)
```

* search all
'''
db.blog.find()
'''

### Postgresql
Login as user postgres:
```
sudo -u postgres bash
```

Login as postgres and start psql client
```
sudo -u postgres psql postgres
```

Start postgres client

Default database is the same as username
```
psql
psql -U <username> -d <database>
```
e.g.
```
psql -U fra -d ucidb
```

###### Database Administration
Create user login (at bash)
```
createuser --interactive fra
```

Create new user with password
```
createuser -P fra
```
alternatively,
```
postgres=# CREATE USER yourname WITH SUPERUSER PASSWORD 'yourpassword';
```

create new database
```
createdb ucidb
```
alternatively,
```
<user>=# CREATE DATABASE <dbname> WITH OWNER = <ownerName>;
```

To grant permission to create db
```
<user>=# ALTER USE <user> CREATEDB;
```
To grant permission
```
<user>=# GRANT <privilege> TO <user>;
```

###### Basic Postgres SQL commands
To list all tables
```
\dt
```
To connect to database <db>:
```
\c db
```
To show schema
```
\d+ <tablename>
```

To list all users:
```
<user>=# \du
```

To set user password
```
<user>=# \password <user>
```

To run query at terminal, e.g.
```
psql -d ucidb -c "select * from abalone limit 10"
```

###### Import csv file to postgressql database
Create table schema
```
csvsql abalone.csv > maketable.sql
psql -d <dbname> < maketable.sql
```

To load data (type inside cli)
```
\copy <table name> FROM <csv file>  CSV HEADER;
```

To export table to
```
\copy customers TO '/tmp/customers.csv' CSV HEADER;
```

###### Extension
```
SELECT name, default_version, installed_version, left(comment,30) As comment
FROM pg_available_extensions
WHERE installed_version IS NOT NULL
ORDER BY name;
```

To install extension, download extension file, then
```
CREATE EXTENSION <extension>, e.g:
CREATE EXTENSION fuzzystrmatch;
```

### CLI Data Science installation
Installation
```
pip install csvkit
sudo npm install xml2json-command
sudo apt-get install jq
```
json2csv - no sudo, user based (need golang)
```
go get github.com/jehiah/json2csv
```

###### Data Science Command Line
```
cat hello-world | wc -w
< hello-world wc -w
```

To convert xlsx to csv
```
in2csv <excel input file> > <csv out file>
```

A quick look at csv file
```
cat imdb-250.csv | head -n 10 | csvcut -c Title,Year | csvlook
```

To download file with curl
```
curl <url>
```
Curl with ftp with login credentials
```
curl -u username:password ftp://host/file
```

To translate fro lower to upper
```
echo "hi" | tr '[:lower:]' '[:upper:]'
```

Examples: word count and sort by frequency
```
cat shakes.txt | tr '[:upper:]' '[:lower:]' | grep -oE '\w+' | sort | uniq -c | sort -nr | head -n 10
```

###### python / R command line
```
#! /usr/bin/env python
#! /usr/bin/env Rscript
```

###### Header / body / cols
To get the header of a csv file
```
< tips.csv header
```

To remove the header
```
< tips.csv header -d
```

To add a header
```
< tips.csv header -a newheader
```

To use 'tr' to transform text, but apply to the 'body' only and only to the 'day' col only
```
< tips.csv cols -c day body "tr '[a-z]' '[A-Z]'" | head -n 5 | csvlook
```

###### csvcut
To select all cols except species
```
< iris.csv csvcut -C species | head -n 5 | csvlook
```

###### csvsql
```
< iris.csv csvsql --query "SELECT sepal_length, petal_length FROM stdin WHERE sepal_length > 6" | head -n 5 | csvlook
```

###### filtering - csvgrep
To select size with is 5
```
csvgrep -c size -r "5" tips.csv | csvlook
```

###### create new cols -- transformation
```
< names.csv csvsql --query "SELECT id, first_name || ' ' || last_name AS full_name, born FROM stdin" | csvlook
```

###### stack csv (vertical)
```
csvstack Iris-*.csv
```

###### horizontal stack of the three files: bills.csv, customers.csv and datetime.csv
```
paste -d, {bills,customers,datetime}.csv
```

###### inner join
```
csvjoin -c species iris.csv irismeta.csv | csvcut -c sepal_length,sepal_width,species,usda_id | csvlook
```

###### csvsql
```
csvsql --query 'SELECT i.sepal_length, i.sepal_width, i.species, m.usda_id FROM iris i JOIN irismeta m ON (i.species = m.species)' iris.csv irismeta.csv | csvlook
```

### Data Science Basic Commands
login name
```
whoami
```
host name
```
hostname
```
current date
```
date
```
data structure
```
tree
```

which
```
home/fra/Project/GoProj/bin/json2csv
```

word count
```
wc -l xxx.csv
```

view files
```
head / less / more / tail
```

To set an executable python script, put this at the first line
```
#!/usr/bin/env python
```

To set an executable R script,  put this at the first line
```
#!/usr/bin/env Rscript
```

To convert excel file to csv file
```
in2csv xxx.xlsx > xxx.csv
```

To quickly view xlsx file
```
in2csv xxx.xlsx | head | csvcut -c <column names> | csvlook
in2csv xxx.xlsx --sheet <sheet name> | head | csvcut -c <column names> | csvlook
```

To download from the web
```
curl -s <url> -o out_file
curl -u username:password ftp://host/file
```

word count
```
cat shakes.txt | tr '[:upper:]' '[:lower:]' | grep -oE '\w+' | sort |
uniq -c | sort -nr | head -n 10
```

random sample with specified rate (e.g. 10%)
```
sample -r 10%
```

replace values
```
tr <original_value> <new_value>
```
e.g.
```
echo 'hello world!' | tr ' ' '_'
```

To delete characters
```
echo 'hello world!' | tr -d -c '[a-z]'
```

To munipulate adder
```
e.g. to add a header
seq 5 | header -a count
```

To extract header
```
cat tips.csv | header
< tips.csv header
```

To delete header
```
cat tips.csv header -d | head
```

To apply a certain command only to the body
```
body
```
To apply a certain command only to some columns
```
cols
```
e.g. to change the column 'day' to uppercase
```
< tips.csv cols -c day body "tr '[a-z]' '[A-Z]'" | head
```

To do sql query on csv
```
seq 5 | header -a value | csvsql --query "SELECT SUM(value) AS sum FROM stdin"
```

To convert XML (HTML) to json
```
< table.html xml2json > table.json
< table.json jq '.' | head -n 25
```

jq : extract and reshape json data
```
e.g. take the values and give them labels
< table.json jq -c '.html.body.tr[] | {country: .td[1][],border:'\ '.td[2][], surface: .td[3][]}' > countries.json
```

To convert json to csv
```
< countries.json json2csv -p -k border,surface > countries.csv
```

###### CSV scrub operations
To extract and reordering
```
< iris.csv csvcut -c sepal_length,petal_length,sepal_width,petal_width | head | csvlook
```

select columns
```
< tips.csv csvcut -c bill,tip
```
select columns and save the results
```
< tips.csv csvcut -c day,time | tee datetime.csv | head -n 3 | csvlook
< tips.csv csvcut -c sex,smoker,size | tee customers.csv | head -n 3 | csvlook
```

exclude species
```
< iris.csv csvcut -C species | head -n 5 | csvlook
```

Filtering
```
e.g.exclude size with values 1 to 4:
csvgrep -c size -i -r "[1-4]" tips.csv | csvlook
```

Using csvsql
```
< iris.csv csvsql --query "SELECT sepal_length, petal_length, sepal_width, petal_width FROM stdin" | head -n 5 | csvlook
< tips.csv csvsql --query "SELECT * FROM stdin WHERE bill > 40 AND day LIKE '%S%'" | csvlook
```

###### Explore Data
To check the data types
```
e.g.
csvsql iris.csv
```

To count num unique values
```
cat data/iris.csv | csvcut -c species | body "uniq | wc -l"
```

To show number of unique values in each column
```
csvstat data/iris.csv --unique
```

To get all statistics
```
csvstat data/iris.csv
```

To stat for some selected columns only
```
csvstat data/iris.csv -c 2,14
```

To explore data using R
```
data/iris.csv Rio -e 'summary(df)'
```

Find files and Combine into one
```
find data/ -name '*.json' -exec cat {} \; > uber.json
```

Data visualization
examples:
```
< data/tips.csv Rio -ge 'g+geom_histogram(aes(bill))' | display
< data/tips.csv Rio -ge 'g+geom_density(aes(tip / bill * 100, fill=sex), alpha=0.3) + xlab("percent")' | display
```

###### Parallel Pipeline
```
echo "2.1^3" | bc
```

command line for loop
```
for i in {0..100..2}; do echo "$i^2" | bc ; done
```

GNU Parallel
```
seq 5 | parallel --no-notice "echo {}^2 | bc"
```

Exmaples
```
zcat *.json.gz | jq -r '.borough' | tr '[A-Z] ' '[a-z]_' | sort | uniq -c
```

###### Modeling
To view multiple files

```
head wine-{red,white}.csv
wc -l wine-{red,white}.csv
```

To check missing data
```
csvstat wine-both-clean.csv --nulls
```

To install tapkee
```
sudo apt-get install libeigen3-dev
curl -sL https://github.com/lisitsyn/tapkee/archive/master.tar.gz > tapkee-master.tar.gz
```

ERROR: eigen3 lib problems
```
tar -xzf tapkee-master.tar.gz
cd tapkee-master
mkdir build && cd build
```

### Networking
check port usage:
```
netstat -tulpn | grep LISTEN
```

write to port
```
nc -lk 9999
cat data.txt | ncat -l -p 9999
```

### Programming languages

###### Python
```
doctest
python -m doctest -v <source_file or txt_file>
```

To enable interact in jupyter
```
pip install ipywidgets
jupyter nbextension enable --py widgetsnbextension
```

To start bokeh server
```
bokeh serve eda --show --args abalone.csv
```

###### gcc / g++
To compilation c++11
```
g++ -std=c++11 <file_name>
gcc -std=c99 -Wall problem3.c -lm
```

To generate debug info
```
gcc -g filename.c
```

To specify lib path
```
gcc -I <header folder>
```
To specify output executable name
```
gcc -o <output executable>
```

To generate object file
```
gcc -c <src file>
```

To get the size of file
```
size <object file>
```

To get a list of symbols
```
objdump --syms <object file>
```

To disassemble
```
objdump -d <object file>
```

T find the location of glibc shared library
```
ldd <executatable> | grep libc
```

###### GDB

gdb init file
```
~/.gdbinit
```

TUI mode
```
gdb -tui <executable>
```

gdb debug
```
objdump -M intel -D a.out \ grep -A20 main.:
```

with debug info
```
gcc -g <filename>
```

inside GDB:
```
info register (i r)
```

set intel format
```
set disassembly-flavor intel
```

display assembly code
```
disassemble <function>
example:
disass main
```

To show content
```
x/i (instruction) var
x/x (hex) var
x/d (decimal) var
x/b (binary) var
x/o (octal) var
x/s (string) var (pointer)
```

To examine variables
```
print &pointer (address)
print pointer (content)
```

To display value of var
```
p <varName>

rbp : frame pointer
rip : execution pointer
rsp : stack pointer
```

check intstruction (5 lines) at register rip
```
x/5i $rip
```
