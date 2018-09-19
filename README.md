<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />

    <title>Page Title</title>
    <script src="js/jquery.min.js"></script>
    <script src="js/template-native.js"></script>
   
   <style>
       body{
           background-image: url(img/bg.jpg);
       }
   .container{
       width:700px;
       height: 500px;
       /*background-color: rgb(216, 186, 186);*/
       margin: auto;
   }
   .search{
       width:100%;
       height: 50px;
       /*background-color: green;*/
       text-align: center;
       transition: all 0.3s;
   }
 .search input{
       width: 140px;
       border:o;
       border-bottom: 3px solid#ff3300;
       background-color: transparent;
       font-size: 20px;
       outline: none;
       padding-left: 120px;
       padding-bottom: 2px;
       line-height: 35px;
       
   }
   .search .botton{
       width: 60px;
       height: 30px;
       display: inline-block;
       background-color: #ff3300;
       line-height: 30px;
       border-radius: 10%;
       box-shadow: 0 0 10px 0 #ff6600;
       opacity: 0.7;
       cursor:pointer;

   }
   .search:hover{transform: scale(1.1);

   }
   </style>
   
</head>
<body>
    <div class="container">
        <div class="search">
            <input type="text">
            <div class="botton">查询</div>
        </div>
        <table id="result">
            <!--<tr>
               <td>周一12月11日 实时4C° </td>
                <td><img src=""alt</td>



            </tr>-->


        </table>
    </div>
    <script type="text/template" id="templateid">
        <%for(var i=0;i<list.length;i++){%>
            <tr>
                <td><%= list[i].date %></td>
                <td><img src="<%= list[i].dayPictureUrl %>" alt=""></td>
                <td><img src="<%= list[i].nightPictureUrl %>" alt=""></td>
                <td><%= list[i].temperature %></td>
                <td><%= list[i].weather %></td>
                <td><%= list[i].wind %></td>  
                </tr>
            <% } %>
        </script>
    <script>
    $(".botton").click(function(){
        var cityName=$("input").val();
        $.ajax({
            url:"http://api.map.baidu.com/telematics/v3/weather",
            type:"get",
            data:{
                location:cityName,
                output:'json',
                ak:'6tYzTvGZSOpYB5Oc2YGGOKt8'
            },
            dataType:'jsonp',
            success:function(data){
                var weatherData=data.results[0],weather_data;
                var obj={
                    list:weatherData
                }
var html=template("templateid",obj);
console.log(obj);
$("#result").html(html);

            }

            



        })


    })
        </script>
</body>
</html>
