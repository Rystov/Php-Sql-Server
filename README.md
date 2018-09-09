# Php-Sql-Server
extracion de ruta de imagen  de php con java script img no randon/
<?php
$serverName = "B-PC\SQLSERVER"; //<?php
$connectionInfo = array( "Database"=>"d", "UID"=>"root", "PWD"=>"root");
$conn = sqlsrv_connect( $serverName, $connectionInfo);
if( $conn ) {
     echo "Conexión establecida.<br />";
}else{
     echo "Conexión no se pudo establecer.<br />";
     die( print_r( sqlsrv_errors(), true));
}
$arrayPic=array();
$arrayTxt=array();
$cont =0;

$tsql= "SELECT ima,txt FROM d.dbo.pic;";
$getResults= sqlsrv_query($conn, $tsql);
if ($getResults == FALSE)
    die(FormatErrors(sqlsrv_errors()));
while( $row = sqlsrv_fetch_array( $getResults, SQLSRV_FETCH_ASSOC) ) {
     $arrayPic[$cont]=$row['ima'];
     $arrayTxt[$cont]=$row['txt'];
     $cont+=1;
}
sqlsrv_free_stmt($getResults);
?>
<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>
<center>
    <img src="" id="imagen" width="500" height="500"></a> <br>
             <span id="txto"> </span>
</center>
</body>
</html>

<script>
     var numero=0;
    var imagenes=<?php echo json_encode($arrayPic);?>;
    var txto=<?php echo json_encode($arrayTxt);?>;
    //new Array( ["googl1"], ["googl1d"], ["googl1www"], ["googl1qqq"] );
    function cambiar() {        
        document.getElementById("imagen").src=imagenes[numero]; 
        document.getElementById("txto").innerHTML=txto[numero];
        numero=numero+1;
        if (numero==imagenes.length) {
            numero=0;
        } 
    }   
onload=function() {  
            cambiar();
            setInterval(cambiar,1000); 
    }
</script>
