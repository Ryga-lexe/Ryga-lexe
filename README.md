- 👋 Hi, I’m @Ryga-lexe
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Ryga-lexe/Ryga-lexe is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
<!DOCTYPE html>
<html>
<head>
	<link rel="stylesheet" type="text/css" href="../style/qstyle.css">
	<title>Answers</title>
</head>
<body>
	<div id="big">Simple StackExchange</div>
	<div  class="mediumbaru">	
	<?php $conn = mysqli_connect("localhost", "root", "", "stackoverflow");
		if(!$conn) 
			die("connection failed : " . $conn->connect_error);
		$sql = "SELECT * FROM questions WHERE no=".$_GET['id'];
		$result = mysqli_query($conn,$sql);
		while($row = mysqli_fetch_assoc($result)) {
			echo "<div id=\"m1\">".$row['question']."</div>
			<div class=\"div1\">
				<div class=\"ans2\" id=\"voting\">
					<div class=\"ans4\">
					<span onclick=\"vote('question',".$row['no'].",0,'up')\">▲</span>
					<span id=\"qvote\">".$row['vote']."</span>
					<span onclick=\"vote('question',".$row['no'].",0,'down')\")>▼</span>
					</div>
				</div>
				<div class=\"ans3\">
					<div class=\"div6\">".$row['content']."</div>
					<div class=\"div7\">asked by ".$row['name']." at ".$row['time']." | <a href=\"../questions/editquestions.php?id=".$row['no']."\">edit</a> | <a href=\"../questions/deletequestions.php?id=".$row['no']."\">delete</a></div>
				</div>	
			</div>
			";
		}
		$sql = "SELECT COUNT(*) AS SHIT FROM answers WHERE question_no=".$_GET['id'];
		$result = mysqli_query($conn,$sql);
		while($row = mysqli_fetch_assoc($result)) {
			echo "<div id=\"m1\">".$row['SHIT']. " Answers</div>";
		}
	echo "<div> ";
		$sql = "SELECT * FROM answers WHERE question_no=".$_GET['id'];
		$result = mysqli_query($conn,$sql);
		while($row = mysqli_fetch_assoc($result)) {
			echo "
			<div class=\"div1\">
				<div class=\"ans2\" id=\"voting\">
					<div class=\"ans4\">
					<span onclick=\"vote('answer',".$row['question_no'].",".$row['no'].",'up')\">▲</span>
					<span id=\"avote".$row['no']."\">".$row['vote']."</span>
					<span onclick=\"vote('answer',".$row['question_no'].",".$row['no'].",'down')\">▼</span>
					</div>
				</div>
				<div class=\"ans3\">
					<div class=\"div6\">".$row['content']."</div>
					<div class=\"div7\">answered by ".$row['name']." at ".$row['time']."</div>
				</div>	
			</div>
			";
		}
		if($conn->query($sql) == FALSE) {
			echo "error : ". $sql . "<br>". $conn->error;
		}
	$conn -> close(); ?>
	</div> 
	<div id="m2">Your Answer</div>
	<form name="makeanswer" method="post" action="sendanswers.php" onsubmit="return validateFormAnswer(this);">
		 <input type="text" name="name" placeholder="Name" class="medium">
		 <input type="email" name="email" placeholder="Email" class="medium">
		 <textarea type="text" name="content" placeholder="Content" class="medium" id="content"></textarea> 
		 <input type="hidden" name="id" value="<?php echo $_GET['id'] ?>"> 
		 <input type="submit" value="Post" id="button">
	 </form>
	 </div>
</body>
	<script src="../script/validation.js"></script>
</html>
