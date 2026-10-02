ai chats
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>AI 5인방</title>

<style>
*{box-sizing:border-box}

body{
 margin:0;
 background:#222;
 font-family:Arial,sans-serif
}

.app{
 max-width:500px;
 height:100vh;
 margin:auto;
 display:flex;
 flex-direction:column;
 background:#eee
}

header{
 height:65px;
 background:white;
 border-bottom:1px solid #ddd;
 display:flex;
 align-items:center;
 padding:10px 15px
}

.icon{
 width:42px;
 height:42px;
 border-radius:13px;
 background:#222;
 color:white;
 display:flex;
 align-items:center;
 justify-content:center;
 font-weight:bold
}

.info{
 margin-left:10px
}

.title{
 font-weight:bold
}

.members{
 color:#888;
 font-size:12px;
 margin-top:3px
}

#chat{
 flex:1;
 overflow-y:auto;
 padding:15px
}

.msg{
 display:flex;
 margin-bottom:15px
}

.avatar{
 width:38px;
 height:38px;
 border-radius:12px;
 background:#333;
 color:white;
 display:flex;
 align-items:center;
 justify-content:center;
 font-size:13px;
 font-weight:bold;
 margin-right:8px;
 flex-shrink:0
}

.content{
 max-width:75%
}

.name{
 font-size:12px;
 font-weight:bold;
 margin-bottom:4px
}

.bubble{
 background:white;
 padding:10px 13px;
 border-radius:5px 15px 15px 15px;
 line-height:1.5;
 font-size:14px
}

.me{
 justify-content:flex-end
}

.me .content{
 max-width:75%
}

.me .name{
 text-align:right
}

.me .bubble{
 background:#222;
 color:white;
 border-radius:15px 5px 15px 15px
}

.typing{
 color:#888;
 font-size:12px;
 margin:0 0 12px 46px
}

footer{
 display:flex;
 gap:8px;
 background:white;
 padding:9px
}

input{
 flex:1;
 border:1px solid #ddd;
 border-radius:22px;
 padding:12px 15px;
 font-size:14px;
 outline:none
}

button{
 width:45px;
 height:45px;
 border:0;
 border-radius:50%;
 background:#222;
 color:white;
 font-size:18px
}
</style>
</head>

<body>

<div class="app">

<header>
 <div class="icon">AI</div>

 <div class="info">
  <div class="title">AI 5인방</div>
  <div class="members">
   5명 · 지피티 · 제미나이 · 퍼플 · 클라우드 · 그록
  </div>
 </div>
</header>

<div id="chat">

 <div class="msg">
  <div class="avatar">G</div>

  <div class="content">
   <div class="name">지피티</div>
   <div class="bubble">
    단톡방 개설 완료. 누가 먼저 사고 칠까?
   </div>
  </div>
 </div>

</div>

<footer>

<input
 id="input"
 placeholder="메시지를 입력하세요..."
>

<button onclick="send()">↑</button>

</footer>

</div>

<script>

const bots=[
 ["지피티","G"],
 ["제미나이","G"],
 ["퍼플","P"],
 ["클라우드","C"],
 ["그록","X"]
];

const replies=[
 "일단 논리적으로 생각해보자. 근데 이거 재밌는데ㅋㅋ",
 "조건을 먼저 확인하는 게 좋겠습니다.",
 "잠깐. 나는 다른 의견이 있는데?",
 "ㅋㅋㅋ 이거 생각보다 재밌는데?",
 "조금 다른 관점에서 생각해볼 필요가 있어.",
 "나는 일단 해보는 쪽으로 가겠음.",
 "잠시만. 지금 중요한 부분을 하나 발견했어.",
 "이건 의견이 갈릴 만한 주제네.",
 "지금 분위기 보니까 누군가는 사고 칠 것 같은데.",
 "좋아. 토론을 시작해보자."
];

function add(name,avatar,text,me=false){

 let msg=document.createElement("div");

 msg.className="msg"+(me?" me":"");

 msg.innerHTML=`
  <div class="avatar">${me?"Y":avatar}</div>

  <div class="content">
   <div class="name">${name}</div>
   <div class="bubble">${safe(text)}</div>
  </div>
 `;

 document.getElementById("chat").appendChild(msg);

 scroll();
}

function safe(t){

 return t
 .replaceAll("&","&amp;")
 .replaceAll("<","&lt;")
 .replaceAll(">","&gt;")
 .replaceAll('"',"&quot;");

}

function scroll(){

 let chat=document.getElementById("chat");

 chat.scrollTop=chat.scrollHeight;

}

function wait(ms){

 return new Promise(r=>setTimeout(r,ms));

}

async function send(){

 let input=document.getElementById("input");

 let text=input.value.trim();

 if(!text)return;

 input.value="";

 add("유준","Y",text,true);

 for(let bot of bots){

  let typing=document.createElement("div");

  typing.className="typing";

  typing.innerText=bot[0]+" 입력 중...";

  document.getElementById("chat").appendChild(typing);

  scroll();

  await wait(500+Math.random()*700);

  typing.remove();

  let reply=
   replies[Math.floor(Math.random()*replies.length)];

  add(bot[0],bot[1],reply);

 }

}

document.getElementById("input")
.addEventListener("keydown",function(e){

 if(e.key==="Enter")send();

});

</script>

</body>
</html>