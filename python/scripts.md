# Python

# Colors

```python
from colorama import init, Fore, Back, Style
init() # Needed for windows to work
print(Fore.RED + 'some red text')
print(Back.GREEN + 'and with a green background')
print(Style.DIM + 'and in dim text')
print(Style.RESET_ALL)
print('back to normal now')
```

# Command Line Args

```python
import argparse

def str2bool(v):
    if isinstance(v, bool):
       return v
    if v.lower() in ('yes', 'true', 't', 'y', '1'):
        return True
    elif v.lower() in ('no', 'false', 'f', 'n', '0'):
        return False
    else:
        raise argparse.ArgumentTypeError('Boolean value expected.')

parser = argparse.ArgumentParser(description='Generates Table Cache.')
parser.add_argument('--input', dest='sqlpath', type=str, nargs='?',
                    default="../input.txt",
                    help='Path of the SQL file')
parser.add_argument('--output', dest='phppath', type=str, nargs='?',
                    default="../output.txt",
                    help='Path of the table cache PHP file')
parser.add_argument('--temppath', dest='temppath', type=str, nargs='?',
                    default="./temp.txt",
                    help='Path of temporary table cache PHP file which will be compared to original')
parser.add_argument('-a', dest='auto', type=str2bool, nargs='?',
                    const=True, default=False,
                    help='Temp file is directly copied to real file location instead of being manually compared by the user.')
parser.add_argument('--bcpath', dest='bcpath', type=str, nargs='?',
                    default="C:\\Program Files\\Beyond Compare 4\\BCompare.exe",
                    help='Location of the Beyond Compare Tool (default: C:\\Program Files\\Beyond Compare 4\\BCompare.exe)')
args = parser.parse_args()

print args
```

# Open File Dialog

```python

```

# Logging

```python
import logging
import sys

class StreamToLogger(object):
   """
   Fake file-like stream object that redirects writes to a logger instance.
   """
   def __init__(self, logger, log_level=logging.INFO):
      self.logger = logger
      self.log_level = log_level
      self.linebuf = ''

   def write(self, buf):
      for line in buf.rstrip().splitlines():
         self.logger.log(self.log_level, line.rstrip())

   def flush(self):
      pass

logging.basicConfig(
   level=logging.DEBUG,
   format='%(asctime)s [%(levelname)s] %(message)s',
   filename="out.log",
   filemode='a'
)

# stdout_logger = logging.getLogger('STDOUT')
# sl = StreamToLogger(stdout_logger, logging.INFO)
# sys.stdout = sl

# stderr_logger = logging.getLogger('STDERR')
# sl = StreamToLogger(stderr_logger, logging.ERROR)
# sys.stderr = sl

sys.stdout = StreamToLogger(logging, logging.INFO)
sys.stderr = StreamToLogger(logging, logging.ERROR)

print("Test to standard out")
raise Exception('Test to standard error')
```

# Progress Bar

```python
from tqdm import tqdm
import time

for item in tqdm(range(10000)):
    time.sleep(.001)
```

# SQL Builder

```python
import MySQLdb

DEBUG = False

# Tries to get row ID of given table. If row is not in table, it adds it
def getOrInsertSqlRow(sqlcur, table, select, cols, vals):
    idx = getSqlRow(sqlcur, table, select, cols, vals)
    if idx is None:
        idx = insertSqlRow(sqlcur, table, cols, vals)
    return idx

# Returns the row ID of a given table and where clause from the DB
def getSqlRows(sqlcur, table, select, cols, vals, where = None):

    if where is None:
        whereList = []
        for idx, col in enumerate(cols):
            whereList.append("`{0}` = '{1}'".format(cols[idx], vals[idx]))
        where = " AND ".join(whereList)

    cmd = "SELECT `{0}` FROM `{1}` WHERE {2}".format(select, table, where)
    return getSqlRowsByQuery(sqlcur, cmd)

# Returns the row ID of a given table and where clause from the DB
def getSqlRow(sqlcur, table, select, cols, vals, where = None):

    if where is None:
        whereList = []
        for col, val in zip(cols, vals):
            whereList.append("`{0}` = '{1}'".format(col, val))
        where = " AND ".join(whereList)

    cmd = "SELECT `{0}` FROM `{1}` WHERE {2}".format(select, table, where)
    return getSqlRowByQuery(sqlcur, cmd)

def getSqlRowByQuery(sqlcur, query):
    if DEBUG == True:
        print "\t\t\t{0}".format(query)
    sqlcur.execute(query)

    row_id = None
    if sqlcur.rowcount > 0:
        rows = sqlcur.fetchall()
        row_id = rows[0][0]

    return row_id

def getSqlRowsByQuery(sqlcur, query):
    if DEBUG == True:
        print "\t\t\t{0}".format(query)
    sqlcur.execute(query)

    rows = None
    if sqlcur.rowcount > 0:
        rows = sqlcur.fetchall()

    return rows

# Inserts data into a certain table in the DB.
# insertCols is an array of all columns
# insertVals is an array of all values for the above columns
def insertSqlRow(sqlcur, table, insertCols, insertVals):

    insertColsStr = "`" + "`, `".join([str(i) for i in insertCols]) + "`"
    insertValsStr = ", ".join(["%s" for i in insertVals])

    cmd = "INSERT INTO `{0}` ({1}) VALUES ({2})".format(table, insertColsStr, insertValsStr)
    if DEBUG == True:
        print "\t\t\t{0}: {1}".format(cmd, insertVals)

    sqlcur.execute( cmd, tuple(insertVals))

    return sqlcur.lastrowid

# Updates data from a certain table in the DB.
# updateCols is an array of all columns
# updateVals is an array of all values for the above columns
def updateSqlRow(sqlcur, table, updateCols, updateVals, where):

    updateStr = ", ".join(["`{0}` = '{1}'".format(c, v) for c, v in zip(updateCols, updateVals)])

    cmd = "UPDATE `{0}` SET {1} WHERE {2}".format(table, updateStr, where)
    if DEBUG == True:
        print "\t\t\t{0}".format(cmd)

    sqlcur.execute( cmd )
```

# Wait For Input

```python
import os
import msvcrt

print "Press any key to exit..."
os.system('pause >nul')
```

# Running a Script