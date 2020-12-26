# fix-malformed-db
To fix 'malformed db' try these steps

### Requirements
- Sqlite3

  * The latest version of SQLite always comes pre-installed within Mac OSX or macOS. You don’t have to download or install anything else, it’s located in the directory: /usr/bin/.

  * For other OS, please see: https://www.sqlitetutorial.net/download-install-sqlite/

### Usage
For each corrupted db, follow these steps:
- open a prompt from sqlite3

  ```
  sqlite3 ./accelerometer.db
  ```
- run these SQL scripts

  ```.mode insert
  .output ./dump_all.sql
  .dump
  .exit
  ```

- editing dump_all.sql file

  ```
  cat /dump_all.sql | grep -v TRANSACTION | grep -v ROLLBACK | grep -v COMMIT >/dump_all_notrans.sql
  ```

- remove corrupted db from the file repository being worked on (make sure you take backup file before that):

  ```
  rm ./accelerometer.db
  ```

- creation of fixed db from dump_all_notrans.sql

  ```
  sqlite3 ./accelerometer.db ".read dump_all_notrans.sql"
  ```



