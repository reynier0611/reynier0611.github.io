## Fixing exposed database <img src="img/sql_logo.jpg" width="40" height="40" style="float: right;" />

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> 

We need to find our ```postgresql.conf``` file. In my case, I found it in ```/Library/PostgreSQL/15/data/```. Then we need to open this, for instance, with ```vim```, but we won't have the permissions to open this file. To access and edit it do:

```shell
sudo -u postgres vim /Library/PostgreSQL/15/data/postgresql.conf
```

and change ```'*'``` in ```listen_addresses = '*'``` to ```localhost```.

See comments [here](https://dba.stackexchange.com/questions/220700/how-to-edit-postgresql-conf-with-pgadmin-4).