PLSQL流程控制语句

1、IF-THEN

```
IF  条件 THEN
	执行语句；
	执行语句n
END IF;

delcare
	var_num number;
	var_first_name employees.first_name%type := '&first_name';
begin
	select count(*) into var_num from employees where first_name = var_first_name;
	if var_num >= 1 then
		dbms_output.put_line('threr exists :'||var_first_name    );
end;
```

2、条件

