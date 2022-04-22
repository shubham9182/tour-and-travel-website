
<html>
<head>
		  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js"></script>
  <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
    <script type="text/javascript" >// <![CDATA[ 
        function loading(){
            $("#loading").show();
            $("#content").hide();       
        }
// ]]></script>
	<title>Alexa</title>
	
	<style>
		
    
 .heading { color: hsl(0, 0%, 3%);}  

.page th {
    background-color: #add8e6;
    color: rgb(51, 21, 21);
}
body {

  
	
  background-image: url("https://th.bing.com/th/id/R.23d210484ee2e67880b826cd414b8edd?rik=Nu41w%2brrPCUyoA&riu=http%3a%2f%2fpavbca.com%2fwalldb%2foriginal%2fd%2ff%2f4%2f482983.jpg&ehk=LHSLM1PxYrrtYbrmdhLvvR67%2bak%2bySUmcgRmFhR6Otg%3d&risl=&pid=ImgRaw&r=0");
  background-color: #cccccc;
  height: 755px;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  position: relative;
    
   
}
div#loading {
 
    width: 1700px;
    height: 35px;
    display: none;
    background: url('{{ url_for('static', filename='loading_bar.gif' ) }}') no-repeat;
    cursor: wait;
    
  }
  
.center {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 30px;}

.center1 {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 5px;
}


</style>
</head>
<body>
 <div>
	<h1 class="heading center"> </h1>
	<h1 class="heading center"> </h1>
	<form method="POST" action="/" enctype="multipart/form-data">	
	 <button type="submit" class="btn btn-primary button_add" style="margin: 0 auto;display: block; border-radius: 12px;width:100px;"><i class="fa fa-microphone"></i></button>
   <h1 class="heading center1">TAP TO SPEAK</h1>
   	</form>
	<form method="GET" action="/" enctype="multipart/form-data">
		

</body>
</html>

