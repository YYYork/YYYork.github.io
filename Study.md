<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
	</head>
	<script>
		window.onload = function(){
			var oBtn = document.getElementById("btn");
			var oLists = document.getElementById("lists");
			oBtn.onclick = function(){
				var oLi = document.createElement("li");
				oLi.innerHTML = "哈哈";
				oLists.appendChild(oLi);
			}
			
		}
	</script>
	<body>	
    <h1>York的学习记录</h1>

    <h2>2021/9/4</h2>

    <p><img src="icons/QQ截图20210904122241.png" alt="2021/9/4" title="" /></p>
	</body>
</html>
