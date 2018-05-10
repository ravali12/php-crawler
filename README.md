<?php
$crawl = "http://clv0.com/angali/demo.html";
$visited = array();

function crawl_alllinks($url){
	global $visited;
	
	$rec = new DOMDocument();
	$rec->loadHTML(file_get_contents($url));
	
	
	$alllinks = $rec->getElementsByTagName("a");
	
	
	foreach($alllinks as $link){
		
		 $finallist = $link->getAttribute("href");
		 
		 if (substr($finallist,0,1)=="/" && substr($finallist,0,2)!="//"){
		 	
		 	$finallist = $finallist;
		
		} elseif (substr($finallist,0,2)=="//"){
			
			$finallist = parse_url($url)["scheme"].":".$finallist;
		}
		
		if (!in_array($finallist, $visited)){
			
			$visited[] = $finallist;
		
		echo $finallist."\n";
		}
	}
	
	
}
crawl_alllinks("http://cnn.com");

print_r($visited);
