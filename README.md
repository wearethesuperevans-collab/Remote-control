
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<meta name="theme-color" content="#050b08">
<title>HACKER OS</title>
<style>
:root{
 --bg:#050907;--panel:#0b1510;--panel2:#101e16;
 --green:#39ff88;--green2:#16c765;--text:#d9ffe6;
 --muted:#83a891;--border:#1b4930;--red:#ff4c65;
 --yellow:#ffd166;--blue:#50c8ff;--purple:#c18aff;
}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--text);
 font-family:Consolas,Monaco,monospace;min-height:100vh}
button,input,textarea,select{font:inherit}
button{cursor:pointer}
button:focus-visible,input:focus-visible,textarea:focus-visible,select:focus-visible{
 outline:2px solid var(--green);outline-offset:2px
}
#matrix{position:fixed;inset:0;width:100%;height:100%;
 z-index:-1;opacity:.10;pointer-events:none}
header{position:sticky;top:0;z-index:10;background:#050907ed;
 border-bottom:1px solid var(--border);backdrop-filter:blur(12px)}
.top{display:flex;align-items:center;justify-content:space-between;
 padding:14px 18px;gap:12px;flex-wrap:wrap}
.logo{font-size:21px;font-weight:bold;color:var(--green);letter-spacing:3px}
.logo span{color:white}
.status{font-size:11px;color:var(--green)}
nav{display:flex;gap:7px;padding:0 12px 12px;overflow-x:auto}
nav button,.btn{
 background:var(--panel2);border:1px solid var(--border);
 color:var(--text);padding:9px 12px;border-radius:7px;
 white-space:nowrap;font-size:12px
}
nav button.active,nav button:hover,.btn.primary{
 background:#12351f;border-color:var(--green);color:var(--green)
}
main{max-width:1250px;margin:auto;padding:20px}
.page{display:none}.page.active{display:block}
h1{font-size:23px;color:var(--green);margin:0 0 8px}
h2{font-size:14px;color:var(--green);letter-spacing:1px;margin:0 0 13px}
h3{font-size:13px;margin:0 0 9px;color:var(--text)}
p{color:var(--muted);font-size:12px;line-height:1.6}
.small{font-size:11px;color:var(--muted)}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:13px}
.grid.wide{grid-template-columns:repeat(auto-fit,minmax(290px,1fr))}
.panel{background:linear-gradient(145deg,var(--panel),#08110c);
 border:1px solid var(--border);border-radius:10px;padding:16px;
 min-width:0;box-shadow:0 5px 22px #0005}
.stat{font-size:25px;color:var(--green);margin:8px 0}
.meter{height:8px;background:#17251c;border-radius:10px;overflow:hidden;margin:8px 0}
.meter div{height:100%;width:30%;background:var(--green);transition:width .3s}
input,textarea,select{width:100%;background:#050b08;color:var(--text);
 border:1px solid var(--border);border-radius:6px;padding:10px;margin:5px 0}
textarea{resize:vertical;min-height:90px}
button.action{background:#10291a;border:1px solid var(--green2);
 color:var(--green);padding:9px 12px;border-radius:6px;margin:4px 3px 4px 0}
button.action:hover{background:#174027}
button.danger{border-color:var(--red);color:var(--red)}
button:disabled{opacity:.4;cursor:not-allowed}
.row{display:flex;gap:8px;align-items:center;flex-wrap:wrap}
.row>*{flex:1}
.row button{flex:0 0 auto}
.output{background:#030705;border:1px solid #183923;padding:12px;
 border-radius:6px;min-height:40px;white-space:pre-wrap;overflow-wrap:anywhere;
 color:var(--green);font-size:12px;margin-top:9px}
.terminal{background:#020503;border:1px solid #1b4930;border-radius:8px;
 padding:13px;height:330px;overflow:auto;font-size:12px}
.termline{margin:0 0 7px;white-space:pre-wrap;overflow-wrap:anywhere}
.termgreen{color:var(--green)}.termred{color:var(--red)}
.termblue{color:var(--blue)}
.task{display:flex;align-items:center;gap:8px;border-bottom:1px solid var(--border);
 padding:9px 0;font-size:12px}
.task span{flex:1}.done{text-decoration:line-through;color:var(--muted)}
.toolcard{cursor:pointer;transition:.15s}
.toolcard:hover{border-color:var(--green);transform:translateY(-2px)}
.toolcard .symbol{font-size:22px;color:var(--green);margin-bottom:10px}
.pill{display:inline-block;border:1px solid var(--border);border-radius:20px;
 padding:4px 8px;color:var(--muted);font-size:10px;margin:3px}
#toast{position:fixed;bottom:18px;left:50%;transform:translateX(-50%);
 background:#14351f;color:var(--green);border:1px solid var(--green);
 padding:10px 15px;border-radius:7px;display:none;z-index:50;font-size:12px}
footer{text-align:center;padding:25px;color:var(--muted);font-size:10px}
iframe{width:100%;height:260px;background:white;border:1px solid var(--border);
 border-radius:6px}
canvas.chart{width:100%;height:110px;background:#030705;border-radius:6px}
pre{white-space:pre-wrap;overflow-wrap:anywhere}
hr{border:0;border-top:1px solid var(--border);margin:14px 0}
@media(max-width:600px){
 main{padding:12px}.top{padding:12px}.logo{font-size:17px}
 .grid{grid-template-columns:1fr}.grid.wide{grid-template-columns:1fr}
 .panel{padding:13px}h1{font-size:20px}
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
  <button class="active" data-page="dashboard">HOME</button>
  <button data-page="terminal">TERMINAL</button>
  <button data-page="tools">TOOLS</button>
  <button data-page="security">SECURITY</button>
  <button data-page="developer">DEV LAB</button>
  <button data-page="network">NETWORK</button>
  <button data-page="files">FILES</button>
  <button data-page="organizer">ORGANIZER</button>
  <button data-page="media">MEDIA</button>
  <button data-page="assistant">AI PANEL</button>
  <button data-page="settings">SETTINGS</button>
  <button data-page="secret">SECRET</button>
 </nav>
</header>

<main>
<!-- DASHBOARD -->
<section class="page active" id="dashboard">
 <h1>WELCOME, OPERATOR.</h1>
 <p>Your personal digital command center.</p>
 <div class="grid">
  <div class="panel"><h2>LOCAL TIME</h2><div class="stat" id="clock">--:--:--</div><div class="small" id="date"></div></div>
  <div class="panel"><h2>SESSION UPTIME</h2><div class="stat" id="uptime">00:00:00</div><div class="small">Current browser session</div></div>
  <div class="panel"><h2>CONNECTION</h2><div class="stat" id="connection">CHECKING</div><div class="small">Browser online status</div></div>
  <div class="panel"><h2>LOCAL STORAGE</h2><div class="stat" id="storageStatus">READY</div><div class="small">Notes and tasks are stored on this device</div></div>
 </div>
 <br>
 <div class="grid wide">
  <div class="panel">
   <h2>SYSTEM MONITOR</h2>
   <div class="row"><span class="small">CPU SIMULATION</span><strong id="cpuText">--%</strong></div>
   <div class="meter"><div id="cpuBar"></div></div>
   <div class="row"><span class="small">RAM SIMULATION</span><strong id="ramText">--%</strong></div>
   <div class="meter"><div id="ramBar"></div></div>
   <p>These are visual demo readings, not actual hardware measurements.</p>
  </div>
  <div class="panel">
   <h2>QUICK LAUNCH</h2>
   <div class="grid">
    <button class="action" onclick="page('terminal')">Terminal</button>
    <button class="action" onclick="page('tools')">Tool library</button>
    <button class="action" onclick="page('security')">Security</button>
    <button class="action" onclick="page('developer')">Dev lab</button>
    <button class="action" onclick="page('organizer')">My tasks</button>
    <button class="action" onclick="page('media')">Music player</button>
   </div>
  </div>
 </div>
 <br>
 <div class="panel"><h2>ACTIVITY FEED</h2><div id="activity" class="small">System initialized.</div></div>
 <br>
 <div class="panel"><h2>YOUR DASHBOARD WIDGETS</h2><div id="dashboardWidgets" class="grid"></div><button class="action" onclick="page('widgets')">OPEN WIDGET BUILDER</button></div>
</section>

<!-- TERMINAL -->
<section class="page" id="terminal">
 <h1>COMMAND TERMINAL</h1>
 <p>Type HELP to see available commands. Commands are local demonstrations.</p>
 <div class="terminal" id="terminalOutput"></div>
 <div class="row">
  <input id="commandInput" placeholder="Enter command..." autocomplete="off">
  <button class="action" onclick="runCommand()">EXECUTE</button>
 </div>
 <button class="action" onclick="clearTerminal()">CLEAR TERMINAL</button>
 <button class="action" onclick="terminalCommand('HELP')">HELP</button>
</section>

<!-- TOOL LIBRARY -->
<section class="page" id="tools">
 <h1>TOOL LIBRARY</h1>
 <p>Search your built-in utilities and open the tool you need.</p>
 <input id="toolSearch" placeholder="Search tools..." oninput="filterTools()">
 <div class="row" id="toolFilters">
  <button class="action" onclick="filterCategory('all')">ALL</button>
  <button class="action" onclick="filterCategory('text')">TEXT</button>
  <button class="action" onclick="filterCategory('utility')">UTILITY</button>
  <button class="action" onclick="filterCategory('developer')">DEVELOPER</button>
 </div>
 <div class="grid" id="toolGrid"></div>
 <br>
 <div class="panel" id="toolWorkspace"><h2>TOOL WORKSPACE</h2><p>Select a tool above to open it here.</p></div>
</section>

<!-- SECURITY -->
<section class="page" id="security">
 <h1>SECURITY CENTER</h1>
 <p>Educational security tools. Never enter a real password into a demo website.</p>
 <div class="grid wide">
  <div class="panel">
   <h2>PASSWORD STRENGTH DEMO</h2>
   <input id="passCheck" type="password" placeholder="Enter a sample password">
   <button class="action" onclick="checkPassword()">ANALYZE</button>
   <div class="output" id="passResult">Waiting for sample input...</div>
  </div>
  <div class="panel">
   <h2>PASSWORD GENERATOR</h2>
   <div class="row"><label class="small">Length <input id="passLength" type="number" min="8" max="64" value="20"></label>
   <label class="small">Symbols <input id="passSymbols" type="checkbox" checked></label></div>
   <button class="action" onclick="generatePassword()">GENERATE</button>
   <div class="output" id="generatedPassword"></div>
   <button class="action" onclick="copyText('generatedPassword')">COPY</button>
  </div>
  <div class="panel">
   <h2>BASE64 ENCODER / DECODER</h2>
   <textarea id="baseInput" placeholder="Enter text..."></textarea>
   <button class="action" onclick="base64Tool('encode')">ENCODE</button>
   <button class="action" onclick="base64Tool('decode')">DECODE</button>
   <div class="output" id="baseOutput"></div>
  </div>
  <div class="panel">
   <h2>TEXT CIPHER DEMO</h2>
   <textarea id="cipherInput" placeholder="Enter a message..."></textarea>
   <div class="row"><input id="cipherShift" type="number" value="3" min="1" max="25"></div>
   <button class="action" onclick="cipherTool(1)">ENCODE</button>
   <button class="action" onclick="cipherTool(-1)">DECODE</button>
   <div class="output" id="cipherOutput"></div>
  </div>
  <div class="panel">
   <h2>SHA-256 HASH GENERATOR</h2>
   <textarea id="hashInput" placeholder="Enter text to hash..."></textarea>
   <button class="action" onclick="makeHash()">GENERATE HASH</button>
   <div class="output" id="hashOutput"></div>
  </div>
  <div class="panel">
   <h2>PHISHING AWARENESS CHECKLIST</h2>
   <p>Before opening a suspicious message, check:</p>
   <label><input type="checkbox"> Is the sender address familiar?</label><br>
   <label><input type="checkbox"> Does the link match the real website?</label><br>
   <label><input type="checkbox"> Is it asking for passwords or codes?</label><br>
   <label><input type="checkbox"> Is it using urgent or threatening language?</label>
   <p>When unsure, don't click. Visit the official website directly.</p>
  </div>
  <div class="panel">
   <h2>URL CHECKLIST</h2>
   <input id="urlCheck" placeholder="Paste a URL to inspect">
   <button class="action" onclick="inspectURL()">INSPECT</button>
   <div class="output" id="urlResult"></div>
  </div>
  <div class="panel">
   <h2>PRIVACY CHECKLIST</h2>
   <label><input type="checkbox"> Use unique passwords</label><br>
   <label><input type="checkbox"> Enable two-factor authentication</label><br>
   <label><input type="checkbox"> Review app permissions</label><br>
   <label><input type="checkbox"> Keep software updated</label><br>
   <label><input type="checkbox"> Avoid sharing verification codes</label>
  </div>
 </div>
</section>

<!-- DEVELOPER LAB -->
<section class="page" id="developer">
 <h1>DEVELOPER LAB</h1>
 <p>Build, format, and test your own code locally in your browser.</p>
 <div class="grid wide">
  <div class="panel">
   <h2>HTML PREVIEWER</h2>
   <textarea id="htmlCode" placeholder="<h1>Hello world!</h1>"></textarea>
   <button class="action" onclick="previewHTML()">PREVIEW</button>
   <iframe id="htmlPreview" sandbox=""></iframe>
  </div>
  <div class="panel">
   <h2>CSS PLAYGROUND</h2>
   <textarea id="cssCode">body { background: #101010; color: lime; font-family: monospace; }</textarea>
   <textarea id="cssHTML"><h1>CSS Playground</h1><p>Change the CSS to customize this page.</p></textarea>
   <button class="action" onclick="previewCSS()">RUN CSS</button>
   <iframe id="cssPreview" sandbox=""></iframe>
  </div>
  <div class="panel">
   <h2>JAVASCRIPT PLAYGROUND</h2>
   <p>Runs inside a separate sandboxed frame.</p>
   <textarea id="jsCode" placeholder="document.body.innerHTML = 'Hello!';"></textarea>
   <button class="action" onclick="runJS()">RUN CODE</button>
   <iframe id="jsPreview" sandbox="allow-scripts"></iframe>
  </div>
  <div class="panel">
   <h2>JSON FORMATTER</h2>
   <textarea id="jsonInput" placeholder='{"name":"operator","status":"online"}'></textarea>
   <button class="action" onclick="formatJSON()">FORMAT</button>
   <button class="action" onclick="minifyJSON()">MINIFY</button>
   <div class="output" id="jsonOutput"></div>
  </div>
  <div class="panel">
   <h2>XML FORMATTER</h2>
   <textarea id="xmlInput" placeholder="<root><item>Hello</item></root>"></textarea>
   <button class="action" onclick="formatXML()">FORMAT XML</button>
   <div class="output" id="xmlOutput"></div>
  </div>
  <div class="panel">
   <h2>REGEX TESTER</h2>
   <input id="regexPattern" placeholder="Regular expression">
   <input id="regexFlags" value="gi" placeholder="Flags">
   <textarea id="regexText" placeholder="Text to test..."></textarea>
   <button class="action" onclick="testRegex()">TEST</button>
   <div class="output" id="regexOutput"></div>
  </div>
  <div class="panel">
   <h2>COLOR PALETTE</h2>
   <input type="color" id="colorPicker" value="#39ff88">
   <button class="action" onclick="showColor()">GET COLOR</button>
   <div class="output" id="colorOutput"></div>
  </div>
  <div class="panel">
   <h2>GRADIENT GENERATOR</h2>
   <div class="row"><input type="color" id="gradA" value="#39ff88"><input type="color" id="gradB" value="#050907"></div>
   <button class="action" onclick="makeGradient()">GENERATE</button>
   <div id="gradientPreview" style="height:80px;border-radius:7px;border:1px solid var(--border)"></div>
   <div class="output" id="gradientOutput"></div>
  </div>
  <div class="panel">
   <h2>UUID GENERATOR</h2>
   <button class="action" onclick="makeUUID()">GENERATE ID</button>
   <div class="output" id="uuidOutput"></div>
  </div>
  <div class="panel">
   <h2>URL ENCODER / DECODER</h2>
   <textarea id="urlInput" placeholder="Enter text or URL..."></textarea>
   <button class="action" onclick="urlTool(true)">ENCODE</button>
   <button class="action" onclick="urlTool(false)">DECODE</button>
   <div class="output" id="urlOutput"></div>
  </div>
  <div class="panel">
   <h2>TEXT ANALYZER</h2>
   <textarea id="analyzeInput" placeholder="Enter text..."></textarea>
   <button class="action" onclick="analyzeText()">ANALYZE</button>
   <div class="output" id="analyzeOutput"></div>
  </div>
  <div class="panel">
   <h2>MARKDOWN PREVIEW</h2>
   <textarea id="mdInput" placeholder="# Hello&#10;Write **Markdown** here."></textarea>
   <button class="action" onclick="previewMarkdown()">PREVIEW</button>
   <iframe id="mdPreview" sandbox=""></iframe>
  </div>
  <div class="panel">
   <h2>UNIT CONVERTER</h2>
   <input id="unitValue" type="number" placeholder="Value">
   <select id="unitType"><option value="km">Kilometers to miles</option><option value="mi">Miles to kilometers</option><option value="kg">Kilograms to pounds</option><option value="lb">Pounds to kilograms</option><option value="c">Celsius to Fahrenheit</option><option value="f">Fahrenheit to Celsius</option></select>
   <button class="action" onclick="convertUnit()">CONVERT</button>
   <div class="output" id="unitOutput"></div>
  </div>
  <div class="panel">
   <h2>TIMESTAMP CONVERTER</h2>
   <input id="timestampInput" placeholder="Unix timestamp">
   <button class="action" onclick="convertTimestamp()">CONVERT</button>
   <div class="output" id="timestampOutput"></div>
  </div>
  <div class="panel">
   <h2>RANDOM NUMBER GENERATOR</h2>
   <div class="row"><input id="randMin" type="number" value="1"><input id="randMax" type="number" value="100"></div>
   <button class="action" onclick="randomNumber()">GENERATE</button>
   <div class="output" id="randomOutput"></div>
  </div>
 </div>
</section>

<!-- NETWORK -->
<section class="page" id="network">
 <h1>NETWORK CENTER</h1>
 <p>Browser-level connection information and safe network demonstrations.</p>
 <div class="grid wide">
  <div class="panel"><h2>CONNECTION STATUS</h2><div class="stat" id="netStatus">--</div><button class="action" onclick="checkConnection()">REFRESH STATUS</button></div>
  <div class="panel"><h2>CONNECTION DETAILS</h2><div class="output" id="netDetails">Checking browser information...</div></div>
  <div class="panel"><h2>LATENCY TEST</h2><p>Tests whether a public endpoint responds. Results depend on your connection.</p><button class="action" onclick="latencyTest()">TEST CONNECTION</button><div class="output" id="latencyOutput"></div></div>
  <div class="panel"><h2>DEVICE SIMULATOR</h2><p>Example devices for your dashboard. This does not scan your Wi-Fi.</p><button class="action" onclick="simulateDevices()">REFRESH DEMO DEVICES</button><div class="output" id="deviceOutput">Demo device list is ready.</div></div>
  <div class="panel"><h2>NETWORK ACTIVITY SIMULATOR</h2><canvas class="chart" id="networkChart" width="500" height="120"></canvas><button class="action" onclick="drawNetwork()">REFRESH VISUALIZATION</button></div>
  <div class="panel"><h2>WI-FI QR CARD</h2><p>Enter your Wi-Fi details to create a QR code. The information is sent to an external QR image service to generate the code.</p>
   <input id="wifiName" placeholder="Network name (SSID)">
   <input id="wifiPass" type="password" placeholder="Wi-Fi password">
   <select id="wifiSecurity"><option value="WPA">WPA/WPA2</option><option value="WEP">WEP</option><option value="nopass">No password</option></select>
   <button class="action" onclick="wifiQR()">CREATE QR</button><div id="wifiQRResult"></div>
  </div>
 </div>
</section>

<!-- FILES -->
<section class="page" id="files">
 <h1>FILE MANAGER</h1>
 <p>Choose files from this device to inspect basic information or preview text files.</p>
 <div class="panel">
  <input type="file" id="fileInput" multiple onchange="inspectFiles()">
  <div id="fileResults" class="output">No files selected.</div>
 </div>
 <br>
 <div class="panel">
  <h2>LOCAL TEXT FILE VIEWER</h2>
  <input type="file" id="textFile" accept=".txt,.json,.html,.css,.js,.md,.csv" onchange="readTextFile()">
  <textarea id="filePreview" placeholder="Text file contents appear here..."></textarea>
  <button class="action" onclick="downloadText('filePreview','edited-file.txt')">DOWNLOAD TEXT</button>
 </div>
 <br>
 <div class="panel">
  <h2>IMAGE METADATA VIEWER</h2>
  <input type="file" id="imageFile" accept="image/*" onchange="imageInfo()">
  <div id="imageInfoOutput" class="output"></div>
  <img id="imageDisplay" style="max-width:100%;max-height:240px;display:none;margin-top:10px">
 </div>
</section>

<!-- ORGANIZER -->
<section class="page" id="organizer">
 <h1>PERSONAL ORGANIZER</h1>
 <div class="grid wide">
  <div class="panel">
   <h2>TO-DO MANAGER</h2>
   <div class="row"><input id="taskInput" placeholder="Add a task..."><button class="action" onclick="addTask()">ADD</button></div>
   <div id="taskList"></div>
   <button class="action danger" onclick="clearTasks()">CLEAR ALL</button>
  </div>
  <div class="panel">
   <h2>NOTES</h2>
   <input id="noteTitle" placeholder="Note title">
   <textarea id="noteText" placeholder="Write your notes..."></textarea>
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
   <h2>COUNTDOWN TIMER</h2>
   <input id="timerSeconds" type="number" min="1" value="60" placeholder="Seconds">
   <div class="stat" id="countdown">01:00</div>
   <button class="action" onclick="startTimer()">START</button>
   <button class="action" onclick="pauseTimer()">PAUSE</button>
   <button class="action" onclick="resetTimer()">RESET</button>
  </div>
  <div class="panel">
   <h2>CALCULATOR</h2>
   <input id="calcInput" placeholder="Example: (12 + 4) * 3">
   <button class="action" onclick="calculate()">CALCULATE</button>
   <div class="output" id="calcOutput"></div>
  </div>
  <div class="panel">
   <h2>WORLD CLOCK</h2>
   <select id="worldZone" onchange="worldClock()">
    <option value="America/New_York">New York</option><option value="America/Los_Angeles">Los Angeles</option>
    <option value="Europe/London">London</option><option value="Europe/Paris">Paris</option>
    <option value="Asia/Tokyo">Tokyo</option><option value="Australia/Sydney">Sydney</option>
   </select>
   <div class="stat" id="worldTime"></div>
  </div>
  <div class="panel">
   <h2>CALENDAR</h2>
   <input type="date" id="calendarDate">
   <input id="calendarEvent" placeholder="Event name">
   <button class="action" onclick="saveEvent()">SAVE EVENT</button>
   <div id="eventList"></div>
  </div>
 </div>
</section>

<!-- MEDIA -->
<section class="page" id="media">
 <h1>MEDIA CENTER</h1>
 <div class="grid wide">
  <div class="panel">
   <h2>MUSIC PLAYER</h2>
   <input type="file" id="musicFile" accept="audio/*" onchange="loadMusic()">
   <audio id="audioPlayer" controls style="width:100%;margin-top:12px"></audio>
   <p>Choose an audio file stored on your device.</p>
  </div>
  <div class="panel">
   <h2>SOUNDBOARD</h2>
   <p>Generate simple interface sounds.</p>
   <button class="action" onclick="beep(440)">BEEP</button>
   <button class="action" onclick="beep(660)">ALERT</button>
   <button class="action" onclick="beep(880)">HIGH PING</button>
   <button class="action" onclick="beep(220)">LOW PING</button>
  </div>
  <div class="panel">
   <h2>RANDOM MISSION GENERATOR</h2>
   <button class="action" onclick="mission()">GENERATE MISSION</button>
   <div class="output" id="missionOutput">Awaiting mission...</div>
  </div>
  <div class="panel">
   <h2>DIGITAL PET</h2>
   <div class="stat" id="petFace">🤖</div>
   <div id="petStatus" class="small">Your digital companion is waiting.</div>
   <button class="action" onclick="feedPet()">FEED</button>
   <button class="action" onclick="playPet()">PLAY</button>
   <button class="action" onclick="petSleep()">SLEEP</button>
  </div>
 </div>
</section>

<!-- ASSISTANT -->
<section class="page" id="assistant">
 <h1>AI-STYLE ASSISTANT PANEL</h1>
 <p>This is an offline demo assistant with preset responses. It does not connect to an AI service.</p>
 <div class="panel">
  <div class="terminal" id="chatOutput"><div class="termline termgreen">SYSTEM: Offline helper initialized. Ask for a command, tool, or tip.</div></div>
  <div class="row"><input id="chatInput" placeholder="Message the helper..."><button class="action" onclick="sendChat()">SEND</button></div>
  <button class="action" onclick="clearChat()">CLEAR CHAT</button>
 </div>
</section>

<!-- SETTINGS -->
<section class="page" id="settings">
 <h1>SYSTEM SETTINGS</h1>
 <div class="grid wide">
  <div class="panel">
   <h2>OPERATOR PROFILE</h2>
   <input id="operatorName" placeholder="Operator name">
   <button class="action" onclick="saveOperator()">SAVE NAME</button>
  </div>
  <div class="panel">
   <h2>COLOR THEME</h2>
   <select id="themeChoice" onchange="setTheme(this.value)">
    <option value="green">Matrix Green</option><option value="red">Red Alert</option>
    <option value="purple">Purple Neon</option><option value="blue">Cyber Blue</option>
   </select>
  </div>
  <div class="panel">
   <h2>VISUAL EFFECTS</h2>
   <label><input type="checkbox" id="matrixToggle" checked onchange="toggleMatrix(this.checked)"> Matrix background</label>
   <label><input type="checkbox" id="soundToggle" checked> Sound effects</label>
   <button class="action" onclick="toggleFullscreen()">FULLSCREEN</button>
  </div>
  <div class="panel">
   <h2>DATA MANAGEMENT</h2>
   <button class="action" onclick="exportData()">EXPORT NOTES & TASKS</button>
   <button class="action danger" onclick="resetApp()">RESET LOCAL DATA</button>
   <p>Export your data before resetting. Reset clears locally saved notes, tasks, events and settings.</p>
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

<!-- WIDGET BUILDER -->
<section class="page" id="widgets">
 <h1>WIDGET BUILDER</h1>
 <p>Choose which quick widgets appear on your dashboard.</p>
 <div class="panel">
  <label><input type="checkbox" id="widgetClock" checked onchange="saveWidgets()"> Clock</label>
  <label><input type="checkbox" id="widgetTasks" checked onchange="saveWidgets()"> Task count</label>
  <label><input type="checkbox" id="widgetNotes" checked onchange="saveWidgets()"> Saved notes count</label>
  <label><input type="checkbox" id="widgetConnection" checked onchange="saveWidgets()"> Connection status</label>
  <button class="action" onclick="saveWidgets()">SAVE WIDGETS</button>
 </div>
</section>

<!-- SECRET -->
<section class="page" id="secret">
 <h1>CLASSIFIED AREA</h1>
 <p>Find the secret command in the terminal to unlock the easter egg.</p>
 <div class="panel">
  <h2>SECRET ACCESS</h2>
  <input id="secretCode" placeholder="Enter secret code">
  <button class="action" onclick="unlockSecret()">UNLOCK</button>
  <div id="secretResult" class="output">ACCESS LOCKED</div>
 </div>
 <div class="panel" style="margin-top:13px">
  <h2>OPERATOR ACHIEVEMENTS</h2>
  <div id="achievements" class="small">No achievements yet.</div>
 </div>
</section>
</main>
<footer>HACKER_OS // PERSONAL LOCAL DASHBOARD // VERSION 2.0</footer>
<div id="toast"></div>

<script>
const $=id=>document.getElementById(id);
const get=(key,def)=>{try{return JSON.parse(localStorage.getItem(key))??def}catch{return def}};
const put=(key,val)=>localStorage.setItem(key,JSON.stringify(val));
let startTime=Date.now(),stopStart=0,stopElapsed=0,stopInterval=null;
let timerRemaining=60,timerInterval=null,petMood=0;
let activeCategory='all',matrixEnabled=true;
function toast(msg){let t=$('toast');t.textContent=msg;t.style.display='block';clearTimeout(toast.t);toast.t=setTimeout(()=>t.style.display='none',2200)}
function logActivity(msg){let a=get('activity',[]);a.unshift(new Date().toLocaleTimeString()+' — '+msg);put('activity',a.slice(0,8));renderActivity()}
function renderActivity(){$('activity').innerHTML=get('activity',['System initialized.']).map(x=>'<div>› '+escapeHTML(x)+'</div>').join('')}
function escapeHTML(s){return String(s).replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]))}
function page(id){
 document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
 let target=$(id);if(!target)return;
 target.classList.add('active');
 document.querySelectorAll('nav button').forEach(b=>b.classList.toggle('active',b.dataset.page===id));
 if(id==='organizer'){renderTasks();renderNotes();renderEvents()}
 if(id==='settings'){renderApps()}
 if(id==='dashboard')renderWidgets();
 if(id==='secret')renderAchievements();
}
$('nav').addEventListener('click',e=>{let b=e.target.closest('button[data-page]');if(b)page(b.dataset.page)});
function updateClock(){
 let d=new Date();$('clock').textContent=d.toLocaleTimeString();
 $('date').textContent=d.toLocaleDateString(undefined,{weekday:'long',year:'numeric',month:'long',day:'numeric'});
 let sec=Math.floor((Date.now()-startTime)/1000);
 $('uptime').textContent=[Math.floor(sec/3600),Math.floor(sec/60)%60,sec%60].map(x=>String(x).padStart(2,'0')).join(':');
 $('connection').textContent=navigator.onLine?'ONLINE':'OFFLINE';
 $('headerStatus').textContent=navigator.onLine?'● SYSTEM ONLINE':'● OFFLINE';
 $('cpuText').textContent=Math.floor(12+Math.random()*70)+'%';
 $('ramText').textContent=Math.floor(20+Math.random()*65)+'%';
 $('cpuBar').style.width=$('cpuText').textContent;
 $('ramBar').style.width=$('ramText').textContent;
 worldClock();
}
setInterval(updateClock,1000);updateClock();
window.addEventListener('online',checkConnection);window.addEventListener('offline',checkConnection);
function checkConnection(){
 $('netStatus').textContent=navigator.onLine?'ONLINE':'OFFLINE';
 let c=navigator.connection;
 $('netDetails').textContent='Browser online: '+navigator.onLine+
 '\nConnection type: '+(c?.type||'Not provided by browser')+
 '\nEffective type: '+(c?.effectiveType||'Not provided')+
 '\nDownlink estimate: '+(c?.downlink?c.downlink+' Mbps':'Not provided')+
 '\nDevice language: '+navigator.language;
}
checkConnection();

<!-- MATRIX BACKGROUND -->
const mc=$('matrix'),ctx=mc.getContext('2d');let drops=[];
function resizeMatrix(){mc.width=innerWidth;mc.height=innerHeight;drops=Array(Math.ceil(mc.width/17)).fill(1)}
window.addEventListener('resize',resizeMatrix);resizeMatrix();
setInterval(()=>{
 if(!matrixEnabled)return;
 ctx.fillStyle='rgba(5,9,7,.09)';ctx.fillRect(0,0,mc.width,mc.height);
 ctx.fillStyle=getComputedStyle(document.documentElement).getPropertyValue('--green')||'#39ff88';
 ctx.font='14px monospace';
 drops.forEach((y,i)=>{ctx.fillText(String.fromCharCode(0x30A0+Math.random()*96),i*17,y*17);
 if(y*17>mc.height&&Math.random()>.975)drops[i]=0;drops[i]++});
},65);

function terminalLine(text,cls=''){
 let d=document.createElement('div');d.className='termline '+cls;d.textContent=text;
 $('terminalOutput').appendChild(d);$('terminalOutput').scrollTop=$('terminalOutput').scrollHeight;
}
function terminalCommand(cmd){
 let c=cmd.trim().toUpperCase();if(!c)return;
 terminalLine('operator@hacker-os:~$ '+cmd,'termblue');
 const commands={
 HELP:'COMMANDS: HELP, STATUS, TIME, ABOUT, SCAN, MATRIX, SECRET, TOOLS, CLEAR',
 STATUS:'SYSTEM STATUS: ONLINE\nLOCAL DASHBOARD ACTIVE\nNETWORK SCAN: NOT AVAILABLE',
 TIME:new Date().toString(),
 ABOUT:'HACKER OS — A local browser-based command center.',
 SCAN:'SIMULATION ONLY: No real devices or networks are scanned.',
 MATRIX:'MATRIX EFFECT IS '+(matrixEnabled?'ON':'OFF'),
 SECRET:'EASTER EGG HINT: Try the code MATRIX in the Secret Room.',
 TOOLS:'Available sections: SECURITY, DEV LAB, ORGANIZER, FILES, MEDIA.'
 };
 if(c==='CLEAR'){clearTerminal();return}
 if(c==='SECRET')put('achievementSecret',true);
 terminalLine(commands[c]||'Unknown command. Type HELP for commands.','termgreen');
 logActivity('Terminal command: '+c);
}
function runCommand(){let v=$('commandInput').value;terminalCommand(v);$('commandInput').value=''}
$('commandInput').addEventListener('keydown',e=>{if(e.key==='Enter')runCommand()});
function clearTerminal(){$('terminalOutput').innerHTML='';terminalLine('HACKER OS TERMINAL READY. TYPE HELP.','termgreen')}
clearTerminal();

const toolData=[
 ['Base64 Encoder','text','Convert text to Base64.','base'],
 ['Text Analyzer','text','Count words, lines and characters.','analyze'],
 ['URL Encoder','text','Encode or decode URL text.','url'],
 ['JSON Formatter','developer','Format JSON data.','json'],
 ['UUID Generator','utility','Generate unique IDs.','uuid'],
 ['Color Generator','developer','Pick a color code.','color'],
 ['Gradient Generator','developer','Create a CSS gradient.','gradient'],
 ['Random Number','utility','Generate random numbers.','random'],
 ['Unit Converter','utility','Convert common units.','unit'],
 ['Timestamp Converter','utility','Convert Unix timestamps.','timestamp'],
 ['Regex Tester','developer','Test a regular expression.','regex'],
 ['Markdown Preview','developer','Preview Markdown text.','markdown'],
 ['XML Formatter','developer','Format XML text.','xml']
];
function renderTools(list=toolData){
 $('toolGrid').innerHTML=list.map(t=>`<div class="panel toolcard" onclick="openTool('${t[3]}')"><div class="symbol">⌘</div><h3>${t[0]}</h3><p>${t[2]}</p><span class="pill">${t[1]}</span></div>`).join('');
}
function filterTools(){let q=$('toolSearch').value.toLowerCase();renderTools(toolData.filter(t=>(t[0]+t[2]+t[1]).toLowerCase().includes(q)&&(activeCategory==='all'||t[1]===activeCategory)))}
function filterCategory(c){activeCategory=c;filterTools()}
function openTool(id){page('tools');let t=toolData.find(x=>x[3]===id);$('toolWorkspace').innerHTML='<h2>'+escapeHTML(t?.[0]||'TOOL')+'</h2><p>'+escapeHTML(t?.[2]||'')+'</p><p>Open the matching tool in its section below.</p>';if(id==='base')page('security');if(['json','regex','markdown','xml','color','gradient','uuid','url','analyze','unit','timestamp','random'].includes(id))page('developer')}
renderTools();

function base64Tool(mode){try{let s=$('baseInput').value;let result=mode==='encode'?btoa(unescape(encodeURIComponent(s))):decodeURIComponent(escape(atob(s)));$('baseOutput').textContent=result}catch(e){$('baseOutput').textContent='Invalid input.'}}
function cipherTool(dir){let s=$('cipherInput').value,n=Math.max(1,Math.min(25,Number($('cipherShift').value)||3))*dir;$('cipherOutput').textContent=s.replace(/[a-z]/gi,ch=>{let base=ch<='Z'?65:97;return String.fromCharCode((ch.charCodeAt(0)-base+n+260)%26+base)})}
function checkPassword(){
 let s=$('passCheck').value,score=0;
 if(s.length>=12)score++;if(/[a-z]/.test(s)&&/[A-Z]/.test(s))score++;
 if(/\d/.test(s))score++;if(/[^A-Za-z0-9]/.test(s))score++;
 $('passResult').textContent=!s?'Enter a sample password.':['Very weak','Weak','Fair','Strong','Very strong'][score]+' demo rating. Length: '+s.length;
}
function generatePassword(){
 let len=Math.max(8,Math.min(64,Number($('passLength').value)||20));
 let chars='ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz23456789'+($('passSymbols').checked?'!@#$%&*+-_?':'');
 let a=new Uint32Array(len);crypto.getRandomValues(a);
 let p=Array.from(a,x=>chars[x%chars.length]).join('');
 $('generatedPassword').textContent=p;logActivity('Generated a sample password');
}
async function makeHash(){
 let data=new TextEncoder().encode($('hashInput').value);
 if(!crypto.subtle){$('hashOutput').textContent='Secure hashing is unavailable in this browser context.';return}
 let h=await crypto.subtle.digest('SHA-256',data);
 $('hashOutput').textContent=Array.from(new Uint8Array(h)).map(x=>x.toString(16).padStart(2,'0')).join('');
}
function inspectURL(){
 try{let u=new URL($('urlCheck').value);$('urlResult').textContent='Protocol: '+u.protocol+'\nHost: '+u.hostname+'\nHTTPS: '+(u.protocol==='https:'?'Yes':'No')+'\nNote: This is a format check, not a reputation or malware scan.'}
 catch{$('urlResult').textContent='That does not look like a valid full URL.'}
}
function formatJSON(){try{$('jsonOutput').textContent=JSON.stringify(JSON.parse($('jsonInput').value),null,2)}catch(e){$('jsonOutput').textContent='Invalid JSON: '+e.message}}
function minifyJSON(){try{$('jsonOutput').textContent=JSON.stringify(JSON.parse($('jsonInput').value))}catch(e){$('jsonOutput').textContent='Invalid JSON: '+e.message}}
function formatXML(){
 try{let s=$('xmlInput').value.replace(/>\s*</g,'><').replace(/</g,'\n<').trim();let level=0;
 $('xmlOutput').textContent=s.split('\n').map(line=>{if(/^<\//.test(line))level=Math.max(0,level-1);let out='  '.repeat(level)+line;if(/^<[^!?/][^>]*[^/]?>$/.test(line)&&!/<\/[^>]+>$/.test(line))level++;return out}).join('\n')}
 catch(e){$('xmlOutput').textContent='Could not format XML.'}
}
function testRegex(){try{let r=new RegExp($('regexPattern').value,$('regexFlags').value);let s=$('regexText').value,m=[...s.matchAll(r)];$('regexOutput').textContent=m.length+' match(es):\n'+m.map(x=>x[0]).join('\n')}catch(e){$('regexOutput').textContent='Regex error: '+e.message}}
function showColor(){let c=$('colorPicker').value;$('colorOutput').textContent='HEX: '+c+'\nRGB: '+parseInt(c.slice(1,3),16)+', '+parseInt(c.slice(3,5),16)+', '+parseInt(c.slice(5,7),16)}
function makeGradient(){let g=`linear-gradient(120deg, ${$('gradA').value}, ${$('gradB').value})`;$('gradientPreview').style.background=g;$('gradientOutput').textContent='background: '+g+';'}
function makeUUID(){$('uuidOutput').textContent=crypto.randomUUID?crypto.randomUUID():'UUID generation is unavailable.'}
function urlTool(enc){try{$('urlOutput').textContent=enc?encodeURIComponent($('urlInput').value):decodeURIComponent($('urlInput').value)}catch{$('urlOutput').textContent='Invalid encoded text.'}}
function analyzeText(){let s=$('analyzeInput').value;$('analyzeOutput').textContent='Characters: '+s.length+'\nWords: '+(s.trim()?s.trim().split(/\s+/).length:0)+'\nLines: '+(s?s.split(/\n/).length:0)+'\nLetters: '+(s.match(/[a-z]/gi)||[]).length+'\nDigits: '+(s.match(/\d/g)||[]).length}
function convertUnit(){let v=Number($('unitValue').value),t=$('unitType').value;if(!Number.isFinite(v))return $('unitOutput').textContent='Enter a valid number.';let r={km:v*.621371,mi:v*1.60934,kg:v*2.20462,lb:v/2.20462,c:v*9/5+32,f:(v-32)*5/9}[t];$('unitOutput').textContent=r.toFixed(4)}
function convertTimestamp(){let v=Number($('timestampInput').value);if(!Number.isFinite(v))return $('timestampOutput').textContent='Enter a timestamp.';let d=new Date(v*1000);$('timestampOutput').textContent=isNaN(d)?'Invalid timestamp':d.toString()}
function randomNumber(){let a=Number($('randMin').value),b=Number($('randMax').value);if(!Number.isInteger(a)||!Number.isInteger(b)||b<a)return $('randomOutput').textContent='Enter valid minimum and maximum.';let x=new Uint32Array(1);crypto.getRandomValues(x);$('randomOutput').textContent=String(a+x[0]%(b-a+1))}
function previewHTML(){$('htmlPreview').srcdoc=$('htmlCode').value}
function previewCSS(){$('cssPreview').srcdoc='<!doctype html><html><head><style>'+ $('cssCode').value+'</style></head><body>'+ $('cssHTML').value+'</body></html>'}
function runJS(){$('jsPreview').srcdoc='<!doctype html><body><pre id="out"></pre><script>try{'+$('jsCode').value+'}catch(e){document.body.innerText=e.message}<\/script></body>'}
function previewMarkdown(){
 let s=escapeHTML($('mdInput').value);
 s=s.replace(/^### (.*)$/gm,'<h3>$1</h3>').replace(/^## (.*)$/gm,'<h2>$1</h2>').replace(/^# (.*)$/gm,'<h1>$1</h1>').replace(/\*\*(.*?)\*\*/g,'<b>$1</b>').replace(/\*(.*?)\*/g,'<i>$1</i>').replace(/\n/g,'<br>');
 $('mdPreview').srcdoc='<body style="font-family:Arial;padding:12px">'+s+'</body>';
}
function calculate(){
 let s=$('calcInput').value.replace(/\s/g,'');
 if(!/^[0-9+\-*/().%^]+$/.test(s))return $('calcOutput').textContent='Only numbers and basic math operators are allowed.';
 try{
 let i=0;
 function expr(){let v=term();while(s[i]==='+'||s[i]==='-'){let op=s[i++],n=term();v=op==='+'?v+n:v-n}return v}
 function term(){let v=power();while(['*','/','%'].includes(s[i])){let op=s[i++],n=power();if((op==='/'||op==='%')&&n===0)throw Error('Cannot divide by zero');v=op==='*'?v*n:op==='/'?v/n:v%n}return v}
 function power(){let v=atom();if(s[i]==='^'){i++;v=Math.pow(v,power())}return v}
 function atom(){if(s[i]==='+'||s[i]==='-'){let op=s[i++];return (op==='-'?-1:1)*atom()}if(s[i]==='('){i++;let v=expr();if(s[i++]!==')')throw Error('Missing closing parenthesis');return v}let start=i;while(/[0-9.]/.test(s[i]||'')&&i<s.length)i++;if(start===i)throw Error('Invalid expression');let v=Number(s.slice(start,i));if(!Number.isFinite(v))throw Error('Invalid number');return v}
 let result=expr();if(i!==s.length||!Number.isFinite(result))throw Error('Invalid expression');$('calcOutput').textContent=String(result);
 }catch(e){$('calcOutput').textContent=e.message||'Invalid expression.'}
}
function worldClock(){$('worldTime').textContent=new Date().toLocaleTimeString('en-US',{timeZone:$('worldZone').value})}

function latencyTest(){
 $('latencyOutput').textContent='Testing...';let start=performance.now();
 fetch('https://www.cloudflare.com/cdn-cgi/trace?check='+Date.now(),{cache:'no-store',mode:'no-cors'})
 .then(()=> $('latencyOutput').textContent='Request completed in approximately '+Math.round(performance.now()-start)+' ms.\nThis is a rough browser request time, not a full internet speed test.')
 .catch(()=> $('latencyOutput').textContent='Could not complete the test. Check your connection.');
}
function simulateDevices(){$('deviceOutput').textContent='DEMO DEVICE A — STATUS: ONLINE\nDEMO DEVICE B — STATUS: ONLINE\nDEMO DEVICE C — STATUS: IDLE\n\nThese are fictional demo devices, not real devices on your network.'}
function drawNetwork(){
 let c=$('networkChart'),x=c.getContext('2d');x.clearRect(0,0,c.width,c.height);x.strokeStyle='#39ff88';x.beginPath();
 for(let i=0;i<100;i++){let y=60+Math.sin(i*.2)*20+(Math.random()*20-10);i?x.lineTo(i*5,y):x.moveTo(i*5,y)}x.stroke();
}
drawNetwork();
function wifiQR(){
 let ssid=$('wifiName').value,pass=$('wifiPass').value,sec=$('wifiSecurity').value;
 if(!ssid)return toast('Enter a network name.');
 let payload=`WIFI:T:${sec};S:${ssid};P:${pass};;`;
 let img=document.createElement('img');img.alt='Wi-Fi QR code';img.style.maxWidth='220px';img.style.display='block';img.style.marginTop='12px';
 img.src='https://api.qrserver.com/v1/create-qr-code/?size=220x220&data='+encodeURIComponent(payload);
 let box=$('wifiQRResult');box.innerHTML='';box.appendChild(img);
 box.insertAdjacentText('beforeend',' QR generation uses an external service. Avoid entering sensitive network details if you do not want them sent to that service.');
}
function inspectFiles(){
 let fs=[...$('fileInput').files];$('fileResults').textContent=fs.map(f=>f.name+'\nType: '+(f.type||'Unknown')+'\nSize: '+(f.size/1024).toFixed(2)+' KB\nLast modified: '+new Date(f.lastModified).toLocaleString()).join('\n\n')||'No files selected.';
}
function readTextFile(){let f=$('textFile').files[0];if(!f)return;let r=new FileReader();r.onload=()=> $('filePreview').value=r.result;r.readAsText(f)}
function imageInfo(){
 let f=$('imageFile').files[0];if(!f)return;
 $('imageInfoOutput').textContent='Name: '+f.name+'\nType: '+f.type+'\nSize: '+(f.size/1024).toFixed(2)+' KB';
 let url=URL.createObjectURL(f),img=$('imageDisplay');img.src=url;img.style.display='block';
 img.onload=()=>{$('imageInfoOutput').textContent+='\nDimensions: '+img.naturalWidth+' × '+img.naturalHeight}
}
function downloadText(id,name){let blob=new Blob([$(id).value],{type:'text/plain'}),a=document.createElement('a');a.href=URL.createObjectURL(blob);a.download=name;a.click();URL.revokeObjectURL(a.href)}
function tasks(){return get('tasks',[])}
function renderTasks(){$('taskList').innerHTML=tasks().map((t,i)=>`<div class="task"><input type="checkbox" ${t.done?'checked':''} onchange="toggleTask(${i})"><span class="${t.done?'done':''}">${escapeHTML(t.text)}</span><button class="action danger" onclick="deleteTask(${i})">×</button></div>`).join('')||'<p>No tasks yet.</p>'}
function addTask(){let v=$('taskInput').value.trim();if(!v)return;let a=tasks();a.push({text:v,done:false});put('tasks',a);$('taskInput').value='';renderTasks();renderWidgets();logActivity('Task added')}
function toggleTask(i){let a=tasks();a[i].done=!a[i].done;put('tasks',a);renderTasks();renderWidgets()}
function deleteTask(i){let a=tasks();a.splice(i,1);put('tasks',a);renderTasks();renderWidgets()}
function clearTasks(){if(confirm('Clear all tasks?')){put('tasks',[]);renderTasks();renderWidgets()}}
function renderNotes(){let a=get('notes',[]);$('notesList').innerHTML=a.map((n,i)=>`<div class="task"><span><b>${escapeHTML(n.title)}</b><br>${escapeHTML(n.text.slice(0,70))}</span><button class="action" onclick="loadNote(${i})">OPEN</button><button class="action danger" onclick="deleteNote(${i})">×</button></div>`).join('')||'<p>No saved notes.</p>'}
function saveNote(){let title=$('noteTitle').value.trim()||'Untitled',text=$('noteText').value;if(!text.trim())return toast('Write something first.');let a=get('notes',[]);a.unshift({title,text});put('notes',a);renderNotes();renderWidgets();toast('Note saved')}
function loadNote(i){let n=get('notes',[])[i];$('noteTitle').value=n.title;$('noteText').value=n.text}
function deleteNote(i){let a=get('notes',[]);a.splice(i,1);put('notes',a);renderNotes();renderWidgets()}
function startStopwatch(){if(stopInterval)return;stopStart=Date.now()-stopElapsed;stopInterval=setInterval(()=>{stopElapsed=Date.now()-stopStart;$('stopwatch').textContent=formatTime(stopElapsed)},250)}
function pauseStopwatch(){clearInterval(stopInterval);stopInterval=null}
function resetStopwatch(){pauseStopwatch();stopElapsed=0;$('stopwatch').textContent='00:00:00'}
function formatTime(ms){let s=Math.floor(ms/1000);return [Math.floor(s/3600),Math.floor(s/60)%60,s%60].map(x=>String(x).padStart(2,'0')).join(':')}
function startTimer(){if(timerInterval)return;let input=Number($('timerSeconds').value);if(timerRemaining<=0)timerRemaining=Math.max(1,input);timerInterval=setInterval(()=>{timerRemaining--;showTimer();if(timerRemaining<=0){pauseTimer();toast('Timer finished!');beep(660)}},1000);showTimer()}
function pauseTimer(){clearInterval(timerInterval);timerInterval=null}
function resetTimer(){pauseTimer();timerRemaining=Math.max(1,Number($('timerSeconds').value)||60);showTimer()}
function showTimer(){$('countdown').textContent=String(Math.floor(timerRemaining/60)).padStart(2,'0')+':'+String(timerRemaining%60).padStart(2,'0')}
function saveEvent(){let d=$('calendarDate').value,n=$('calendarEvent').value.trim();if(!d||!n)return toast('Enter a date and event.');let a=get('events',[]);a.push({date:d,name:n});put('events',a);renderEvents();$('calendarEvent').value=''}
function renderEvents(){$('eventList').innerHTML=get('events',[]).sort((a,b)=>a.date.localeCompare(b.date)).map((e,i)=>`<div class="task"><span>${escapeHTML(e.date)} — ${escapeHTML(e.name)}</span><button class="action danger" onclick="deleteEvent(${i})">×</button></div>`).join('')||'<p>No events saved.</p>'}
function deleteEvent(i){let a=get('events',[]);a.splice(i,1);put('events',a);renderEvents()}
function loadMusic(){let f=$('musicFile').files[0];if(!f)return;$('audioPlayer').src=URL.createObjectURL(f);$('audioPlayer').load();toast('Audio loaded')}
function beep(freq){if(!$('soundToggle').checked)return;try{let A=window.AudioContext||window.webkitAudioContext,c=new A(),o=c.createOscillator(),g=c.createGain();o.frequency.value=freq;o.connect(g);g.connect(c.destination);g.gain.value=.08;o.start();o.stop(c.currentTime+.16);o.onended=()=>c.close()}catch{}}
function mission(){let a=['Organize your digital workspace','Create a new color theme','Write a useful note','Build a tiny HTML page','Complete three tasks','Explore the developer lab','Generate a new dashboard widget','Learn a new keyboard shortcut'];$('missionOutput').textContent=a[Math.floor(Math.random()*a.length)]}
function feedPet(){petMood++;$('petFace').textContent='🤖';$('petStatus').textContent='Your companion appreciates the energy. Happiness: '+petMood}
function playPet(){petMood++;$('petFace').textContent='😎';$('petStatus').textContent='Your companion is having fun. Happiness: '+petMood}
function petSleep(){$('petFace').textContent='😴';$('petStatus').textContent='Your companion is resting.'}
function sendChat(){
 let q=$('chatInput').value.trim();if(!q)return;let box=$('chatOutput');
 let u=document.createElement('div');u.className='termline termblue';u.textContent='YOU: '+q;box.appendChild(u);
 let l=q.toLowerCase(),reply='I am an offline demo helper. Try asking about the terminal, tools, notes, or settings.';
 if(l.includes('help'))reply='Try the TOOLS library, SECURITY center, DEV LAB, FILE MANAGER, or ORGANIZER.';
 else if(l.includes('time'))reply='The current local time is '+new Date().toLocaleTimeString()+'.';
 else if(l.includes('password'))reply='Use unique passwords and enable two-factor authentication. Never share verification codes.';
 else if(l.includes('terminal'))reply='Open TERMINAL and type HELP to see the available demo commands.';
 else if(l.includes('note'))reply='Open ORGANIZER to create and save notes in this browser.';
 else if(l.includes('theme'))reply='Open SETTINGS and choose Green, Red, Purple, or Blue.';
 let a=document.createElement('div');a.className='termline termgreen';a.textContent='HELPER: '+reply;box.appendChild(a);box.scrollTop=box.scrollHeight;$('chatInput').value='';
}
function clearChat(){$('chatOutput').innerHTML=''}
$('chatInput').addEventListener('keydown',e=>{if(e.key==='Enter')sendChat()});
function saveOperator(){put('operator',$('operatorName').value.trim());toast('Operator name saved')}
function setTheme(t){
 let themes={green:['#39ff88','#16c765'],red:['#ff5268','#c72b43'],purple:['#c18aff','#8745c9'],blue:['#50c8ff','#258ac4']};
 let v=themes[t]||themes.green;document.documentElement.style.setProperty('--green',v[0]);document.documentElement.style.setProperty('--green2',v[1]);put('theme',t);
}
function toggleMatrix(v){matrixEnabled=v;mc.style.display=v?'block':'none';put('matrix',v)}
function toggleFullscreen(){if(!document.fullscreenElement)document.documentElement.requestFullscreen?.();else document.exitFullscreen?.()}
function addApp(){let n=$('appName').value.trim(),u=$('appURL').value.trim();try{let url=new URL(u);if(!['http:','https:'].includes(url.protocol))throw 0;let a=get('apps',[]);a.push({name:n||url.hostname,url:url.href});put('apps',a);renderApps();$('appName').value='';$('appURL').value=''}catch{toast('Enter a valid http or https website URL.')}}
function renderApps(){$('appList').innerHTML=get('apps',[]).map((a,i)=>`<div class="task"><a href="${escapeHTML(a.url)}" target="_blank" rel="noopener noreferrer" style="color:var(--green)">${escapeHTML(a.name)}</a><button class="action danger" onclick="deleteApp(${i})">×</button></div>`).join('')||'<p>No saved websites.</p>'}
function deleteApp(i){let a=get('apps',[]);a.splice(i,1);put('apps',a);renderApps()}
function renderWidgets(){
 let enabled=get('widgets',{clock:true,tasks:true,notes:true,connection:true}),w=[];
 if(enabled.clock)w.push(['LOCAL TIME',new Date().toLocaleTimeString()]);
 if(enabled.tasks)w.push(['TASKS',tasks().filter(x=>!x.done).length+' unfinished']);
 if(enabled.notes)w.push(['NOTES',get('notes',[]).length+' saved']);
 if(enabled.connection)w.push(['CONNECTION',navigator.onLine?'ONLINE':'OFFLINE']);
 $('dashboardWidgets').innerHTML=w.map(x=>`<div class="panel"><h3>${x[0]}</h3><div class="stat">${escapeHTML(x[1])}</div></div>`).join('');
}
function saveWidgets(){put('widgets',{clock:$('widgetClock').checked,tasks:$('widgetTasks').checked,notes:$('widgetNotes').checked,connection:$('widgetConnection').checked});renderWidgets();toast('Widgets updated')}
function renderAchievements(){let a=[];if(get('achievementSecret',false))a.push('★ Secret room discovered');if(get('tasks',[]).length>=5)a.push('★ Task collector');if(get('notes',[]).length>=3)a.push('★ Note keeper');$('achievements').textContent=a.join('\n')||'Keep exploring to unlock achievements.'}
function unlockSecret(){let c=$('secretCode').value.trim().toUpperCase();if(c==='MATRIX'){$('secretResult').textContent='ACCESS GRANTED. WELCOME TO THE SECRET ROOM.';put('achievementSecret',true);renderAchievements();toast('Secret unlocked')}else $('secretResult').textContent='ACCESS DENIED.'}
function exportData(){
 let data={tasks:get('tasks',[]),notes:get('notes',[]),events:get('events',[]),apps:get('apps',[]),activity:get('activity',[])};
 let blob=new Blob([JSON.stringify(data,null,2)],{type:'application/json'}),a=document.createElement('a');
 a.href=URL.createObjectURL(blob);a.download='hacker-os-backup.json';a.click();URL.revokeObjectURL(a.href);
}
function resetApp(){if(!confirm('This clears locally saved HACKER OS data. Continue?'))return;
 ['tasks','notes','events','apps','activity','operator','theme','widgets','achievementSecret'].forEach(k=>localStorage.removeItem(k));
 location.reload();
}
function copyText(id){let s=$(id).textContent;navigator.clipboard?.writeText(s).then(()=>toast('Copied')).catch(()=>toast('Clipboard access unavailable'))}
function saveSettingsToUI(){
 $('operatorName').value=get('operator','');let theme=get('theme','green');$('themeChoice').value=theme;setTheme(theme);
 matrixEnabled=get('matrix',true);$('matrixToggle').checked=matrixEnabled;toggleMatrix(matrixEnabled);
 let w=get('widgets',{clock:true,tasks:true,notes:true,connection:true});
 $('widgetClock').checked=w.clock;$('widgetTasks').checked=w.tasks;$('widgetNotes').checked=w.notes;$('widgetConnection').checked=w.connection;
}
saveSettingsToUI();renderActivity();renderWidgets();renderTasks();renderNotes();renderEvents();renderApps();simulateDevices();showTimer();
logActivity('HACKER OS dashboard started');
</script>
</body>
</html>
