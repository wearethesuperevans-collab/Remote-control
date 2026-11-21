
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<meta name="theme-color" content="#050805">
<title>HACKER OS</title>

<style>
*{box-sizing:border-box}
body{
 margin:0;background:#030603;color:#00ff66;
 font-family:monospace;min-height:100vh;
}
header{
 padding:20px;border-bottom:1px solid #124b25;
 display:flex;justify-content:space-between;align-items:center;
 background:#050b06;
}
.logo{font-size:22px;font-weight:bold;letter-spacing:3px}
.status{font-size:11px;color:#00ff66}
main{padding:15px;max-width:900px;margin:auto}
.panel{
 border:1px solid #145329;background:#071008;
 padding:15px;margin-bottom:15px;
 box-shadow:0 0 12px #00ff6610;
}
h3{font-size:13px;letter-spacing:2px;margin-top:0}
.devices{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.device{
 border:1px solid #17632f;padding:15px;
 background:#050a06;
}
.device strong{display:block;margin-bottom:12px}
.online{color:#00ff66;font-size:12px}
.offline{color:#ff4444;font-size:12px}
button{
 background:#071a0b;color:#00ff66;
 border:1px solid #00a83e;padding:12px;
 font-family:monospace;cursor:pointer;
}
button:active{background:#00ff66;color:black}
.actions{display:grid;grid-template-columns:1fr 1fr;gap:8px}
input{
 width:100%;padding:14px;background:#020502;
 border:1px solid #17632f;color:#00ff66;
 font-family:monospace;outline:none;
}
#terminal{
 height:220px;overflow-y:auto;background:#020502;
 padding:12px;font-size:12px;line-height:1.7;
 border:1px solid #124b25;
}
.line{margin-bottom:4px;overflow-wrap:anywhere}
.muted{color:#6a9a75}
.green{color:#00ff66}
.red{color:#ff4545}
.yellow{color:#d6d65b}
.command-row{display:flex;gap:7px;margin-top:10px}
.command-row input{min-width:0;flex:1}
footer{text-align:center;padding:25px;color:#477b53;font-size:11px}
.scan{
 height:2px;background:#00ff66;
 animation:scan 3s linear infinite;
 box-shadow:0 0 12px #00ff66;
}
@keyframes scan{
 0%{transform:translateY(0)}
 50%{transform:translateY(180px)}
 100%{transform:translateY(0)}
}
@media(max-width:420px){
 .devices{grid-template-columns:1fr}
 .logo{font-size:18px}
}
</style>
</head>

<body>

<header>
 <div class="logo">HACKER_OS<span class="green">_</span></div>
 <div class="status">● SYSTEM ACTIVE</div>
</header>

<main>

<div class="panel">
 <h3> SYSTEM OVERVIEW //</h3>
 <div class="muted">DUAL DEVICE CONTROL NETWORK</div>
 <p>NETWORK: <span class="green">LOCAL INTERFACE</span></p>
 <p>SECURITY: <span class="green">AUTHENTICATION REQUIRED</span></p>
 <p>MODE: <span class="yellow">DEMO</span></p>
</div>

<div class="panel">
 <h3> CONNECTED DEVICES //</h3>
 <div class="devices">
  <div class="device">
   <strong>IPHONE</strong>
   <div id="phoneStatus" class="offline">● NOT CONNECTED</div>
   <p class="muted">DEVICE 01</p>
   <button onclick="connectDevice('phone')">CONNECT</button>
  </div>

  <div class="device">
   <strong>IPAD</strong>
   <div id="ipadStatus" class="offline">● NOT CONNECTED</div>
   <p class="muted">DEVICE 02</p>
   <button onclick="connectDevice('ipad')">CONNECT</button>
  </div>
 </div>
</div>

<div class="panel">
 <h3> COMMAND CENTER //</h3>
 <div class="actions">
  <button onclick="runCommand('HELP')">HELP</button>
  <button onclick="runCommand('STATUS')">SYSTEM STATUS</button>
  <button onclick="runCommand('DEVICES')">SCAN DEVICES</button>
  <button onclick="runCommand('NETWORK')">NETWORK INFO</button>
  <button onclick="runCommand('TIME')">SYSTEM TIME</button>
  <button onclick="runCommand('CLEAR')">CLEAR TERMINAL</button>
 </div>
</div>

<div class="panel">
 <h3> TERMINAL // ROOT ACCESS SIMULATION</h3>
 <div id="terminal">
  <div class="line green">HACKER_OS TERMINAL v1.0</div>
  <div class="line muted">Initializing interface...</div>
  <div class="line green">Interface ready.</div>
  <div class="line yellow">Type HELP to view commands.</div>
 </div>

 <div class="command-row">
  <input id="commandInput" placeholder="Enter command..." autocomplete="off">
  <button onclick="submitCommand()">EXECUTE</button>
 </div>
</div>

<div class="panel">
 <h3> QUICK CONTROLS //</h3>
 <div class="actions">
  <button onclick="runCommand('PING PHONE')">PING IPHONE</button>
  <button onclick="runCommand('PING IPAD')">PING IPAD</button>
  <button onclick="runCommand('PAIR')">PAIR DEVICES</button>
  <button onclick="runCommand('LOCK')">LOCK INTERFACE</button>
 </div>
</div>

</main>

<footer>
 HACKER_OS // DUAL DEVICE EDITION<br>
 SECURE CONNECTION REQUIRED
</footer>

<script>
const terminal=document.getElementById("terminal");
const devices={phone:false,ipad:false};

function log(message,type="green"){
 const line=document.createElement("div");
 line.className="line "+type;
 line.textContent="> "+message;
 terminal.appendChild(line);
 terminal.scrollTop=terminal.scrollHeight;
}

function connectDevice(device){
 devices[device]=!devices[device];
 const status=document.getElementById(
  device==="phone"?"phoneStatus":"ipadStatus"
 );

 if(devices[device]){
  status.textContent="● DEMO CONNECTED";
  status.className="online";
  log(device.toUpperCase()+" demo connection enabled.");
 }else{
  status.textContent="● NOT CONNECTED";
  status.className="offline";
  log(device.toUpperCase()+" demo connection disabled.","yellow");
 }
}

function runCommand(command){
 const cmd=command.toUpperCase();

 if(cmd==="CLEAR"){
  terminal.innerHTML="";
  return;
 }

 log(cmd);

 switch(cmd){
  case "HELP":
   log("AVAILABLE COMMANDS:");
   log("STATUS / DEVICES / NETWORK / TIME");
   log("PING PHONE / PING IPAD / PAIR / LOCK");
   break;

  case "STATUS":
   log("HACKER_OS INTERFACE: ACTIVE");
   log("PHONE DEMO: "+(devices.phone?"CONNECTED":"DISCONNECTED"));
   log("IPAD DEMO: "+(devices.ipad?"CONNECTED":"DISCONNECTED"));
   log("REAL DEVICE CONTROL: NOT CONFIGURED","yellow");
   break;

  case "DEVICES":
   log("IPHONE: "+(devices.phone?"DEMO ONLINE":"NOT CONNECTED"));
   log("IPAD: "+(devices.ipad?"DEMO ONLINE":"NOT CONNECTED"));
   break;

  case "NETWORK":
   log("BROWSER NETWORK STATUS: "+navigator.onLine);
   log("REMOTE RELAY: NOT CONFIGURED","yellow");
   break;

  case "TIME":
   log(new Date().toLocaleString());
   break;

  case "PING PHONE":
   log(devices.phone?"PHONE DEMO RESPONDED":"PHONE NOT CONNECTED",
    devices.phone?"green":"red");
   break;

  case "PING IPAD":
   log(devices.ipad?"IPAD DEMO RESPONDED":"IPAD NOT CONNECTED",
    devices.ipad?"green":"red");
   break;

  case "PAIR":
   if(devices.phone&&devices.ipad){
    log("BOTH DEMO DEVICES ARE MARKED CONNECTED.");
   }else{
    log("CONNECT BOTH DEVICE DEMOS FIRST.","yellow");
   }
   break;

  case "LOCK":
   log("INTERFACE LOCK REQUESTED. NO DEVICE ACTION TAKEN.","yellow");
   break;

  default:
   log("UNKNOWN COMMAND. TYPE HELP.","red");
 }
}

function submitCommand(){
 const input=document.getElementById("commandInput");
 const command=input.value.trim();
 if(!command)return;
 input.value="";
 runCommand(command);
}

document.getElementById("commandInput")
.addEventListener("keydown",e=>{
 if(e.key==="Enter")submitCommand();
});

</script>
</body>
</html>
