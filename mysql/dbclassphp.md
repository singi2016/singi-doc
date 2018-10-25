# db单例类

```php
class Db
{
    private static $instance;

    private function __construct(){}
    private function __clone(){}

    public static function instance(){
        $database = require_once dirname(__DIR__).'/database.php';
        if (!self::$instance){
            $dsn = 'mysql:dbname='.$database['database'].';host='.$database['hostname'].':'.$database['hostport'];
            $user = $database['username'];
            $password = $database['password'];

            try {
                self::$instance = new \PDO($dsn, $user, $password);
            } catch (PDOException $e) {
                echo 'Connection failed: ' . $e->getMessage();
            }
        }
        return self::$instance;
    }
}
```