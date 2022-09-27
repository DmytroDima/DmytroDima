!DOCTYPE html>
<html>
    <style>
            body{
    margin:0;
    background:#222;
    text-align:center;
    color:#fff;
}
h1,h2{
    font-family:'Patua One';
    font-weight:400;
    margin:0;
}
.grid{
    background:#222;
    display:flex;
    width:100vw;
    height:100vw;
    flex-wrap:wrap;
    justify-content:center;
    margin:6px 0;
    font-family:arial;
    font-weight:600;
}
.grid div{
    width:9%;
    height:9%;
    display:flex;
    align-items:center;
    justify-content:center;
    background:#0066ff;
    font-size:12px;
    margin:1px;
    border-radius:5px;
    transition:background .2s linear;
}
.restart{
    margin-top: 10px;
    font-family:'Patua One';
    font-size:26px;
    padding: 10px 14px;
    background: #333;
    border-radius:8px;
    display:inline-block;
}
.link{
    margin-top: 10px;
    font-family:'Patua One';
    font-size:26px;
    padding: 10px 14px;
    border-radius:8px;
    display:inline-block;
}

//+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

button{
    cursor:pointer;
}
//body{
//    background-color:rgba(0,0,0,.8);
//}
.login{
    position:absolute;
    top:50%;
    left:50%;
    transform:translate(-50%,-50%);
    width:50%;
    background:#2156f3;
    color:white;
    padding:15px;
    border-radius:10px;
    border:none;
    outline:none;
}
.modal{
    position: absolute;
    top: -200%;
    left: 50%;
    transform: translateX(-50%);
    background-color: rgb(104, 104, 104); //Бывший цвет (50,2,10)
    width: 80%;
    height: 80%;
    padding: 10px 15px 10px;
    color: white;
    border-radius: 5px;
    transition: 1s ease-out;
}
.header{
    font-size: 20px;
    text-align: center;
}
.header span{
    position: absolute;
    top: 0;
    right:0;
    padding: 5px 10px;
    font-size: 30px;
    font-weight: bolder;
    color: white;
    cursor: pointer;
}
.header img{
    width: 80px;
    height: 80px;
    border-radius: 50%;
}

.body{
    margin: 10px 0;
    font-weight: bold;
    position: relative;
}
.body input{
    min-width: 20%;
    width: 95%;
    padding: 10px;
    border-radius: 5px;
    border: none;
    margin: 5px 0;
}
.body input[type=submit]{
    width: 30%;
    background: #2196f3;
    color: white;
    font-size: 16px;
    font-weight: 500;
    transform: translateX(120%);
    cursor: pointer;
}
.footer{
    margin: 10px;
}
.footer button{
    position: relative;
    background-color: rgba(33, 150, 243); //(255,50,90,.9);
    border: none;
    width: 50%;
    left: 50%;
    transform:translateX(-100%);
    padding: 10px;
    margin: 0 20px 20px;
    border-radius: 5px;
    color: white;
}

@media screen and (max-width:768px){
    .modal{
        width:85%;
        height:auto;
    }
}
//-----------------------------------------------------------
    </style>   
    <head>
        <script src="https://code.jquery.com/jquery-3.1.1.js"></script>
        <link href="https://fonts.googleapis.com/css?family=Patua+One" rel="stylesheet">
        <!-- +++++++++++++++++++ -->
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>modal</title>
        <link rel="stylesheet" href="css/bootstrap.css" type="text/css">
        <!-- ------------------- -->
    </head>
    <body>
        <h1><span id="headline"></span></h1>
        <h2><span id="rec"></span></h2>
        <h2>Your attempts: <span id="att">Press on Restart😝</span></h2>
        <h2>Remaining attempts: <span id="ratt">Press on Restart😜</span></h2>
        <div class="grid"></div>
        <div class="restart">Restart</span></div>
        <form>
        <a class="link" href="https://github.com/BohdanFW/guess-the-number/blob/main/index.htm" target="_blank">Show code</span></a>
        </form>
        <!-- ++++++++++++++++++++++++++++++++++++ -->
            <div class="modal" id="mymodal">
            <div class="header">
                <h2 id="message_text1"></h2><hr>
                <h2 id="message_text2"></h2>
                <h2 id="message_text3"></h2>
                <span class="Close" onclick="modalClose()">&times;</span> 
            </div>
            <div class="footer">
                <button class="Close" onclick="okey();"> Yes </button>
            </div>
        </div>

        <!-- ------------------------------------ -->
    </body>
    <script>
          

        attempts = 0; //Переменная для хранения количества использованных попыток
coins = 0; //Переменная для хранения щета етого раунда
flag1 = 3; //Флажок для Отключения кнопок ввода
record = 0;
$("document").ready(function (){
 $("#headline").html("GUESS THE NUMBER"); //Выводит текст GUESS THE NUMBER
 number = Math.floor(Math.random()*99)+1;
 for(i=1; i<=100; i++){
  $(".grid").append("<div>"+i+"</div>");
 }

 $("#message_text1").html("Welcome to guess the number game!");
 $("#message_text2").html("I will guess the number, and you need to guess it. Be careful, you have only 7 attempts in one round! But don't worry, I'll tell you which way to guess.<hr>");
 $("#message_text3").html("Let's start?");
 modal();

 $(".grid div").click(function(){
	 
     if(flag1==0){
	 openFullscreen();
         if(attempts<7){
             ++attempts;
             $("#att").html(attempts);
             $("#ratt").html(7-attempts);
             dnum = $(this).text();
                 if(dnum<number){
                     for(i=1; i<=dnum; i++){
                         $(".grid div:nth-child("+i+")").css("background","#2f2f2f");
                     }  
                 }
             else if(dnum>number){
                 for(i=100; i>=dnum; i--){
                     $(".grid div:nth-child("+i+")").css("background","#2f2f2f");
                 }
             }
             else if(dnum==number){
                 flag1=1;
                 $(this).css("background","green");
                 $("#message_text1").html("Congratulations! You guessed the number with "+attempts+" attempts");
                 $("#message_text2").html("Play more?");
                 $("#message_text3").html("");
                 modal();
                 coins = coins+7-attempts;
                 if(coins==1){
                     $("#headline").html("You have "+coins+" coin"); //Выводит заработаные баллы, вместо GUESS THE NUMBER
                 }
                 else{
                     $("#headline").html("You have "+coins+" coins"); //Выводит заработаные баллы, вместо GUESS THE NUMBER
                 }
             }
         }
             else{
             flag1 = 2;
             coins = coins+7-attempts;
             $("#message_text1").html("You have used all attempts. Your result is "+coins); // Прписывает "You have used all attempts. Your result is" и в конце добавляет баллы
             if(coins>record){
                 $("#message_text2").html("Congratulations! You just broke your record!👑 By " +(coins-record)+ " points! <hr>"); // Прписывает "You have used all attempts. Your result is" и в конце добавляет баллы
                 $("#message_text3").html("Let's set another record, shall we?");
                 record = coins;
                 $("#rec").html("Your record: " +record+ "👑"); //Выводит на экран рекорд
             }
             else{
                 $("#message_text2").html("");
                 $("#message_text3").html("Do you want to play more?");
             }
             modal();  // Обращаемся к функции вывода сообщения
             coins=0;
             $("#headline").html("You have "+coins+" coins"); //Выводит заработаные баллы, вместо GUESS THE NUMBER
             }
     }

 });
 $(".restart").click(function(){
     if(attempts>0){
         again();
         coins=0;
         $("#headline").html("You have "+coins+" coins"); //Выводит заработаные баллы, вместо GUESS THE NUMBER

     }
 });
});

 function again(){
	   openFullscreen();
       attempts = 0;
       $("#att").html(attempts);
       $("#ratt").html(7);
       number = Math.floor(Math.random()*99)+1;
       for(i=1; i<=100; i++){
           $(".grid div").css("background","#0066ff");
           flag1=0;
       }    
 }
function okey(){
    again();
    modalClose();
}
 var elem = document.documentElement;
function openFullscreen() {
if (elem.requestFullscreen) {
    elem.requestFullscreen();
  } else if (elem.webkitRequestFullscreen) { /* Safari */
    elem.webkitRequestFullscreen();
  } else if 
(elem.msRequestFullscreen) { /* IE11 */
    elem.msRequestFullscreen();
  }
}
//++++++++++++++++++++++++++++++++++++++++++++++

var login = document.getElementsByClassName('login')[0];
var closeIcon = document.getElementsByClassName('Close')[0];
var closeBtn = document.getElementsByClassName('Close')[1];
function modal() {
    var modal = document.getElementsByClassName('modal')[0];
    modal.style.top = "0";
}
function modalClose() {
    var modal = document.getElementsByClassName('modal')[0];
    modal.style.top = "-200%";
}
//----------------------------------------------

</script>
</html>
