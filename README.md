# Restdata-table

HTML REST DATA TABLE


   <html>
  <head>
  	<title>Person Information</title>
  	<meta charset="UTF-8">	<link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.10.19/css/jquery.dataTables.min.css">
	<script type="text/javascript" language="javascript" src="https://code.jquery.com/jquery-3.3.1.js"></script>
	<script type="text/javascript" language="javascript" src="https://cdn.datatables.net/1.10.19/js/jquery.dataTables.min.js"></script>
    <script>
      $(document).ready(function(){
    	 var baseurl = "http://localhost:8080/persons";
    	 var xmlhttp = new XMLHttpRequest();
    	 xmlhttp.open("GET",baseurl+"/all",true);
    	 xmlhttp.onreadystatechange = function(){
    		 if(xmlhttp.readyState==4 && xmlhttp.status ==200){
    			 var persons = JSON.parse(xmlhttp.responseText);
    			 $("#example").DataTable({
    				data:persons,
    				"columns":[
    					{"data":"id"},
    					{"data":"firstName"},
    					{"data":"lastName"},
    					{"data":"age"}
    				]
    			 });
    		 }
    	 };
    	 xmlhttp.send();
      });
    </script>  
  </head>
  <body>
    <table id="example" class="display" style="width:100%">
    <thead>
	    <tr>
	      <th>Id</th>
	      <th>First Name</th>
	      <th>Last Name</th>
	      <th>Age</th>
	    </tr>
    </thead>
    <tfoot>
	    <tr>
	      <th>Id</th>
	      <th>First Name</th>
	      <th>Last Name</th>
	      <th>Age</th>
	    </tr>
    </tfoot>
    </table>
  </body>
</html>



           <html>
  <head>
    <title> Person Information </title>
    <meta charset="UTF-8">
    <script>
      var baseurl = "http://localhost:8080/persons";
      function loadPersons(){
        var xmlhttp = new XMLHttpRequest();
        xmlhttp.open("GET",baseurl + "/all",true);
        xmlhttp.onreadystatechange = function() {
          if(xmlhttp.readyState ===4 && xmlhttp.status ===200){
            var persons = JSON.parse(xmlhttp.responseText);
            var tbltop = `<table>
			    <tr><th>Id</th><th>First Name</th><th>Last Name</th><th>Age</th></tr>`;
            //main table content we fill from data from the rest call
            var main ="";
            for (i = 0; i < persons.length; i++){
              main += "<tr><td>"+persons[i].id+"</td><td>"+persons[i].firstName+"</td><td>"+persons[i].lastName+"</td><td>"+persons[i].age+"</td></tr>";
            }
            var tblbottom = "</table>";
            var tbl = tbltop + main + tblbottom;
            document.getElementById("personinfo").innerHTML = tbl;
          }
        };
        xmlhttp.send();
      }
      window.onload = function(){
        loadPersons();
      }
    </script>
  </head>
  <body>
    <div id="personinfo"> </div>
  </body>
</html>
