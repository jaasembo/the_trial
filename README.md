<?php
require_once "../moss/Database_Connect.php";

//using $_Request below because by default it contains $_Get $_Post $_cookie 
$VIN = $_REQUEST['VIN'];
//The below code was a Eureka moment relating the two tables using inner join under getting the id of a particular object //via the url
$query = "SELECT * FROM cars INNER JOIN images ON cars.image_path_id=images.image_path_id WHERE VIN =" . $VIN; 
if($result=mysql_query($query)){
}else
echo "Sorry, a vehicle with VIN of $VIN cannot be found" .mysql_error()."<br>";


while($result_ar=mysql_fetch_assoc($result)){
$year = $result_ar['YEAR'];
$make = $result_ar['Make'];
$model = $result_ar['Model'];
$trim = $result_ar['TRIM'];
$color = $result_ar['EXT_COLOR'];
$interior = $result_ar['INTERIOR_COLOR'];
$mileage = $result_ar['MILEAGE'];
$transmission = $result_ar['TRANSMISSION'];
$price= $result_ar['ASKING_PRICE'];
$car_image=get_web_path($result_ar['user_pic_path']);
$thumb_nail=$result_ar['image_path_id'];
$image_Front=get_web_path($result_ar['FrontSide_Right']);
$image_Fside=get_web_path($result_ar['FrontSide_Left']);
$image_Back=get_web_path($result_ar['BackSide_Right']);
$image_Bside=get_web_path($result_ar['BackSide_Left']);
$image_Engine=get_web_path($result_ar['Engine']);


}
?>
<div class="row">
<div class="col-lg-1 col-md-2">
<h1 class="hidden-lg" >Gallery for  <?php echo "{$model}";?> </h1>
<hr class="hidden-lg">
<div id="gallery">
<a href ="uploads/Engine/1405112337_Brown Wedding Suit.jpg"><img  src="<?php echo ($image_Engine); ?>"width="70" height="70" /></a>
<div id='float'>
<a href =""><img  src="<?php echo ($image_Bside); ?>"width="70" height="70" /></a>
</div>
<div id='float'>
<a href =""><img  src="<?php echo ($image_Back); ?>"width="70" height="70" /></a>
</div>
<div id='float'>
<a href =""><img  src="<?php echo ($image_Fside); ?>"width="70" height="70" /></a>
</div>
<div id='float'>
<a href =""><img src="<?php echo ($image_Front); ?>"width="70" height="70" /></a>
</div>
</div>
</div>
<!--the below div only seen on large devices-->
<div class="col-lg-7  visible-lg">
<h1 class="hidden-xs" >Gallery for  <?php echo "{$model}";?> </h1>
<hr>
<div id="photo">
<img src="<?php echo ($car_image); ?>"width="400" height="300" />
</div>
</div>
<!--the below div only seen on md devices-->
<div class="col-lg-7 col-md-10 visible-lg">
<div id="photo">
<img src="<?php echo ($car_image); ?>"width="400" height="300" />
</div>
</div>
<!--the below div only seen on xs devices-->
<div class="col-lg-7 col-sm-5 hidden-lg ">
<div id="photo">
<img src="<?php echo ($car_image); ?>"width="300" height="300" />
</div>
<h1/><?php echo"{$make}";?><h1>
</div>
<div class="col-lg-4 col-sm-6 visible-lg ">
<div  id='table' width="50" height="30">
<?php
echo"<table id='tem'><tr >";
echo"<th style='width:50px'>MAKE </th>";
echo"<th style='width:50px'> MODEL</th>";
echo"<th style='width:50px'> ASKING PRICE</th>";
echo"<th style='width:50px'> EXTERIOR COLOR </th>";
echo"<th style='width:50px'> INTERIOR COLOR</th>";
echo"<th style='width:50px'> INFO</th>";
echo "</tr>";
$class="odd";
echo "<tr class=\"$class\">";
echo"<td style='width:50px'>{$make} </td>";
echo"<td style='width:50px'> {$model}</td>";
echo "<td style='width:50px'>{$price}</td>";
echo "<td style='width:50px'>{$color}</td>";
echo "<td style='width:50px'>{$interior}</td>";
echo "<td ><a href='ask.php' style='text-decoration:none;'><span style='color:#006699;'>Ask about this car<span></a></td>";
echo "</tr>";
echo "<tr style='background-color:#383838 ;'>";
echo "<td style='width:100px' ><span  style='color:#E8E8E8 '>Kindly find below quote for a <span style='color:#006699'>{$make} {$model}</span>
ready for Import.If any of the quotes pleases you and you confirm,
please click the ask about this car link below  fill your details and
someone will be in touch with you. Many thanks.We look forward to the order</span> 
</td>";
echo "</tr>\n";
echo"</table>";
?>
