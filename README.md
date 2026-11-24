
# blwh-app-V2.1node_modules/
ios/
android/
build/
dist/
*.ipa
*.apk
windows/Output/

{
  "appId": "com.blwh.wdm501",
  "appName": "BLwH-WDM-501",
  "webDir": "www",
  "backgroundColor": "#eef7ff",
  "server": {
    "allowNavigation": ["*"],
    "cleartext": true,
    "androidScheme": "http"
  },
  "android": {
    "allowMixedContent": true
  },
  "ios": {
    "contentInset": "always"
  }
}

{
  "name": "blwh-wdm-501-app",
  "version": "1.0.0",
  "private": true,
  "description": "Apps for the BLwH/WDM-501 PC remote: Android and iOS wrappers",
  "dependencies": {
    "@capacitor/android": "^8.0.0",
    "@capacitor/core": "^8.0.0",
    "@capacitor/ios": "^8.0.0"
  },
  "devDependencies": {
    "@capacitor/cli": "^8.0.0"
  }
}

# BLwH/WDM-501: برنامج ويندوز + تطبيق أندرويد (+ ايفون)

> صراحةً: ما أقدر أجرّب هذي البناءات هنا (تحتاج ويندوز وأندرويد)، فالملفات مكتوبة حسب توثيق الأدوات وفحصت صياغتها فقط. لو فشلت أي خطوة، انسخ آخر 30 سطر من سجل الخطوة الحمراء في GitHub وأرسلها لي وأصلحها.

## وش بتحصل عليه
- **ويندوز:** ملف تثبيت واحد `BLwH-WDM-501-Setup.exe`. فيه كل شي (Node.js مضمّن)، فما تحتاج تثبّت أي برنامج ولا تفتح CMD. أيقونة بجانب الساعة، وتشغيل تلقائي مع ويندوز (اختياري).
- **أندرويد:** ملف `app-debug.apk` تثبّته على الجوال. يفتح موقعك بملء الشاشة. لا ينتهي بعد 7 أيام مثل ايفون.
- **ايفون:** كما قبل (AltStore)، الخطوات في الأسفل.

## 1) الرفع على GitHub (مرة وحدة)
1. حساب مجاني في github.com ثم **New repository** باسم `blwh-app` واختر **Public**.
2. **Add file ← Upload files**، واسحب كل محتويات هذا المجلد (مع مجلدات `.github` و`windows` و`www`) ثم **Commit changes**.
   - لو `.github` ما انرفع: **Add file ← Create new file** باسم `.github/workflows/build-windows.yml` والصق محتوى الملف (وكذلك `build-android.yml`).

## 2) ويندوز
1. تبويب **Actions** ← **Build Windows installer** ← **Run workflow**. ينتهي بعد 3 إلى 6 دقايق.
2. افتح التشغيل ونزّل **BLwH-WDM-501-Windows-Setup** من Artifacts، وفكّ الـ ZIP.
3. شغّل `BLwH-WDM-501-Setup.exe`. يطلع تحذير "Windows protected your PC" لأن الملف غير موقّع: اضغط **More info ← Run anyway**.
4. يتثبّت في `%LOCALAPPDATA%\BLwH-WDM-501` بدون صلاحيات مسؤول. اترك خيار "Start automatically" مفعّل لو تبيه يشتغل مع ويندوز.
5. أول تشغيل يطلع جدار ويندوز: اضغط **Allow access** (الشبكات الخاصة). أو من أيقونة البرنامج: **فتح المنفذ 3000 في الجدار الناري**.
6. الأيقونة تظهر بجانب الساعة (قد تكون داخل السهم ^). اضغط عليها يمين:
   - **ربط جهاز جديد (QR):** يفتح صفحة الـ QR، تمسحها بالجوال.
   - **عرض رابط الجوال:** ينسخ العنوان اللي تفتحه من الجوال.
   - **فتح مجلد البرنامج:** ضع فيه `PresentMon-x.x.x-x64.exe` لو تبي FPS.
   - **تشغيل كمسؤول (لقياس FPS)** و**إعادة تشغيل السيرفر** و**خروج**.
7. **بياناتك القديمة:** أوقف السيرفر القديم، ثم انسخ `data.json` من `C:\remote` إلى مجلد البرنامج الجديد (من "فتح مجلد البرنامج") وأعد تشغيل السيرفر.
8. **التحديثات:** من الجوال (تحديث السيرفر) مثل قبل، أو شغّل مثبّتاً جديداً فوق القديم.
9. **الحذف:** إعدادات ويندوز ← التطبيقات.

## 3) أندرويد
1. **Actions** ← **Build Android APK** ← **Run workflow** (حوالي 8 إلى 12 دقيقة)، ثم نزّل **BLwH-WDM-501-apk** وفكّ الـ ZIP.
2. انقل `app-debug.apk` للجوال (كيبل أو واتساب لنفسك أو Drive) وافتحه. اسمح بـ **التثبيت من هذا المصدر** لما يسألك. لو ظهر تحذير Play Protect اضغط **Install anyway**.
3. افتح التطبيق، اكتب عنوان السيرفر (يفضّل عنوان Tailscale الذي يبدأ بـ 100: `http://100.x.x.x:3000`).
4. التطبيق جهاز جديد في الموقع: من أيقونة البرنامج على ويندوز اختر **ربط جهاز جديد (QR)** واضغط **فتح التسجيل** ثم ادخل بالـ PIN من التطبيق، وأغلق التسجيل بعدها.
5. **بدون بناء أي شي:** في كروم على أندرويد افتح الموقع، ثم ⋮ ← **إضافة إلى الشاشة الرئيسية**. يعطيك اختصاراً بسرعة، لكنه يفتح في كروم.

## 4) ايفون (اختياري)
**Actions** ← **Build iOS app (unsigned IPA)**، ثم ثبّت الملف بـ AltStore. يحتاج تجديد كل 7 أيام.

## ملاحظات
- عنوان واحد دائماً: كل عنوان مختلف يُسجَّل كجهاز جديد.
- لو انفتح الموقع في المتصفح بدل التطبيق، في `capacitor.config.json` غيّر `["*"]` في `allowNavigation` إلى عنوانك فقط وأعد البناء.
- لو غيّرت عنوان السيرفر في التطبيق: أطفئ السيرفر مؤقتاً ثم افتح التطبيق، فيظهر لك نموذج العنوان.

const http = require('http'), fs = require('fs'), path = require('path');
const crypto = require('crypto'), dgram = require('dgram'), os = require('os'), zlib = require('zlib'), vm = require('vm');
const { exec, spawn } = require('child_process');

// ================= Settings =================
const PIN = '13733';
const PORT = +process.env.BLWH_PORT || 3000;
const VERSION = '2026.11.24';
const TEST = !!process.env.BLWH_TEST;      // used by the update self-test only
const STARTED = Date.now();
const MAX_DEVICES = 2;          // iPhone Safari + home-screen app (extra devices need "pair")
const PW_SECS = 30;             // countdown before shutdown/restart (can be cancelled from the page)
let pending = null;
const PALETTE = ['#0ea5e9', '#38bdf8', '#f472b6', '#a78bfa', '#34d399', '#fbbf24'];
const DATA = process.env.BLWH_DATA || path.join(__dirname, 'data.json');
const IDLE_PS = path.join(__dirname, 'idle.ps1');

// ================= Data =================
let D = {};
try { D = JSON.parse(fs.readFileSync(DATA, 'utf8')); } catch {}
if (!D.apps) {
  try { D.apps = JSON.parse(fs.readFileSync(path.join(__dirname, 'apps.json'), 'utf8')); }
  catch { D.apps = [
    { name: 'Chrome', target: 'chrome' },
    { name: 'YouTube', target: 'https://youtube.com' },
    { name: 'Discord', target: 'discord:' },
  ]; }
}
D.apps.forEach((a, i) => { if (!a.color) a.color = PALETTE[i % PALETTE.length]; });
D.scenes = D.scenes || [
  { name: 'وضع اللعب', steps: ['app:steam:', 'app:discord:', 'do:volup'], color: PALETTE[2] },
  { name: 'وضع النوم', steps: ['do:stop', 'bright:10', 'wait:2', 'do:lock'], color: PALETTE[3] },
];
D.commands = D.commands || [
  { name: 'تنظيف المؤقتة', cmd: 'del /q /f /s "%temp%\\*"', color: PALETTE[4] },
  { name: 'مسح DNS', cmd: 'ipconfig /flushdns', color: PALETTE[0] },
  { name: 'تفريغ السلة', cmd: 'powershell -c "Clear-RecycleBin -Force"', color: PALETTE[5] },
];
D.schedules = D.schedules || [];
D.log = D.log || [];
D.devices = D.devices || [];
D.key = D.key || crypto.randomBytes(12).toString('hex');
D.viewKey = D.viewKey || crypto.randomBytes(9).toString('hex');
D.wolMac = D.wolMac || '';
D.settings = Object.assign({ idleMin: 60, morningScene: '', morningFrom: 5, morningTo: 12, morningLast: '',
  obsPort: 4455, obsPassword: '', obsMic: 'Mic/Aux',
  sessLog: true, sessMin: 60, sessGap: 30,
  sessIgnore: 'chrome,msedge,firefox,brave,opera,explorer,dwm,discord,spotify,vlc,mpv,obs64,obs32,steamwebhelper,searchhost,shellexperiencehost,applicationframehost,textinputhost,widgets,taskmgr,mspaint,notepad,code,wallpaper64,wallpaper32,snippingtool,calculatorapp' }, D.settings || {});
D.profiles = D.profiles && D.profiles.length ? D.profiles : [{ id: 'main', name: 'الرئيسية' }];
['apps', 'scenes', 'commands'].forEach(k => D[k].forEach(it => { if (!it.p) it.p = D.profiles[0].id; }));
const L = { app: 'apps', scene: 'scenes', cmd: 'commands' };
const save = () => fs.writeFileSync(DATA, JSON.stringify(D, null, 2));
save();

// ================= Actions =================
const key = n => exec('powershell -c "(New-Object -ComObject WScript.Shell).SendKeys([char]' + n + ')"');
const keyN = (n, c) => exec('powershell -NoProfile -c "1..' + c + ' | ForEach-Object { (New-Object -ComObject WScript.Shell).SendKeys([char]' + n + ') }"');
const actions = {
  lock:     () => exec('rundll32.exe user32.dll,LockWorkStation'),
  sleep:    () => exec('rundll32.exe powrprof.dll,SetSuspendState 0,1,0'),
  shutdown: () => { exec('shutdown /s /t ' + PW_SECS); pending = { kind: 'shutdown', until: Date.now() + PW_SECS * 1000 }; },
  restart:  () => { exec('shutdown /r /t ' + PW_SECS); pending = { kind: 'restart', until: Date.now() + PW_SECS * 1000 }; },
  cancel:   () => { exec('shutdown /a'); pending = null; },
  volup: () => key(175), voldown: () => key(174), mute: () => key(173),
  play: () => key(179), next: () => key(176), prev: () => key(177), stop: () => key(178),
  volup5: () => keyN(175, 5), voldown5: () => keyN(174, 5),
};
const launch = t => exec('start "" "' + String(t).replace(/"/g, '') + '"');
const bright = n => exec('powershell -c "(Get-WmiObject -Namespace root/WMI -Class WmiMonitorBrightnessMethods).WmiSetBrightness(1,' +
  Math.max(0, Math.min(100, +n || 0)) + ')"');
const sleep = ms => new Promise(r => setTimeout(r, ms));

function validStep(s) {
  const m = /^(do|app|cmd|wait|bright|key|text|click|obs|kill):([\s\S]+)$/.exec(s);
  if (!m) return false;
  const v = m[2];
  if (m[1] === 'do') return !!actions[v];
  if (m[1] === 'wait' || m[1] === 'bright') return /^\d+(\.\d+)?$/.test(v);
  if (m[1] === 'key') return !!combo(v);
  if (m[1] === 'click') return /^(l|r|m|d)$/.test(v);
  if (m[1] === 'obs') return /^(record|stream|mute|scene:.+)$/.test(v);
  if (m[1] === 'kill') return /^[\w .\-]{1,60}$/.test(v);
  return true;
}
async function step(s) {
  const i = s.indexOf(':'), k = s.slice(0, i), v = s.slice(i + 1);
  if (k === 'do') { const a = actions[v]; if (a) a(); }
  else if (k === 'app') launch(v);
  else if (k === 'cmd') exec(v);
  else if (k === 'wait') await sleep(Math.min(+v || 1, 60) * 1000);
  else if (k === 'bright') bright(v);
  else if (k === 'key') inp.keys(v);
  else if (k === 'text') inp.text(v);
  else if (k === 'click') inp.click(v);
  else if (k === 'obs') { try { await obsAct(v); } catch {} }
  else if (k === 'kill') { const n = v.replace(/\.exe$/i, ''); if (/^[\w .\-]{1,60}$/.test(n)) exec('taskkill /IM "' + n + '.exe" /F'); }
  if (k !== 'wait') await sleep(120);
}
async function runWhat(w) {
  const i = w.indexOf(':'), k = w.slice(0, i), v = w.slice(i + 1);
  if (k === 'scene') { const s = D.scenes.find(x => x.name === v); if (s) for (const t of s.steps) await step(t); }
  else if (k === 'saved') { const c = D.commands.find(x => x.name === v); if (c) exec(c.cmd); }
  else await step(w);
}
function findBtn(name) {
  for (const [k, key] of [['scene', 'scenes'], ['app', 'apps'], ['cmd', 'commands']]) {
    const it = D[key].find(x => x.name === name);
    if (it) return { kind: k, it };
  }
  return null;
}
async function runButton(kind, it, long) {
  if (long) { if (it.long && it.long.length) for (const st of it.long) await step(st); return; }
  if (kind === 'app') launch(it.target);
  else if (kind === 'cmd') exec(it.cmd);
  else for (const st of it.steps) await step(st);
}
function validWhat(w) {
  const i = w.indexOf(':'), k = w.slice(0, i), v = w.slice(i + 1);
  if (k === 'do') return !!actions[v];
  if (k === 'scene') return D.scenes.some(x => x.name === v);
  if (k === 'saved') return D.commands.some(x => x.name === v);
  if (k === 'app') return !!v;
  return false;
}
function nowPlaying() {
  return new Promise(r => exec(
    'powershell -c "(Get-Process Spotify -ErrorAction SilentlyContinue | Where-Object {$_.MainWindowTitle} | Select-Object -First 1).MainWindowTitle"',
    { timeout: 4000 }, (e, o) => r(String(o || '').trim())));
}
function wol(mac) {
  const hex = String(mac).replace(/[^0-9a-f]/gi, '');
  if (hex.length !== 12) return false;
  const m = Buffer.from(hex, 'hex');
  const pkt = Buffer.concat([Buffer.alloc(6, 0xff), ...Array(16).fill(m)]);
  const s = dgram.createSocket('udp4');
  s.bind(() => { s.setBroadcast(true); s.send(pkt, 9, '255.255.255.255', () => s.close()); });
  return true;
}

// ================= Keyboard / mouse helper (Windows PowerShell, no extra packages) =================
const INPUT_PS = path.join(__dirname, 'input.ps1');
const inputPs = `Add-Type @"
using System;
using System.Runtime.InteropServices;
public class W32 {
  [DllImport("user32.dll")] public static extern void mouse_event(uint f, int dx, int dy, int d, UIntPtr e);
  [DllImport("user32.dll")] public static extern void keybd_event(byte vk, byte sc, uint fl, UIntPtr e);
}
"@
$ErrorActionPreference = 'SilentlyContinue'
function Press($codes) {
  $list = $codes.Split(',')
  foreach ($c in $list) { $a = $c.Split(':'); [W32]::keybd_event([byte][int]$a[0], 0, [uint32][int]$a[1], [UIntPtr]::Zero) }
  [array]::Reverse($list)
  foreach ($c in $list) { $a = $c.Split(':'); [W32]::keybd_event([byte][int]$a[0], 0, ([uint32][int]$a[1] -bor 2), [UIntPtr]::Zero) }
}
while ($true) {
  $line = [Console]::In.ReadLine()
  if ($line -eq $null) { break }
  $p = $line.Split(' ', 2)
  $cmd = $p[0]
  $arg = $p[1]
  if ($cmd -eq 'm') {
    $a = $arg.Split(' ')
    [W32]::mouse_event(1, [int]$a[0], [int]$a[1], 0, [UIntPtr]::Zero)
  }
  elseif ($cmd -eq 'b') {
    if ($arg -eq 'ld') { [W32]::mouse_event(2, 0, 0, 0, [UIntPtr]::Zero) }
    elseif ($arg -eq 'lu') { [W32]::mouse_event(4, 0, 0, 0, [UIntPtr]::Zero) }
    elseif ($arg -eq 'r') { [W32]::mouse_event(8, 0, 0, 0, [UIntPtr]::Zero); [W32]::mouse_event(16, 0, 0, 0, [UIntPtr]::Zero) }
    elseif ($arg -eq 'm') { [W32]::mouse_event(32, 0, 0, 0, [UIntPtr]::Zero); [W32]::mouse_event(64, 0, 0, 0, [UIntPtr]::Zero) }
    else {
      [W32]::mouse_event(2, 0, 0, 0, [UIntPtr]::Zero); [W32]::mouse_event(4, 0, 0, 0, [UIntPtr]::Zero)
      if ($arg -eq 'd') { Start-Sleep -Milliseconds 40; [W32]::mouse_event(2, 0, 0, 0, [UIntPtr]::Zero); [W32]::mouse_event(4, 0, 0, 0, [UIntPtr]::Zero) }
    }
  }
  elseif ($cmd -eq 's') { [W32]::mouse_event(2048, 0, 0, [int]$arg, [UIntPtr]::Zero) }
  elseif ($cmd -eq 'k') { Press $arg }
  elseif ($cmd -eq 't') {
    $txt = [Text.Encoding]::UTF8.GetString([Convert]::FromBase64String($arg))
    $old = Get-Clipboard -Raw
    Set-Clipboard -Value $txt
    Press '17:0,86:0'
    Start-Sleep -Milliseconds 200
    if ($old) { Set-Clipboard -Value $old }
  }
}
`;
try { fs.writeFileSync(INPUT_PS, inputPs.replace(/\n/g, '\r\n')); } catch {}

const VK = { ctrl: 0x11, control: 0x11, alt: 0x12, shift: 0x10, win: 0x5B, enter: 0x0D, esc: 0x1B, escape: 0x1B, tab: 0x09, space: 0x20,
  backspace: 0x08, delete: 0x2E, del: 0x2E, insert: 0x2D, home: 0x24, end: 0x23, pageup: 0x21, pagedown: 0x22,
  left: 0x25, up: 0x26, right: 0x27, down: 0x28, printscreen: 0x2C, capslock: 0x14 };
for (let i = 1; i <= 12; i++) VK['f' + i] = 0x6F + i;
for (let c = 97; c <= 122; c++) VK[String.fromCharCode(c)] = c - 32;
for (let d = 0; d <= 9; d++) VK[String(d)] = 0x30 + d;
const EXT = new Set([0x21, 0x22, 0x23, 0x24, 0x25, 0x26, 0x27, 0x28, 0x2D, 0x2E, 0x5B]);
function combo(s) {
  const parts = String(s).toLowerCase().split('+').map(x => x.trim()).filter(Boolean);
  const codes = parts.map(x => VK[x]);
  if (!codes.length || codes.length > 5 || codes.some(c => c === undefined)) return null;
  return codes.map(c => c + ':' + (EXT.has(c) ? 1 : 0)).join(',');
}
let helper = null;
function helperSend(line) {
  try {
    if (!helper) {
      helper = spawn('powershell', ['-NoProfile', '-ExecutionPolicy', 'Bypass', '-File', INPUT_PS],
        { windowsHide: true, stdio: ['pipe', 'ignore', 'ignore'] });
      helper.on('error', () => { helper = null; });
      helper.on('exit', () => { helper = null; });
      helper.stdin.on('error', () => {});
    }
    helper.stdin.write(line + '\n');
  } catch { helper = null; }
}
const inp = {
  move: (dx, dy) => helperSend('m ' + (dx | 0) + ' ' + (dy | 0)),
  click: b => helperSend('b ' + b),
  scroll: d => helperSend('s ' + (d | 0)),
  keys: s => { const c = combo(s); if (c) helperSend('k ' + c); return !!c; },
  text: s => helperSend('t ' + Buffer.from(String(s).slice(0, 500), 'utf8').toString('base64')),
};

// ================= CPU / GPU / RAM =================
const GPU_PS = path.join(__dirname, 'gpu.ps1');
const gpuPs = `$ErrorActionPreference = 'SilentlyContinue'
$s = (Get-Counter '\\GPU Engine(*engtype_3D)\\Utilization Percentage').CounterSamples | Measure-Object -Property CookedValue -Sum
if ($s.Sum -ne $null) { [int][math]::Min(100, $s.Sum) }
`;
try { fs.writeFileSync(GPU_PS, gpuPs.replace(/\n/g, '\r\n')); } catch {}
let cpuPrev = os.cpus(), cpuNow = 0;
setInterval(() => {
  const cur = os.cpus(); let idle = 0, total = 0;
  cur.forEach((c, i) => {
    const p = cpuPrev[i]; if (!p) return;
    for (const k in c.times) total += c.times[k] - p.times[k];
    idle += c.times.idle - p.times.idle;
  });
  cpuPrev = cur; cpuNow = total ? Math.round(100 * (1 - idle / total)) : 0;
}, 2000);
let gpuC = { t: 0, v: null }, gpuBusy = false;
function gpuInfo(ttl) {
  return new Promise(r => {
    if (Date.now() - gpuC.t < (ttl || 3000) || gpuBusy) return r(gpuC.v);
    gpuBusy = true;
    const done = v => { gpuC = { t: Date.now(), v }; gpuBusy = false; r(v); };
    exec('nvidia-smi --query-gpu=utilization.gpu,temperature.gpu --format=csv,noheader,nounits', { timeout: 3000 }, (e, o) => {
      if (!e && o) {
        const a = String(o).trim().split(/\r?\n/)[0].split(',').map(x => parseInt(x, 10));
        if (!isNaN(a[0])) return done({ pct: a[0], temp: isNaN(a[1]) ? null : a[1] });
      }
      exec('powershell -NoProfile -ExecutionPolicy Bypass -File "' + GPU_PS + '"', { timeout: 8000 }, (e2, o2) => {
        const n = parseInt(String(o2 || '').trim(), 10);
        done(isNaN(n) ? null : { pct: n, temp: null });
      });
    });
  });
}
async function statsInfo(fast) {
  const total = os.totalmem(), used = total - os.freemem();
  return { cpu: cpuNow, ram: { pct: Math.round(100 * used / total), used: +(used / 1073741824).toFixed(1), total: +(total / 1073741824).toFixed(1) }, gpu: await gpuInfo(fast ? 1000 : 3000), fps: fpsInfo(), sess: sessInfo() };
}

// ================= OBS Studio (obs-websocket v5, built into OBS 28+) =================
let obsWs = null, obsReady = false, obsPending = new Map(), obsId = 0, obsConnecting = null;
function obsConnect() {
  if (obsReady) return Promise.resolve();
  if (obsConnecting) return obsConnecting;
  obsConnecting = new Promise((resolve, reject) => {
    let done = false;
    const fin = err => { if (done) return; done = true; obsConnecting = null; err ? reject(err) : resolve(); };
    let ws;
    try { ws = new WebSocket('ws://127.0.0.1:' + D.settings.obsPort); } catch (e) { return fin(e); }
    const timer = setTimeout(() => { try { ws.close(); } catch {} fin(new Error('timeout')); }, 4000);
    ws.onmessage = ev => {
      let m; try { m = JSON.parse(ev.data); } catch { return; }
      if (m.op === 0) {
        const id = { op: 1, d: { rpcVersion: 1, eventSubscriptions: 0 } };
        const a = m.d && m.d.authentication;
        if (a) {
          const secret = crypto.createHash('sha256').update(D.settings.obsPassword + a.salt).digest('base64');
          id.d.authentication = crypto.createHash('sha256').update(secret + a.challenge).digest('base64');
        }
        ws.send(JSON.stringify(id));
      } else if (m.op === 2) {
        clearTimeout(timer); obsWs = ws; obsReady = true; fin();
      } else if (m.op === 7) {
        const p = obsPending.get(m.d.requestId);
        if (p) {
          obsPending.delete(m.d.requestId);
          m.d.requestStatus && m.d.requestStatus.result ? p.res(m.d.responseData || {}) : p.rej(new Error('request failed'));
        }
      }
    };
    ws.onclose = () => {
      clearTimeout(timer); obsReady = false; obsWs = null;
      obsPending.forEach(p => p.rej(new Error('closed'))); obsPending.clear();
      fin(new Error('closed'));
    };
    ws.onerror = () => {};
  });
  return obsConnecting;
}
async function obs(type, data) {
  await obsConnect();
  return new Promise((res, rej) => {
    const id = String(++obsId);
    obsPending.set(id, { res, rej });
    try { obsWs.send(JSON.stringify({ op: 6, d: { requestType: type, requestId: id, requestData: data || {} } })); }
    catch (e) { obsPending.delete(id); return rej(e); }
    setTimeout(() => { if (obsPending.has(id)) { obsPending.delete(id); rej(new Error('timeout')); } }, 4000);
  });
}
async function obsStatus() {
  try {
    const [rec, str, sc] = await Promise.all([obs('GetRecordStatus'), obs('GetStreamStatus'), obs('GetSceneList')]);
    const scenes = (sc.scenes || []).slice().sort((a, b) => b.sceneIndex - a.sceneIndex).map(s => s.sceneName);
    return { ok: true, rec: !!rec.outputActive, stream: !!str.outputActive, scene: sc.currentProgramSceneName, scenes };
  } catch { return { ok: false }; }
}
async function obsAct(a) {
  if (a === 'record') return obs('ToggleRecord');
  if (a === 'stream') return obs('ToggleStream');
  if (a === 'mute') return obs('ToggleInputMute', { inputName: D.settings.obsMic });
  if (a.startsWith('scene:')) return obs('SetCurrentProgramScene', { sceneName: a.slice(6) });
}

// ===== QR START (versions 1-6, error correction M, byte mode) =====
const QR_ECC = [10, 16, 26, 18, 24, 16], QR_BLK = [1, 1, 1, 2, 2, 4];
function gfMul(x, y) { let z = 0; for (let i = 7; i >= 0; i--) { z = (z << 1) ^ ((z >>> 7) * 0x11D); z ^= ((y >>> i) & 1) * x; } return z; }
function rsDivisor(deg) {
  const r = new Array(deg - 1).fill(0); r.push(1); let root = 1;
  for (let i = 0; i < deg; i++) {
    for (let j = 0; j < r.length; j++) { r[j] = gfMul(r[j], root); if (j + 1 < r.length) r[j] ^= r[j + 1]; }
    root = gfMul(root, 2);
  }
  return r;
}
function rsRemainder(data, div) {
  const r = new Array(div.length).fill(0);
  for (const b of data) { const f = b ^ r.shift(); r.push(0); div.forEach((c, i) => { r[i] ^= gfMul(c, f); }); }
  return r;
}
function qrRaw(ver) {
  let r = (16 * ver + 128) * ver + 64;
  if (ver >= 2) { const na = Math.floor(ver / 7) + 2; r -= (25 * na - 10) * na - 55; }
  return r;
}
function qrMatrix(text) {
  const data = Buffer.from(String(text), 'utf8');
  let ver = 0;
  for (let v = 1; v <= 6; v++) {
    const cap = Math.floor(qrRaw(v) / 8) - QR_ECC[v - 1] * QR_BLK[v - 1];
    if (12 + 8 * data.length <= cap * 8) { ver = v; break; }
  }
  if (!ver) throw new Error('text too long for QR');
  const size = ver * 4 + 17, nEcc = QR_ECC[ver - 1], nBlk = QR_BLK[ver - 1];
  const rawCw = Math.floor(qrRaw(ver) / 8), dataCw = rawCw - nEcc * nBlk;
  const bits = [];
  const put = (val, len) => { for (let i = len - 1; i >= 0; i--) bits.push((val >>> i) & 1); };
  put(4, 4); put(data.length, 8); for (const b of data) put(b, 8);
  put(0, Math.min(4, dataCw * 8 - bits.length));
  while (bits.length % 8) bits.push(0);
  const cws = [];
  for (let i = 0; i < bits.length; i += 8) { let b = 0; for (let j = 0; j < 8; j++) b = (b << 1) | bits[i + j]; cws.push(b); }
  for (let pad = 0xEC; cws.length < dataCw; pad ^= 0xEC ^ 0x11) cws.push(pad);
  const nShort = nBlk - rawCw % nBlk, shortLen = Math.floor(rawCw / nBlk);
  const div = rsDivisor(nEcc), blocks = [];
  for (let i = 0, k = 0; i < nBlk; i++) {
    const dat = cws.slice(k, k + shortLen - nEcc + (i < nShort ? 0 : 1)); k += dat.length;
    const ecc = rsRemainder(dat, div);
    if (i < nShort) dat.push(0);
    blocks.push(dat.concat(ecc));
  }
  const all = [];
  for (let i = 0; i < blocks[0].length; i++) blocks.forEach((bl, j) => { if (i !== shortLen - nEcc || j >= nShort) all.push(bl[i]); });

  const m = Array.from({ length: size }, () => new Array(size).fill(false));
  const fn = Array.from({ length: size }, () => new Array(size).fill(false));
  const setF = (x, y, v) => { m[y][x] = v; fn[y][x] = true; };
  for (let i = 0; i < size; i++) { setF(6, i, i % 2 === 0); setF(i, 6, i % 2 === 0); }
  const finder = (cx, cy) => {
    for (let dy = -4; dy <= 4; dy++) for (let dx = -4; dx <= 4; dx++) {
      const d = Math.max(Math.abs(dx), Math.abs(dy)), x = cx + dx, y = cy + dy;
      if (x >= 0 && x < size && y >= 0 && y < size) setF(x, y, d !== 2 && d !== 4);
    }
  };
  finder(3, 3); finder(size - 4, 3); finder(3, size - 4);
  const ap = [];
  if (ver > 1) {
    const na = Math.floor(ver / 7) + 2, step = Math.ceil((ver * 4 + 4) / (na * 2 - 2)) * 2;
    ap.push(6);
    for (let pos = size - 7; ap.length < na; pos -= step) ap.splice(1, 0, pos);
  }
  for (let i = 0; i < ap.length; i++) for (let j = 0; j < ap.length; j++) {
    if ((i === 0 && j === 0) || (i === 0 && j === ap.length - 1) || (i === ap.length - 1 && j === 0)) continue;
    for (let dy = -2; dy <= 2; dy++) for (let dx = -2; dx <= 2; dx++) setF(ap[i] + dx, ap[j] + dy, Math.max(Math.abs(dx), Math.abs(dy)) !== 1);
  }
  const fmt = mask => {
    const d = mask;
    let rem = d; for (let i = 0; i < 10; i++) rem = (rem << 1) ^ ((rem >>> 9) * 0x537);
    const fb = ((d << 10) | rem) ^ 0x5412;
    const bit = i => ((fb >>> i) & 1) !== 0;
    for (let i = 0; i <= 5; i++) setF(8, i, bit(i));
    setF(8, 7, bit(6)); setF(8, 8, bit(7)); setF(7, 8, bit(8));
    for (let i = 9; i < 15; i++) setF(14 - i, 8, bit(i));
    for (let i = 0; i < 8; i++) setF(size - 1 - i, 8, bit(i));
    for (let i = 8; i < 15; i++) setF(8, size - 15 + i, bit(i));
    setF(8, size - 8, true);
  };
  fmt(0);
  let bi = 0;
  for (let right = size - 1; right >= 1; right -= 2) {
    if (right === 6) right = 5;
    for (let vert = 0; vert < size; vert++) for (let j = 0; j < 2; j++) {
      const x = right - j, upward = ((right + 1) & 2) === 0, y = upward ? size - 1 - vert : vert;
      if (!fn[y][x] && bi < all.length * 8) { m[y][x] = ((all[bi >>> 3] >>> (7 - (bi & 7))) & 1) !== 0; bi++; }
    }
  }
  const applyMask = mask => {
    for (let y = 0; y < size; y++) for (let x = 0; x < size; x++) {
      let inv;
      switch (mask) {
        case 0: inv = (x + y) % 2 === 0; break;
        case 1: inv = y % 2 === 0; break;
        case 2: inv = x % 3 === 0; break;
        case 3: inv = (x + y) % 3 === 0; break;
        case 4: inv = (Math.floor(x / 3) + Math.floor(y / 2)) % 2 === 0; break;
        case 5: inv = x * y % 2 + x * y % 3 === 0; break;
        case 6: inv = (x * y % 2 + x * y % 3) % 2 === 0; break;
        default: inv = ((x + y) % 2 + x * y % 3) % 2 === 0;
      }
      if (!fn[y][x] && inv) m[y][x] = !m[y][x];
    }
  };
  const penalty = () => {
    let p = 0;
    const lines = [];
    for (let y = 0; y < size; y++) lines.push(m[y].map(v => v ? 1 : 0));
    for (let x = 0; x < size; x++) lines.push(m.map(r => r[x] ? 1 : 0));
    for (const Ln of lines) {
      let run = 1;
      for (let i = 1; i <= size; i++) { if (i < size && Ln[i] === Ln[i - 1]) run++; else { if (run >= 5) p += 3 + run - 5; run = 1; } }
      const s = Ln.join('');
      for (let i = 0; i + 11 <= size; i++) { const w = s.substr(i, 11); if (w === '10111010000' || w === '00001011101') p += 40; }
    }
    for (let y = 0; y < size - 1; y++) for (let x = 0; x < size - 1; x++) {
      const v = m[y][x]; if (v === m[y][x + 1] && v === m[y + 1][x] && v === m[y + 1][x + 1]) p += 3;
    }
    let dark = 0; for (const r of m) for (const v of r) if (v) dark++;
    p += Math.floor(Math.abs(dark * 20 - size * size * 10) / (size * size)) * 10;
    return p;
  };
  let best = 0, bestP = Infinity;
  for (let mk = 0; mk < 8; mk++) { applyMask(mk); fmt(mk); const pn = penalty(); if (pn < bestP) { bestP = pn; best = mk; } applyMask(mk); }
  applyMask(best); fmt(best);
  return m;
}
function qrSvg(text) {
  const m = qrMatrix(text), n = m.length, q = 4, S = n + 2 * q;
  let d = '';
  m.forEach((row, y) => row.forEach((v, x) => { if (v) d += 'M' + (x + q) + ' ' + (y + q) + 'h1v1h-1z'; }));
  return '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 ' + S + ' ' + S + '" shape-rendering="crispEdges">' +
    '<rect width="' + S + '" height="' + S + '" fill="#fff"/><path d="' + d + '" fill="#000"/></svg>';
}
// ===== QR END =====
const pairTokens = new Map();
function newPairToken() {
  pairTokens.clear();
  const t = crypto.randomBytes(9).toString('hex');
  pairTokens.set(t, 1);
  return t;
}
function lanAddrs() {
  const out = [];
  Object.values(os.networkInterfaces()).flat().forEach(n => {
    if (!n || n.family !== 'IPv4' || n.internal) return;
    const a = n.address.split('.').map(Number);
    let label = 'شبكة';
    if (a[0] === 192 && a[1] === 168 || a[0] === 10 || (a[0] === 172 && a[1] >= 16 && a[1] <= 31)) label = 'شبكة البيت';
    else if (a[0] === 100 && a[1] >= 64 && a[1] <= 127) label = 'Tailscale';
    else if (a[0] === 26) label = 'Radmin VPN';
    out.push({ ip: n.address, label });
  });
  out.sort((x, y) => (x.label === 'شبكة البيت' ? 0 : 1) - (y.label === 'شبكة البيت' ? 0 : 1));
  return out;
}
const pubSettings = () => { const { obsPassword, ...rest } = D.settings; return { ...rest, hasObsPass: !!obsPassword }; };

// ================= FPS (optional: needs PresentMon.exe next to server.js) =================
const fpsS = { proc: null, hdr: null, frames: [], last: 0, buf: '', err: '', exited: false, retried: false, startedAt: 0 };
function presentMonExe() { try { return fs.readdirSync(__dirname).find(f => /^presentmon.*\.exe$/i.test(f)) || null; } catch { return null; } }
function fpsStart(v1) {
  const exe = presentMonExe(); if (!exe) return;
  const args = v1 ? ['-output_stdout', '-stop_existing_session', '-session_name', 'blwhfps', '-no_top']
                  : ['--output_stdout', '--stop_existing_session', '--session_name', 'blwhfps', '--no_console_stats'];
  fpsS.hdr = null; fpsS.buf = ''; fpsS.err = ''; fpsS.exited = false; fpsS.startedAt = Date.now();
  let pr;
  try { pr = spawn(path.join(__dirname, exe), args, { windowsHide: true, stdio: ['ignore', 'pipe', 'pipe'] }); }
  catch { fpsS.exited = true; return; }
  fpsS.proc = pr;
  pr.stdout.on('data', d => fpsParse(String(d)));
  pr.stderr.on('data', d => { fpsS.err = (fpsS.err + String(d)).slice(-400); });
  pr.on('error', () => { if (fpsS.proc === pr) fpsS.proc = null; fpsS.exited = true; });
  pr.on('exit', () => {
    if (fpsS.proc === pr) fpsS.proc = null;
    fpsS.exited = true;
    if (!v1 && !fpsS.retried && !fpsS.hdr && !/access/i.test(fpsS.err)) { fpsS.retried = true; fpsStart(true); }
  });
}
function fpsParse(chunk) {
  fpsS.buf += chunk;
  const lines = fpsS.buf.split(/\r?\n/); fpsS.buf = lines.pop();
  for (const ln of lines) {
    if (!ln) continue;
    const c = ln.split(',');
    if (!fpsS.hdr) {
      const h = c.map(x => x.trim().toLowerCase());
      const ms = h.includes('frametime') ? h.indexOf('frametime') : h.indexOf('msbetweenpresents');
      const app = h.indexOf('application');
      if (ms >= 0 && app >= 0) fpsS.hdr = { ms, app };
      continue;
    }
    const ms = parseFloat(c[fpsS.hdr.ms]), app = (c[fpsS.hdr.app] || '').trim();
    if (!(ms > 0) || !app || /^(dwm\.exe|explorer\.exe|<unknown>|<error>)$/i.test(app)) continue;
    fpsS.frames.push({ t: Date.now(), app, ms });
  }
  const cut = Date.now() - 6000;
  while (fpsS.frames.length && fpsS.frames[0].t < cut) fpsS.frames.shift();
  if (fpsS.frames.length > 30000) fpsS.frames.splice(0, 10000);
}
setInterval(() => {
  if (fpsS.proc && Date.now() - fpsS.last > 20000) { try { fpsS.proc.kill(); } catch {} fpsS.proc = null; fpsS.frames = []; }
}, 5000);
function fpsInfo() {
  if (!presentMonExe()) return { state: 'missing', dir: __dirname };
  fpsS.last = Date.now();
  if (!fpsS.proc) {
    if (fpsS.exited && /access/i.test(fpsS.err)) return { state: 'denied' };
    if (Date.now() - fpsS.startedAt < 10000 && fpsS.startedAt) return { state: 'error' };
    fpsS.retried = false; fpsStart(false);
    return { state: 'starting' };
  }
  const now = Date.now(), recent = fpsS.frames.filter(f => now - f.t <= 1000), cnt = {};
  recent.forEach(f => { cnt[f.app] = (cnt[f.app] || 0) + 1; });
  const app = Object.keys(cnt).sort((a, b) => cnt[b] - cnt[a])[0];
  if (!app) return { state: 'idle' };
  const win = fpsS.frames.filter(f => f.app === app && now - f.t <= 5000).map(f => f.ms).sort((a, b) => a - b);
  const p99 = win[Math.min(win.length - 1, Math.floor(win.length * 0.99))];
  const avg = recent.filter(f => f.app === app).reduce((s, f) => s + f.ms, 0) / cnt[app];
  return { state: 'ok', app: app.replace(/\.exe$/i, ''), fps: cnt[app], ms: +avg.toFixed(1), low: Math.round(1000 / p99) };
}

// ================= Steam library (so games can be added with one tap) =================
function steamGames() {
  const base = process.env.STEAM_DIR || path.join(process.env['ProgramFiles(x86)'] || 'C:\\Program Files (x86)', 'Steam');
  const dirs = [base];
  try {
    const vdf = fs.readFileSync(path.join(base, 'steamapps', 'libraryfolders.vdf'), 'utf8');
    for (const m of vdf.matchAll(/"path"\s+"([^"]+)"/g)) dirs.push(m[1].replace(/\\\\/g, '\\'));
  } catch {}
  const out = [], seen = new Set();
  for (const d of new Set(dirs)) {
    let files = [];
    try { files = fs.readdirSync(path.join(d, 'steamapps')); } catch { continue; }
    for (const f of files) {
      if (!/^appmanifest_\d+\.acf$/.test(f)) continue;
      try {
        const t = fs.readFileSync(path.join(d, 'steamapps', f), 'utf8');
        const id = /"appid"\s+"(\d+)"/.exec(t), nm = /"name"\s+"([^"]+)"/.exec(t);
        if (id && nm && !seen.has(id[1]) && !/steamworks|redistributable|proton|runtime/i.test(nm[1])) { seen.add(id[1]); out.push({ id: id[1], name: nm[1] }); }
      } catch {}
    }
  }
  return out.sort((a, b) => a.name.localeCompare(b.name)).slice(0, 300);
}

// ================= Game sessions (needs PresentMon) =================
const SESS = path.join(path.dirname(DATA), 'sessions.json');
let sessions = [];
try { sessions = JSON.parse(fs.readFileSync(SESS, 'utf8')); } catch {}
let sess = null;
const ignoreSet = () => new Set(String(D.settings.sessIgnore || '').toLowerCase().split(',').map(x => x.trim().replace(/\.exe$/, '')).filter(Boolean));
function closeSession() {
  if (!sess) return;
  const s = sess; sess = null;
  const secs = Math.round((s.last - s.start) / 1000);
  if (secs < D.settings.sessMin || !s.n) return;
  sessions.push({ app: s.app, start: s.start, end: s.last, secs, avg: Math.round(s.fpsSum / s.n), low: Math.round(s.lowSum / s.n),
    min: s.fpsMin, max: s.fpsMax, cpu: Math.round(s.cpuSum / s.n), gpu: s.gpuN ? Math.round(s.gpuSum / s.gpuN) : null, maxTemp: s.maxTemp });
  if (sessions.length > 300) sessions.splice(0, sessions.length - 300);
  try { fs.writeFileSync(SESS, JSON.stringify(sessions)); } catch {}
}
process.on('exit', closeSession);
process.on('SIGINT', () => process.exit(0));
if (!TEST) setInterval(async () => {
  try {
    if (!D.settings.sessLog || !presentMonExe()) return;
    const f = fpsInfo(), g = await gpuInfo(3000), now = Date.now();
    if (f.state === 'ok' && f.fps >= 10 && !ignoreSet().has(f.app.toLowerCase())) {
      if (sess && sess.app !== f.app) closeSession();
      if (!sess) sess = { app: f.app, start: now, last: now, n: 0, fpsSum: 0, lowSum: 0, fpsMin: f.fps, fpsMax: f.fps, cpuSum: 0, gpuSum: 0, gpuN: 0, maxTemp: null };
      sess.last = now; sess.n++; sess.fpsSum += f.fps; sess.lowSum += f.low;
      sess.fpsMin = Math.min(sess.fpsMin, f.fps); sess.fpsMax = Math.max(sess.fpsMax, f.fps); sess.cpuSum += cpuNow;
      if (g) { sess.gpuSum += g.pct; sess.gpuN++; if (g.temp != null) sess.maxTemp = Math.max(sess.maxTemp == null ? 0 : sess.maxTemp, g.temp); }
    } else if (sess && now - sess.last > D.settings.sessGap * 1000) closeSession();
  } catch {}
}, 2000);
function sessInfo() {
  return sess ? { app: sess.app, secs: Math.round((Date.now() - sess.start) / 1000), avg: Math.round(sess.fpsSum / Math.max(1, sess.n)) } : null;
}
function sessionsSummary() {
  const m = {};
  sessions.forEach(s => {
    const a = m[s.app] = m[s.app] || { app: s.app, count: 0, secs: 0, w: 0, maxTemp: null };
    a.count++; a.secs += s.secs; a.w += s.avg * s.secs;
    if (s.maxTemp != null) a.maxTemp = Math.max(a.maxTemp || 0, s.maxTemp);
  });
  return Object.values(m).map(a => ({ app: a.app, count: a.count, secs: a.secs, avg: Math.round(a.w / Math.max(1, a.secs)), maxTemp: a.maxTemp }))
    .sort((x, y) => y.secs - x.secs);
}

// ================= Self-update from the phone (with a safety test run) =================
function listBackups() {
  try {
    const dir = path.join(__dirname, 'backups');
    return fs.readdirSync(dir).filter(f => /^server-[\w.\-]+\.js$/.test(f))
      .map(f => ({ name: f, size: fs.statSync(path.join(dir, f)).size, t: fs.statSync(path.join(dir, f)).mtimeMs }))
      .sort((a, b) => b.t - a.t);
  } catch { return []; }
}
async function verifyCode(code) {
  if (code.length < 2000 || code.length > 3e6) return { ok: false, error: 'حجم الملف غير منطقي' };
  if (!code.includes('http.createServer') || !code.includes('BLwH/WDM-501')) return { ok: false, error: 'هذا ليس ملف السيرفر' };
  try { new vm.Script(code, { filename: 'candidate.js' }); } catch (e) { return { ok: false, error: 'خطأ في صياغة الملف: ' + e.message }; }
  const cand = path.join(__dirname, 'server.candidate.js');
  fs.writeFileSync(cand, code);
  const port = 39000 + Math.floor(Math.random() * 900), tmpData = path.join(os.tmpdir(), 'blwh-test-' + Date.now() + '.json');
  const res = await new Promise(resolve => {
    const pr = spawn(process.execPath, [cand], { env: { ...process.env, BLWH_PORT: String(port), BLWH_DATA: tmpData, BLWH_TEST: '1' },
      stdio: ['ignore', 'ignore', 'pipe'], windowsHide: true, cwd: __dirname });
    let err = '', done = false, tries = 0, iv = null;
    const finish = r => { if (done) return; done = true; clearInterval(iv); try { pr.kill(); } catch {} resolve(r); };
    pr.stderr.on('data', d => { err = (err + d).slice(0, 4000); });
    pr.on('error', e => finish({ ok: false, error: 'تعذر تشغيل الاختبار: ' + e.message }));
    pr.on('exit', () => {
      const m = /(?:^|\n)([A-Za-z]*Error[^\n]*)/.exec(err);
      finish({ ok: false, error: 'فشل التشغيل التجريبي: ' + (m ? m[1] : err.trim().slice(0, 200) || 'خرج فجأة') });
    });
    iv = setInterval(() => {
      tries++;
      http.get({ host: '127.0.0.1', port, path: '/api/ping', timeout: 800 }, r => { r.resume(); if (r.statusCode === 200) finish({ ok: true }); }).on('error', () => {});
      if (tries > 20) finish({ ok: false, error: 'السيرفر الجديد لم يستجب خلال 6 ثواني' });
    }, 300);
  });
  try { fs.unlinkSync(tmpData); } catch {}
  if (!res.ok) { try { fs.unlinkSync(cand); } catch {} return res; }
  const m = /const VERSION = '([^']+)'/.exec(code);
  return { ok: true, version: m ? m[1] : 'unknown', cand };
}
function swapIn(cand) {
  const dir = path.join(__dirname, 'backups');
  fs.mkdirSync(dir, { recursive: true });
  const stamp = new Date().toISOString().replace(/[:.]/g, '-').slice(0, 19);
  fs.copyFileSync(__filename, path.join(dir, 'server-' + VERSION + '-' + stamp + '.js'));
  fs.renameSync(cand, __filename);
  listBackups().slice(8).forEach(b => { try { fs.unlinkSync(path.join(dir, b.name)); } catch {} });
}
function restartSelf() {
  setTimeout(() => {
    closeSession();
    if (process.env.BLWH_LOOP === '1') process.exit(42);
    try { srv.closeAllConnections(); } catch {}
    srv.close(() => {
      spawn(process.execPath, [__filename], { detached: true, stdio: 'ignore', windowsHide: true, cwd: __dirname }).unref();
      process.exit(0);
    });
    setTimeout(() => process.exit(0), 4000);
  }, 600);
}

// ================= Idle time (Windows) =================
const idlePs = `Add-Type @"
using System;
using System.Runtime.InteropServices;
public class Idle {
  [StructLayout(LayoutKind.Sequential)] struct LASTINPUTINFO { public uint cbSize; public uint dwTime; }
  [DllImport("user32.dll")] static extern bool GetLastInputInfo(ref LASTINPUTINFO p);
  public static uint Seconds() {
    LASTINPUTINFO l = new LASTINPUTINFO();
    l.cbSize = (uint)Marshal.SizeOf(l);
    GetLastInputInfo(ref l);
    return ((uint)Environment.TickCount - l.dwTime) / 1000;
  }
}
"@
[Idle]::Seconds()
`;
try { fs.writeFileSync(IDLE_PS, idlePs.replace(/\n/g, '\r\n')); } catch {}
let idleC = { t: 0, s: -1 };
function idleSec() {
  return new Promise(r => {
    if (Date.now() - idleC.t < 20000) return r(idleC.s);
    exec('powershell -NoProfile -ExecutionPolicy Bypass -File "' + IDLE_PS + '"', { timeout: 10000 }, (e, o) => {
      const n = parseInt(String(o || '').trim(), 10);
      idleC = { t: Date.now(), s: isNaN(n) ? -1 : n };
      r(idleC.s);
    });
  });
}
const ar2en = s => String(s).replace(/[٠-٩]/g, d => '٠١٢٣٤٥٦٧٨٩'.indexOf(d));

// ================= Home-screen icon (PNG generated in code) =================
const crcT = (() => { const t = []; for (let n = 0; n < 256; n++) { let c = n; for (let k = 0; k < 8; k++) c = c & 1 ? 0xedb88320 ^ (c >>> 1) : c >>> 1; t[n] = c >>> 0; } return t; })();
const crc32 = b => { let c = 0xffffffff; for (const x of b) c = crcT[(c ^ x) & 255] ^ (c >>> 8); return (c ^ 0xffffffff) >>> 0; };
function chunk(type, data) {
  const t = Buffer.from(type), l = Buffer.alloc(4), c = Buffer.alloc(4);
  l.writeUInt32BE(data.length); c.writeUInt32BE(crc32(Buffer.concat([t, data])));
  return Buffer.concat([l, t, data, c]);
}
const pngCache = {};
function png(s) {
  if (pngCache[s]) return pngCache[s];
  const k = s / 180, row = s * 4 + 1, raw = Buffer.alloc(row * s);
  const rr = (x, y, x0, y0, x1, y1, r) => {
    if (x < x0 || x >= x1 || y < y0 || y >= y1) return false;
    const cx = x < x0 + r ? x0 + r : x >= x1 - r ? x1 - r : x, cy = y < y0 + r ? y0 + r : y >= y1 - r ? y1 - r : y;
    return (x - cx) * (x - cx) + (y - cy) * (y - cy) <= r * r;
  };
  for (let y = 0; y < s; y++) {
    for (let x = 0; x < s; x++) {
      const u = x / k, v = y / k;
      let c = [14, 165, 233];
      if (rr(u, v, 34, 46, 146, 114, 12)) c = [255, 255, 255];
      if (rr(u, v, 42, 54, 138, 106, 6)) c = [14, 165, 233];
      if (rr(u, v, 60, 70, 120, 76, 3)) c = [247, 220, 232];
      if (rr(u, v, 60, 86, 100, 92, 3)) c = [255, 255, 255];
      if (u >= 84 && u < 96 && v >= 114 && v < 132) c = [255, 255, 255];
      if (rr(u, v, 62, 130, 118, 138, 4)) c = [255, 255, 255];
      const o = y * row + 1 + x * 4;
      raw[o] = c[0]; raw[o + 1] = c[1]; raw[o + 2] = c[2]; raw[o + 3] = 255;
    }
  }
  const ihdr = Buffer.alloc(13); ihdr.writeUInt32BE(s, 0); ihdr.writeUInt32BE(s, 4); ihdr[8] = 8; ihdr[9] = 6;
  return (pngCache[s] = Buffer.concat([Buffer.from([137, 80, 78, 71, 13, 10, 26, 10]),
    chunk('IHDR', ihdr), chunk('IDAT', zlib.deflateSync(raw)), chunk('IEND', Buffer.alloc(0))]));
}

// ================= Security =================
const ip = req => String(req.socket.remoteAddress || '').replace('::ffff:', '');
const fails = new Map();
const locked = i => { const f = fails.get(i); return f && f.until > Date.now() ? Math.ceil((f.until - Date.now()) / 60000) : 0; };
function fail(i) {
  const f = fails.get(i) || { n: 0, until: 0 };
  if (f.until && f.until <= Date.now()) { f.n = 0; f.until = 0; }
  f.n++;
  if (f.n >= 5) f.until = Date.now() + 10 * 60000;
  fails.set(i, f);
  return f.n;
}
function cookie(req, n) {
  const m = (req.headers.cookie || '').split(';').map(s => s.trim()).find(s => s.startsWith(n + '='));
  return m ? m.slice(n.length + 1) : '';
}
const device = req => { const t = cookie(req, 'dev'); return t ? D.devices.find(d => d.token === t) : undefined; };
function uaName(req) {
  const u = req.headers['user-agent'] || '';
  return /iPhone/.test(u) ? 'iPhone' : /iPad/.test(u) ? 'iPad' : /Android/.test(u) ? 'Android'
    : /Windows/.test(u) ? 'Windows' : /Mac/.test(u) ? 'Mac' : 'جهاز';
}
function log(who, what) {
  D.log.unshift({ t: Date.now(), who, what });
  D.log.length = Math.min(D.log.length, 150);
  save();
}
let pairOpen = false;
try {
  process.stdin.on('data', d => {
    const w = String(d).trim().toLowerCase();
    if (w === 'pair') { pairOpen = true; console.log('Pairing is OPEN (no time limit). Type  unpair  to close it.'); }
    else if (w === 'unpair') { pairOpen = false; console.log('Pairing is closed.'); }
  });
} catch {}

// ================= Scheduler =================
setInterval(() => {
  const n = Date.now(), d = new Date(), day = d.toDateString();
  const hm = ('0' + d.getHours()).slice(-2) + ':' + ('0' + d.getMinutes()).slice(-2);
  let ch = false;
  D.schedules = D.schedules.filter(s => {
    if (s.kind === 'once') {
      if (n >= s.ts) { if (n - s.ts < 120000) { log('جدولة', s.label); runWhat(s.what); } ch = true; return false; }
    } else if (s.hm === hm && s.last !== day) {
      s.last = day; ch = true; log('جدولة', s.label); runWhat(s.what);
    }
    return true;
  });
  if (ch) save();
}, 15000);

// ================= Page =================
const icons = {
  volup5: '<polygon points="11 5 6 9 2 9 2 15 6 15 11 19 11 5"/><path d="M19.07 4.93a10 10 0 0 1 0 14.14M15.54 8.46a5 5 0 0 1 0 7.07"/>',
  voldown5: '<polygon points="11 5 6 9 2 9 2 15 6 15 11 19 11 5"/><path d="M15.54 8.46a5 5 0 0 1 0 7.07"/>',
  lock: '<rect x="3" y="11" width="18" height="11" rx="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/>',
  sleep: '<path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/>',
  shutdown: '<path d="M18.36 6.64a9 9 0 1 1-12.73 0"/><line x1="12" y1="2" x2="12" y2="12"/>',
  restart: '<polyline points="23 4 23 10 17 10"/><polyline points="1 20 1 14 7 14"/><path d="M3.51 9a9 9 0 0 1 14.85-3.36L23 10M1 14l4.64 4.36A9 9 0 0 0 20.49 15"/>',
  volup: '<polygon points="11 5 6 9 2 9 2 15 6 15 11 19 11 5"/><path d="M19.07 4.93a10 10 0 0 1 0 14.14M15.54 8.46a5 5 0 0 1 0 7.07"/>',
  voldown: '<polygon points="11 5 6 9 2 9 2 15 6 15 11 19 11 5"/><path d="M15.54 8.46a5 5 0 0 1 0 7.07"/>',
  mute: '<polygon points="11 5 6 9 2 9 2 15 6 15 11 19 11 5"/><line x1="23" y1="9" x2="17" y2="15"/><line x1="17" y1="9" x2="23" y2="15"/>',
  prev: '<polygon points="19 20 9 12 19 4 19 20"/><line x1="5" y1="19" x2="5" y2="5"/>',
  play: '<polygon points="5 3 19 12 5 21 5 3"/>',
  next: '<polygon points="5 4 15 12 5 20 5 4"/><line x1="19" y1="5" x2="19" y2="19"/>',
};
const labels = {
  lock: 'قفل', sleep: 'سكون', shutdown: 'إيقاف التشغيل', restart: 'إعادة التشغيل',
  volup: 'رفع', voldown: 'خفض', volup5: 'رفع ×5', voldown5: 'خفض ×5', mute: 'كتم', prev: 'السابق', play: 'تشغيل / إيقاف', next: 'التالي'
};
function sbtn(a) {
  const cls = 'b' + (a === 'shutdown' || a === 'restart' ? ' d' : '');
  return '<button class="' + cls + '" data-a="do" data-v="' + a + '"><svg viewBox="0 0 24 24">' + icons[a] + '</svg>' + labels[a] + '</button>';
}
function card(title, inner, extra) {
  return '<section class="card"><div class="ct"><span>' + title + '</span><i></i>' + (extra || '') + '</div>' + inner + '</section>';
}
const grid = (names, cls) => '<div class="g ' + (cls || '') + '">' + names.map(sbtn).join('') + '</div>';
const plus = k => '<button class="sm" data-a="add" data-k="' + k + '">+ إضافة</button>';

const css = `
:root{--bg:#eef7ff;--b1:#7dd3fc;--b2:#fbcfe8;--b3:#c7d2fe;--glass:rgba(255,255,255,.5);--glass2:rgba(255,255,255,.64);--glassb:rgba(255,255,255,.8);--hi:rgba(255,255,255,.95);--solid:rgba(255,255,255,.86);--ink:#0b2a3f;--mute:#6b8296;--sky:#0ea5e9;--bt:#0369a1;--line:rgba(244,168,201,.55);--shade:rgba(20,70,120,.14);--dbg:rgba(255,232,242,.75);--dt:#be4a72}
@media (prefers-color-scheme:dark){:root{--bg:#070d14;--b1:#0c4a6e;--b2:#5b2146;--b3:#312e81;--glass:rgba(30,41,59,.42);--glass2:rgba(255,255,255,.09);--glassb:rgba(255,255,255,.16);--hi:rgba(255,255,255,.2);--solid:rgba(17,27,38,.9);--ink:#e8f4ff;--mute:#93a9bd;--bt:#7dd3fc;--line:rgba(244,168,201,.25);--shade:rgba(0,0,0,.45);--dbg:rgba(120,30,60,.35);--dt:#f9a8c4}}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html{background:var(--bg)}
body{margin:0;min-height:100vh;color:var(--ink);font-family:-apple-system,"SF Pro Display","SF Pro Text",system-ui,Tahoma,sans-serif;-webkit-font-smoothing:antialiased}
body::before{content:"";position:fixed;inset:0;z-index:-1;background:radial-gradient(55% 38% at 12% 8%,var(--b1),transparent 70%),radial-gradient(48% 34% at 95% 22%,var(--b2),transparent 70%),radial-gradient(60% 45% at 40% 100%,var(--b3),transparent 70%)}
.wrap{max-width:520px;margin:0 auto;padding:calc(12px + env(safe-area-inset-top,0px)) 14px 90px}
header{position:sticky;top:calc(8px + env(safe-area-inset-top,0px));z-index:6;display:flex;align-items:center;gap:10px;padding:9px 12px;border-radius:30px;background:var(--glass);-webkit-backdrop-filter:blur(30px) saturate(180%);backdrop-filter:blur(30px) saturate(180%);border:1px solid var(--glassb);box-shadow:0 10px 30px var(--shade),inset 0 1px 0 var(--hi)}
.logo{width:40px;height:40px;flex:none;border-radius:14px;display:flex;align-items:center;justify-content:center;background:linear-gradient(145deg,#7dd3fc,var(--sky));box-shadow:0 6px 16px rgba(14,165,233,.35),inset 0 1px 0 rgba(255,255,255,.6)}
.logo svg{width:21px;height:21px;stroke:#fff;fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round}
header h1{font-size:16px;margin:0;font-weight:700;letter-spacing:.2px}
.sub{font-size:11px;color:var(--mute);display:flex;align-items:center;gap:6px}
.st{width:8px;height:8px;border-radius:50%;background:#9ca3af}.st.ok{background:#22c55e;box-shadow:0 0 8px #22c55e}.st.bad{background:#ef4444}
header .sp{flex:1}
.card{position:relative;background:var(--glass);-webkit-backdrop-filter:blur(28px) saturate(170%);backdrop-filter:blur(28px) saturate(170%);border:1px solid var(--glassb);border-radius:28px;padding:14px;margin-top:14px;box-shadow:0 12px 34px var(--shade),inset 0 1px 0 var(--hi),inset 0 -1px 0 rgba(255,255,255,.12)}
.card::before{content:"";position:absolute;inset:0;border-radius:inherit;pointer-events:none;background:linear-gradient(125deg,rgba(255,255,255,.3),rgba(255,255,255,0) 38%)}
.ct{display:flex;align-items:center;gap:8px;margin-bottom:11px;font-size:13px;font-weight:600;color:var(--bt)}
.ct i{flex:1;height:1px;background:linear-gradient(90deg,var(--line),transparent)}
.g{display:grid;grid-template-columns:repeat(3,1fr);gap:9px;direction:ltr}
.g.two{grid-template-columns:repeat(2,1fr)}
.g.four{grid-template-columns:repeat(4,1fr)}
.b{position:relative;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:6px;min-height:60px;padding:12px 4px;width:100%;font:inherit;font-size:13px;font-weight:500;color:var(--bt);background:var(--glass2);border:1px solid var(--glassb);border-radius:22px;cursor:pointer;box-shadow:inset 0 1px 0 var(--hi),0 3px 10px var(--shade);transition:transform .15s,background .15s,box-shadow .15s}
.b svg{width:21px;height:21px;stroke:currentColor;fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round}
.b:active{transform:scale(.95);background:var(--sky);color:#fff;border-color:transparent;box-shadow:0 6px 18px rgba(14,165,233,.45)}
.b.d{color:var(--dt);background:var(--dbg)}
.b.d:active{background:#f472b6;color:#fff}
.b.pr,.b.on{background:linear-gradient(160deg,#38bdf8,var(--sky));color:#fff;border-color:transparent;box-shadow:0 8px 20px rgba(14,165,233,.4),inset 0 1px 0 rgba(255,255,255,.5)}
.b.kk{min-height:44px;padding:8px 2px;font-size:12px;border-radius:18px}
.dot{width:28px;height:28px;border-radius:50%;color:#fff;display:flex;align-items:center;justify-content:center;font-size:13px;font-weight:600;box-shadow:inset 0 1px 0 rgba(255,255,255,.5),0 3px 8px rgba(0,0,0,.18)}
.sm{padding:6px 13px;font:inherit;font-size:12px;font-weight:500;color:var(--bt);background:var(--glass2);border:1px solid var(--glassb);border-radius:999px;cursor:pointer;box-shadow:inset 0 1px 0 var(--hi)}
.sm.on{background:linear-gradient(160deg,#38bdf8,var(--sky));color:#fff;border-color:transparent}
.ec{display:flex;justify-content:center;gap:4px;margin-top:5px}
.ec button{flex:1;padding:5px 0;font-size:13px;color:var(--bt);background:var(--glass2);border:1px solid var(--glassb);border-radius:12px;cursor:pointer}
.np{font-size:12px;color:var(--mute);text-align:center;margin-top:10px;min-height:16px}
.empty{font-size:12px;color:var(--mute);text-align:center;grid-column:1/-1;padding:8px;line-height:1.7}
.row{display:flex;align-items:center;gap:8px;padding:9px 2px;border-bottom:1px solid var(--line);font-size:13px}
.row:last-child{border-bottom:0}.row span{flex:1}.row em{font-style:normal;color:var(--mute);font-size:11px}
details.card summary{font-size:13px;font-weight:600;color:var(--bt);cursor:pointer;list-style:none}
details.card summary::-webkit-details-marker{display:none}
details .in{margin-top:10px;font-size:12px}
.hint{color:var(--mute);font-size:11px;margin:8px 0 4px;line-height:1.7}
code{display:block;direction:ltr;text-align:left;background:var(--glass2);border:1px solid var(--glassb);border-radius:12px;padding:7px 9px;font-size:11px;word-break:break-all;margin:3px 0}
#t{position:fixed;bottom:calc(26px + env(safe-area-inset-bottom,0px));left:50%;transform:translateX(-50%) translateY(10px);background:var(--solid);color:var(--ink);border:1px solid var(--glassb);-webkit-backdrop-filter:blur(20px);backdrop-filter:blur(20px);padding:10px 22px;border-radius:999px;font-size:13px;font-weight:500;opacity:0;transition:.25s;pointer-events:none;z-index:20;box-shadow:0 10px 30px var(--shade)}
#t.on{opacity:1;transform:translateX(-50%)}
.mb{position:fixed;inset:0;background:rgba(8,25,45,.35);-webkit-backdrop-filter:blur(10px);backdrop-filter:blur(10px);display:flex;align-items:flex-end;justify-content:center;z-index:10}
.mc{background:var(--solid);-webkit-backdrop-filter:blur(40px) saturate(180%);backdrop-filter:blur(40px) saturate(180%);border:1px solid var(--glassb);width:100%;max-width:520px;border-radius:30px 30px 0 0;padding:18px 16px 28px;box-shadow:0 -10px 40px var(--shade),inset 0 1px 0 var(--hi)}
.mc h3{margin:0 0 6px;font-size:17px}
.mc label{display:block;font-size:12px;color:var(--mute);margin:10px 0 4px}
.mc input,.mc textarea,.mc select,.kb input{width:100%;font:inherit;font-size:16px;color:var(--ink);background:var(--glass2);border:1px solid var(--glassb);border-radius:16px;padding:11px;box-shadow:inset 0 1px 2px var(--shade)}
.mc .rw{display:flex;gap:10px;margin-top:16px}
.er{color:#e11d48;font-size:12px;margin-top:8px;min-height:14px}
#lg{position:fixed;inset:0;background:var(--bg);display:none;align-items:center;justify-content:center;z-index:30;padding:20px}
#lg::before{content:"";position:absolute;inset:0;z-index:-1;background:radial-gradient(55% 38% at 12% 8%,var(--b1),transparent 70%),radial-gradient(48% 34% at 95% 22%,var(--b2),transparent 70%),radial-gradient(60% 45% at 40% 100%,var(--b3),transparent 70%)}
#lg .mc{border-radius:30px;max-width:340px;text-align:center}
#lg input{text-align:center;letter-spacing:6px;margin-top:12px}
.chips{display:flex;gap:7px;flex-wrap:wrap;margin:6px 0 10px}
.sw{width:32px;height:32px;border-radius:50%;border:3px solid var(--solid);outline:1px solid var(--glassb);padding:0;cursor:pointer;box-shadow:0 3px 8px var(--shade)}
.sw.on{outline:2px solid var(--ink)}
.tp{height:200px;border-radius:24px;border:1px solid var(--glassb);background:var(--glass2);display:flex;align-items:center;justify-content:center;text-align:center;padding:0 24px;line-height:1.8;color:var(--mute);font-size:12px;touch-action:none;-webkit-user-select:none;user-select:none;-webkit-touch-callout:none;box-shadow:inset 0 2px 10px var(--shade),inset 0 1px 0 var(--hi)}
.kb{display:flex;gap:8px;margin-top:9px;align-items:center}.kb input{flex:1;min-width:0;padding:9px 11px}
.sl{display:flex;flex-direction:column;justify-content:center;gap:4px;font-size:11px;color:var(--mute);padding:0 4px}
.sl input{width:100%;accent-color:var(--sky)}
.fps{display:flex;align-items:center;gap:14px;margin-bottom:10px;direction:ltr}
.fv{font-size:44px;font-weight:700;line-height:1;color:var(--sky);text-shadow:0 4px 18px rgba(14,165,233,.35)}.fv small{font-size:13px;color:var(--mute);margin-left:6px;font-weight:500}
.fi{display:flex;flex-direction:column;gap:3px;font-size:12px;color:var(--mute)}.fi b{color:var(--ink);font-size:13px}
.srow{display:flex;align-items:center;gap:8px;margin:9px 0;font-size:12px;direction:ltr}
.sn{width:34px;color:var(--mute);font-weight:600}
.bar{flex:1;height:9px;border-radius:6px;background:var(--glass2);border:1px solid var(--glassb);overflow:hidden;box-shadow:inset 0 1px 2px var(--shade)}
.bar i{display:block;height:100%;background:linear-gradient(90deg,#7dd3fc,var(--sky));border-radius:6px;transition:width .4s}
.sv{width:104px;text-align:right}.spk{width:60px;height:16px;color:var(--sky)}
.pill{display:inline-block;padding:5px 14px;border-radius:999px;font-size:12px;background:var(--glass2);border:1px solid var(--glassb)}.pill.on{background:var(--dbg);color:var(--dt)}
.qrbox{width:230px;margin:12px auto;background:#fff;padding:8px;border-radius:20px;box-shadow:0 12px 30px var(--shade)}.qrbox svg{width:100%;height:auto;display:block}
[hidden]{display:none!important}
a.sm{text-decoration:none;display:inline-block}
.inp{width:100%;font:inherit;font-size:16px;color:var(--ink);background:var(--glass2);border:1px solid var(--glassb);border-radius:16px;padding:10px;margin-top:8px}
#mon{position:fixed;inset:0;z-index:25;background:#04070b;color:#e8f4ff;padding:calc(12px + env(safe-area-inset-top,0px)) 16px calc(14px + env(safe-area-inset-bottom,0px));display:flex;flex-direction:column;gap:10px;overflow:hidden}
.mtop{display:flex;justify-content:space-between;align-items:center;font-size:13px;color:#93a9bd}
#monb{flex:1;display:flex;flex-direction:column;justify-content:center;gap:16px;direction:ltr}
.mf{text-align:center;font-size:min(30vw,170px);font-weight:700;line-height:1}
.mf small{display:block;font-size:14px;letter-spacing:3px;color:#93a9bd;font-weight:500}
.ma{text-align:center;font-size:14px;color:#93a9bd;margin-top:8px}
.mg{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
.mt{border:1px solid rgba(255,255,255,.14);border-radius:22px;padding:12px 6px;background:rgba(255,255,255,.06);text-align:center}
.mt b{display:block;font-size:min(9vw,40px);margin:4px 0}.mt span{font-size:11px;color:#93a9bd}
.mhint{text-align:center;font-size:11px;color:#6b8296;min-height:14px}
@media (orientation:landscape){#monb{flex-direction:row;align-items:center}#monb>div:first-child{flex:1}.mg{flex:1;grid-template-columns:1fr}.mf{font-size:min(24vw,150px)}}
.b{-webkit-touch-callout:none;-webkit-user-select:none;user-select:none}
.lp{position:absolute;top:9px;left:11px;width:8px;height:8px;border-radius:50%;border:1.5px solid var(--mute);opacity:.75}
`;

const themeJs = `
var TH={
 sky:{a:'#0ea5e9',ink:'#0b2a3f',l:{b1:'#7dd3fc',b2:'#fbcfe8',b3:'#c7d2fe',bt:'#0369a1',line:'rgba(244,168,201,.55)'},d:{b1:'#0c4a6e',b2:'#5b2146',b3:'#312e81',bt:'#7dd3fc',line:'rgba(244,168,201,.25)'}},
 rose:{a:'#ec4899',ink:'#4a0d27',l:{b1:'#f9a8d4',b2:'#fecdd3',b3:'#c7d2fe',bt:'#be185d',line:'rgba(236,72,153,.35)',dt:'#b91c1c',dbg:'rgba(254,226,226,.8)'},d:{b1:'#831843',b2:'#4c1d95',b3:'#1e3a8a',bt:'#f9a8d4',line:'rgba(249,168,212,.28)',dt:'#fca5a5',dbg:'rgba(127,29,29,.4)'}},
 violet:{a:'#8b5cf6',ink:'#25104f',l:{b1:'#c4b5fd',b2:'#fbcfe8',b3:'#bae6fd',bt:'#6d28d9',line:'rgba(139,92,246,.3)'},d:{b1:'#4c1d95',b2:'#701a75',b3:'#1e3a8a',bt:'#c4b5fd',line:'rgba(196,181,253,.28)'}},
 green:{a:'#10b981',ink:'#06402f',l:{b1:'#86efac',b2:'#bae6fd',b3:'#fde68a',bt:'#047857',line:'rgba(16,185,129,.3)'},d:{b1:'#064e3b',b2:'#0c4a6e',b3:'#365314',bt:'#6ee7b7',line:'rgba(110,231,183,.25)'}}
};
var BASE={
 l:{bg:'#eef7ff',glass:'rgba(255,255,255,.5)',glass2:'rgba(255,255,255,.64)',glassb:'rgba(255,255,255,.8)',hi:'rgba(255,255,255,.95)',solid:'rgba(255,255,255,.86)',mute:'#6b8296',shade:'rgba(20,70,120,.14)',dbg:'rgba(255,232,242,.75)',dt:'#be4a72'},
 d:{bg:'#070d14',glass:'rgba(30,41,59,.42)',glass2:'rgba(255,255,255,.09)',glassb:'rgba(255,255,255,.16)',hi:'rgba(255,255,255,.2)',solid:'rgba(17,27,38,.9)',mute:'#93a9bd',shade:'rgba(0,0,0,.45)',dbg:'rgba(120,30,60,.35)',dt:'#f9a8c4'}
};
function pref(k,d){try{return localStorage.getItem(k)||d}catch(e){return d}}
function setPref(k,v){try{localStorage.setItem(k,v)}catch(e){}}
function applyTheme(){
  var mode=pref('mode','auto'),acc=TH[pref('accent','sky')]||TH.sky;
  var dark=mode=='dark'||(mode=='auto'&&window.matchMedia&&matchMedia('(prefers-color-scheme: dark)').matches);
  var k=dark?'d':'l',v={},st=document.documentElement.style,i;
  for(i in BASE[k])v[i]=BASE[k][i];
  for(i in acc[k])v[i]=acc[k][i];
  v.sky=acc.a;v.ink=dark?'#e8f4ff':acc.ink;
  for(i in v)st.setProperty('--'+i,v[i]);
  st.colorScheme=dark?'dark':'light';
}
applyTheme();
try{matchMedia('(prefers-color-scheme: dark)').addEventListener('change',applyTheme)}catch(e){}
`;

const js = `
var S={},edit=false,snooze=0,prof='',BF=null;
var $=function(i){return document.getElementById(i)};
function esc(s){return String(s).replace(/[&<>"']/g,function(c){return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]})}
function tap(){try{navigator.vibrate&&navigator.vibrate(12)}catch(e){}var h=$('hp');if(h)h.click()}
function toast(m){var t=$('t');t.textContent=m||'تم ✓';t.classList.add('on');setTimeout(function(){t.classList.remove('on')},1000)}
function tm(t){var d=new Date(t);return d.toLocaleDateString('ar-SA',{day:'numeric',month:'short'})+' '+d.toLocaleTimeString('ar-SA',{hour:'2-digit',minute:'2-digit'})}
function dur(m){return m>=60?Math.floor(m/60)+' ساعة'+(m%60?' و'+(m%60)+' دقيقة':''):m+' دقيقة'}
function showLogin(){$('lg').style.display='flex';setTimeout(function(){$('pin').focus()},50)}
async function get(u){var r=await fetch(u,{cache:'no-store'});if(r.status==401){showLogin();throw new Error('login')}return r.json()}
async function api(u,body){
  var o={method:'POST',headers:{'Content-Type':'application/json'}};
  if(body!==undefined)o.body=JSON.stringify(body);
  var r=await fetch(u,o);
  if(r.status==401){showLogin();throw new Error('login')}
  if(!r.ok)throw new Error('fail');
  return r;
}
async function login(){
  var e=$('le');e.textContent='';
  var r=await fetch('/api/login',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({pin:$('pin').value,app:navigator.standalone?1:0})});
  var j={};try{j=await r.json()}catch(x){}
  if(r.ok){$('lg').style.display='none';$('pin').value='';boot();return}
  e.textContent=(j.error||'تعذر الدخول')+(j.left!==undefined&&j.left<5?' (باقي '+j.left+' محاولات)':'');
}

/* ---------- step types for macros ---------- */
var DO_OPTS=[['volup','رفع الصوت'],['voldown','خفض الصوت'],['mute','كتم'],['play','تشغيل / إيقاف'],['next','التالي'],['prev','السابق'],['stop','إيقاف الميديا'],['lock','قفل'],['sleep','سكون'],['restart','إعادة التشغيل'],['shutdown','إيقاف التشغيل']];
var STEPS=[
 {n:'برنامج / لعبة / موقع',pre:'app:',ph:'https://youtube.com أو steam://rungameid/ID'},
 {n:'اختصار كيبورد',pre:'key:',ph:'ctrl+shift+m'},
 {n:'كتابة نص',pre:'text:',ph:'النص'},
 {n:'نقرة ماوس',pre:'click:',opts:[['l','يسار'],['r','يمين'],['d','مزدوجة'],['m','وسط']]},
 {n:'انتظار بالثواني',pre:'wait:',ph:'2'},
 {n:'إجراء نظام',pre:'do:',opts:DO_OPTS},
 {n:'أمر ويندوز',pre:'cmd:',ph:'ipconfig /flushdns'},
 {n:'إغلاق برنامج',pre:'kill:',ph:'discord.exe'},
 {n:'سطوع الشاشة (0-100)',pre:'bright:',ph:'50'},
 {n:'OBS',pre:'obs:',opts:[['record','تسجيل'],['stream','بث'],['mute','كتم المايك']]},
 {n:'OBS: تبديل مشهد',pre:'obs:scene:',ph:'اسم المشهد'}
];
function stepLabel(s){
  var best=null;
  STEPS.forEach(function(st){if(s.indexOf(st.pre)==0&&(!best||st.pre.length>best.pre.length))best=st});
  if(!best)return s;
  var v=s.slice(best.pre.length);
  if(best.opts)best.opts.forEach(function(o){if(o[0]==v)v=o[1]});
  return best.n+': '+v;
}

/* ---------- profiles and buttons ---------- */
var KINDS=[['app','apps'],['scene','scenes'],['cmd','commands']];
function fixProf(){
  var ok=function(id){return S.profiles.some(function(p){return p.id==id})};
  if(!ok(prof)){prof=pref('prof','');if(!ok(prof))prof=S.profiles[0].id}
}
function btnList(){
  var out=[];
  KINDS.forEach(function(k){(S[k[1]]||[]).forEach(function(it,i){if((it.p||S.profiles[0].id)==prof)out.push({k:k[0],i:i,it:it})})});
  return out;
}
function tile(o){
  var it=o.it,c=/^#[0-9a-f]{6}$/i.test(it.color||'')?it.color:'#0ea5e9';
  var ic=it.icon?esc(it.icon):esc(it.name.charAt(0));
  var a='data-k="'+o.k+'" data-i="'+o.i+'"';
  var lg=it.long&&it.long.length;
  var h='<div><button class="b" data-a="run" '+a+(lg?' data-long="1"':'')+'>'+(lg?'<i class="lp"></i>':'')+'<span class="dot" style="background:'+c+'">'+ic+'</span>'+esc(it.name)+'</button>';
  if(edit)h+='<div class="ec"><button data-a="mv" '+a+' data-d="-1">‹</button><button data-a="mv" '+a+' data-d="1">›</button><button data-a="ed" '+a+'>✎</button><button data-a="col" '+a+'>●</button><button data-a="del" '+a+'>×</button></div>';
  return h+'</div>';
}
function renderProf(){
  var h='';
  S.profiles.forEach(function(p){h+='<button class="sm'+(p.id==prof?' on':'')+'" data-a="prof" data-v="'+esc(p.id)+'">'+esc(p.name)+'</button>'});
  h+='<button class="sm" data-a="profadd">+ بروفايل</button>';
  if(edit)h+='<button class="sm" data-a="profren">إعادة تسمية</button><button class="sm" data-a="profdel">حذف البروفايل</button>';
  $('profs').innerHTML=h;
}

/* ---------- rendering ---------- */
function render(){
  renderProf();
  var h='';btnList().forEach(function(o){h+=tile(o)});
  $('btns').innerHTML=h||'<div class="empty">لا توجد أزرار في هذا البروفايل. اضغط + زر</div>';
  $('ed').textContent=edit?'تم':'تعديل';
  $('md').textContent={auto:'تلقائي',light:'فاتح',dark:'داكن'}[pref('mode','auto')];
  var s2='';
  S.schedules.forEach(function(s){
    s2+='<div class="row"><span>'+esc(s.label)+'<br><em>'+(s.kind=='daily'?'يومياً '+esc(s.hm):'مرة واحدة '+tm(s.ts))+'</em></span><button class="sm" data-a="sdel" data-v="'+esc(s.id)+'">حذف</button></div>';
  });
  $('sch').innerHTML=s2||'<div class="empty">لا توجد مهام مجدولة</div>';
  var l='';
  S.log.forEach(function(x){l+='<div class="row"><span>'+esc(x.what)+'<br><em>'+esc(x.who)+' · '+tm(x.t)+'</em></span></div>'});
  $('logs').innerHTML=l||'<div class="empty">السجل فارغ</div>';
  var base=location.origin,sc=S.scenes[0]?S.scenes[0].name:'scene',st=S.settings||{};
  var mode=pref('mode','auto'),acc=pref('accent','sky');
  var h2='<p class="hint">المظهر (يُحفظ في هذا الجهاز فقط)</p><div class="chips">';
  [['auto','تلقائي'],['light','فاتح'],['dark','داكن']].forEach(function(m){h2+='<button class="sm'+(mode==m[0]?' on':'')+'" data-a="theme" data-v="'+m[0]+'">'+m[1]+'</button>'});
  h2+='</div><div class="chips">';
  [['sky','#0ea5e9'],['rose','#ec4899'],['violet','#8b5cf6'],['green','#10b981']].forEach(function(c){h2+='<button class="sw'+(acc==c[0]?' on':'')+'" data-a="accent" data-v="'+c[0]+'" style="background:'+c[1]+'" aria-label="'+c[0]+'"></button>'});
  h2+='</div>';
  h2+='<div class="row"><span>تنبيه الخمول: '+(st.idleMin?'بعد '+st.idleMin+' دقيقة':'متوقف')+'</span><button class="sm" data-a="setidle">ضبط</button></div>';
  h2+='<div class="row"><span>مجموعة الصباح: '+esc(st.morningScene||'متوقفة')+'<br><em>من '+st.morningFrom+' إلى '+st.morningTo+' عند أول دخول للموقع</em></span><button class="sm" data-a="setmorning">ضبط</button></div>';
  h2+='<div class="row"><span>OBS: المنفذ '+esc(st.obsPort)+(st.hasObsPass?' · بكلمة سر':' · بدون كلمة سر')+'<br><em>مصدر المايك: '+esc(st.obsMic||'')+'</em></span><button class="sm" data-a="setobs">ضبط</button></div>';
  h2+='<div class="row"><span>تسجيل جلسات الألعاب: '+(st.sessLog?'مفعّل':'متوقف')+'<br><em>يحتاج PresentMon، ويتجاهل المتصفحات وديسكورد وغيرها</em></span><button class="sm" data-a="sesstoggle">'+(st.sessLog?'إيقاف':'تفعيل')+'</button><button class="sm" data-a="sessignore">التجاهل</button></div>';
  h2+='<div class="row"><span>نسخة السيرفر: '+esc(S.version||'')+'</span></div>';
  h2+='<div class="row"><span>الشاشة الجانبية<br><em>رابط يعرض الأداء فقط بدون تسجيل دخول</em></span><button class="sm" data-a="side">الرابط</button><button class="sm" data-a="sidereset">تغيير</button></div>';
  h2+='<p class="hint">مفتاح الاختصارات (لا تشاركه):</p><code>'+esc(S.key)+'</code>';
  h2+='<p class="hint"><b>Siri</b>: انسخ رابط الزر، ثم في تطبيق اختصارات (Shortcuts) اضغط + وأضف إجراء "الحصول على محتويات عنوان URL" والصق الرابط، وسمّ الاختصار باسم الزر. بعدها قل: يا Siri، واسم الزر. الايفون لازم يكون على نفس الشبكة أو Tailscale.</p>';
  [['scene',S.scenes,'ماكرو / اختصار / نص'],['app',S.apps,'برنامج / لعبة'],['cmd',S.commands,'أمر']].forEach(function(g){
    g[1].forEach(function(it){
      var u=base+'/s/btn/'+encodeURIComponent(it.name)+'?key='+S.key;
      h2+='<div class="row"><span>'+esc(it.name)+'<br><em>'+g[2]+'</em></span><button class="sm" data-a="copy" data-v="'+esc(u)+'">نسخ الرابط</button>'+(it.long&&it.long.length?'<button class="sm" data-a="copy" data-v="'+esc(u+'&long=1')+'">المطوّلة</button>':'')+'</div>';
    });
  });
  h2+='<div class="row"><span>HomeKit (عبر Homebridge)<br><em>ينسخ إعداد إضافة homebridge-http-switch لكل الأزرار</em></span><button class="sm" data-a="hkcopy">نسخ الإعداد</button></div>';
  h2+='<p class="hint">الأجهزة المسجلة (الحد '+S.maxDevices+'). لإضافة جهاز جديد افتح localhost:3000/pair على الكمبيوتر وامسح رمز QR، أو افتح التسجيل بالـ PIN من نفس الصفحة (أو اكتب pair في نافذة CMD) وأغلقه بعد التسجيل.</p>';
  S.devices.forEach(function(d,i){h2+='<div class="row"><span>'+esc(d.name)+'<br><em>'+tm(d.added)+'</em></span><button class="sm" data-a="devdel" data-i="'+i+'">حذف</button></div>'});
  h2+='<div class="row"><span>جهاز Wake-on-LAN: '+esc(S.wolMac||'غير مضبوط')+'</span><button class="sm" data-a="setwol">ضبط</button></div>';
  h2+='<div class="row"><span>نسيان هذا الجهاز</span><button class="sm" data-a="forget">خروج</button></div>';
  $('set').innerHTML=h2;
  $('wolbox').innerHTML=S.wol?'<div style="margin-top:9px"><button class="b" data-a="wol">تشغيل جهاز (Wake-on-LAN)</button></div>':'';
}
async function init(){S=await get('/api/state');fixProf();render()}

/* ---------- generic form ---------- */
function form(title,hint,fields,cb){
  var h='<div class="mb"><div class="mc"><h3>'+title+'</h3>'+(hint?'<div class="hint">'+hint+'</div>':'');
  fields.forEach(function(f){
    h+='<label>'+f.label+'</label>';
    if(f.t=='area')h+='<textarea id="f_'+f.id+'" rows="5"></textarea>';
    else if(f.t=='sel')h+='<select id="f_'+f.id+'">'+f.opts.map(function(o){return '<option value="'+esc(o[0])+'">'+esc(o[1])+'</option>'}).join('')+'</select>';
    else h+='<input id="f_'+f.id+'" value="'+esc(f.val||'')+'" placeholder="'+esc(f.ph||'')+'">';
  });
  h+='<div class="rw"><button class="b" id="fc">إلغاء</button><button class="b pr" id="fo">حفظ</button></div><div id="fe" class="er"></div></div></div>';
  $('m').innerHTML=h;
  $('fc').onclick=function(){$('m').innerHTML=''};
  $('fo').onclick=async function(){
    var v={};
    for(var i=0;i<fields.length;i++){var f=fields[i];v[f.id]=$('f_'+f.id).value.trim();if(!v[f.id]&&!f.opt){$('fe').textContent='عبّ كل الحقول';return}}
    try{await cb(v);$('m').innerHTML='';await init()}catch(e){$('fe').textContent='تعذر الحفظ'}
  };
}

/* ---------- button editor (apps, games, hotkeys, text, commands, macros) ---------- */
function btnForm(ed){
  var cur={type:'app',target:'',keys:'',text:'',cmd:'',steps:[],sel:0,long:[],lsel:0,longOpen:false};
  var name='',icon='';
  if(ed){
    var it=ed.it;name=it.name;icon=it.icon||'';
    cur.long=(it.long||[]).slice();cur.longOpen=cur.long.length>0;
    if(ed.k=='app'){cur.type='app';cur.target=it.target}
    else if(ed.k=='cmd'){cur.type='cmd';cur.cmd=it.cmd}
    else{
      cur.steps=it.steps.slice();cur.type='macro';
      if(it.steps.length==1&&it.steps[0].indexOf('key:')==0){cur.type='key';cur.keys=it.steps[0].slice(4)}
      else if(it.steps.length==1&&it.steps[0].indexOf('text:')==0){cur.type='text';cur.text=it.steps[0].slice(5)}
    }
  }
  var TYPES=[['app','برنامج / لعبة / موقع'],['key','اختصار كيبورد'],['text','نص جاهز'],['cmd','أمر ويندوز'],['macro','إجراءات متعددة / ماكرو']];
  if(ed){var grp=ed.k=='app'?['app']:ed.k=='cmd'?['cmd']:['key','text','macro'];TYPES=TYPES.filter(function(t){return grp.indexOf(t[0])>=0})}
  function selOf(P){return P=='b'?cur.sel:cur.lsel}
  function grab(){
    var g=function(i){var e=$(i);return e?e.value:null},v;
    if((v=g('b_target'))!==null)cur.target=v;
    if((v=g('b_key'))!==null)cur.keys=v;
    if((v=g('b_text'))!==null)cur.text=v;
    if((v=g('b_cmd'))!==null)cur.cmd=v;
    if((v=g('b_st'))!==null)cur.sel=+v;
    if((v=g('l_st'))!==null)cur.lsel=+v;
  }
  function svDraw(P){
    var st=STEPS[selOf(P)]||STEPS[0],h='';
    if(st.opts)h='<select id="'+P+'_sval">'+st.opts.map(function(o){return '<option value="'+esc(o[0])+'">'+esc(o[1])+'</option>'}).join('')+'</select>';
    else h='<input id="'+P+'_sval" placeholder="'+esc(st.ph||'')+'">';
    $(P+'_sv').innerHTML=h;
  }
  function listHtml(P,arr,title){
    var op=P=='b'?'ms':'ls';
    var h='<label>'+title+'</label><div id="'+P+'_steps">';
    arr.forEach(function(s,i){
      h+='<div class="row"><span>'+(i+1)+'. '+esc(stepLabel(s))+'</span><button class="sm" data-a="'+op+'" data-o="up" data-i="'+i+'">↑</button><button class="sm" data-a="'+op+'" data-o="dn" data-i="'+i+'">↓</button><button class="sm" data-a="'+op+'" data-o="del" data-i="'+i+'">×</button></div>';
    });
    if(!arr.length)h+='<div class="empty">لا توجد خطوات بعد</div>';
    h+='</div><label>إضافة خطوة</label><select id="'+P+'_st">'+STEPS.map(function(s,i){return '<option value="'+i+'"'+(i==selOf(P)?' selected':'')+'>'+esc(s.n)+'</option>'}).join('')+'</select><div id="'+P+'_sv" style="margin-top:8px"></div><button class="b" id="'+P+'_add" style="margin-top:8px;min-height:44px">+ إضافة الخطوة</button>';
    return h;
  }
  function wire(P,arr){
    $(P+'_st').onchange=function(){grab();svDraw(P)};
    $(P+'_add').onclick=function(){
      grab();var st=STEPS[selOf(P)],el=$(P+'_sval'),v=el?el.value.trim():'';
      if(!v){err('اكتب قيمة الخطوة');return}
      arr.push(st.pre+v);err('');draw();
    };
    svDraw(P);
  }
  function draw(){
    var t=cur.type,h='';
    if(t=='app')h='<label>الرابط أو المسار أو بروتوكول اللعبة</label><input id="b_target" value="'+esc(cur.target)+'" placeholder="https://… أو C:/…/app.exe أو steam://rungameid/ID"><button class="sm" id="b_steam" style="margin-top:8px">اختيار لعبة من Steam</button>';
    else if(t=='key')h='<label>الاختصار</label><input id="b_key" value="'+esc(cur.keys)+'" placeholder="ctrl+shift+m"><div class="hint">الأسماء: ctrl alt shift win enter esc tab space f1 إلى f12 والحروف والأرقام والأسهم left up right down</div>';
    else if(t=='text')h='<label>النص الذي يُكتب على الكمبيوتر</label><textarea id="b_text" rows="3">'+esc(cur.text)+'</textarea>';
    else if(t=='cmd')h='<label>الأمر</label><input id="b_cmd" value="'+esc(cur.cmd)+'" placeholder="ipconfig /flushdns">';
    else h=listHtml('b',cur.steps,'الخطوات (تُنفّذ بالترتيب)');
    $('b_fields').innerHTML=h;
    if(t=='app')$('b_steam').onclick=steamList;
    if(t=='macro')wire('b',cur.steps);
    $('b_long').innerHTML='<details id="b_ld"'+(cur.longOpen?' open':'')+'><summary>ضغطة مطوّلة (اختياري): إجراء ثاني</summary><div class="hint">لما تمسك الزر نصف ثانية تُنفَّذ هذي الخطوات بدل الإجراء العادي. مثال: الضغطة العادية تفتح Discord والمطوّلة تقفله بخطوة "إغلاق برنامج".</div>'+listHtml('l',cur.long,'خطوات الضغطة المطوّلة')+'</details>';
    $('b_ld').addEventListener('toggle',function(){cur.longOpen=this.open});
    wire('l',cur.long);
  }
  function err(m){$('fe').textContent=m}
  async function steamList(){
    grab();
    try{
      var j=await get('/api/steam'),h='<label>ألعاب Steam المثبتة</label>';
      if(!j.games.length)h+='<div class="empty">لم أجد ألعاب Steam على هذا الجهاز</div>';
      j.games.forEach(function(g){h+='<div class="row"><span>'+esc(g.name)+'</span><button class="sm" data-a="steampick" data-id="'+esc(g.id)+'" data-n="'+esc(g.name)+'">اختيار</button></div>'});
      h+='<button class="sm" id="b_back" style="margin-top:8px">رجوع</button>';
      $('b_fields').innerHTML=h;$('b_back').onclick=draw;
    }catch(e){err('تعذر قراءة ألعاب Steam')}
  }
  async function save(){
    grab();
    var nm=$('b_name').value.trim(),ic=$('b_icon').value.trim(),t=cur.type,kind,body={name:nm,icon:ic,p:prof,long:cur.long.slice()};
    if(!nm){err('اكتب اسم الزر');return}
    if(t=='app'){kind='app';if(!cur.target.trim()){err('اكتب الرابط أو المسار');return}body.target=cur.target.trim()}
    else if(t=='cmd'){kind='cmd';if(!cur.cmd.trim()){err('اكتب الأمر');return}body.cmd=cur.cmd.trim()}
    else{
      kind='scene';
      if(t=='key'){if(!cur.keys.trim()){err('اكتب الاختصار');return}body.steps=['key:'+cur.keys.trim()]}
      else if(t=='text'){if(!cur.text.trim()){err('اكتب النص');return}body.steps=['text:'+cur.text]}
      else{if(!cur.steps.length){err('أضف خطوة واحدة على الأقل');return}body.steps=cur.steps}
    }
    try{
      if(ed)await api('/api/edit/'+kind+'?i='+ed.i,body);else await api('/api/add/'+kind,body);
      BF=null;$('m').innerHTML='';await init();
    }catch(e){err('تعذر الحفظ (قد يكون الاسم مكرراً أو الاختصار غير صحيح)')}
  }
  var h='<div class="mb"><div class="mc" style="max-height:90vh;overflow:auto"><h3>'+(ed?'تعديل الزر':'زر جديد')+'</h3>'+
    '<label>الاسم (وهو الذي تناديه به Siri)</label><input id="b_name" value="'+esc(name)+'">'+
    '<label>رمز (حرف أو إيموجي، اختياري)</label><input id="b_icon" maxlength="4" value="'+esc(icon)+'">'+
    '<label>النوع</label><select id="b_type">'+TYPES.map(function(t){return '<option value="'+t[0]+'"'+(t[0]==cur.type?' selected':'')+'>'+t[1]+'</option>'}).join('')+'</select>'+
    '<div id="b_fields"></div><div id="b_long" style="margin-top:12px"></div>'+
    '<div class="rw"><button class="b" id="fc">إلغاء</button><button class="b pr" id="fo">حفظ</button></div><div id="fe" class="er"></div></div></div>';
  $('m').innerHTML=h;
  BF={steam:function(id,n){cur.target='steam://rungameid/'+id;var ni=$('b_name');if(ni&&!ni.value.trim())ni.value=n;draw()},
    step:function(o,i,w){
      grab();var a=cur[w];
      if(o=='del')a.splice(i,1);
      else if(o=='up'&&i>0){var t=a[i];a[i]=a[i-1];a[i-1]=t}
      else if(o=='dn'&&i<a.length-1){var t2=a[i];a[i]=a[i+1];a[i+1]=t2}
      draw();
    }};
  $('b_type').onchange=function(){grab();cur.type=this.value;draw()};
  $('fc').onclick=function(){BF=null;$('m').innerHTML=''};
  $('fo').onclick=save;
  draw();
}

function openSched(){
  var o=[['do:shutdown','إيقاف التشغيل'],['do:restart','إعادة التشغيل'],['do:sleep','سكون'],['do:lock','قفل']];
  S.scenes.forEach(function(s){o.push(['scene:'+s.name,'زر: '+s.name])});
  S.commands.forEach(function(s){o.push(['saved:'+s.name,'أمر: '+s.name])});
  S.apps.forEach(function(s){o.push(['app:'+s.target,'برنامج: '+s.name])});
  form('مهمة مجدولة','اكتب +30 للتنفيذ بعد 30 دقيقة مرة واحدة، أو 23:30 للتنفيذ يومياً',[{id:'when',label:'الوقت',ph:'+30'},{id:'what',label:'ماذا يُنفّذ',t:'sel',opts:o}],function(v){
    var sel=$('f_what');v.label=sel.options[sel.selectedIndex].text;return api('/api/sched',v)});
}
function openIdle(){
  form('تنبيه الخمول','عدد الدقائق بدون استخدام قبل ظهور التنبيه (اكتب 0 لإيقافه)',[{id:'idleMin',label:'الدقائق',ph:'60'}],function(v){return api('/api/settings',{idleMin:v.idleMin})});
}
function openMorning(){
  var o=[['none','متوقفة']];S.scenes.forEach(function(s){o.push([s.name,s.name])});
  form('مجموعة الصباح','تُنفَّذ مرة واحدة عند أول دخول للموقع داخل هذي الساعات',[{id:'scene',label:'الزر (ماكرو)',t:'sel',opts:o},{id:'from',label:'من الساعة',ph:'5'},{id:'to',label:'إلى الساعة',ph:'12'}],function(v){return api('/api/settings',{morningScene:v.scene,morningFrom:v.from,morningTo:v.to})});
}
function openObs(){
  var st=S.settings||{};
  form('إعدادات OBS','في OBS: قائمة Tools ثم WebSocket Server Settings، فعّل الخادم وانسخ المنفذ وكلمة السر',[{id:'obsPort',label:'المنفذ',val:String(st.obsPort||4455)},{id:'obsMic',label:'اسم مصدر المايك في OBS',val:st.obsMic||'Mic/Aux'},{id:'obsPassword',label:'كلمة السر (اتركها فارغة لعدم التغيير، أو اكتب - لمسحها)',opt:true}],function(v){
    var b={obsPort:v.obsPort,obsMic:v.obsMic};if(v.obsPassword)b.obsPassword=v.obsPassword;return api('/api/settings',b)});
}

/* ---------- pending shutdown banner, idle banner ---------- */
var pw=null;
async function pend(){
  if(document.hidden)return;
  try{var j=await get('/api/pending');pw=j.kind?{kind:j.kind,end:Date.now()+j.left*1000}:null;pwTick()}catch(e){}
}
function pwTick(){
  var b=$('pw');
  if(!pw){b.style.display='none';return}
  var l=Math.max(0,Math.ceil((pw.end-Date.now())/1000));
  b.style.display='block';
  $('pwTxt').textContent=(pw.kind=='restart'?'إعادة التشغيل':'إيقاف التشغيل')+' بعد '+l+' ثانية';
  if(l<=0&&Date.now()-pw.end>6000)pw=null;
}
async function idle(){
  if(document.hidden||!S.settings)return;
  var lim=S.settings.idleMin;
  if(!lim){$('idle').style.display='none';return}
  try{
    var j=await get('/api/idle'),m=Math.floor(j.sec/60);
    var show=j.sec>=0&&m>=lim&&Date.now()>snooze;
    $('idle').style.display=show?'block':'none';
    if(show)$('idleTxt').textContent='الكمبيوتر خامل من '+dur(m)+'. تبي تقفله أو تطفيه؟';
  }catch(e){}
}

/* ---------- mouse and keyboard ---------- */
var TP={on:false,max:0,sx:0,sy:0,lx:0,ly:0,t0:0,moved:false,ax:0,ay:0,as:0,tmr:null,drag:false};
function send(b){
  fetch('/api/in',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify(b),keepalive:true})
   .then(function(r){if(r.status==401)showLogin()}).catch(function(){});
}
function tpPos(e){var t=e.touches,x=0,y=0;for(var i=0;i<t.length;i++){x+=t[i].clientX;y+=t[i].clientY}return {x:x/t.length,y:y/t.length,n:t.length}}
function tpStart(e){
  e.preventDefault();var p=tpPos(e);
  if(!TP.on){TP.on=true;TP.t0=Date.now();TP.moved=false;TP.max=0;TP.sx=p.x;TP.sy=p.y}
  TP.max=Math.max(TP.max,p.n);TP.lx=p.x;TP.ly=p.y;
  if(!TP.tmr)TP.tmr=setInterval(tpFlush,30);
}
function tpMove(e){
  e.preventDefault();var p=tpPos(e),dx=p.x-TP.lx,dy=p.y-TP.ly;TP.lx=p.x;TP.ly=p.y;
  if(Math.abs(p.x-TP.sx)+Math.abs(p.y-TP.sy)>6)TP.moved=true;
  var s=parseFloat($('sens').value)||1.6;
  if(p.n>=2)TP.as+=dy*0.9;else{TP.ax+=dx*s;TP.ay+=dy*s}
}
function tpEnd(e){
  e.preventDefault();
  if(e.touches.length>0){var p=tpPos(e);TP.lx=p.x;TP.ly=p.y;return}
  if(!TP.moved&&Date.now()-TP.t0<300)send({b:TP.max>=2?'r':'l'});
  TP.on=false;tpFlush();clearInterval(TP.tmr);TP.tmr=null;
}
function tpFlush(){
  var mx=Math.trunc(TP.ax),my=Math.trunc(TP.ay),sc=Math.trunc(TP.as);
  if(!mx&&!my&&!sc)return;
  TP.ax-=mx;TP.ay-=my;TP.as-=sc;
  var b={};if(mx||my)b.m=[mx,my];if(sc)b.s=sc*3;
  send(b);
}

/* ---------- performance and OBS ---------- */
var HIST={cpu:[],gpu:[],ram:[],fps:[]};
function pushH(k,v){var a=HIST[k];a.push(v);if(a.length>30)a.shift()}
function spark(a){
  if(a.length<2)return '';
  var pts=a.map(function(v,i){return (i*60/(a.length-1)).toFixed(1)+','+(15-v*0.14).toFixed(1)}).join(' ');
  return '<svg class="spk" viewBox="0 0 60 16" preserveAspectRatio="none"><polyline points="'+pts+'" fill="none" stroke="currentColor" stroke-width="1.2"/></svg>';
}
function srow(n,v,txt,k){
  if(v===null)return '<div class="srow"><span class="sn">'+n+'</span><span class="sv" style="width:auto;flex:1;text-align:left;color:var(--mute)">غير متاح</span></div>';
  return '<div class="srow"><span class="sn">'+n+'</span><div class="bar"><i style="width:'+v+'%"></i></div><span class="sv">'+txt+'</span>'+spark(HIST[k])+'</div>';
}
function fpsRow(f){
  var msg=FPSMSG;
  if(!f||f.state!='ok')return '<div class="hint" style="margin:0 0 8px">'+esc(fpsMsg(f))+'</div>';
  return '<div class="fps"><div class="fv">'+f.fps+'<small>FPS</small></div><div class="fi"><b>'+esc(f.app)+'</b><span>'+f.ms+' ms · 1% low '+f.low+'</span></div></div>';
}
async function stat(){
  if(document.hidden||!S.apps||MON)return;
  try{
    var j=await get('/api/stats');
    pushH('cpu',j.cpu);pushH('ram',j.ram.pct);if(j.gpu)pushH('gpu',j.gpu.pct);
    $('stats').innerHTML=fpsRow(j.fps)+srow('CPU',j.cpu,j.cpu+'%','cpu')+
      srow('GPU',j.gpu?j.gpu.pct:null,j.gpu?j.gpu.pct+'%'+(j.gpu.temp!=null?' · '+j.gpu.temp+'°':''):'','gpu')+
      srow('RAM',j.ram.pct,j.ram.pct+'% · '+j.ram.used+'/'+j.ram.total+' GB','ram');
  }catch(e){}
}
function renderObs(o){
  var b=$('obs');
  if(!o.ok){b.innerHTML='<div class="empty">OBS غير متصل. شغّل OBS، ثم من Tools اختر WebSocket Server Settings وفعّل الخادم، واضبط المنفذ وكلمة السر من إعدادات الموقع.</div>';return}
  var h='<div class="np">'+(o.rec?'<b style="color:#e11d48">● يسجّل</b> ':'')+(o.stream?'<b style="color:#e11d48">● يبث</b>':'')+(!o.rec&&!o.stream?'متصل':'')+'</div>';
  h+='<div class="g"><button class="b'+(o.rec?' d':'')+'" data-a="obs" data-v="record">'+(o.rec?'إيقاف التسجيل':'بدء التسجيل')+'</button>'+
     '<button class="b'+(o.stream?' d':'')+'" data-a="obs" data-v="stream">'+(o.stream?'إيقاف البث':'بدء البث')+'</button>'+
     '<button class="b" data-a="obs" data-v="mute">كتم المايك</button></div>';
  if(o.scenes&&o.scenes.length){
    h+='<div class="hint">المشاهد</div><div class="g two">';
    o.scenes.forEach(function(s){h+='<button class="b'+(s==o.scene?' on':'')+'" data-a="obsscene" data-v="'+esc(s)+'">'+esc(s)+'</button>'});
    h+='</div>';
  }
  b.innerHTML=h;
}
async function obsPoll(){
  if(document.hidden||!S.apps||!$('obsd').open)return;
  try{renderObs(await get('/api/obs'))}catch(e){}
}
async function np(){
  if(document.hidden||!S.apps)return;
  try{var j=await get('/api/now');var t=j.title||'';$('np').textContent=t.indexOf(' - ')>0?'يعمل الآن: '+t:''}catch(e){}
}

/* ---------- click handling ---------- */
var FPSMSG={missing:'FPS غير مفعّل: ضع PresentMon.exe بجانب server.js وشغّل السيرفر كمسؤول',denied:'تعذر تشغيل PresentMon: شغّل السيرفر كمسؤول (Run as administrator)',error:'تعذر تشغيل PresentMon، جرّب بعد قليل',starting:'جاري تشغيل قياس FPS…',idle:'FPS: لا توجد لعبة تعمل الآن'};
var MON=false,WL=null,updBusy=false;
function fpsMsg(f){return (FPSMSG[f&&f.state]||FPSMSG.missing)+(f&&f.state=='missing'&&f.dir?' ('+f.dir+')':'')}
function pad2(n){return n<10?'0'+n:''+n}
function hms(s){return Math.floor(s/3600)+':'+pad2(Math.floor(s%3600/60))+':'+pad2(s%60)}
function dsec(s){var h=Math.floor(s/3600),m=Math.floor(s%3600/60);return h?h+'س '+m+'د':m+'د'}

/* ---------- full-screen monitor ---------- */
function bigSpark(a){
  if(a.length<2)return '';
  var mx=Math.max.apply(null,a.concat([30])),pts=a.map(function(v,i){return (i*300/(a.length-1)).toFixed(1)+','+(70-v/mx*66).toFixed(1)}).join(' ');
  return '<svg viewBox="0 0 300 72" preserveAspectRatio="none" style="width:100%;height:70px;color:#38bdf8"><polyline points="'+pts+'" fill="none" stroke="currentColor" stroke-width="2"/></svg>';
}
function tileM(n,v,sub,hot){return '<div class="mt"><span>'+n+'</span><b'+(hot?' style="color:#ef4444"':'')+'>'+v+'</b><span>'+sub+'</span></div>'}
function renderMon(j){
  var f=j.fps&&j.fps.state=='ok'?j.fps:null,h='';
  if(f){
    HIST.fps.push(f.fps);if(HIST.fps.length>60)HIST.fps.shift();
    var c=f.fps>=60?'#22c55e':f.fps>=30?'#f59e0b':'#ef4444';
    h+='<div><div class="mf" style="color:'+c+'">'+f.fps+'<small>FPS</small></div><div class="ma">'+esc(f.app)+' · 1% low '+f.low+' · '+f.ms+' ms'+(j.sess?' · الجلسة '+hms(j.sess.secs)+' · متوسط '+j.sess.avg:'')+'</div></div>'+bigSpark(HIST.fps);
  }else h+='<div class="ma" style="font-size:15px;line-height:1.9">'+esc(fpsMsg(j.fps))+'</div>';
  var g=j.gpu;
  h+='<div class="mg">'+tileM('CPU',j.cpu+'%','',j.cpu>=90)+tileM('GPU',g?g.pct+'%':'-',g&&g.temp!=null?g.temp+'°C':'غير متاح',!!(g&&g.temp>=85))+tileM('RAM',j.ram.pct+'%',j.ram.used+'/'+j.ram.total+' GB',j.ram.pct>=92)+'</div>';
  $('monb').innerHTML=h;
}
async function monTick(){
  if(!MON)return;
  try{renderMon(await get('/api/stats?fast=1'))}catch(e){}
}
async function wakeOn(){
  try{if(navigator.wakeLock){WL=await navigator.wakeLock.request('screen');return}}catch(e){}
  try{var v=$('nosleep');if(v&&v.play)v.play()}catch(e){}
}
function wakeOff(){
  try{if(WL){WL.release();WL=null}}catch(e){}
  try{var v=$('nosleep');if(v&&v.pause)v.pause()}catch(e){}
}
function monOpen(){
  MON=true;HIST.fps=[];$('mon').hidden=false;
  $('monh').textContent=navigator.wakeLock?'':'لو انطفت الشاشة: الإعدادات ← العرض والسطوع ← القفل التلقائي ← أبداً';
  wakeOn();monTick();
}
function monClose(){MON=false;$('mon').hidden=true;wakeOff()}
document.addEventListener('visibilitychange',function(){if(MON&&!document.hidden){wakeOn();monTick()}});

/* ---------- game sessions ---------- */
async function sessLoad(){
  if(document.hidden||!S.apps||!$('sessd').open)return;
  try{renderSess(await get('/api/sessions'))}catch(e){}
}
function renderSess(j){
  var h='';
  if(j.active)h+='<div class="hint">جلسة جارية: '+esc(j.active.app)+' · '+dsec(j.active.secs)+' · متوسط '+j.active.avg+' FPS</div>';
  if(!j.pm)h+='<div class="empty">تسجيل الجلسات يحتاج PresentMon.exe بجانب server.js وتشغيل السيرفر كمسؤول.</div>';
  else if(!j.enabled)h+='<div class="empty">تسجيل الجلسات متوقف (فعّله من الإعدادات).</div>';
  if(!j.list.length){h+='<div class="empty">لا توجد جلسات مسجّلة بعد. تُسجَّل الألعاب تلقائياً بعد دقيقة لعب أو أكثر.</div>'}
  else{
    h+='<div class="hint">ملخص كل لعبة</div>';
    j.summary.forEach(function(g){h+='<div class="row"><span>'+esc(g.app)+'<br><em>'+g.count+' جلسة · '+dsec(g.secs)+'</em></span><b style="direction:ltr">'+g.avg+' FPS</b>'+(g.maxTemp!=null?'<span style="flex:none;color:var(--mute);font-size:11px;direction:ltr">'+g.maxTemp+'°</span>':'')+'</div>'});
    h+='<div class="hint">آخر الجلسات</div>';
    j.list.slice(0,20).forEach(function(s){h+='<div class="row"><span>'+esc(s.app)+'<br><em>'+tm(s.start)+' · '+dsec(s.secs)+'</em></span><span style="flex:none;text-align:left;font-size:12px;direction:ltr">'+s.avg+' FPS<br><em>1% '+s.low+(s.maxTemp!=null?' · '+s.maxTemp+'°':'')+'</em></span></div>'});
  }
  h+='<div style="display:flex;gap:8px;margin-top:10px"><a class="sm" href="/api/sessions.csv" download>تنزيل CSV</a><button class="sm" data-a="sessclear">مسح السجل</button></div>';
  $('sess').innerHTML=h;
}

/* ---------- server update from the phone ---------- */
function updMsg(m){$('upm').textContent=m}
function waitBack(){
  var n=0,t0=null;
  fetch('/api/ping',{cache:'no-store'}).then(function(r){return r.json()}).then(function(j){t0=j.t}).catch(function(){});
  var iv=setInterval(async function(){
    n++;
    try{var r=await fetch('/api/ping',{cache:'no-store'}),j=await r.json();if(j.t&&t0&&j.t!=t0){clearInterval(iv);updMsg('رجع السيرفر ✓');setTimeout(function(){location.reload()},600);return}}catch(e){}
    if(n>40){clearInterval(iv);updBusy=false;updMsg('لم يرجع السيرفر خلال دقيقة، تحقق من الكمبيوتر')}
  },1500);
}
async function updSend(url,body,okText){
  var r=await fetch(url,{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify(body)});
  var j={};try{j=await r.json()}catch(x){}
  if(r.status==401){showLogin();updBusy=false;return}
  if(!r.ok){updMsg('رُفض: '+(j.error||r.status));updBusy=false;return}
  updMsg(okText+' '+j.version+'. جاري إعادة التشغيل…');
  waitBack();
}
async function updGo(){
  if(updBusy)return;
  var f=$('upf').files&&$('upf').files[0],pin=$('upin').value;
  if(!f){updMsg('اختر ملف server.js أولاً');return}
  if(!pin){updMsg('اكتب الـ PIN');return}
  if(!confirm('تحديث السيرفر من الملف '+f.name+'؟ تُحفظ نسخة احتياطية ويُعاد التشغيل.'))return;
  updBusy=true;updMsg('جاري قراءة الملف…');
  try{var code=await f.text();updMsg('جاري الفحص والتشغيل التجريبي…');await updSend('/api/update',{code:code,pin:pin},'تم التحديث إلى')}
  catch(e){updMsg('تعذر الرفع');updBusy=false}
}
async function restoreGo(name){
  if(updBusy)return;
  var pin=$('upin').value;
  if(!pin){updMsg('اكتب الـ PIN');return}
  if(!confirm('استرجاع '+name+'؟'))return;
  updBusy=true;updMsg('جاري الفحص…');
  try{await updSend('/api/restore',{name:name,pin:pin},'تم الاسترجاع إلى')}catch(e){updMsg('تعذر الاسترجاع');updBusy=false}
}
async function bkLoad(){
  if(!$('updd').open)return;
  try{
    var j=await get('/api/backups'),h='<div class="hint">النسخ الاحتياطية (آخر 8). الاسترجاع يحتاج الـ PIN المكتوب فوق.</div>';
    j.backups.forEach(function(b){h+='<div class="row"><span>'+esc(b.name)+'<br><em>'+tm(b.t)+'</em></span><button class="sm" data-a="restore" data-n="'+esc(b.name)+'">استرجاع</button></div>'});
    if(!j.backups.length)h+='<div class="empty">لا توجد نسخ بعد</div>';
    $('bk').innerHTML=h;$('upv').textContent='النسخة الحالية: '+j.version;
  }catch(e){}
}

function sideUrl(){return location.origin+'/side?k='+S.viewKey}
function sideInfo(){
  var u=sideUrl();
  $('m').innerHTML='<div class="mb"><div class="mc"><h3>الشاشة الجانبية</h3>'+
    '<div class="hint">صفحة بسيطة تعرض FPS وحرارة وحمل الكرت وCPU وRAM، بدون أي أزرار وبدون تسجيل دخول. تشتغل مثل شاشة ثانية بجانب شاشتك.</div>'+
    '<code>'+esc(u)+'</code>'+
    '<div class="hint">للتثبيت بملء الشاشة بدون شريط سفاري: افتح الرابط في سفاري، ثم زر المشاركة، ثم "إضافة إلى الشاشة الرئيسية". افتحه من الأيقونة واضغط "اضغط للبدء" عشان ما تنطفي الشاشة.</div>'+
    '<div class="hint">تقدر تمسحه بالكاميرا من صفحة localhost:3000/pair على الكمبيوتر.</div>'+
    '<div class="rw"><button class="b" id="fc">إغلاق</button><button class="b pr" id="sc">نسخ الرابط</button></div></div></div>';
  $('fc').onclick=function(){$('m').innerHTML=''};
  $('sc').onclick=function(){if(copyText(u))toast('تم النسخ ✓');else prompt('انسخ الرابط من هنا',u)};
}
function copyText(t){
  try{if(navigator.clipboard&&window.isSecureContext){navigator.clipboard.writeText(t);return true}}catch(e){}
  var ok=false;
  try{
    var ta=document.createElement('textarea');
    ta.value=t;ta.style.position='fixed';ta.style.opacity='0';
    document.body.appendChild(ta);ta.focus();ta.select();ta.setSelectionRange(0,t.length);
    ok=document.execCommand('copy');document.body.removeChild(ta);
  }catch(e){}
  return ok;
}
function hkConfig(){
  var base=location.origin,seen={},acc=[];
  [S.scenes,S.apps,S.commands].forEach(function(arr){arr.forEach(function(it){
    if(seen[it.name])return;seen[it.name]=1;
    acc.push({accessory:'HTTP-SWITCH',name:it.name,switchType:'stateless',timeout:1000,onUrl:base+'/s/btn/'+encodeURIComponent(it.name)+'?key='+S.key});
  })});
  return JSON.stringify({accessories:acc},null,2);
}
async function handle(d){
  tap();var a=d.a;
  try{
    if(a=='login')return login();
    if(a=='do'){var pwr=(d.v=='shutdown'||d.v=='restart');if(pwr&&!confirm('متأكد؟ يبدأ العدّ التنازلي 30 ثانية وتقدر تلغيه.'))return;await api('/api/do/'+d.v);toast();if(pwr)pend()}
    else if(a=='run'){if(edit)return;await api('/api/run/'+d.k+'?i='+d.i);toast()}
    else if(a=='del'){if(confirm('حذف؟')){await api('/api/del/'+d.k+'?i='+d.i);await init()}}
    else if(a=='mv'){await api('/api/move/'+d.k+'?i='+d.i+'&d='+d.d);await init()}
    else if(a=='col'){await api('/api/color/'+d.k+'?i='+d.i);await init()}
    else if(a=='ed'){var arr=S[d.k=='app'?'apps':d.k=='cmd'?'commands':'scenes'];btnForm({k:d.k,i:+d.i,it:arr[+d.i]})}
    else if(a=='addbtn')btnForm(null);
    else if(a=='ms'){if(BF)BF.step(d.o,+d.i,'steps')}
    else if(a=='ls'){if(BF)BF.step(d.o,+d.i,'long')}
    else if(a=='steampick'){if(BF)BF.steam(d.id,d.n)}
    else if(a=='prof'){prof=d.v;setPref('prof',prof);render()}
    else if(a=='profadd')form('بروفايل جديد','مثل: ألعاب، شغل، نوم',[{id:'name',label:'الاسم'}],async function(v){var r=await api('/api/profile/add',{name:v.name}),j=await r.json();prof=j.id;setPref('prof',prof)});
    else if(a=='profren'){var cp=S.profiles.filter(function(p){return p.id==prof})[0];form('إعادة تسمية البروفايل','',[{id:'name',label:'الاسم',val:cp?cp.name:''}],function(v){return api('/api/profile/ren?id='+prof,{name:v.name})})}
    else if(a=='profdel'){if(S.profiles.length<2){toast('لا يمكن حذف آخر بروفايل');return}if(confirm('حذف البروفايل وكل أزراره؟')){await api('/api/profile/del?id='+prof);prof='';await init()}}
    else if(a=='edit'){edit=!edit;render()}
    else if(a=='cycle'){var ms=['auto','light','dark'],cm=pref('mode','auto');setPref('mode',ms[(ms.indexOf(cm)+1)%3]);applyTheme();render()}
    else if(a=='theme'){setPref('mode',d.v);applyTheme();render()}
    else if(a=='accent'){setPref('accent',d.v);applyTheme();render()}
    else if(a=='sadd')openSched();
    else if(a=='sdel'){await api('/api/sdel?id='+d.v);await init()}
    else if(a=='wol'){await api('/api/wol');toast('تم الإرسال')}
    else if(a=='setwol'){var m=prompt('MAC address (مثل AA:BB:CC:DD:EE:FF)');if(m){await api('/api/setwol',{mac:m});await init()}}
    else if(a=='copy'){if(copyText(d.v))toast('تم النسخ ✓');else prompt('انسخ الرابط من هنا',d.v)}
    else if(a=='hkcopy'){var hk=hkConfig();if(copyText(hk))toast('تم نسخ الإعداد ✓');else prompt('انسخ الإعداد من هنا',hk)}
    else if(a=='setidle')openIdle();
    else if(a=='setmorning')openMorning();
    else if(a=='setobs')openObs();
    else if(a=='devdel'){if(confirm('حذف هذا الجهاز؟')){await api('/api/devdel?i='+d.i);await init()}}
    else if(a=='forget'){if(confirm('نسيان هذا الجهاز؟')){await api('/api/forget');location.reload()}}
    else if(a=='pwcancel'){await api('/api/do/cancel');pw=null;pwTick();toast('تم الإلغاء')}
    else if(a=='idlelock'){await api('/api/do/lock');snooze=Date.now()+1800000;$('idle').style.display='none';toast()}
    else if(a=='idleoff'){if(confirm('إطفاء الكمبيوتر؟')){await api('/api/do/shutdown');toast()}}
    else if(a=='snooze'){snooze=Date.now()+1800000;$('idle').style.display='none'}
    else if(a=='mb')send({b:d.v});
    else if(a=='drag'){TP.drag=!TP.drag;send({b:TP.drag?'ld':'lu'});$('dragb').textContent=TP.drag?'إفلات السحب':'سحب (إمساك الزر)';$('dragb').className='b'+(TP.drag?' on':'')}
    else if(a=='kt'||a=='kte'){var tv=$('kt').value;if(!tv)return;send({t:tv});$('kt').value='';if(a=='kte')setTimeout(function(){send({k:'enter'})},350)}
    else if(a=='key'){if(d.v=='alt+f4'&&!confirm('إغلاق النافذة الحالية؟'))return;send({k:d.v})}
    else if(a=='side')sideInfo();
    else if(a=='sidereset'){if(confirm('تغيير رابط الشاشة الجانبية؟ الرابط القديم يتوقف عن العمل.')){await api('/api/viewkey/reset');await init();toast('تم التغيير ✓')}}
    else if(a=='mon')monOpen();
    else if(a=='monx')monClose();
    else if(a=='sessclear'){if(confirm('مسح سجل الجلسات كله؟')){await api('/api/sessions/clear');sessLoad()}}
    else if(a=='sesstoggle'){await api('/api/settings',{sessLog:!(S.settings&&S.settings.sessLog)});await init();sessLoad()}
    else if(a=='sessignore'){var ss=S.settings||{};form('قائمة التجاهل','أسماء برامج مفصولة بفواصل لا تُحسب ألعاباً (مثل chrome,discord)',[{id:'sessIgnore',label:'القائمة',val:ss.sessIgnore||''}],function(v){return api('/api/settings',{sessIgnore:v.sessIgnore})})}
    else if(a=='updgo')updGo();
    else if(a=='restore')restoreGo(d.n);
    else if(a=='obs'){await api('/api/obs/do',{a:d.v});toast();obsPoll()}
    else if(a=='obsscene'){await api('/api/obs/do',{a:'scene',v:d.v});obsPoll()}
  }catch(e){if(a=='obs'||a=='obsscene')toast('تعذر الاتصال بـ OBS')}
}
var LP={t:null,fired:false};
document.addEventListener('pointerdown',function(e){
  var b=e.target.closest('[data-long]');if(!b||edit)return;
  LP.fired=false;clearTimeout(LP.t);
  LP.t=setTimeout(function(){
    LP.fired=true;tap();
    api('/api/run/'+b.dataset.k+'?i='+b.dataset.i+'&long=1').then(function(){toast('ضغطة مطوّلة ✓')}).catch(function(){});
  },550);
});
document.addEventListener('pointerup',function(){clearTimeout(LP.t);setTimeout(function(){LP.fired=false},350)});
document.addEventListener('pointercancel',function(){clearTimeout(LP.t);LP.fired=false});
document.addEventListener('contextmenu',function(e){if(e.target.closest&&e.target.closest('[data-long]'))e.preventDefault()});
document.addEventListener('click',function(e){
  if(LP.fired){LP.fired=false;return}
  var b=e.target.closest('[data-a]');if(b)handle(b.dataset);
});
$('pin').addEventListener('keydown',function(e){if(e.key=='Enter')login()});
var tpEl=$('tp');
$('obsd').addEventListener('toggle',obsPoll);
$('sessd').addEventListener('toggle',sessLoad);
$('updd').addEventListener('toggle',bkLoad);
tpEl.addEventListener('touchstart',tpStart,{passive:false});
tpEl.addEventListener('touchmove',tpMove,{passive:false});
tpEl.addEventListener('touchend',tpEnd,{passive:false});
tpEl.addEventListener('touchcancel',tpEnd,{passive:false});
$('sens').value=pref('sens','1.6');
$('sens').addEventListener('input',function(){setPref('sens',this.value)});
async function ping(){
  try{var r=await fetch('/api/ping',{cache:'no-store'});$('st').className='st '+(r.ok?'ok':'bad')}catch(e){$('st').className='st bad'}
}
async function boot(){
  try{
    await init();
    var r=await api('/api/open'),j=await r.json();
    if(j.ran)toast('صباح الخير: '+j.ran);
    np();idle();pend();stat();obsPoll();sessLoad();
  }catch(e){}
}
setInterval(ping,5000);setInterval(np,10000);setInterval(idle,60000);setInterval(pend,3000);setInterval(pwTick,1000);
setInterval(stat,2000);setInterval(obsPoll,3000);setInterval(monTick,1000);setInterval(sessLoad,15000);ping();
boot();
`;

const noSleepSrc = 'data:video/mp4;base64,AAAAIGZ0eXBpc29tAAACAGlzb21pc28yYXZjMW1wNDEAAAM1bW9vdgAAAGxtdmhkAAAAAAAAAAAAAAAAAAAD6AAAA+gAAQAAAQAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAgAAAl90cmFrAAAAXHRraGQAAAADAAAAAAAAAAAAAAABAAAAAAAAA+gAAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAABAAAAAABAAAAAQAAAAAAAkZWR0cwAAABxlbHN0AAAAAAAAAAEAAAPoAAAAAAABAAAAAAHXbWRpYQAAACBtZGhkAAAAAAAAAAAAAAAAAAAoAAAAKABVxAAAAAAALWhkbHIAAAAAAAAAAHZpZGUAAAAAAAAAAAAAAABWaWRlb0hhbmRsZXIAAAABgm1pbmYAAAAUdm1oZAAAAAEAAAAAAAAAAAAAACRkaW5mAAAAHGRyZWYAAAAAAAAAAQAAAAx1cmwgAAAAAQAAAUJzdGJsAAAAtnN0c2QAAAAAAAAAAQAAAKZhdmMxAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAABAAEABIAAAASAAAAAAAAAABFUxhdmM2MC4zMS4xMDIgbGlieDI2NAAAAAAAAAAAAAAAGP//AAAALGF2Y0MBQsAK/+EAFWdCwAraewEQAAADABAAAAMAoPEiagEABGjOPIAAAAAQcGFzcAAAAAEAAAABAAAAFGJ0cnQAAAAAAAAVoAAAFaAAAAAYc3R0cwAAAAAAAAABAAAABQAACAAAAAAUc3RzcwAAAAAAAAABAAAAAQAAABxzdHNjAAAAAAAAAAEAAAABAAAABQAAAAEAAAAoc3RzegAAAAAAAAAAAAAABQAAApAAAAAJAAAACQAAAAkAAAAJAAAAFHN0Y28AAAAAAAAAAQAAA2UAAABidWR0YQAAAFptZXRhAAAAAAAAACFoZGxyAAAAAAAAAABtZGlyYXBwbAAAAAAAAAAAAAAAAC1pbHN0AAAAJal0b28AAAAdZGF0YQAAAAEAAAAATGF2ZjYwLjE2LjEwMAAAAAhmcmVlAAACvG1kYXQAAAJ6BgX//3bcRem95tlIt5Ys2CDZI+7veDI2NCAtIGNvcmUgMTY0IHIzMTA4IDMxZTE5ZjkgLSBILjI2NC9NUEVHLTQgQVZDIGNvZGVjIC0gQ29weWxlZnQgMjAwMy0yMDIzIC0gaHR0cDovL3d3dy52aWRlb2xhbi5vcmcveDI2NC5odG1sIC0gb3B0aW9uczogY2FiYWM9MCByZWY9MSBkZWJsb2NrPTE6MDowIGFuYWx5c2U9MHgxOjB4MSBtZT1oZXggc3VibWU9MiBwc3k9MSBwc3lfcmQ9MS4wMDowLjAwIG1peGVkX3JlZj0wIG1lX3JhbmdlPTE2IGNocm9tYV9tZT0xIHRyZWxsaXM9MCA4eDhkY3Q9MCBjcW09MCBkZWFkem9uZT0yMSwxMSBmYXN0X3Bza2lwPTEgY2hyb21hX3FwX29mZnNldD0wIHRocmVhZHM9MSBsb29rYWhlYWRfdGhyZWFkcz0xIHNsaWNlZF90aHJlYWRzPTAgbnI9MCBkZWNpbWF0ZT0xIGludGVybGFjZWQ9MCBibHVyYXlfY29tcGF0PTAgc3RpdGNoYWJsZT0xIGNvbnN0cmFpbmVkX2ludHJhPTAgYmZyYW1lcz0wIHdlaWdodHA9MCBrZXlpbnQ9MjUwIGtleWludF9taW49NSBzY2VuZWN1dD00MCBpbnRyYV9yZWZyZXNoPTAgcmNfbG9va2FoZWFkPTEwIHJjPWNyZiBtYnRyZWU9MSBjcmY9MjMuMCBxY29tcD0wLjYwIHFwbWluPTAgcXBtYXg9NjkgcXBzdGVwPTQgaXBfcmF0aW89MS40MCBhcT0xOjEuMDAAgAAAAA5liIQFP///D0UAASq/gAAAAAVBmiAU9QAAAAVBmkAU9QAAAAVBmmAT9QAAAAVBmoAS9Q==';
const kbtn = (v, t) => '<button class="b kk" data-a="key" data-v="' + v + '">' + t + '</button>';
const keysHtml = '<div class="g four">' + [['esc', 'Esc'], ['tab', 'Tab'], ['backspace', '⌫'], ['enter', 'Enter'],
  ['left', '◄'], ['up', '▲'], ['down', '▼'], ['right', '►'], ['alt+tab', 'Alt+Tab'], ['win', 'Win'], ['win+d', 'Win+D'],
  ['f11', 'F11'], ['ctrl+c', 'Ctrl+C'], ['ctrl+v', 'Ctrl+V'], ['ctrl+z', 'Ctrl+Z'], ['alt+f4', 'Alt+F4']].map(x => kbtn(x[0], x[1])).join('') + '</div>';
const logoSvg = '<svg viewBox="0 0 24 24"><rect x="2" y="3" width="20" height="14" rx="2"/><line x1="8" y1="21" x2="16" y2="21"/><line x1="12" y1="17" x2="12" y2="21"/></svg>';
const mouseCard = card('الماوس والكيبورد',
  '<div id="tp" class="tp"><span>لوحة اللمس: إصبع للتحريك، نقرة خفيفة للنقر، إصبعان للتمرير أو النقر يميناً</span></div>' +
  '<div class="g" style="margin-top:9px"><button class="b kk" data-a="mb" data-v="l">نقر يسار</button><button class="b kk" data-a="mb" data-v="d">نقر مزدوج</button><button class="b kk" data-a="mb" data-v="r">نقر يمين</button></div>' +
  '<div class="g two" style="margin-top:9px"><button class="b kk" id="dragb" data-a="drag">سحب (إمساك الزر)</button>' +
  '<label class="sl"><span>الحساسية</span><input type="range" id="sens" min="0.6" max="4" step="0.1" value="1.6"></label></div>' +
  '<div class="kb"><input id="kt" placeholder="اكتب نصاً ليُكتب على الكمبيوتر"><button class="sm" data-a="kt">كتابة</button><button class="sm" data-a="kte">+ Enter</button></div>' +
  '<div style="height:9px"></div>' + keysHtml);

const page = '<!doctype html><html dir="rtl" lang="ar"><head><meta charset="utf-8">' +
  '<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">' +
  '<meta name="apple-mobile-web-app-capable" content="yes"><meta name="color-scheme" content="light dark">' +
  '<meta name="apple-mobile-web-app-title" content="BLwH/WDM-501"><meta name="apple-mobile-web-app-status-bar-style" content="default">' +
  '<meta name="theme-color" content="#0ea5e9"><link rel="apple-touch-icon" href="/icon-180.png"><link rel="manifest" href="/manifest.webmanifest">' +
  '<title>BLwH/WDM-501</title><style>' + css + '</style><script>' + themeJs + '</script></head><body><div class="wrap">' +
  '<header><div class="logo">' + logoSvg + '</div>' +
  '<div><h1 dir="ltr">BLwH/WDM-501</h1><div class="sub"><span class="st" id="st"></span>PC Remote</div></div><div class="sp"></div>' +
  '<button class="sm" id="md" data-a="cycle"></button><button class="sm" id="ed" data-a="edit">تعديل</button></header>' +
  '<section class="card" id="pw" style="display:none;border-color:#e11d48"><div id="pwTxt" style="font-size:14px;font-weight:600;text-align:center"></div>' +
  '<div style="margin-top:10px"><button class="b pr" data-a="pwcancel">إلغاء</button></div></section>' +
  '<section class="card" id="idle" style="display:none;border-color:var(--sky)"><div id="idleTxt" style="font-size:13px"></div>' +
  '<div class="g two" style="margin-top:10px"><button class="b" data-a="idlelock">قفل</button><button class="b d" data-a="idleoff">إطفاء</button></div>' +
  '<div style="text-align:center;margin-top:8px"><button class="sm" data-a="snooze">ذكّرني بعد 30 دقيقة</button></div></section>' +
  '<section class="card"><div class="ct"><span>أزرارك (برامج وألعاب مسموحة، اختصارات، ماكرو)</span><i></i><button class="sm" data-a="addbtn">+ زر</button></div>' +
  '<div class="chips" id="profs"></div><div class="g" id="btns"></div></section>' +
  card('الصوت', grid(['voldown', 'mute', 'volup']) + '<div style="height:9px"></div>' + grid(['voldown5', 'volup5'], 'two')) +
  card('الميديا', grid(['prev', 'play', 'next']) + '<div class="np" id="np"></div>') +
  mouseCard +
  card('أداء الجهاز', '<div id="stats"><div class="empty">جاري القياس…</div></div>', '<button class="sm" data-a="side">شاشة جانبية</button><button class="sm" data-a="mon">مراقبة</button>') +
  '<details class="card" id="sessd"><summary>سجل الألعاب</summary><div class="in" id="sess"></div></details>' +
  card('الجدولة', '<div id="sch"></div>', '<button class="sm" data-a="sadd">+ مهمة</button>') +
  card('النظام', grid(['lock', 'sleep', 'restart', 'shutdown'], 'two') + '<div id="wolbox"></div>') +
  '<details class="card" id="obsd"><summary>OBS Studio (اختياري)</summary><div class="in" id="obs"></div></details>' +
  '<details class="card"><summary>سجل الأوامر</summary><div class="in" id="logs"></div></details>' +
  '<details class="card"><summary>الإعدادات والأمان</summary><div class="in" id="set"></div></details>' +
  '<details class="card" id="updd"><summary>تحديث السيرفر من الجوال</summary><div class="in"><div class="hint" id="upv"></div>' +
  '<div class="hint">اختر ملف server.js الجديد، واكتب الـ PIN. يفحص السيرفر الملف بتشغيل تجريبي قبل ما يستبدله، ويحفظ نسخة احتياطية.</div>' +
  '<input type="file" id="upf" accept=".js,text/javascript,application/javascript" class="inp">' +
  '<input type="password" id="upin" inputmode="numeric" autocomplete="off" placeholder="PIN للتأكيد" class="inp">' +
  '<button class="b pr" data-a="updgo" style="margin-top:10px;min-height:46px">رفع وتحديث</button><div class="hint" id="upm" style="color:var(--bt)"></div><div id="bk"></div></div></details>' +
  '</div><div id="t">تم ✓</div><div id="m"></div>' +
  '<div id="mon" hidden><div class="mtop"><span>مراقبة الأداء</span><button class="sm" data-a="monx">إغلاق</button></div><div id="monb"></div><div class="mhint" id="monh"></div></div>' +
  '<video id="nosleep" playsinline muted loop src="' + noSleepSrc + '" style="position:fixed;width:1px;height:1px;opacity:0;pointer-events:none"></video>' +
  '<div id="lg"><div class="mc"><h3>أدخل رمز الدخول</h3><div class="hint">يُطلب مرة واحدة فقط لهذا الجهاز</div>' +
  '<input id="pin" type="password" inputmode="numeric" autocomplete="off" placeholder="PIN">' +
  '<div class="rw"><button class="b pr" data-a="login">دخول</button></div><div class="er" id="le"></div></div></div>' +
  '<label id="hp" style="position:absolute;opacity:0;pointer-events:none;width:1px;height:1px"><input type="checkbox" switch></label>' +
  '<script>' + js + '</script></body></html>';

const pairJs = `
var $=function(i){return document.getElementById(i)},isOpen=false;
function esc(s){return String(s).replace(/[&<>"']/g,function(c){return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]})}
function paint(j){
  isOpen=j.open;
  $('stt').textContent=j.open?'التسجيل بالـ PIN مفتوح (بدون وقت محدد)':'التسجيل بالـ PIN مغلق';
  $('stt').className='pill'+(j.open?' on':'');
  $('go').textContent=j.open?'إغلاق التسجيل':'فتح التسجيل';
  $('go').className='b'+(j.open?' d':' pr');
  $('dv').innerHTML=j.devices.map(function(d){return '<div class="row"><span>'+esc(d.name)+'<br><em>'+new Date(d.added).toLocaleString('ar-SA')+'</em></span></div>'}).join('')||'<div class="empty">لا توجد أجهزة</div>';
  $('mx').textContent='الحد المعتاد: '+j.max+' أجهزة. التسجيل بالـ QR أو أثناء فتح التسجيل يتجاوز هذا الحد.';
}
async function qr(){
  var h=$('ad').value;if(!h)return;
  var j=await (await fetch('/pair/qr?h='+encodeURIComponent(h))).json();
  $('qr').innerHTML=j.svg;$('qu').textContent=j.url;
}
async function sqr(){
  var h=$('ad').value;if(!h)return;
  var j=await (await fetch('/pair/sideqr?h='+encodeURIComponent(h))).json();
  $('sqr').innerHTML=j.svg;$('squ').textContent=j.url;
}
async function st(first){
  var j=await (await fetch('/pair/status',{cache:'no-store'})).json();
  paint(j);
  if(first){
    $('ad').innerHTML=j.addrs.map(function(a){return '<option value="'+esc(a.ip)+'">'+esc(a.label)+' - '+esc(a.ip)+'</option>'}).join('');
    if(j.addrs.length){qr();sqr()}else $('qr').innerHTML='<div class="empty">لا توجد شبكة متاحة</div>';
  }
}
$('ad').onchange=function(){qr();sqr()};$('nq').onclick=qr;
$('go').onclick=async function(){await fetch('/pair/open',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({open:!isOpen})});await st(false)};
st(true);setInterval(function(){st(false)},4000);
`;
const pairPage = '<!doctype html><html dir="rtl" lang="ar"><head><meta charset="utf-8">' +
  '<meta name="viewport" content="width=device-width,initial-scale=1"><title>تسجيل جهاز جديد</title>' +
  '<style>' + css + '</style><script>' + themeJs + '</script></head><body><div class="wrap">' +
  '<header><div class="logo">' + logoSvg + '</div>' +
  '<div><h1 dir="ltr">BLwH/WDM-501</h1><div class="sub">تسجيل جهاز جديد (من هذا الكمبيوتر فقط)</div></div></header>' +
  '<section class="card"><div class="ct"><span>رمز QR (لا ينتهي حتى يُستخدم أو تنشئ رمزاً جديداً)</span><i></i></div>' +
  '<label class="sl"><span>العنوان الذي سيفتحه الجوال</span><select id="ad" style="width:100%;font:inherit;font-size:15px;color:var(--ink);background:var(--glass2);border:1px solid var(--glassb);border-radius:14px;padding:9px"></select></label>' +
  '<div class="qrbox" id="qr"></div><code id="qu"></code>' +
  '<div style="margin-top:10px"><button class="b" id="nq" style="min-height:44px">رمز جديد</button></div>' +
  '<p class="hint">امسح الرمز بكاميرا الايفون وسيُسجَّل الجهاز مباشرة بدون PIN. الرمز يعمل لمرة واحدة. كل عنوان مختلف يُسجَّل كجهاز مستقل.</p></section>' +
  '<section class="card"><div class="ct"><span>الشاشة الجانبية (رمز QR)</span><i></i></div>' +
  '<div class="qrbox" id="sqr"></div><code id="squ"></code>' +
  '<p class="hint">امسحه بالايفون، وفي سفاري اضغط المشاركة ثم "إضافة إلى الشاشة الرئيسية". يفتح بملء الشاشة ويعرض الأداء فقط، بدون تسجيل دخول.</p></section>' +
  '<section class="card"><div class="ct"><span>التسجيل بالـ PIN</span><i></i></div>' +
  '<div style="text-align:center;margin-bottom:12px"><span class="pill" id="stt"></span></div>' +
  '<button class="b pr" id="go"></button>' +
  '<p class="hint">وهو مفتوح، أي جهاز يعرف الـ PIN يقدر يسجل نفسه. أغلقه بعد ما تسجّل جهازك.</p></section>' +
  '<section class="card"><div class="ct"><span>الأجهزة المسجلة</span><i></i></div><div id="dv"></div><div class="hint" id="mx"></div></section>' +
  '</div><script>' + pairJs + '</script></body></html>';

// ================= Simple side screen (no login, read-only, opened with a view key) =================
const sideCss = `
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{margin:0;height:100%;background:#000;overflow:hidden}
body{color:#e8f4ff;font-family:-apple-system,"SF Pro Display",system-ui,Tahoma,sans-serif;-webkit-user-select:none;user-select:none}
#s{position:fixed;inset:0;display:grid;grid-template-rows:auto 1fr auto;gap:12px;direction:ltr;padding:calc(12px + env(safe-area-inset-top,0px)) calc(16px + env(safe-area-inset-right,0px)) calc(14px + env(safe-area-inset-bottom,0px)) calc(16px + env(safe-area-inset-left,0px))}
.top{display:flex;justify-content:space-between;align-items:center;color:#6b8296;font-size:15px}
.d{width:10px;height:10px;border-radius:50%;background:#555}.d.ok{background:#22c55e;box-shadow:0 0 10px #22c55e}.d.bad{background:#ef4444}
#main{display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:0}
.big{font-size:min(36vw,210px);font-weight:700;line-height:1;letter-spacing:-2px}
.lbl{font-size:15px;letter-spacing:5px;color:#93a9bd;margin-top:4px}
.sub{color:#93a9bd;font-size:15px;margin-top:10px;text-align:center;line-height:1.7;direction:rtl}
.tiles{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
.t{border:1px solid rgba(255,255,255,.14);border-radius:24px;background:rgba(255,255,255,.06);text-align:center;padding:14px 6px}
.t b{display:block;font-size:min(10vw,46px);margin:4px 0}.t span{color:#93a9bd;font-size:12px;min-height:14px;display:block}
#dim{position:fixed;inset:0;background:#000;opacity:0;pointer-events:none;transition:opacity .4s}#dim.on{opacity:.9}
#go{position:fixed;inset:0;z-index:5;background:#000;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:10px;font-size:26px;direction:rtl}
#go small{font-size:13px;color:#6b8296}
#v{position:fixed;width:1px;height:1px;opacity:0;pointer-events:none}
@media (orientation:landscape){#s{grid-template-columns:1.3fr 1fr;grid-template-rows:auto 1fr}.top{grid-column:1/-1}.tiles{grid-template-columns:1fr;align-content:center}.big{font-size:min(30vh,190px)}}
`;
const sideJs = `
var $=function(i){return document.getElementById(i)},HIST=[],started=false,WL=null,dead=false;
function esc(s){return String(s).replace(/[&<>"']/g,function(c){return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]})}
function pad(n){return n<10?'0'+n:''+n}
function hms(s){return Math.floor(s/3600)+':'+pad(Math.floor(s%3600/60))+':'+pad(s%60)}
var MSG={missing:'FPS غير مفعّل: ضع PresentMon.exe داخل مجلد السيرفر',denied:'شغّل السيرفر كمسؤول ليعمل FPS',error:'تعذر تشغيل PresentMon',starting:'جاري تشغيل قياس FPS…',idle:''};
function clock(){var d=new Date();return pad(d.getHours())+':'+pad(d.getMinutes())}
function tile(n,v,sub,hot){return '<div class="t"><span>'+n+'</span><b'+(hot?' style="color:#ef4444"':'')+'>'+v+'</b><span>'+sub+'</span></div>'}
function spark(a){
  if(a.length<2)return '';
  var mx=Math.max.apply(null,a.concat([30])),pts=a.map(function(v,i){return (i*300/(a.length-1)).toFixed(1)+','+(60-v/mx*56).toFixed(1)}).join(' ');
  return '<svg viewBox="0 0 300 62" preserveAspectRatio="none" style="width:90%;height:56px;margin-top:10px;color:#38bdf8"><polyline points="'+pts+'" fill="none" stroke="currentColor" stroke-width="2"/></svg>';
}
function render(j){
  var f=j.fps&&j.fps.state=='ok'?j.fps:null,h='';
  if(f){
    HIST.push(f.fps);if(HIST.length>60)HIST.shift();
    var c=f.fps>=60?'#22c55e':f.fps>=30?'#f59e0b':'#ef4444';
    h='<div class="big" style="color:'+c+'">'+f.fps+'</div><div class="lbl">FPS</div><div class="sub">'+esc(f.app)+' · 1% low '+f.low+' · '+f.ms+' ms'+(j.sess?' · '+hms(j.sess.secs):'')+'</div>'+spark(HIST);
  }else{
    HIST=[];
    var m=(j.fps&&MSG[j.fps.state])||'';
    if(j.fps&&j.fps.state=='missing'&&j.fps.dir)m+=' ('+j.fps.dir+')';
    h='<div class="big">'+clock()+'</div><div class="sub">'+esc(m)+'</div>';
  }
  $('main').innerHTML=h;
  var g=j.gpu;
  $('tiles').innerHTML=tile('CPU',j.cpu+'%','',j.cpu>=90)+tile('GPU',g?g.pct+'%':'-',g&&g.temp!=null?g.temp+'°C':'',!!(g&&g.temp>=85))+tile('RAM',j.ram.pct+'%',j.ram.used+'/'+j.ram.total+' GB',j.ram.pct>=92);
}
async function poll(){
  if(dead)return;
  try{
    var r=await fetch('/side/stats?k='+K,{cache:'no-store'});
    if(r.status==403){dead=true;$('dot').className='d bad';$('main').innerHTML='<div class="sub">الرابط لم يعد صالحاً. انسخ رابطاً جديداً من الموقع.</div>';return}
    render(await r.json());$('dot').className='d ok';
  }catch(e){$('dot').className='d bad'}
}
function tick(){$('clk').textContent=clock()}
async function wake(){
  try{if(navigator.wakeLock){WL=await navigator.wakeLock.request('screen');return}}catch(e){}
  try{var v=$('v');if(v&&v.play)v.play()}catch(e){}
}
$('go').addEventListener('click',function(){started=true;$('go').style.display='none';wake()});
$('s').addEventListener('click',function(){$('dim').classList.toggle('on')});
document.addEventListener('visibilitychange',function(){if(started&&!document.hidden){wake();poll()}});
tick();setInterval(tick,10000);poll();setInterval(poll,1000);
`;
function sidePage(key) {
  return '<!doctype html><html dir="rtl" lang="ar"><head><meta charset="utf-8">' +
    '<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover,user-scalable=no">' +
    '<meta name="apple-mobile-web-app-capable" content="yes"><meta name="apple-mobile-web-app-title" content="شاشة جانبية">' +
    '<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent"><meta name="theme-color" content="#000000">' +
    '<link rel="apple-touch-icon" href="/icon-180.png"><title>شاشة جانبية</title><style>' + sideCss + '</style></head><body>' +
    '<div id="s"><div class="top"><span id="clk"></span><span id="dot" class="d"></span></div><div id="main"></div><div class="tiles" id="tiles"></div></div>' +
    '<div id="dim"></div><div id="go"><div>اضغط للبدء</div><small>اللمس مرة يخفّف السطوع، ومرة ثانية يرجّعه</small></div>' +
    '<video id="v" playsinline muted loop src="' + noSleepSrc + '"></video>' +
    '<script>var K=' + JSON.stringify(key) + ';' + sideJs + '</script></body></html>';
}

function buildItem(kind, b) {
  const name = String(b.name || '').trim().slice(0, 30);
  if (!name) return null;
  const n = { name };
  if (kind === 'app') { if (!b.target || !String(b.target).trim()) return null; n.target = String(b.target).trim().slice(0, 300); }
  else if (kind === 'cmd') { if (!b.cmd || !String(b.cmd).trim()) return null; n.cmd = String(b.cmd).trim().slice(0, 500); }
  else if (kind === 'scene') {
    const raw = Array.isArray(b.steps) ? b.steps : String(b.steps || '').split(/\r?\n/);
    const steps = raw.map(x => String(x)).filter(validStep).slice(0, 60);
    if (!steps.length) return null;
    n.steps = steps;
  } else return null;
  const icon = Array.from(String(b.icon || '').trim())[0];
  if (icon) n.icon = icon;
  if (Array.isArray(b.long)) { const lg = b.long.map(x => String(x)).filter(validStep).slice(0, 30); if (lg.length) n.long = lg; }
  return n;
}

// ================= Server =================
const json = (res, code, o) => { res.writeHead(code, { 'Content-Type': 'application/json; charset=utf-8' }); res.end(JSON.stringify(o)); };
const bodyBig = (req, max) => new Promise(r => {
  let b = ''; req.on('data', d => { b += d; if (b.length > max) { req.destroy(); r({}); } });
  req.on('end', () => { try { r(JSON.parse(b || '{}')); } catch { r({}); } });
  req.on('error', () => r({}));
});
const body = req => new Promise(r => {
  let b = ''; req.on('data', d => { b += d; if (b.length > 1e5) req.destroy(); });
  req.on('end', () => { try { r(JSON.parse(b || '{}')); } catch { r({}); } });
});

const srv = http.createServer(async (req, res) => {
  try {
    const u = new URL(req.url, 'http://x'), p = u.pathname, I = ip(req), q = n => u.searchParams.get(n);

    if (p === '/') { res.setHeader('Content-Type', 'text/html; charset=utf-8'); return res.end(page); }
    if (p === '/side' || p === '/side/stats') {
      if (u.searchParams.get('k') !== D.viewKey) {
        if (p === '/side/stats') return json(res, 403, {});
        res.writeHead(403, { 'Content-Type': 'text/html; charset=utf-8' });
        return res.end('<meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1"><body style="background:#000;color:#e8f4ff;font-family:sans-serif;text-align:center;padding:40px;direction:rtl">الرابط غير صالح. انسخ رابط الشاشة الجانبية من الموقع (الإعدادات).</body>');
      }
      if (p === '/side/stats') return json(res, 200, await statsInfo(true));
      res.setHeader('Content-Type', 'text/html; charset=utf-8');
      return res.end(sidePage(D.viewKey));
    }
    if (p === '/api/ping') return json(res, 200, { ok: 1, v: VERSION, t: STARTED });
    const mi = /^\/icon-(\d+)\.png$/.exec(p);
    if (mi && [180, 192, 512].includes(+mi[1])) {
      res.writeHead(200, { 'Content-Type': 'image/png', 'Cache-Control': 'max-age=86400' });
      return res.end(png(+mi[1]));
    }
    if (p === '/manifest.webmanifest') {
      res.writeHead(200, { 'Content-Type': 'application/manifest+json; charset=utf-8' });
      return res.end(JSON.stringify({ name: 'BLwH/WDM-501', short_name: 'BLwH/WDM-501', start_url: '/', display: 'standalone',
        background_color: '#ffffff', theme_color: '#0ea5e9', lang: 'ar', dir: 'rtl',
        icons: [{ src: '/icon-192.png', sizes: '192x192', type: 'image/png' }, { src: '/icon-512.png', sizes: '512x512', type: 'image/png' }] }));
    }

    // ---- QR pairing: one-time token, valid for 2 minutes ----
    const pm = /^\/p\/([0-9a-f]{18})$/.exec(p);
    if (pm) {
      if (locked(I)) return res.writeHead(429).end();
      let d = device(req);
      const exp = pairTokens.get(pm[1]);
      if (!d && !exp) {
        fail(I); log(I, 'رمز QR غير صالح');
        res.writeHead(410, { 'Content-Type': 'text/html; charset=utf-8' });
        return res.end('<meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1"><body style="font-family:sans-serif;text-align:center;padding:40px;direction:rtl">الرمز منتهي أو مستخدم. أنشئ رمزاً جديداً من الكمبيوتر.</body>');
      }
      if (!d) {
        pairTokens.delete(pm[1]);
        d = { token: crypto.randomBytes(24).toString('hex'), name: uaName(req) + ' (QR)', added: Date.now() };
        D.devices.push(d); save(); log(I, 'تسجيل جهاز بالـ QR: ' + d.name);
      }
      res.setHeader('Set-Cookie', 'dev=' + d.token + '; Path=/; Max-Age=31536000; HttpOnly; SameSite=Strict');
      res.writeHead(302, { Location: '/' });
      return res.end();
    }

    // ---- device pairing page: only from this PC (localhost) ----
    if (p === '/pair' || p === '/pair/status' || p === '/pair/open' || p === '/pair/qr' || p === '/pair/sideqr') {
      const local = (I === '127.0.0.1' || I === '::1') && /^(localhost|127\.0\.0\.1|\[::1\])(:\d+)?$/.test(req.headers.host || '');
      if (!local) return res.writeHead(404).end();
      if (p === '/pair') { res.setHeader('Content-Type', 'text/html; charset=utf-8'); return res.end(pairPage); }
      if (p === '/pair/status') {
        return json(res, 200, { open: pairOpen, max: MAX_DEVICES,
          addrs: lanAddrs(), devices: D.devices.map(d => ({ name: d.name, added: d.added })) });
      }
      if (p === '/pair/sideqr') {
        const h = u.searchParams.get('h') || '';
        if (!lanAddrs().some(a => a.ip === h)) return json(res, 400, {});
        const url = 'http://' + h + ':' + PORT + '/side?k=' + D.viewKey;
        return json(res, 200, { url, svg: qrSvg(url) });
      }
      if (p === '/pair/qr') {
        const h = u.searchParams.get('h') || '';
        if (!lanAddrs().some(a => a.ip === h)) return json(res, 400, {});
        const url = 'http://' + h + ':' + PORT + '/p/' + newPairToken();
        return json(res, 200, { url, svg: qrSvg(url) });
      }
      if (req.method !== 'POST') return res.writeHead(405).end();
      const o = req.headers.origin;
      if (!(req.headers['content-type'] || '').startsWith('application/json') ||
          (o && !/^http:\/\/(localhost|127\.0\.0\.1|\[::1\])(:\d+)?$/.test(o))) return res.writeHead(403).end();
      const pb = await body(req);
      pairOpen = pb.open !== false;
      log('هذا الكمبيوتر', pairOpen ? 'فتح التسجيل بالـ PIN (بدون وقت محدد)' : 'إغلاق التسجيل بالـ PIN');
      return json(res, 200, { open: pairOpen });
    }

    // ---- iOS Shortcuts / Siri (secret key, no cookie) ----
    if (p.startsWith('/s/')) {
      const lk = locked(I);
      if (lk) return json(res, 429, { error: 'blocked ' + lk + ' min' });
      if (q('key') !== D.key) { const n = fail(I); log(I, 'مفتاح اختصار خاطئ (' + n + ')'); return json(res, 403, {}); }
      const parts = p.slice(3).split('/').map(decodeURIComponent);
      if (parts[0] === 'btn') {
        const f = findBtn(parts[1] || '');
        if (!f) return json(res, 404, { error: 'unknown' });
        const lg = q('long') === '1';
        log(I + ' (اختصار)', (lg ? 'زر (مطوّلة): ' : 'زر: ') + f.it.name);
        runButton(f.kind, f.it, lg);
        return json(res, 200, { ok: 1 });
      }
      const w = parts[0] === 'scene' ? 'scene:' + parts[1] : parts[0] === 'saved' ? 'saved:' + parts[1] : 'do:' + parts[0];
      if (!validWhat(w)) return json(res, 404, { error: 'unknown' });
      log(I + ' (اختصار)', 'تنفيذ: ' + w);
      runWhat(w);
      return json(res, 200, { ok: 1 });
    }

    // ---- login ----
    if (p === '/api/login' && req.method === 'POST') {
      const lk = locked(I);
      if (lk) return json(res, 429, { error: 'محظور مؤقتاً، حاول بعد ' + lk + ' دقيقة' });
      const b = await body(req);
      if (String(b.pin) !== PIN) {
        const n = fail(I); log(I, 'PIN خاطئ (' + n + ' من 5)');
        return json(res, 403, { error: 'PIN خطأ', left: Math.max(0, 5 - n) });
      }
      fails.delete(I);
      let d = device(req);
      if (!d) {
        if (D.devices.length < MAX_DEVICES || pairOpen) {
          d = { token: crypto.randomBytes(24).toString('hex'), name: uaName(req) + (b.app ? ' (تطبيق)' : /iPhone|iPad|Android/.test(req.headers['user-agent'] || '') ? ' (متصفح)' : ''), added: Date.now() };
          D.devices.push(d); save(); log(I, 'تسجيل جهاز جديد: ' + d.name);
        } else {
          log(I, 'جهاز غير مسجّل حاول الدخول (PIN صحيح)');
          return json(res, 403, { error: 'هذا الجهاز غير مسموح. افتح localhost:3000/pair على الكمبيوتر ثم جرّب' });
        }
      }
      res.setHeader('Set-Cookie', 'dev=' + d.token + '; Path=/; Max-Age=31536000; HttpOnly; SameSite=Strict');
      return json(res, 200, { ok: 1 });
    }

    // ---- everything else needs a registered device ----
    if (!p.startsWith('/api/')) return res.writeHead(404).end();
    const dv = device(req);
    if (!dv) return json(res, 401, { error: 'login' });
    const who = dv.name + ' (' + I + ')';

    if (p === '/api/state') {
      return json(res, 200, {
        apps: D.apps, scenes: D.scenes, commands: D.commands, schedules: D.schedules,
        log: D.log.slice(0, 50), settings: pubSettings(), profiles: D.profiles, version: VERSION, viewKey: D.viewKey, maxDevices: MAX_DEVICES, key: D.key, wol: !!D.wolMac, wolMac: D.wolMac,
        devices: D.devices.map(d => ({ name: d.name, added: d.added })),
      });
    }
    if (p === '/api/now') return json(res, 200, { title: await nowPlaying() });
    if (p === '/api/idle') return json(res, 200, { sec: await idleSec() });
    if (p === '/api/stats') return json(res, 200, await statsInfo(q('fast') === '1'));
    if (p === '/api/obs') return json(res, 200, await obsStatus());
    if (p === '/api/steam') return json(res, 200, { games: steamGames() });
    if (p === '/api/backups') return json(res, 200, { backups: listBackups(), version: VERSION });
    if (p === '/api/sessions') return json(res, 200, { list: sessions.slice().reverse(), summary: sessionsSummary(), active: sessInfo(), enabled: !!D.settings.sessLog, pm: !!presentMonExe() });
    if (p === '/api/sessions.csv') {
      const rows = ['app,start,end,seconds,avg_fps,low1_fps,min_fps,max_fps,avg_cpu_pct,avg_gpu_pct,max_gpu_temp'];
      sessions.forEach(x => rows.push([x.app, new Date(x.start).toISOString(), new Date(x.end).toISOString(), x.secs, x.avg, x.low, x.min, x.max, x.cpu,
        x.gpu == null ? '' : x.gpu, x.maxTemp == null ? '' : x.maxTemp].map(v => '"' + String(v).replace(/"/g, '""') + '"').join(',')));
      res.writeHead(200, { 'Content-Type': 'text/csv; charset=utf-8', 'Content-Disposition': 'attachment; filename="game-sessions.csv"' });
      return res.end('\uFEFF' + rows.join('\r\n'));
    }
    if (p === '/api/pending') {
      if (pending && pending.until < Date.now() - 5000) pending = null;
      return json(res, 200, pending ? { kind: pending.kind, left: Math.max(0, Math.ceil((pending.until - Date.now()) / 1000)) } : {});
    }
    if (req.method !== 'POST') return res.writeHead(405).end();

    if (p.startsWith('/api/do/')) {
      const n = p.slice(8), a = actions[n];
      if (!a) return json(res, 404, {});
      a(); log(who, 'أمر: ' + (labels[n] || n)); return json(res, 200, { ok: 1 });
    }

    const kind = p.split('/')[3];
    if (p.startsWith('/api/run/') || p.startsWith('/api/del/') || p.startsWith('/api/move/') ||
        p.startsWith('/api/color/') || p.startsWith('/api/add/') || p.startsWith('/api/edit/')) {
      if (!L[kind]) return json(res, 404, {});
      const arr = D[L[kind]], i = +q('i'), it = arr[i];

      if (p.startsWith('/api/add/') || p.startsWith('/api/edit/')) {
        const b = await body(req), isEdit = p.startsWith('/api/edit/');
        if (isEdit && !it) return json(res, 404, {});
        const n = buildItem(kind, b);
        if (!n) return json(res, 400, { error: 'bad' });
        if (kind === 'scene' && D.scenes.some((x, j) => !(isEdit && j === i) && x.name === n.name)) return json(res, 409, { error: 'dup' });
        if (isEdit) {
          if (kind === 'scene' && it.name !== n.name) {
            D.schedules.forEach(sc => { if (sc.what === 'scene:' + it.name) sc.what = 'scene:' + n.name; });
            if (D.settings.morningScene === it.name) D.settings.morningScene = n.name;
          }
          n.p = it.p; n.color = it.color; arr[i] = n; save(); log(who, 'تعديل زر: ' + n.name);
        } else {
          n.p = D.profiles.some(x => x.id === b.p) ? b.p : D.profiles[0].id;
          n.color = PALETTE[arr.length % PALETTE.length];
          arr.push(n); save(); log(who, 'إضافة زر: ' + n.name);
        }
        return json(res, 200, { ok: 1 });
      }
      if (!it) return json(res, 404, {});
      if (p.startsWith('/api/run/')) {
        const lg = q('long') === '1';
        log(who, (lg ? 'ضغطة مطوّلة: ' : 'تشغيل: ') + it.name);
        runButton(kind, it, lg);
      } else if (p.startsWith('/api/del/')) {
        arr.splice(i, 1); save(); log(who, 'حذف: ' + it.name);
      } else if (p.startsWith('/api/move/')) {
        const dir = +q('d') > 0 ? 1 : -1;
        let j = i + dir;
        while (arr[j] && arr[j].p !== it.p) j += dir;
        if (arr[j]) { [arr[i], arr[j]] = [arr[j], arr[i]]; save(); }
      } else if (p.startsWith('/api/color/')) {
        it.color = PALETTE[(PALETTE.indexOf(it.color) + 1) % PALETTE.length]; save();
      }
      return json(res, 200, { ok: 1 });
    }

    if (p === '/api/in') {
      const b = await body(req), cl = (v, mx) => Math.max(-mx, Math.min(mx, Math.round(+v || 0)));
      if (Array.isArray(b.m)) { const dx = cl(b.m[0], 300), dy = cl(b.m[1], 300); if (dx || dy) inp.move(dx, dy); }
      if (b.s) inp.scroll(cl(b.s, 1200));
      if (typeof b.b === 'string' && /^(l|r|m|d|ld|lu)$/.test(b.b)) inp.click(b.b);
      if (typeof b.k === 'string') {
        if (!inp.keys(b.k)) return json(res, 400, { error: 'key' });
        log(who, 'اختصار: ' + b.k.slice(0, 40));
      }
      if (typeof b.t === 'string' && b.t) { inp.text(b.t); log(who, 'كتابة نص (' + Math.min(b.t.length, 500) + ' حرف)'); }
      return json(res, 200, { ok: 1 });
    }
    if (p === '/api/obs/do') {
      const b = await body(req), a = b.a === 'scene' ? 'scene:' + String(b.v || '') : String(b.a || '');
      if (!/^(record|stream|mute|scene:.+)$/.test(a)) return json(res, 400, {});
      try { await obsAct(a); log(who, 'OBS: ' + a); return json(res, 200, { ok: 1 }); }
      catch { return json(res, 502, { error: 'obs' }); }
    }
    if (p === '/api/profile/add') {
      const b = await body(req), name = String(b.name || '').trim().slice(0, 24);
      if (!name || D.profiles.length >= 12) return json(res, 400, {});
      const pr = { id: crypto.randomBytes(3).toString('hex'), name };
      D.profiles.push(pr); save(); log(who, 'بروفايل جديد: ' + name);
      return json(res, 200, { id: pr.id });
    }
    if (p === '/api/profile/ren') {
      const b = await body(req), name = String(b.name || '').trim().slice(0, 24), pr = D.profiles.find(x => x.id === q('id'));
      if (!pr || !name) return json(res, 400, {});
      pr.name = name; save(); return json(res, 200, { ok: 1 });
    }
    if (p === '/api/profile/del') {
      const id = q('id');
      if (D.profiles.length < 2 || !D.profiles.some(x => x.id === id)) return json(res, 400, {});
      D.profiles = D.profiles.filter(x => x.id !== id);
      ['apps', 'scenes', 'commands'].forEach(k => { D[k] = D[k].filter(x => x.p !== id); });
      save(); log(who, 'حذف بروفايل'); return json(res, 200, { ok: 1 });
    }
    if (p === '/api/sessions/clear') { sessions = []; try { fs.writeFileSync(SESS, '[]'); } catch {} log(who, 'مسح سجل الجلسات'); return json(res, 200, { ok: 1 }); }
    if (p === '/api/update' || p === '/api/restore') {
      if (locked(I)) return json(res, 429, { error: 'محظور مؤقتاً' });
      const b = await bodyBig(req, 3e6);
      if (String(b.pin) !== PIN) { fail(I); log(who, 'محاولة تحديث بـ PIN خاطئ'); return json(res, 403, { error: 'PIN خطأ' }); }
      let code = '';
      if (p === '/api/update') code = String(b.code || '');
      else {
        const nm = String(b.name || '');
        if (!/^server-[\w.\-]+\.js$/.test(nm)) return json(res, 400, { error: 'اسم غير صالح' });
        try { code = fs.readFileSync(path.join(__dirname, 'backups', nm), 'utf8'); } catch { return json(res, 404, { error: 'النسخة غير موجودة' }); }
      }
      const chk = await verifyCode(code);
      if (!chk.ok) return json(res, 422, { error: chk.error });
      swapIn(chk.cand);
      log(who, (p === '/api/update' ? 'تحديث السيرفر إلى ' : 'استرجاع نسخة ') + chk.version);
      json(res, 200, { ok: 1, version: chk.version, from: VERSION });
      restartSelf();
      return;
    }
    if (p === '/api/viewkey/reset') {
      D.viewKey = crypto.randomBytes(9).toString('hex'); save(); log(who, 'تغيير رابط الشاشة الجانبية');
      return json(res, 200, { ok: 1 });
    }
    if (p === '/api/open') {
      const st = D.settings, d = new Date(), h = d.getHours(), day = d.toDateString();
      let ran = null;
      if (st.morningScene && st.morningLast !== day && h >= st.morningFrom && h < st.morningTo &&
          D.scenes.some(x => x.name === st.morningScene)) {
        st.morningLast = day; save(); ran = st.morningScene;
        log(who, 'مجموعة الصباح: ' + ran); runWhat('scene:' + ran);
      }
      return json(res, 200, { ran });
    }
    if (p === '/api/settings') {
      const b = await body(req), st = D.settings, bad = () => json(res, 400, { error: 'bad' });
      if (b.idleMin !== undefined) { const n = parseInt(ar2en(b.idleMin), 10); if (!(n >= 0 && n <= 1440)) return bad(); st.idleMin = n; }
      if (b.morningScene !== undefined) {
        if (b.morningScene === 'none') st.morningScene = '';
        else if (D.scenes.some(x => x.name === b.morningScene)) st.morningScene = b.morningScene;
        else return bad();
      }
      if (b.morningFrom !== undefined || b.morningTo !== undefined) {
        const f = parseInt(ar2en(b.morningFrom ?? st.morningFrom), 10), t = parseInt(ar2en(b.morningTo ?? st.morningTo), 10);
        if (!(f >= 0 && t <= 24 && f < t)) return bad();
        st.morningFrom = f; st.morningTo = t;
      }
      if (b.sessLog !== undefined) st.sessLog = !!b.sessLog;
      if (b.sessIgnore !== undefined) st.sessIgnore = String(b.sessIgnore).slice(0, 500);
      if (b.sessMin !== undefined) { const n = parseInt(ar2en(b.sessMin), 10); if (!(n >= 1 && n <= 3600)) return bad(); st.sessMin = n; }
      if (b.sessGap !== undefined) { const n = parseInt(ar2en(b.sessGap), 10); if (!(n >= 3 && n <= 600)) return bad(); st.sessGap = n; }
      if (b.obsPort !== undefined) { const n = parseInt(ar2en(b.obsPort), 10); if (!(n > 0 && n < 65536)) return bad(); st.obsPort = n; }
      if (b.obsMic !== undefined) st.obsMic = String(b.obsMic).slice(0, 80);
      if (b.obsPassword !== undefined && b.obsPassword !== '') st.obsPassword = b.obsPassword === '-' ? '' : String(b.obsPassword).slice(0, 100);
      if (b.obsPort !== undefined || b.obsPassword !== undefined) { try { if (obsWs) obsWs.close(); } catch {} obsReady = false; }
      save(); log(who, 'تعديل الإعدادات');
      return json(res, 200, { ok: 1 });
    }
    if (p === '/api/devdel') {
      const i = +q('i'), d = D.devices[i];
      if (!d) return json(res, 404, {});
      D.devices.splice(i, 1); save(); log(who, 'حذف جهاز: ' + d.name);
      if (d === dv) res.setHeader('Set-Cookie', 'dev=; Path=/; Max-Age=0');
      return json(res, 200, { ok: 1 });
    }
    if (p === '/api/sched') {
      const b = await body(req), w = String(b.what || '');
      const when = String(b.when || '').trim().replace(/[٠-٩]/g, d => '٠١٢٣٤٥٦٧٨٩'.indexOf(d));
      let s = null;
      if (/^\+\d+$/.test(when)) s = { kind: 'once', ts: Date.now() + Math.min(+when.slice(1), 10080) * 60000 };
      else {
        const m = /^(\d{1,2}):(\d{2})$/.exec(when);
        if (m && +m[1] < 24 && +m[2] < 60) s = { kind: 'daily', hm: ('0' + m[1]).slice(-2) + ':' + m[2] };
      }
      if (!s || !validWhat(w)) return json(res, 400, { error: 'bad' });
      s.id = crypto.randomBytes(4).toString('hex'); s.what = w; s.label = String(b.label || w).slice(0, 40);
      D.schedules.push(s); save(); log(who, 'جدولة: ' + s.label);
      return json(res, 200, { ok: 1 });
    }
    if (p === '/api/sdel') {
      D.schedules = D.schedules.filter(s => s.id !== q('id')); save();
      return json(res, 200, { ok: 1 });
    }
    if (p === '/api/setwol') {
      const b = await body(req);
      if (String(b.mac || '').replace(/[^0-9a-f]/gi, '').length !== 12) return json(res, 400, { error: 'mac' });
      D.wolMac = String(b.mac); save(); return json(res, 200, { ok: 1 });
    }
    if (p === '/api/wol') {
      if (!D.wolMac || !wol(D.wolMac)) return json(res, 400, {});
      log(who, 'Wake-on-LAN'); return json(res, 200, { ok: 1 });
    }
    if (p === '/api/forget') {
      D.devices = D.devices.filter(d => d !== dv); save(); log(I, 'إزالة جهاز: ' + dv.name);
      res.setHeader('Set-Cookie', 'dev=; Path=/; Max-Age=0');
      return json(res, 200, { ok: 1 });
    }
    return json(res, 404, {});
  } catch (e) {
    try { json(res, 500, { error: 'server' }); } catch {}
  }
});
srv.listen(PORT, '0.0.0.0', () => {
  console.log('Running on port ' + PORT);
  Object.values(os.networkInterfaces()).flat().filter(n => n.family === 'IPv4' && !n.internal)
    .forEach(n => console.log('  http://' + n.address + ':' + PORT));
  console.log('Shortcuts key: ' + D.key);
  console.log('To add another phone: open http://localhost:' + PORT + '/pair on this PC (or type  pair  here to keep pairing open until you type  unpair ).');
});
