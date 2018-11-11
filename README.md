# Insert_into_mysql
Insert data into MySQL using PDO


<?php
$host = 'localhost';
$db='mydb';           // your database name
$charset = 'utf8';
$userdb = 'your_user';        //you can use root or your user
$passdb = 'your_password';   // enter you password


$pdo=null;
$dsn = "mysql:host=$host;dbname=$db;charset=$charset";

$options = array(
    PDO::ATTR_ERRMODE            => PDO::ERRMODE_EXCEPTION,
    PDO::ATTR_EMULATE_PREPARES   => false,

);

try {

$pdo = new PDO($dsn, $userdb, $passdb, $options);

} catch(PDOException $e) {
echo "Could not connect to database!";
}

$isql="insert into usernames(lastname,firstname,username,password,email,role,city, country, bio, website, active)
values (?,?,?,?,?,?,?,?,?,?,?)";

$lastname="Barry";
$firstname="John";
$username="johnb";
$password="secret";
$email="johnb@yahoo.com";
$role="user";
$city="Brooklyn";
$country="USA";
$bio="I am a great guy!";
$website="http://configure-all.com";
$active=1;

 try {

$stmt = $pdo->prepare($isql);

$stmt->execute([$lastname,$firstname,$username,$password,$email,$role,$city,$country,$bio,$website,$active]);

$insertId = $pdo->lastInsertId();

echo "LastID=".$insertId;

echo "New records created successfully";
    }
        catch(PDOException $e)
    {

   echo "Error: " . $e->getMessage();
    }
?>
