<html>
<head>
<title>Rename it to whatever</title>
</head>
<body>
 
<?php
 
// This part runs for half a day and then the script uploads to database 
  function read_data()
  {     
    var i = 0;
 
    while(1)
    {   
        $a = file_get_contents("http://(change this to host)/analogRead?pin=A3");
        $b = file_get_contents("http://(change this to host/analogRead?pin=A0");
        
        $str = json_decode($a);
        $str1 = json_decode($b);
        
        $fp = fopen("1.csv","a");   
 
        foreach ($str as $key) 
        {
            fwrite($fp, $key);
            fwrite($fp, ",");   
        }
        i = i+150;
        fclose($fp); 
 
        $fp = fopen("2.csv","a");   
        foreach ($str1 as $key1) 
        {
            fwrite($fp, $key1);
            fwrite($fp, ",");   
        }
        fclose($fp); 
        
        sleep(150);
        if(i==43100)
        {
            break;
        }
    }
  }
 
  read_data();
  // This is for authenticating the database
  $connect = mysql_connect('localhost','root','password'); // need to fill in own information dumb dumb
 
  if(!$connect)
  {
    echo "No database found, this means you fucked up the settings.";
  }
 
  // your database name
  $cid = mysql_select_db(floodData,$connect);
 
  define('CSV_PATH','./');
//Yes dev, I did CSV for you, not json or xml, don't @ meh
  $csv_file = CSV_PATH."1.csv";
  $csv_file1 = CSV_PATH."2.csv";
 
  if(($handle = $fopen($csv_file,"r"))!==FALSE)
  {
    fgetcsv($handle);
    while(($data = fgetcsv($handle,1000,","))!==FALSE)
    {
        $num = count($data);
        for($c=0;$c<$num;$c++)
        {
            $col[$c]=$data[$c];
        }
        $col1 = $col[0];
        $col2 = $col[1];
 
    // now upload your database using insert querries or bulk load
        $query = "INSERT INTO flood1node1(pressure,moisture,devIDs,atTime,nodeId) VALUES(,'".$col2"',,,1)" 
        $s = mysql_query($query,$connect);
 
    }
    fclose(handle);
  }
 
  if(($handle = $fopen($csv_file1,"r"))!==FALSE)
  {
    fgetcsv($handle);
    while(($data = fgetcsv($handle,1000,","))!==FALSE)
    {
        $num = count($data);
        for($c=0;$c<$num;$c++)
        {
            $col[$c]=$data[$c];
        }
        $col1 = $col[0];
        $col2 = $col[1];
 
    // now upload your database using insert querries or bulk load
        $query = "INSERT INTO river1node1(pressure,moisture,devIDs,atTime,nodeId) VALUES(,,'".$col2."',,1)" 
 
        $s = mysql_query($query,$connect);
 
    }
    fclose(handle);
  }
 
  mysql_close($connect);
?>
 
</body>
</html>
