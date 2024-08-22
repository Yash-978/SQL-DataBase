# SQL-DataBase


# DataBase

## 👉 Adding Field Names (Table) 👈
### Ex: field names: id, name, role, salary, age, phone
```
CREATE TABLE "employees" (
	"id"	INTEGER NOT NULL UNIQUE,
	"name"	TEXT NOT NULL,
	"role"	TEXT NOT NULL,
	"salary"	INTEGER NOT NULL,
	"age"	INTEGER NOT NULL,
	"address"	TEXT,
	"phone"	INTEGER NOT NULL,
	PRIMARY KEY("id" AUTOINCREMENT)
);
```
## 👉Adding Details in Field Names (Table)👈
```
INSERT INTO employees
	(id, name, role, salary, age, address, phone)
VALUES
	(1, "Yash", "Flutter Dev", 50000, 21, "Surat", 123457989);
```

## 👉Adding Multiple Details in Field Names (Table)👈
```
INSERT INTO employees
	(id, name, role, salary, age, address, phone)
VALUES
	(1, "Yash", "Flutter Dev", 14000, 19, "Surat", 1234567891),
	(2, "Ravi", "Flutter Dev", 24000, 19, "Surat", 3214569771);
```

## 👉Read or Find all Details in Field Names (Table)👈
```
SELECT * FROM employees;
```

## 👉Read or Find specific Details in Field Names (Table)👈
```
SELECT name, salary FROM employees;
```

## 👉Read or Find specific Details in Field Names (Table) by their Category 👈
```
SELECT name, salary FROM employees WHERE role = "Launch Executive";
```

## 👉Search Details in Field Names (Table) by name Containing "Ra" 👈
```
SELECT * FROM employees WHERE name like "Ra%";
```

## 👉Find employees details who are older than 20 and earning more than 20,000👈
```
SELECT * FROM employees WHERE age > 20 AND salary > 20000;
```

## 👉Change the salary of an employee with ID 1👈
```
UPDATE employees SET salary = 17000 WHERE id = 1;
```

## 👉Update the address for employees "Launch Executive" role:👈
```
UPDATE employees SET address = "Udhana, Surat" WHERE role = "Launch Executive";
```

## 👉Remove an employee with ID 4👈
```
DELETE FROM employees WHERE id = 4;
```

## 👉Delete all employees under 20 👈
```
DELETE FROM employees WHERE age < 20;
```
<h3 align = "center"> DB Browser Screen</h3>
<h3 align = "center"></h3>
<p align = "center">
<img src= "https://github.com/user-attachments/assets/4a74484e-f6de-4fb2-9a7d-c04b7258cc4b" >

## 👉SQL Data Base Helper Class👈
```
class DataBaseHelper {
  static DataBaseHelper dataBaseHelper = DataBaseHelper._instance();

  DataBaseHelper._instance();

  Database? _database;

  Future get database async => _database ?? await initDatabase();

  Future initDatabase() async {
    final path = await getDatabasesPath();
    final dbPath = join(path, 'finance.db');

    _database = await openDatabase(
      dbPath,
      version: 1,
      onCreate: (db, version) async {
        String sql = '''CREATE TABLE finance(
      id INTEGER PRIMARY KEY AUTOINCREMENT,
      amount REAL NOT NULL,
      isIncome INTEGER NOT NULL,
      category TEXT);
       ''';
        await db.execute(sql);
      },
    );
    return _database;
  }

  Future insertData() async {
    Database? db = await database;
    String sql = '''INSERT INTO finance(amount,isIncome,category)
    VALUES(500,1,"Hoodie");
     ''';
    await db!.rawInsert(sql);
  }
  Future deleteData() async {
    Database? db = await database;
    String sql = '''DELETE FROM finance(amount,isIncome,category)
    VALUES(500,1,"Hoodie");
     ''';
    await db!.rawDelete(sql);
  }

}

```
## 👉SQL Data Base Helper Class👈
```
class HomeController extends GetxController {
  @override
  void onInit() {
    super.onInit();
    initDb();
  }

  Future initDb() async {
    await DataBaseHelper.dataBaseHelper.database;
  }

  Future insertRecord() async {
    await DataBaseHelper.dataBaseHelper.insertData();
  }
  Future deleteRecord() async {
    await DataBaseHelper.dataBaseHelper.deleteData();
  }
}

```
<h3 align = "center"> DB Browser Screen</h3>
<h3 align = "center"></h3>
<p align = "center">
<img src= "https://github.com/user-attachments/assets/82cf6f97-0cdc-4a34-a7b0-414efa2351af" >


