`$count` - return value how many elements we have in array

```php
<?php
$cars=array("Volvo","BMW","Toyota");
echo count($cars);
// answer: 3
?>
```

`array_search()` - search in array


```php
<?php
$array = array(0 => 'blue', 1 => 'red', 2 => 'green', 3 => 'red');

$key = array_search('green', $array); // $key = 2;
$key = array_search('red', $array);   // $key = 1;
?>
```

`Sum` numbers in array:

```php
<?php function sum_array( $no1, $no2 ) {
  
  $array = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100];
	 //Insert your code here 
	 
	if($no1<0 || $no2<0) return -1;
	if($no1<$no2){
		if (in_array($no1, $array) && $no2>100) 
			return $no1+$no2;
		elseif(in_array($no1, $array) && in_array($no2, $array)){
			$key1 = array_search($no1, $array);
			$key2 = array_search($no2, $array);
			$sum = 0;
			foreach($array as $key => $value){
				if($key>=$key1 && $key<=$key2){
					$sum += $value;
					echo $key2."<br>";
				}
				
			}
			return $sum;
		}elseif(!in_array($no1, $array) && !in_array($no2, $array)) 
			return 0;
	}else{
		return 0;
	}
}
 ?>
```

Sum numbers in array:
`array_slice` - take a slice of array 

```php
<?php function sum_array( $no1, $no2 ) {
  
  $array = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100];
	 //Insert your code here 
	 
	if($no1<0 || $no2<0) return -1;
	if($no1<$no2){
		if (in_array($no1, $array) && $no2>100) 
			return $no1+$no2;
		elseif(in_array($no1, $array) && in_array($no2, $array)){
			$key1 = array_search($no1, $array);
			$key2 = array_search($no2, $array);
			echo "k1: ".$key1." k2: ".$key2."  <br>";
			$new_array = array_slice($array, $key1, $key2-$key1+1,true);
			print_r($new_array);
			return array_sum($new_array);
		}elseif(!in_array($no1, $array) && !in_array($no2, $array)) 
			return 0;
	}else{
		return 0;
	}
}
 ?>
```

`count_chars` - count chars in sentence

```php
class LetterCounter {
  // Write your code here
  public $str = '';
  
  public static function CountLettersAsString($string){  	
	$str = '';
	$string = strtolower($string);
	foreach (count_chars($string, 1) as $i => $val) {
   		$str = $str . chr($i) . ":".$val.",";
	}
	
	//print_r(str_split($string, 1));
	return $str;
  }
}
```

`array_key_exists` - check if key exists in array

`str_split($string, 1);` - split string to array `1` is every single char

```php
<?php function letterCounterCheck( $string ) {
  return LetterCounter::CountLettersAsString($string);
}
// DO NOT MODIFY THE CODE ABOVE

class LetterCounter {
  // Write your code here
  public $str = '';
  
  public static function CountLettersAsString($string){  	
	$unique = [];
	$string = strtolower($string);
	$array_length = strlen($string);
	$string = str_split($string, 1);
	
 	for($i = 0; $i < $array_length; $i++) {
        $char = $string[$i];
		if($char != ' '){
		  if(!array_key_exists($char, $unique))
			  $unique[$char] = '';
		  $unique[$char] = $unique[$char].'*';
		}
    }
	
	$str = '';
	
	foreach($unique as $char => $value){
		$str = $str.$char.':'.$unique[$char].',';
	}
	
	//print_r(str_split($string, 1));
	return substr($str, 0, -1);;
  }
}
?>
```

`array_slice($array, $key1, $key2-$key1+1);` - take slice of array

```php
<?php function sum_array( $no1, $no2 ) {
  
  $array = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100];
	 //Insert your code here 
	 
	if($no1<0 || $no2<0) return -1;
	if($no1<$no2){
		if (in_array($no1, $array) && $no2>100) 
			return $no1+$no2;
		elseif(in_array($no1, $array) && in_array($no2, $array)){
			$key1 = array_search($no1, $array);
			$key2 = array_search($no2, $array);
			echo "k1: ".$key1." k2: ".$key2."  <br>";
			$new_array = array_slice($array, $key1, $key2-$key1+1);
			print_r($new_array);
			return array_sum($new_array);
		}elseif(!in_array($no1, $array) && !in_array($no2, $array)) 
			return 0;
	}else{
		return 0;
	}
}
 ?>
```

```php
<?php function response( $input ) {
	 //Insert your code here 
	 $response = [];
	for ($i=1; $i<=$input; $i++) {
	  if ($i%3==0 && $i%5==0) {
		  array_push($response, 'FizzBuzz');
	  }else if($i%3==0){
		  array_push($response, 'Fizz');
	  }else if($i%5==0){
		  array_push($response, 'Buzz');
	  }else{
		  array_push($response, $i);
	  }
	}
	return $response;
}
 ?>
```

```php
<?php function towerBuilder( $n ) {
  $tower = new Tower($n);
  return $tower->build();
}

class Tower {
  protected $height;
  protected $tower = [];
  
  public function __construct(int $height) {
	$this->height = $height;
  }
  
  public function build() {
	for ($i = 0; $i < $this->height; $i++) {
	  $this->tower[] = $this->addFloor($i);
	}
	
	return $this->tower;
  }
  
  protected function addFloor(int $floor) {
	$result = "";
	// You can add parameters to these method calls
	$result .= $this->addMargin($floor);
	$result .= $this->addBricks($floor);
	$result .= $this->addMargin($floor);
	
	return $result;
  }
  // DO NOT MODIFY THE CODE ABOVE WITH THE EXCEPTION OF METHOD addFloor
  // Write addMargin and addBricks methods here
  public function addMargin($floor){
  
	$str = '';
	for($i=0; $i < $this->height-$floor-1 ;$i++){
		$str .= ' ';
	}
  	
	return $str;
  }
  
  public function addBricks($floor){
  	$str = '';
	for($i=0; $i <	2*$floor+1 ;$i++){
		$str .= '*';
	}
  	return $str;
  }
  
}
?>

```

```php
<?php function odd_even_product( $my_list ) {
	 //Insert your code here
	 
	  print_r($my_list);
	 $sum =0;
	 for($i=0;$i<count($my_list); $i++){
	 	$sum = $sum + intval($my_list[$i]);
	 }
	 
	 if($sum%2){
	 	return 0;
	 }
	 return $sum;
}
 ?>
 ```
