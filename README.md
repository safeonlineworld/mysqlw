# mysql_wrapper (C++)
MySQL C++ Wrapper for web_jsx (FCGI/CGI Application)<br/>
#Include header file
```c++
#include <my_sql.h>
```
Initilize my_sql instance
```c++
my_sql* sql = new my_sql();
```
Create connection detail
```c++
connection_details* con = new connection_details();
con->database = new std::string("test");
con->host = new std::string("localhost");
con->user = new std::string("root");
con->password = new std::string("*****");
con->unix_socket = NULL;
con->port = 0;
con->clientflag = 0;
```
Connect MySQL with this connection detail
```c++
if (sql->connect( con ) == connection_state::CLOSED) {
	std::cout << sql->get_last_error();
}
```
Execute plain sql statement
```c++
int ret = sql.execute("CREATE TABLE Persons ( PersonID int,LastName varchar(255),FirstName varchar(255),Address varchar(255), City varchar(255))");
```
Read the status of current execution
```c++
if ( ret < 0 ) {
	std::cout << sql->get_last_error();
}
```
Execute plain sql statement as like as data reader
```c++
int ret = sql->execute(select * from Persons, [](int index, std::vector<char*>& rows) {
	for (std::vector<char*>::iterator i = rows.begin(); i != rows.end(); ++i){
		std::cout << *i;
	}
	return;
});

if ( ret < 0 ) {
	std::cout << sql->get_last_error();
}
```
Close all connection pool
```c++
sql->close_all_connection();
```
Clear MySQL all connection pool and instance
```c++
sql->exit_all();

```
