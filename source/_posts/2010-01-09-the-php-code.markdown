---
layout: post
title: "一段 PHP 程式碼"
date: 2014-05-12 23:28
comments: true
categories: 
---

PHP 流程控制替代語法:
<!-- more -->
{% codeblock %}
<?php
for ($i=0;$i<=10;$i++):
	echo $i++;
endfor;

for($j=0;$j<=100;$j++) {
	echo $j;
}
# =======================
foreach($todo as $item):
	echo $item;
endforeach;

foreach($todo as $list){
	echo $list;
}
# =======================
if ($username=='boss'):
	echo 'goods';
elseif ($username=='joe'):
	echo 'soso';
else:
	echo 'OMG';
endif;

if ($username=='bill') {
	echo 'Happy';
} else if ($username=='mary') {
	echo 'Beautiful';
} else {
	echo 'So Good';
}
# =======================
while(true):
	echo "Luck!";
endwhile;

while($i<=7) {
	echo "Week";
}	
# =======================
switch($func):
	case 'about':
		echo 'about page';
		break;
	case 'dashborad':
		echo 'DashBorad Page';
		break;
	default:
		echo 'Login Page';
		break;
endswitch;

switch($i) {
	case 1:
		echo '一';
		break;
	case 2:
		echo '二';
		break;
	case 3:
		echo '三';
		break;
	default:
		echo '零';
		break;
}		

?>
{% endcodeblock %}

夾在中間能夠正常!

