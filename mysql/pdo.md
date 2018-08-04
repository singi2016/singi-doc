```
$dsn = 'mysql:dbname='.$database['database'].';host='.$database['hostname'].':'.$database['hostport'];
$user = $database['username'];
$password = $database['password'];
$db = new PDO($dsn, $user, $password);
$sql = 'select * from bre_users where user_id = :user_id';
$sth = $db->prepare($sql_local_user);
$sth->bindParam(':user_id', $uid, PDO::PARAM_INT);
$sth->execute();
```