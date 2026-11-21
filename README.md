
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#030907">
<title>HACKER OS 3.0</title>

<style>
:root{
--bg:#030907;
--panel:rgba(9,24,16,.82);
--green:#48ffa0;
--green2:#00d878;
--border:#20583b;
--text:#e2ffed;
--muted:#83a994;
--red:#ff536b;
--blue:#50cfff;
--purple:#c28aff;
}
*{box-sizing:border-box}
body{
margin:0;
background:
radial-gradient(ellipse at 15% 0%,#123b24 0%,transparent 40%),
radial-gradient(ellipse at 90% 85%,#092c1c 0%,transparent 38%),
#030907;
background-attachment:fixed;
color:var(--text);
font-family:Consolas,Monaco,monospace;
min-height:100vh;
overflow-x:hidden;
}
button,input,textarea,select{font:inherit}
button{cursor:pointer}
#matrix{
position:fixed;inset:0;width:100%;height:100%;
z-index:-3;opacity:.13;pointer-events:none;
}
body:before{
content:"";
position:fixed;inset:0;z-index:20;pointer-events:none;
background:repeating-linear-gradient(
transparent 0px,transparent 3px,#48ffa006 4px
);
}
header{
position:sticky;top:0;z-index:30;
background:rgba(3,10,7,.88);
backdrop-filter:blur(22px);
border-bottom:1px solid #37ff8b50;
box-shadow:0 8px 35px #00ff8818;
}
.top{
display:flex;align-items:center;justify-content:space-between;
padding:15px 20px;gap:12px;flex-wrap:wrap;
}
.logo{
font-size:23px;font-weight:bold;letter-spacing:5px;
color:var(--green);
text-shadow:0 0 12px var(--green),0 0 30px #00ff8850;
}
.logo span{color:white}
.status{font-size:11px;color:var(--green);text-shadow:0 0 10px var(--green)}
nav{
display:flex;gap:7px;padding:0 13px 13px;overflow-x:auto;
scrollbar-width:thin;
}
nav button{
background:linear-gradient(145deg,#10251a,#07120b);
border:1px solid #245b3b;color:var(--muted);
padding:10px 13px;border-radius:7px;
white-space:nowrap;font-size:11px;transition:.2s;
}
nav button:hover,nav button.active{
color:var(--green);border-color:var(--green);
background:linear-gradient(135deg,#164b2c,#092516);
box-shadow:0 0 15px #00ff8830;
}
main{max-width:1400px;margin:auto;padding:22px}
.page{display:none}
.page.active{display:block;animation:appear .35s ease}
@keyframes appear{
from{opacity:0;transform:translateY(9px)}
to{opacity:1;transform:translateY(0)}
}
h1{
font-size:clamp(23px,3vw,35px);
color:var(--green);letter-spacing:3px;
text-shadow:0 0 18px #00ff8840;
margin:0 0 9px;
}
h2{
font-size:13px;color:var(--green);
letter-spacing:2px;margin:0 0 14px;
}
h3{font-size:13px;margin:0 0 9px}
p{color:var(--muted);font-size:12px;line-height:1.6}
.small{font-size:11px;color:var(--muted)}
.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
gap:14px;
}
.wide{grid-template-columns:repeat(auto-fit,minmax(290px,1fr))}
.panel{
position:relative;overflow:hidden;min-width:0;
padding:17px;border-radius:13px;
background:linear-gradient(145deg,rgba(14,34,23,.96),rgba(4,13,8,.97));
border:1px solid #267448;
box-shadow:0 8px 25px #0008,inset 0 1px 0 #ffffff0a;
transition:.25s;
}
.panel:before{
content:"";position:absolute;top:0;left:12%;width:76%;height:1px;
background:linear-gradient(90deg,transparent,#59ffab,transparent);
}
.panel:hover{
border-color:var(--green);
box-shadow:0 12px 32px #0009,0 0 20px #00ff8820;
transform:translateY(-2px);
}
.stat{
font-size:29px;color:var(--green);font-weight:bold;
text-shadow:0 0 15px #00ff8860;margin:12px 0;
}
.meter{
height:10px;background:#101e16;border:1px solid #245b39;
border-radius:20px;overflow:hidden;margin:9px 0;
}
.meter div{
height:100%;width:30%;
background:linear-gradient(90deg,#00a94e,#43ff9a,#c0ffda);
box-shadow:0 0 12px #00ff88;
transition:width .4s;
}
button.action{
background:linear-gradient(135deg,#123a24,#071b10);
border:1px solid #2c9c5b;color:var(--green);
padding:10px 13px;border-radius:7px;margin:4px 3px 4px 0;
transition:.2s;font-size:11px;
}
button.action:hover{
background:linear-gradient(135deg,#1c6038,#0b2a18);
box-shadow:0 0 16px #00ff8840;
transform:translateY(-2px);
}
button.action:active{transform:scale(.97)}
button.danger{border-color:var(--red);color:var(--red)}
input,textarea,select{
width:100%;background:rgba(2,9,5,.9);
border:1px solid #245a39;border-radius:8px;
color:var(--text);padding:11px;margin:5px 0;
}
input:focus,textarea:focus,select:focus{
outline:none;border-color:var(--green);
box-shadow:0 0 14px #00ff8830;
}
textarea{min-height:95px;resize:vertical}
.row{display:flex;gap:8px;align-items:center;flex-wrap:wrap}
.row>*{flex:1}
.row button{flex:0 0 auto}
.output{
background:#020704;border:1px solid #1d5736;
padding:12px;border-radius:8px;min-height:40px;
white-space:pre-wrap;overflow-wrap:anywhere;
color:var(--green);font-size:12px;margin-top:9px;
}
.terminal{
background:rgba(0,5,2,.95);border:1px solid #247445;
border-radius:10px;padding:15px;height:350px;
overflow:auto;font-size:12px;
box-shadow:inset 0 0 25px #00ff8809;
}
.termline{margin:0 0 8px;white-space:pre-wrap;overflow-wrap:anywhere}
.termgreen{color:var(--green)}
.termblue{color:var(--blue)}
.termred{color:var(--red)}
.task{
display:flex;align-items:center;gap:8px;
border-bottom:1px solid var(--border);padding:9px 0;font-size:12px;
}
.task span{flex:1}
.done{text-decoration:line-through;color:var(--muted)}
.toolcard{cursor:pointer;transition:.2s}
.toolcard:hover{border-color:var(--green);transform:translateY(-4px)}
.symbol{font-size:25px;color:var(--green);margin-bottom:12px;text-shadow:0 0 12px var(--green)}
.pill{
display:inline-block;border:1px solid var(--border);
border-radius:20px;padding:4px 9px;color:var(--muted);
font-size:10px;margin:3px;
}
canvas.chart{width:100%;height:110px;background:#030705;border-radius:7px}
iframe{width:100%;height:240px;background:white;border:1px solid var(--border);border-radius:7px}
footer{text-align:center;padding:30px;color:var(--muted);font-size:10px}
#toast{
position:fixed;bottom:20px;left:50%;transform:translateX(-50%);
background:#12351f;color:var(--green);border:1px solid var(--green);
padding:12px 18px;border-radius:8px;display:none;z-index:60;
box-shadow:0 0 20px #00ff8830;font-size:12px;
}
@media(max-width:600px){
main{padding:12px}.top{padding:12px}
.logo{font-size:18px;letter-spacing:3px}
.grid,.wide{grid-template-columns:1fr}
.panel{padding:14px}
}
</style>
</head>

<body>
<canvas id="matrix"></canvas>

<header>
<div class="top">
<div class="logo">HACKER<span>_OS</span></div>
<div class="status" id="headerStatus">● SYSTEM ONLINE</div>
</div>
<nav id="nav">
<button class="active" data-page="dashboard">⌂ HOME</button>
<button data-page="terminal">⌘ TERMINAL</button>
<button data-page="tools">⚙ TOOLS</button>
<button data-page="security">◈ SECURITY</button>
<button data-page="developer">⌨ DEV LAB</button>
<button data-page="network">◎ NETWORK</button>
<button data-page="files">▤ FILES</button>
<button data-page="organizer">▣ ORGANIZER</button>
<button data-page="media">♫ MEDIA</button>
<button data-page="assistant">✧ ASSISTANT</button>
<button data-page="settings">⚙ SETTINGS</button>
<button data-page="secret">◉ SECRET</button>
</nav>
</header>

<main>

<section class="page active" id="dashboard">
<h1>COMMAND CENTER</h1>
<p>WELCOME BACK, OPERATOR. ALL SYSTEMS READY.</p>
<div class="grid">
<div class="panel"><h2>LOCAL TIME</h2><div class="stat" id="clock">--:--:--</div><div class="small" id="date"></div></div>
<div class="panel"><h2>SESSION UPTIME</h2><div class="stat" id="uptime">00:00:00</div><div class="small">Current session</div></div>
<div class="panel"><h2>NETWORK STATUS</h2><div class="stat" id="connection">ONLINE</div><div class="small">Browser connection status</div></div>
<div class="panel"><h2>LOCAL STORAGE</h2><div class="stat">READY</div><div class="small">Local browser data</div></div>
</div>
<br>
<div class="grid wide">
<div class="panel">
<h2>SYSTEM PERFORMANCE</h2>
<div class="row"><span class="small">CPU SIMULATION</span><b id="cpuText">--%</b></div>
<div class="meter"><div id="cpuBar"></div></div>
<div class="row"><span class="small">RAM SIMULATION</span><b id="ramText">--%</b></div>
<div class="meter"><div id="ramBar"></div></div>
<p>Illustrative dashboard readings, not actual hardware measurements.</p>
</div>
<div class="panel">
<h2>QUICK ACCESS</h2>
<div class="grid">
<button class="action" onclick="page('terminal')">TERMINAL</button>
<button class="action" onclick="page('tools')">TOOLS</button>
<button class="action" onclick="page('security')">SECURITY</button>
<button class="action" onclick="page('developer')">DEV LAB</button>
<button class="action" onclick="page('organizer')">TASKS</button>
<button class="action" onclick="page('media')">MEDIA</button>
</div>
</div>
</div>
<br>
<div class="grid wide">
<div class="panel">
<h2>ACTIVITY MONITOR</h2>
<div id="activity" class="small"></div>
</div>
<div class="panel">
<h2>VISUAL SYSTEM MONITOR</h2>
<canvas class="chart" id="systemChart" width="500" height="120"></canvas>
</div>
</div>
<br>
<div class="panel">
<h2>PERSONAL WIDGETS</h2>
<div id="dashboardWidgets" class="grid"></div>
<button class="action" onclick="page('widgets')">CUSTOMIZE DASHBOARD</button>
</div>
</section>

<section class="page" id="terminal">
<h1>COMMAND TERMINAL</h1>
<p>Local demo terminal. Type HELP to see commands.</p>
<div class="terminal" id="terminalOutput"></div>
<div class="row">
<input id="commandInput" placeholder="operator@hacker-os:~$">
<button class="action" onclick="runCommand()">EXECUTE</button>
</div>
<button class="action" onclick="clearTerminal()">CLEAR</button>
<button class="action" onclick="terminalCommand('HELP')">HELP</button>
</section>

<section class="page" id="tools">
<h1>TOOL DATABASE</h1>
<p>SEARCH THE HACKER OS TOOL COLLECTION.</p>
<input id="toolSearch" placeholder="Search tools..." oninput="filterTools()">
<div class="row">
<button class="action" onclick="filterCategory('all')">ALL</button>
<button class="action" onclick="filterCategory('text')">TEXT</button>
<button class="action" onclick="filterCategory('utility')">UTILITY</button>
<button class="action" onclick="filterCategory('developer')">DEVELOPER</button>
</div>
<div class="grid" id="toolGrid"></div>
<div class="panel" id="toolWorkspace" style="margin-top:15px">
<h2>TOOL INFORMATION</h2><p>Select a tool to open its workspace.</p>
</div>
</section>

<section class="page" id="security">
<h1>SECURITY CENTER</h1>
<p>Educational security utilities. Never enter a real password into a demo tool.</p>
<div class="grid wide">
<div class="panel">
<h2>PASSWORD ANALYZER</h2>
<input id="passCheck" type="password" placeholder="Sample password">
<button class="action" onclick="checkPassword()">ANALYZE</button>
<div class="output" id="passResult"></div>
</div>
<div class="panel">
<h2>PASSWORD GENERATOR</h2>
<div class="row"><input id="passLength" type="number" value="20" min="8" max="64"><label><input id="passSymbols" type="checkbox" checked> Symbols</label></div>
<button class="action" onclick="generatePassword()">GENERATE</button>
<div class="output" id="generatedPassword"></div>
<button class="action" onclick="copyText('generatedPassword')">COPY</button>
</div>
<div class="panel">
<h2>BASE64 TOOL</h2>
<textarea id="baseInput" placeholder="Enter text..."></textarea>
<button class="action" onclick="base64Tool('encode')">ENCODE</button>
<button class="action" onclick="base64Tool('decode')">DECODE</button>
<div class="output" id="baseOutput"></div>
</div>
<div class="panel">
<h2>CAESAR CIPHER</h2>
<textarea id="cipherInput" placeholder="Enter message..."></textarea>
<input id="cipherShift" type="number" value="3" min="1" max="25">
<button class="action" onclick="cipherTool(1)">ENCODE</button>
<button class="action" onclick="cipherTool(-1)">DECODE</button>
<div class="output" id="cipherOutput"></div>
</div>
<div class="panel">
<h2>SHA-256 HASH</h2>
<textarea id="hashInput" placeholder="Enter text..."></textarea>
<button class="action" onclick="makeHash()">GENERATE HASH</button>
<div class="output" id="hashOutput"></div>
</div>
<div class="panel">
<h2>PHISHING AWARENESS</h2>
<label><input type="checkbox"> Check the sender address</label>
<label><input type="checkbox"> Check the destination URL</label>
<label><input type="checkbox"> Watch for urgent requests</label>
<label><input type="checkbox"> Never share verification codes</label>
<p>When unsure, don't click. Visit the official website directly.</p>
</div>
<div class="panel">
<h2>URL INSPECTOR</h2>
<input id="urlCheck" placeholder="https://example.com">
<button class="action" onclick="inspectURL()">INSPECT</button>
<div class="output" id="urlResult"></div>
</div>
</div>
</section>

<section class="page" id="developer">
<h1>DEVELOPER LAB</h1>
<p>BUILD AND TEST CODE IN YOUR BROWSER.</p>
<div class="grid wide">
<div class="panel"><h2>HTML PREVIEWER</h2>
<textarea id="htmlCode" placeholder="<h1>Hello World</h1>"></textarea>
<button class="action" onclick="previewHTML()">PREVIEW</button>
<iframe id="htmlPreview" sandbox=""></iframe>
</div>
<div class="panel"><h2>CSS PLAYGROUND</h2>
<textarea id="cssCode">body{background:#101010;color:lime;font-family:monospace}</textarea>
<textarea id="cssHTML"><h1>CSS Playground</h1><p>Customize this page.</p></textarea>
<button class="action" onclick="previewCSS()">RUN CSS</button>
<iframe id="cssPreview" sandbox=""></iframe>
</div>
<div class="panel"><h2>JAVASCRIPT PLAYGROUND</h2>
<textarea id="jsCode" placeholder="document.body.innerHTML = 'Hello!'"></textarea>
<button class="action" onclick="runJS()">RUN CODE</button>
<iframe id="jsPreview" sandbox="allow-scripts"></iframe>
</div>
<div class="panel"><h2>JSON FORMATTER</h2>
<textarea id="jsonInput" placeholder='{"name":"operator"}'></textarea>
<button class="action" onclick="formatJSON()">FORMAT</button>
<button class="action" onclick="minifyJSON()">MINIFY</button>
<div class="output" id="jsonOutput"></div>
</div>
<div class="panel"><h2>REGEX TESTER</h2>
<input id="regexPattern" placeholder="Regular expression">
<input id="regexFlags" value="gi">
<textarea id="regexText" placeholder="Text to test..."></textarea>
<button class="action" onclick="testRegex()">TEST</button>
<div class="output" id="regexOutput"></div>
</div>
<div class="panel"><h2>XML FORMATTER</h2>
<textarea id="xmlInput" placeholder="<root><item>Hello</item></root>"></textarea>
<button class="action" onclick="formatXML()">FORMAT</button>
<div class="output" id="xmlOutput"></div>
</div>
<div class="panel"><h2>COLOR GENERATOR</h2>
<input type="color" id="colorPicker" value="#48ffa0">
<button class="action" onclick="showColor()">GET COLOR</button>
<div class="output" id="colorOutput"></div>
</div>
<div class="panel"><h2>GRADIENT GENERATOR</h2>
<div class="row"><input type="color" id="gradA" value="#48ffa0"><input type="color" id="gradB" value="#030907"></div>
<button class="action" onclick="makeGradient()">GENERATE</button>
<div id="gradientPreview" style="height:80px;border-radius:8px"></div>
<div class="output" id="gradientOutput"></div>
</div>
<div class="panel"><h2>UUID GENERATOR</h2>
<button class="action" onclick="makeUUID()">GENERATE</button>
<div class="output" id="uuidOutput"></div>
</div>
<div class="panel"><h2>URL ENCODER</h2>
<textarea id="urlInput" placeholder="Enter text..."></textarea>
<button class="action" onclick="urlTool(true)">ENCODE</button>
<button class="action" onclick="urlTool(false)">DECODE</button>
<div class="output" id="urlOutput"></div>
</div>
<div class="panel"><h2>TEXT ANALYZER</h2>
<textarea id="analyzeInput" placeholder="Enter text..."></textarea>
<button class="action" onclick="analyzeText()">ANALYZE</button>
<div class="output" id="analyzeOutput"></div>
</div>
<div class="panel"><h2>MARKDOWN PREVIEW</h2>
<textarea id="mdInput" placeholder="# Hello&#10;Write **Markdown** here."></textarea>
<button class="action" onclick="previewMarkdown()">PREVIEW</button>
<iframe id="mdPreview" sandbox=""></iframe>
</div>
<div class="panel"><h2>UNIT CONVERTER</h2>
<input id="unitValue" type="number" placeholder="Value">
<select id="unitType">
<option value="km">Kilometers to miles</option>
<option value="mi">Miles to kilometers</option>
<option value="kg">Kilograms to pounds</option>
<option value="lb">Pounds to kilograms</option>
<option value="c">Celsius to Fahrenheit</option>
<option value="f">Fahrenheit to Celsius</option>
</select>
<button class="action" onclick="convertUnit()">CONVERT</button>
<div class="output" id="unitOutput"></div>
</div>
<div class="panel"><h2>TIMESTAMP CONVERTER</h2>
<input id="timestampInput" placeholder="Unix timestamp">
<button class="action" onclick="convertTimestamp()">CONVERT</button>
<div class="output" id="timestampOutput"></div>
</div>
<div class="panel"><h2>RANDOM NUMBER</h2>
<div class="row"><input id="randMin" type="number" value="1"><input id="randMax" type="number" value="100"></div>
<button class="action" onclick="randomNumber()">GENERATE</button>
<div class="output" id="randomOutput"></div>
</div>
</div>
</section>

<section class="page" id="network">
<h1>NETWORK CENTER</h1>
<p>Browser connection information and simulated network panels.</p>
<div class="grid wide">
<div class="panel"><h2>CONNECTION STATUS</h2><div class="stat" id="netStatus">--</div><button class="action" onclick="checkConnection()">REFRESH</button></div>
<div class="panel"><h2>CONNECTION DETAILS</h2><div class="output" id="netDetails"></div></div>
<div class="panel"><h2>REQUEST LATENCY TEST</h2><button class="action" onclick="latencyTest()">TEST</button><div class="output" id="latencyOutput"></div></div>
<div class="panel"><h2>DEMO DEVICES</h2><button class="action" onclick="simulateDevices()">REFRESH</button><div class="output" id="deviceOutput"></div></div>
<div class="panel"><h2>NETWORK VISUALIZER</h2><canvas class="chart" id="networkChart" width="500" height="120"></canvas><button class="action" onclick="drawNetwork()">REFRESH</button></div>
</div>
</section>

<section class="page" id="files">
<h1>FILE MANAGER</h1>
<p>Inspect files you select from your own device.</p>
<div class="panel">
<input type="file" id="fileInput" multiple onchange="inspectFiles()">
<div class="output" id="fileResults">No files selected.</div>
</div><br>
<div class="panel">
<h2>TEXT FILE VIEWER</h2>
<input type="file" id="textFile" accept=".txt,.json,.html,.css,.js,.md,.csv" onchange="readTextFile()">
<textarea id="filePreview" placeholder="File contents..."></textarea>
<button class="action" onclick="downloadText('filePreview','edited-file.txt')">DOWNLOAD</button>
</div><br>
<div class="panel">
<h2>IMAGE INSPECTOR</h2>
<input type="file" id="imageFile" accept="image/*" onchange="imageInfo()">
<div id="imageInfoOutput" class="output"></div>
<img id="imageDisplay" style="max-width:100%;max-height:240px;display:none">
</div>
</section>

<section class="page" id="organizer">
<h1>PERSONAL ORGANIZER</h1>
<div class="grid wide">
<div class="panel">
<h2>TASK MANAGER</h2>
<div class="row"><input id="taskInput" placeholder="New task..."><button class="action" onclick="addTask()">ADD</button></div>
<div id="taskList"></div>
<button class="action danger" onclick="clearTasks()">CLEAR ALL</button>
</div>
<div class="panel">
<h2>NOTES</h2>
<input id="noteTitle" placeholder="Note title">
<textarea id="noteText" placeholder="Write something..."></textarea>
<button class="action" onclick="saveNote()">SAVE NOTE</button>
<div id="notesList"></div>
</div>
<div class="panel">
<h2>STOPWATCH</h2>
<div class="stat" id="stopwatch">00:00:00</div>
<button class="action" onclick="startStopwatch()">START</button>
<button class="action" onclick="pauseStopwatch()">PAUSE</button>
<button class="action" onclick="resetStopwatch()">RESET</button>
</div>
<div class="panel">
<h2>COUNTDOWN</h2>
<input id="timerSeconds" type="number" min="1" value="60">
<div class="stat" id="countdown">01:00</div>
<button class="action" onclick="startTimer()">START</button>
<button class="action" onclick="pauseTimer()">PAUSE</button>
<button class="action" onclick="resetTimer()">RESET</button>
</div>
<div class="panel">
<h2>CALCULATOR</h2>
<input id="calcInput" placeholder="(12 + 4) * 3">
<button class="action" onclick="calculate()">CALCULATE</button>
<div class="output" id="calcOutput"></div>
</div>
<div class="panel">
<h2>WORLD CLOCK</h2>
<select id="worldZone" onchange="worldClock()">
<option value="America/New_York">New York</option>
<option value="America/Los_Angeles">Los Angeles</option>
<option value="Europe/London">London</option>
<option value="Europe/Paris">Paris</option>
<option value="Asia/Tokyo">Tokyo</option>
<option value="Australia/Sydney">Sydney</option>
</select>
<div class="stat" id="worldTime"></div>
</div>
<div class="panel">
<h2>CALENDAR EVENTS</h2>
<input type="date" id="calendarDate">
<input id="calendarEvent" placeholder="Event name">
<button class="action" onclick="saveEvent()">SAVE</button>
<div id="eventList"></div>
</div>
</div>
</section>

<section class="page" id="media">
<h1>MEDIA CENTER</h1>
<div class="grid wide">
<div class="panel">
<h2>MUSIC PLAYER</h2>
<input type="file" id="musicFile" accept="audio/*" onchange="loadMusic()">
<audio id="audioPlayer" controls style="width:100%;margin-top:15px"></audio>
<p>Play audio files from your device.</p>
</div>
<div class="panel">
<h2>SOUNDBOARD</h2>
<button class="action" onclick="beep(440)">BEEP</button>
<button class="action" onclick="beep(660)">ALERT</button>
<button class="action" onclick="beep(880)">PING</button>
<button class="action" onclick="beep(220)">LOW</button>
</div>
<div class="panel">
<h2>MISSION GENERATOR</h2>
<button class="action" onclick="mission()">GENERATE</button>
<div class="output" id="missionOutput"></div>
</div>
<div class="panel">
<h2>DIGITAL PET</h2>
<div class="stat" id="petFace">🤖</div>
<div id="petStatus" class="small">Your companion is waiting.</div>
<button class="action" onclick="feedPet()">FEED</button>
<button class="action" onclick="playPet()">PLAY</button>
<button class="action" onclick="petSleep()">SLEEP</button>
</div>
</div>
</section>

<section class="page" id="assistant">
<h1>ASSISTANT INTERFACE</h1>
<p>Offline helper with preset responses. Not connected to a live AI service.</p>
<div class="panel">
<div class="terminal" id="chatOutput">
<div class="termline termgreen">SYSTEM: Assistant initialized.</div>
</div>
<div class="row">
<input id="chatInput" placeholder="Enter a message...">
<button class="action" onclick="sendChat()">SEND</button>
</div>
<button class="action" onclick="clearChat()">CLEAR CHAT</button>
</div>
</section>

<section class="page" id="settings">
<h1>SYSTEM SETTINGS</h1>
<div class="grid wide">
<div class="panel">
<h2>OPERATOR PROFILE</h2>
<input id="operatorName" placeholder="Operator name">
<button class="action" onclick="saveOperator()">SAVE</button>
</div>
<div class="panel">
<h2>THEMES</h2>
<select id="themeChoice" onchange="setTheme(this.value)">
<option value="green">Matrix Green</option>
<option value="red">Red Alert</option>
<option value="purple">Purple Neon</option>
<option value="blue">Cyber Blue</option>
</select>
</div>
<div class="panel">
<h2>VISUAL EFFECTS</h2>
<label><input type="checkbox" id="matrixToggle" checked onchange="toggleMatrix(this.checked)"> Matrix background</label>
<label><input type="checkbox" id="soundToggle" checked> Sound effects</label>
<button class="action" onclick="toggleFullscreen()">FULLSCREEN</button>
</div>
<div class="panel">
<h2>DATA BACKUP</h2>
<button class="action" onclick="exportData()">EXPORT DATA</button>
<button class="action danger" onclick="resetApp()">RESET DATA</button>
</div>
<div class="panel">
<h2>APP LAUNCHER</h2>
<input id="appName" placeholder="Website name">
<input id="appURL" placeholder="https://example.com">
<button class="action" onclick="addApp()">ADD WEBSITE</button>
<div id="appList"></div>
</div>
</div>
</section>

<section class="page" id="widgets">
<h1>WIDGET BUILDER</h1>
<div class="panel">
<label><input type="checkbox" id="widgetClock" checked> Clock</label>
<label><input type="checkbox" id="widgetTasks" checked> Task count</label>
<label><input type="checkbox" id="widgetNotes" checked> Saved notes</label>
<label><input type="checkbox" id="widgetConnection" checked> Connection status</label>
<button class="action" onclick="saveWidgets()">SAVE WIDGETS</button>
</div>
</section>

<section class="page" id="secret">
<h1>CLASSIFIED ACCESS</h1>
<p>Welcome to the hidden area.</p>
<div class="panel">
<h2>SECRET ACCESS</h2>
<input id="secretCode" placeholder="Enter code">
<button class="action" onclick="unlockSecret()">UNLOCK</button>
<div class="output" id="secretResult">ACCESS LOCKED</div>
</div>
<div class="panel" style="margin-top:14px">
<h2>ACHIEVEMENTS</h2>
<div id="achievements"></div>
</div>
</section>

</main>
<footer>HACKER_OS 3.0 // DIGITAL COMMAND CENTER // LOCAL WEB APP</footer>
<div id="toast"></div>

<script>
const $=id=>document.getElementById(id);
const get=(k,d)=>{try{return JSON.parse(localStorage.getItem(k))??d}catch{return d}};
const put=(k,v)=>localStorage.setItem(k,JSON.stringify(v));
let startTime=Date.now(),stopStart=0,stopElapsed=0;
let stopInterval=null,timerRemaining=60,timerInterval=null;
let matrixEnabled=true,activeCategory='all',petMood=0;

function escapeHTML(s){return String(s).replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]))}
function toast(s){let t=$('toast');t.textContent=s;t.style.display='block';clearTimeout(toast.t);toast.t=setTimeout(()=>t.style.display='none',2200)}
function logActivity(s){let a=get('activity',[]);a.unshift(new Date().toLocaleTimeString()+' — '+s);put('activity',a.slice(0,8));renderActivity()}
function renderActivity(){$('activity').innerHTML=get('activity',['System initialized.']).map(x=>'<div>› '+escapeHTML(x)+'</div>').join('')}
function page(id){
 document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
 if(!$ (id))return;
 $(id).classList.add('active');
 document.querySelectorAll('nav button').forEach(b=>b.classList.toggle('active',b.dataset.page===id));
 if(id==='organizer'){renderTasks();renderNotes();renderEvents()}
 if(id==='settings')renderApps();
 if(id==='dashboard')renderWidgets();
 if(id==='secret')renderAchievements();
}
$('nav').addEventListener('click',e=>{let b=e.target.closest('button[data-page]');if(b)page(b.dataset.page)});

function updateClock(){
 let d=new Date();
 $('clock').textContent=d.toLocaleTimeString();
 $('date').textContent=d.toLocaleDateString(undefined,{weekday:'long',year:'numeric',month:'long',day:'numeric'});
 let s=Math.floor((Date.now()-startTime)/1000);
 $('uptime').textContent=[Math.floor(s/3600),Math.floor(s/60)%60,s%60].map(x=>String(x).padStart(2,'0')).join(':');
 $('connection').textContent=navigator.onLine?'ONLINE':'OFFLINE';
 $('headerStatus').textContent=navigator.onLine?'● SYSTEM ONLINE':'● OFFLINE';
 let cpu=Math.floor(12+Math.random()*70),ram=Math.floor(20+Math.random()*65);
 $('cpuText').textContent=cpu+'%';$('ramText').textContent=ram+'%';
 $('cpuBar').style.width=cpu+'%';$('ramBar').style.width=ram+'%';
 worldClock();
}
setInterval(updateClock,1000);updateClock();
window.addEventListener('online',checkConnection);
window.addEventListener('offline',checkConnection);

const mc=$('matrix'),ctx=mc.getContext('2d');let drops=[];
function resizeMatrix(){mc.width=innerWidth;mc.height=innerHeight;drops=Array(Math.ceil(mc.width/17)).fill(1)}
window.addEventListener('resize',resizeMatrix);resizeMatrix();
setInterval(()=>{
 if(!matrixEnabled)return;
 ctx.fillStyle='rgba(3,9,6,.09)';ctx.fillRect(0,0,mc.width,mc.height);
 ctx.fillStyle=getComputedStyle(document.documentElement).getPropertyValue('--green')||'#48ffa0';
 ctx.font='14px monospace';
 drops.forEach((y,i)=>{
 ctx.fillText(String.fromCharCode(0x30A0+Math.random()*96),i*17,y*17);
 if(y*17>mc.height&&Math.random()>.975)drops[i]=0;
 drops[i]++;
 });
},65);

function terminalLine(s,c=''){let d=document.createElement('div');d.className='termline '+c;d.textContent=s;$('terminalOutput').appendChild(d);$('terminalOutput').scrollTop=$('terminalOutput').scrollHeight}
function terminalCommand(cmd){
 let c=cmd.trim().toUpperCase();if(!c)return;
 terminalLine('operator@hacker-os:~$ '+cmd,'termblue');
 let data={
 HELP:'HELP | STATUS | TIME | ABOUT | SCAN | MATRIX | SECRET | TOOLS | CLEAR',
 STATUS:'SYSTEM ONLINE\nLOCAL DASHBOARD ACTIVE\nNETWORK SCANNING DISABLED',
 TIME:new Date().toString(),
 ABOUT:'HACKER OS 3.0 — PERSONAL BROWSER DASHBOARD',
 SCAN:'SIMULATION ONLY. No real devices or networks are scanned.',
 MATRIX:'MATRIX EFFECT: '+(matrixEnabled?'ON':'OFF'),
 SECRET:'HINT: Try the code MATRIX in the Secret Room.',
 TOOLS:'TOOLS | SECURITY | DEV LAB | ORGANIZER | FILES | MEDIA'
 };
 if(c==='CLEAR'){clearTerminal();return}
 if(c==='SECRET')put('achievementSecret',true);
 terminalLine(data[c]||'UNKNOWN COMMAND. TYPE HELP.','termgreen');
 logActivity('Terminal command: '+c);
}
function runCommand(){let v=$('commandInput').value;terminalCommand(v);$('commandInput').value=''}
$('commandInput').addEventListener('keydown',e=>{if(e.key==='Enter')runCommand()});
function clearTerminal(){$('terminalOutput').innerHTML='';terminalLine('HACKER OS 3.0 TERMINAL READY. TYPE HELP.','termgreen')}
clearTerminal();

const toolData=[
['Base64 Encoder','text','Convert text to Base64','base'],
['Text Analyzer','text','Count characters and words','analyze'],
['URL Encoder','text','Encode and decode URL text','url'],
['JSON Formatter','developer','Format JSON data','json'],
['UUID Generator','utility','Generate unique IDs','uuid'],
['Color Generator','developer','Create color codes','color'],
['Gradient Generator','developer','Create CSS gradients','gradient'],
['Random Number','utility','Generate random numbers','random'],
['Unit Converter','utility','Convert common units','unit'],
['Timestamp Converter','utility','Convert Unix timestamps','timestamp'],
['Regex Tester','developer','Test regular expressions','regex'],
['Markdown Preview','developer','Preview Markdown','markdown'],
['XML Formatter','developer','Format XML text','xml']
];
function renderTools(list=toolData){$('toolGrid').innerHTML=list.map(t=>`<div class="panel toolcard" onclick="openTool('${t[3]}')"><div class="symbol">⌘</div><h3>${t[0]}</h3><p>${t[2]}</p><span class="pill">${t[1]}</span></div>`).join('')}
function filterTools(){let q=$('toolSearch').value.toLowerCase();renderTools(toolData.filter(t=>(t.join(' ').toLowerCase().includes(q))&&(activeCategory==='all'||t[1]===activeCategory)))}
function filterCategory(c){activeCategory=c;filterTools()}
function openTool(id){let t=toolData.find(x=>x[3]===id);$('toolWorkspace').innerHTML='<h2>'+escapeHTML(t?.[0]||'TOOL')+'</h2><p>'+escapeHTML(t?.[2]||'')+'</p><p>Open the matching utility in the DEV LAB or SECURITY section.</p>';page(['base'].includes(id)?'security':'developer')}
renderTools();

function base64Tool(m){try{let s=$('baseInput').value;$('baseOutput').textContent=m==='encode'?btoa(unescape(encodeURIComponent(s))):decodeURIComponent(escape(atob(s)))}catch{$('baseOutput').textContent='Invalid input.'}}
function cipherTool(dir){let s=$('cipherInput').value,n=Math.max(1,Math.min(25,Number($('cipherShift').value)||3))*dir;$('cipherOutput').textContent=s.replace(/[a-z]/gi,ch=>{let b=ch<='Z'?65:97;return String.fromCharCode((ch.charCodeAt(0)-b+n+260)%26+b)})}
function checkPassword(){let s=$('passCheck').value,n=0;if(s.length>=12)n++;if(/[a-z]/.test(s)&&/[A-Z]/.test(s))n++;if(/\d/.test(s))n++;if(/[^A-Za-z0-9]/.test(s))n++;$('passResult').textContent=s?['Very weak','Weak','Fair','Strong','Very strong'][n]+' demo rating. Length: '+s.length:'Enter a sample password.'}
function generatePassword(){let len=Math.max(8,Math.min(64,Number($('passLength').value)||20)),chars='ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz23456789'+($('passSymbols').checked?'!@#$%&*+-_?':'');let a=new Uint32Array(len);crypto.getRandomValues(a);$('generatedPassword').textContent=Array.from(a,x=>chars[x%chars.length]).join('')}
async function makeHash(){if(!crypto.subtle)return $('hashOutput').textContent='Secure hashing unavailable.';let h=await crypto.subtle.digest('SHA-256',new TextEncoder().encode($('hashInput').value));$('hashOutput').textContent=Array.from(new Uint8Array(h)).map(x=>x.toString(16).padStart(2,'0')).join('')}
function inspectURL(){try{let u=new URL($('urlCheck').value);$('urlResult').textContent='Host: '+u.hostname+'\nProtocol: '+u.protocol+'\nHTTPS: '+(u.protocol==='https:'?'Yes':'No')+'\nThis is a format check, not a malware scan.'}catch{$('urlResult').textContent='Invalid full URL.'}}
function formatJSON(){try{$('jsonOutput').textContent=JSON.stringify(JSON.parse($('jsonInput').value),null,2)}catch(e){$('jsonOutput').textContent='Invalid JSON: '+e.message}}
function minifyJSON(){try{$('jsonOutput').textContent=JSON.stringify(JSON.parse($('jsonInput').value))}catch(e){$('jsonOutput').textContent='Invalid JSON: '+e.message}}
function testRegex(){try{let r=new RegExp($('regexPattern').value,$('regexFlags').value),m=[...$('regexText').value.matchAll(r)];$('regexOutput').textContent=m.length+' match(es):\n'+m.map(x=>x[0]).join('\n')}catch(e){$('regexOutput').textContent=e.message}}
function formatXML(){let s=$('xmlInput').value.replace(/>\s*</g,'><').replace(/</g,'\n<').trim(),level=0;$('xmlOutput').textContent=s.split('\n').map(line=>{if(/^<\//.test(line))level=Math.max(0,level-1);let o='  '.repeat(level)+line;if(/^<[^!?/][^>]*[^/]?>$/.test(line)&&!/<\/[^>]+>$/.test(line))level++;return o}).join('\n')}
function showColor(){let c=$('colorPicker').value;$('colorOutput').textContent='HEX: '+c+'\nRGB: '+parseInt(c.slice(1,3),16)+', '+parseInt(c.slice(3,5),16)+', '+parseInt(c.slice(5,7),16)}
function makeGradient(){let g=`linear-gradient(120deg,${$('gradA').value},${$('gradB').value})`;$('gradientPreview').style.background=g;$('gradientOutput').textContent='background: '+g+';'}
function makeUUID(){$('uuidOutput').textContent=crypto.randomUUID?crypto.randomUUID():'Unavailable'}
function urlTool(enc){try{$('urlOutput').textContent=enc?encodeURIComponent($('urlInput').value):decodeURIComponent($('urlInput').value)}catch{$('urlOutput').textContent='Invalid text'}}
function analyzeText(){let s=$('analyzeInput').value;$('analyzeOutput').textContent='Characters: '+s.length+'\nWords: '+(s.trim()?s.trim().split(/\s+/).length:0)+'\nLines: '+(s?s.split('\n').length:0)+'\nLetters: '+(s.match(/[a-z]/gi)||[]).length+'\nDigits: '+(s.match(/\d/g)||[]).length}
function convertUnit(){let v=Number($('unitValue').value),t=$('unitType').value;if(!Number.isFinite(v))return $('unitOutput').textContent='Enter a number';let r={km:v*.621371,mi:v*1.60934,kg:v*2.20462,lb:v/2.20462,c:v*9/5+32,f:(v-32)*5/9}[t];$('unitOutput').textContent=r.toFixed(4)}
function convertTimestamp(){let v=Number($('timestampInput').value),d=new Date(v*1000);$('timestampOutput').textContent=isNaN(d)?'Invalid timestamp':d.toString()}
function randomNumber(){let a=Number($('randMin').value),b=Number($('randMax').value);if(!Number.isInteger(a)||!Number.isInteger(b)||b<a)return $('randomOutput').textContent='Invalid range';let x=new Uint32Array(1);crypto.getRandomValues(x);$('randomOutput').textContent=String(a+x[0]%(b-a+1))}
function previewHTML(){$('htmlPreview').srcdoc=$('htmlCode').value}
function previewCSS(){$('cssPreview').srcdoc='<style>'+$('cssCode').value+'</style>'+$('cssHTML').value}
function runJS(){$('jsPreview').srcdoc='<body><script>try{'+$('jsCode').value+'}catch(e){document.body.innerText=e.message}<\/script></body>'}
function previewMarkdown(){let s=escapeHTML($('mdInput').value).replace(/^### (.*)$/gm,'<h3>$1</h3>').replace(/^## (.*)$/gm,'<h2>$1</h2>').replace(/^# (.*)$/gm,'<h1>$1</h1>').replace(/\*\*(.*?)\*\*/g,'<b>$1</b>').replace(/\*(.*?)\*/g,'<i>$1</i>').replace(/\n/g,'<br>');$('mdPreview').srcdoc='<body style="font-family:Arial;padding:12px">'+s+'</body>'}

function calculate(){
let s=$('calcInput').value.replace(/\s/g,'');
if(!/^[0-9+\-*/().%^]+$/.test(s))return $('calcOutput').textContent='Only basic math operators allowed.';
try{
let i=0;
function expr(){let v=term();while(s[i]==='+'||s[i]==='-'){let o=s[i++],n=term();v=o==='+'?v+n:v-n}return v}
function term(){let v=power();while(['*','/','%'].includes(s[i])){let o=s[i++],n=power();if((o==='/'||o==='%')&&n===0)throw Error('Divide by zero');v=o==='*'?v*n:o==='/'?v/n:v%n}return v}
function power(){let v=atom();if(s[i]==='^'){i++;v=Math.pow(v,power())}return v}
function atom(){if(s[i]==='+'||s[i]==='-'){let o=s[i++];return (o==='-'?-1:1)*atom()}if(s[i]==='('){i++;let v=expr();if(s[i++]!==')')throw Error('Missing )');return v}let a=i;while(/[0-9.]/.test(s[i]||'')&&i<s.length)i++;if(a===i)throw Error('Invalid expression');return Number(s.slice(a,i))}
let r=expr();if(i!==s.length||!Number.isFinite(r))throw Error('Invalid expression');$('calcOutput').textContent=String(r);
}catch(e){$('calcOutput').textContent=e.message}
}
function worldClock(){$('worldTime').textContent=new Date().toLocaleTimeString('en-US',{timeZone:$('worldZone').value})}

function checkConnection(){$('netStatus').textContent=navigator.onLine?'ONLINE':'OFFLINE';let c=navigator.connection;$('netDetails').textContent='Browser online: '+navigator.onLine+'\nConnection type: '+(c?.type||'Not provided')+'\nEffective type: '+(c?.effectiveType||'Not provided')+'\nLanguage: '+navigator.language}
checkConnection();
function latencyTest(){$('latencyOutput').textContent='Testing...';let t=performance.now();fetch('https://www.cloudflare.com/cdn-cgi/trace?x='+Date.now(),{mode:'no-cors',cache:'no-store'}).then(()=>$('latencyOutput').textContent='Request completed in approximately '+Math.round(performance.now()-t)+' ms. This is not a full speed test.').catch(()=>$('latencyOutput').textContent='Request failed.')}
function simulateDevices(){$('deviceOutput').textContent='DEMO DEVICE A — ONLINE\nDEMO DEVICE B — ONLINE\nDEMO DEVICE C — IDLE\n\nFictional devices for display only.'}
function drawNetwork(){let c=$('networkChart'),x=c.getContext('2d');x.clearRect(0,0,c.width,c.height);x.strokeStyle='#48ffa0';x.lineWidth=2;x.beginPath();for(let i=0;i<100;i++){let y=60+Math.sin(i*.2)*20+Math.random()*20-10;i?x.lineTo(i*5,y):x.moveTo(i*5,y)}x.stroke()}
drawNetwork();

function inspectFiles(){$('fileResults').textContent=[...$('fileInput').files].map(f=>f.name+'\nType: '+f.type+'\nSize: '+(f.size/1024).toFixed(2)+' KB').join('\n\n')||'No files selected'}
function readTextFile(){let f=$('textFile').files[0];if(!f)return;let r=new FileReader();r.onload=()=>$('filePreview').value=r.result;r.readAsText(f)}
function imageInfo(){let f=$('imageFile').files[0];if(!f)return;$('imageInfoOutput').textContent='Name: '+f.name+'\nType: '+f.type+'\nSize: '+(f.size/1024).toFixed(2)+' KB';let u=URL.createObjectURL(f),img=$('imageDisplay');img.src=u;img.style.display='block';img.onload=()=>$('imageInfoOutput').textContent+='\nDimensions: '+img.naturalWidth+' × '+img.naturalHeight}
function downloadText(id,n){let b=new Blob([$(id).value],{type:'text/plain'}),a=document.createElement('a');a.href=URL.createObjectURL(b);a.download=n;a.click();URL.revokeObjectURL(a.href)}

function tasks(){return get('tasks',[])}
function renderTasks(){$('taskList').innerHTML=tasks().map((t,i)=>`<div class="task"><input type="checkbox" ${t.done?'checked':''} onchange="toggleTask(${i})"><span class="${t.done?'done':''}">${escapeHTML(t.text)}</span><button class="action danger" onclick="deleteTask(${i})">×</button></div>`).join('')||'<p>No tasks yet.</p>'}
function addTask(){let v=$('taskInput').value.trim();if(!v)return;let a=tasks();a.push({text:v,done:false});put('tasks',a);$('taskInput').value='';renderTasks();renderWidgets();logActivity('Task added')}
function toggleTask(i){let a=tasks();a[i].done=!a[i].done;put('tasks',a);renderTasks();renderWidgets()}
function deleteTask(i){let a=tasks();a.splice(i,1);put('tasks',a);renderTasks();renderWidgets()}
function clearTasks(){if(confirm('Clear all tasks?')){put('tasks',[]);renderTasks();renderWidgets()}}
function renderNotes(){let a=get('notes',[]);$('notesList').innerHTML=a.map((n,i)=>`<div class="task"><span><b>${escapeHTML(n.title)}</b><br>${escapeHTML(n.text.slice(0,65))}</span><button class="action" onclick="loadNote(${i})">OPEN</button><button class="action danger" onclick="deleteNote(${i})">×</button></div>`).join('')||'<p>No notes yet.</p>'}
function saveNote(){let title=$('noteTitle').value.trim()||'Untitled',text=$('noteText').value;if(!text.trim())return toast('Write a note first');let a=get('notes',[]);a.unshift({title,text});put('notes',a);renderNotes();renderWidgets();toast('Saved')}
function loadNote(i){let n=get('notes',[])[i];$('noteTitle').value=n.title;$('noteText').value=n.text}
function deleteNote(i){let a=get('notes',[]);a.splice(i,1);put('notes',a);renderNotes();renderWidgets()}
function startStopwatch(){if(stopInterval)return;stopStart=Date.now()-stopElapsed;stopInterval=setInterval(()=>{stopElapsed=Date.now()-stopStart;$('stopwatch').textContent=formatTime(stopElapsed)},250)}
function pauseStopwatch(){clearInterval(stopInterval);stopInterval=null}
function resetStopwatch(){pauseStopwatch();stopElapsed=0;$('stopwatch').textContent='00:00:00'}
function formatTime(ms){let s=Math.floor(ms/1000);return [Math.floor(s/3600),Math.floor(s/60)%60,s%60].map(x=>String(x).padStart(2,'0')).join(':')}
function startTimer(){if(timerInterval)return;if(timerRemaining<=0)timerRemaining=Math.max(1,Number($('timerSeconds').value)||60);timerInterval=setInterval(()=>{timerRemaining--;showTimer();if(timerRemaining<=0){pauseTimer();toast('Timer finished');beep(660)}},1000)}
function pauseTimer(){clearInterval(timerInterval);timerInterval=null}
function resetTimer(){pauseTimer();timerRemaining=Math.max(1,Number($('timerSeconds').value)||60);showTimer()}
function showTimer(){$('countdown').textContent=String(Math.floor(timerRemaining/60)).padStart(2,'0')+':'+String(timerRemaining%60).padStart(2,'0')}
function saveEvent(){let d=$('calendarDate').value,n=$('calendarEvent').value.trim();if(!d||!n)return toast('Enter date and event');let a=get('events',[]);a.push({date:d,name:n});put('events',a);renderEvents();$('calendarEvent').value=''}
function renderEvents(){$('eventList').innerHTML=get('events',[]).sort((a,b)=>a.date.localeCompare(b.date)).map((e,i)=>`<div class="task"><span>${escapeHTML(e.date)} — ${escapeHTML(e.name)}</span><button class="action danger" onclick="deleteEvent(${i})">×</button></div>`).join('')||'<p>No events.</p>'}
function deleteEvent(i){let a=get('events',[]);a.splice(i,1);put('events',a);renderEvents()}
function loadMusic(){let f=$('musicFile').files[0];if(!f)return;$('audioPlayer').src=URL.createObjectURL(f);$('audioPlayer').load()}
function beep(freq){if(!$('soundToggle').checked)return;try{let A=AudioContext||webkitAudioContext,c=new A(),o=c.createOscillator(),g=c.createGain();o.frequency.value=freq;o.connect(g);g.connect(c.destination);g.gain.value=.08;o.start();o.stop(c.currentTime+.16);o.onended=()=>c.close()}catch{}}
function mission(){let a=['Organize your workspace','Create a new color theme','Write a useful note','Build a tiny HTML page','Complete three tasks','Explore the developer lab','Create a dashboard widget'];$('missionOutput').textContent=a[Math.floor(Math.random()*a.length)]}
function feedPet(){petMood++;$('petFace').textContent='🤖';$('petStatus').textContent='Your companion is happy. Level '+petMood}
function playPet(){petMood++;$('petFace').textContent='😎';$('petStatus').textContent='Your companion is playing. Level '+petMood}
function petSleep(){$('petFace').textContent='😴';$('petStatus').textContent='Your companion is resting.'}

function sendChat(){let q=$('chatInput').value.trim();if(!q)return;let box=$('chatOutput'),u=document.createElement('div');u.className='termline termblue';u.textContent='YOU: '+q;box.appendChild(u);let l=q.toLowerCase(),r='I am an offline helper. Try asking about tools, notes, or settings.';if(l.includes('help'))r='Try TOOLS, SECURITY, DEV LAB, FILE MANAGER, or ORGANIZER.';else if(l.includes('time'))r='Local time: '+new Date().toLocaleTimeString();else if(l.includes('password'))r='Use unique passwords and two-factor authentication.';else if(l.includes('terminal'))r='Type HELP in the terminal for commands.';else if(l.includes('note'))r='Open ORGANIZER to create a note.';let a=document.createElement('div');a.className='termline termgreen';a.textContent='HELPER: '+r;box.appendChild(a);box.scrollTop=box.scrollHeight;$('chatInput').value=''}
function clearChat(){$('chatOutput').innerHTML=''}
$('chatInput').addEventListener('keydown',e=>{if(e.key==='Enter')sendChat()});

function saveOperator(){put('operator',$('operatorName').value.trim());toast('Saved')}
function setTheme(t){let v={green:['#48ffa0','#00d878'],red:['#ff536b','#c72b43'],purple:['#c28aff','#8745c9'],blue:['#50cfff','#258ac4']}[t]||['#48ffa0','#00d878'];document.documentElement.style.setProperty('--green',v[0]);document.documentElement.style.setProperty('--green2',v[1]);put('theme',t)}
function toggleMatrix(v){matrixEnabled=v;mc.style.display=v?'block':'none';put('matrix',v)}
function toggleFullscreen(){if(!document.fullscreenElement)document.documentElement.requestFullscreen?.();else document.exitFullscreen?.()}
function addApp(){let n=$('appName').value.trim(),s=$('appURL').value.trim();try{let u=new URL(s);if(!['http:','https:'].includes(u.protocol))throw 0;let a=get('apps',[]);a.push({name:n||u.hostname,url:u.href});put('apps',a);renderApps();$('appName').value='';$('appURL').value=''}catch{toast('Enter a valid website URL')}}
function renderApps(){$('appList').innerHTML=get('apps',[]).map((a,i)=>`<div class="task"><a href="${escapeHTML(a.url)}" target="_blank" rel="noopener noreferrer" style="color:var(--green)">${escapeHTML(a.name)}</a><button class="action danger" onclick="deleteApp(${i})">×</button></div>`).join('')||'<p>No websites saved.</p>'}
function deleteApp(i){let a=get('apps',[]);a.splice(i,1);put('apps',a);renderApps()}
function renderWidgets(){let e=get('widgets',{clock:true,tasks:true,notes:true,connection:true}),a=[];if(e.clock)a.push(['LOCAL TIME',new Date().toLocaleTimeString()]);if(e.tasks)a.push(['TASKS',tasks().filter(t=>!t.done).length+' unfinished']);if(e.notes)a.push(['NOTES',get('notes',[]).length+' saved']);if(e.connection)a.push(['CONNECTION',navigator.onLine?'ONLINE':'OFFLINE']);$('dashboardWidgets').innerHTML=a.map(x=>`<div class="panel"><h3>${x[0]}</h3><div class="stat">${escapeHTML(x[1])}</div></div>`).join('')}
function saveWidgets(){put('widgets',{clock:$('widgetClock').checked,tasks:$('widgetTasks').checked,notes:$('widgetNotes').checked,connection:$('widgetConnection').checked});renderWidgets();toast('Widgets saved')}
function renderAchievements(){let a=[];if(get('achievementSecret',false))a.push('★ Secret room discovered');if(tasks().length>=5)a.push('★ Task collector');if(get('notes',[]).length>=3)a.push('★ Note keeper');$('achievements').textContent=a.join('\n')||'Explore to unlock achievements.'}
function unlockSecret(){if($('secretCode').value.trim().toUpperCase()==='MATRIX'){$('secretResult').textContent='ACCESS GRANTED. WELCOME, OPERATOR.';put('achievementSecret',true);renderAchievements();toast('Secret unlocked')}else $('secretResult').textContent='ACCESS DENIED.'}
function exportData(){let data={tasks:tasks(),notes:get('notes',[]),events:get('events',[]),apps:get('apps',[]),activity:get('activity',[])};let b=new Blob([JSON.stringify(data,null,2)],{type:'application/json'}),a=document.createElement('a');a.href=URL.createObjectURL(b);a.download='hacker-os-backup.json';a.click();URL.revokeObjectURL(a.href)}
function resetApp(){if(!confirm('Clear all locally saved HACKER OS data?'))return;['tasks','notes','events','apps','activity','operator','theme','widgets','achievementSecret'].forEach(k=>localStorage.removeItem(k));location.reload()}
function copyText(id){navigator.clipboard?.writeText($(id).textContent).then(()=>toast('Copied')).catch(()=>toast('Clipboard unavailable'))}

function drawSystemChart(){
let c=$('systemChart'),x=c.getContext('2d');x.clearRect(0,0,c.width,c.height);x.strokeStyle='#48ffa0';x.lineWidth=2;x.beginPath();
for(let i=0;i<100;i++){let y=55+Math.sin(i*.15)*17+Math.random()*12;i?x.lineTo(i*5,y):x.moveTo(i*5,y)}x.stroke();
}
setInterval(drawSystemChart,1200);drawSystemChart();

function loadSettings(){
$('operatorName').value=get('operator','');
$('themeChoice').value=get('theme','green');setTheme($('themeChoice').value);
matrixEnabled=get('matrix',true);$('matrixToggle').checked=matrixEnabled;toggleMatrix(matrixEnabled);
let w=get('widgets',{clock:true,tasks:true,notes:true,connection:true});
$('widgetClock').checked=w.clock;$('widgetTasks').checked=w.tasks;$('widgetNotes').checked=w.notes;$('widgetConnection').checked=w.connection;
}
loadSettings();
renderActivity();renderWidgets();renderTasks();renderNotes();renderEvents();renderApps();simulateDevices();showTimer();
logActivity('HACKER OS 3.0 initialized');
</script>
</body>
</html>
