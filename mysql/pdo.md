# 通用

```
$dsn = 'mysql:dbname='.$database['database'].';host='.$database['hostname'].':'.$database['hostport'];
$user = $database['username'];
$password = $database['password'];
$db = new PDO($dsn, $user, $password);
$sql = 'select * from bre_users where user_id = :user_id';
$sth = $db->prepare($sql);
$sth->bindParam(':user_id', $uid, PDO::PARAM_INT);
$sth->execute();
```

## 获取一条记录

```
...
$sth->fetch(PDO::FETCH_ASSOC);
```

## 获取所有记录

```
...
$sth->fetchAll(PDO::FETCH_ASSOC);
```

