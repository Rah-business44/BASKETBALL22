**<!DOCTYPE html>**

**<html lang="en">**

**<head>**

**<meta charset="UTF-8">**

**<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">**

**<title>Mobile Hoops</title>**

**<style>**

&#x20;   **:root {**

&#x20;       **--primary: #ff6b35;**

&#x20;       **--bg-top: #1a1a2e;**

&#x20;       **--bg-bottom: #16213e;**

&#x20;       **--text: #ffffff;**

&#x20;       **--rim: #e63946;**

&#x20;       **--backboard: #f1faee;**

&#x20;   **}**

&#x20;   

&#x20;   **\* { box-sizing: border-box; }**

&#x20;   

&#x20;   **body, html {**

&#x20;       **margin: 0; padding: 0;**

&#x20;       **width: 100%; height: 100%;**

&#x20;       **overflow: hidden;**

&#x20;       **background: linear-gradient(to bottom, var(--bg-top), var(--bg-bottom));**

&#x20;       **font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;**

&#x20;       **touch-action: none;** 

&#x20;       **user-select: none;**

&#x20;       **-webkit-user-select: none;**

&#x20;   **}**



&#x20;   **#gameCanvas {**

&#x20;       **display: block;**

&#x20;       **width: 100%; height: 100%;**

&#x20;       **box-shadow: inset 0 0 100px rgba(0,0,0,0.5);**

&#x20;   **}**



&#x20;   **#uiLayer {**

&#x20;       **position: absolute;**

&#x20;       **top: 0; left: 0;**

&#x20;       **width: 100%; height: 100%;**

&#x20;       **pointer-events: none;**

&#x20;       **display: flex;**

&#x20;       **flex-direction: column;**

&#x20;       **justify-content: space-between;**

&#x20;   **}**



&#x20;   **.hud {**

&#x20;       **padding: 20px;**

&#x20;       **display: flex;**

&#x20;       **justify-content: space-between;**

&#x20;       **background: linear-gradient(to bottom, rgba(0,0,0,0.6), transparent);**

&#x20;   **}**



&#x20;   **.stats { display: flex; flex-direction: column; }**

&#x20;   

&#x20;   **.stat-box {**

&#x20;       **background: rgba(255, 255, 255, 0.1);**

&#x20;       **backdrop-filter: blur(5px);**

&#x20;       **padding: 10px 15px;**

&#x20;       **border-radius: 12px;**

&#x20;       **border: 1px solid rgba(255, 255, 255, 0.2);**

&#x20;       **box-shadow: 0 4px 6px rgba(0,0,0,0.2);**

&#x20;   **}**



&#x20;   **.stat-label {**

&#x20;       **font-size: 0.8rem;**

&#x20;       **color: rgba(255,255,255,0.7);**

&#x20;       **letter-spacing: 1px;**

&#x20;       **text-transform: uppercase;**

&#x20;   **}**



&#x20;   **.stat-value {**

&#x20;       **font-size: 1.8rem;**

&#x20;       **font-weight: 900;**

&#x20;       **color: var(--text);**

&#x20;       **margin-top: -2px;**

&#x20;   **}**



&#x20;   **#feedback {**

&#x20;       **position: absolute;**

&#x20;       **top: 40%; left: 50%;**

&#x20;       **transform: translate(-50%, -50%) scale(0.5);**

&#x20;       **font-size: 4rem;**

&#x20;       **font-weight: 900;**

&#x20;       **color: #ffd166;**

&#x20;       **text-transform: uppercase;**

&#x20;       **text-shadow: 0px 4px 15px rgba(0,0,0,0.6), 0px 0px 20px rgba(255, 209, 102, 0.8);**

&#x20;       **opacity: 0;**

&#x20;       **transition: opacity 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275), transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);**

&#x20;       **pointer-events: none;**

&#x20;   **}**



&#x20;   **#feedback.show {**

&#x20;       **opacity: 1;**

&#x20;       **transform: translate(-50%, -50%) scale(1);**

&#x20;   **}**



&#x20;   **.controls {**

&#x20;       **padding: 20px;**

&#x20;       **display: flex;**

&#x20;       **justify-content: center;**

&#x20;       **margin-bottom: 20px;**

&#x20;   **}**



&#x20;   **#restartBtn {**

&#x20;       **pointer-events: auto;**

&#x20;       **padding: 15px 30px;**

&#x20;       **font-size: 1.2rem;**

&#x20;       **font-weight: bold;**

&#x20;       **color: white;**

&#x20;       **background: var(--primary);**

&#x20;       **border: none;**

&#x20;       **border-radius: 30px;**

&#x20;       **box-shadow: 0 6px 0 #cc4b20, 0 10px 20px rgba(0,0,0,0.4);**

&#x20;       **cursor: pointer;**

&#x20;       **transition: transform 0.1s, box-shadow 0.1s;**

&#x20;       **text-transform: uppercase;**

&#x20;       **letter-spacing: 1px;**

&#x20;   **}**



&#x20;   **#restartBtn:active {**

&#x20;       **transform: translateY(6px);**

&#x20;       **box-shadow: 0 0 0 #cc4b20, 0 4px 10px rgba(0,0,0,0.4);**

&#x20;   **}**

&#x20;   

&#x20;   **#instructions {**

&#x20;       **position: absolute;**

&#x20;       **bottom: 100px;**

&#x20;       **width: 100%;**

&#x20;       **text-align: center;**

&#x20;       **color: rgba(255,255,255,0.5);**

&#x20;       **font-size: 1.1rem;**

&#x20;       **pointer-events: none;**

&#x20;       **transition: opacity 0.5s;**

&#x20;   **}**

**</style>**

**</head>**

**<body>**



**<canvas id="gameCanvas"></canvas>**



**<div id="uiLayer">**

&#x20;   **<div class="hud">**

&#x20;       **<div class="stat-box">**

&#x20;           **<div class="stat-label">Score</div>**

&#x20;           **<div class="stat-value" id="scoreEl">0</div>**

&#x20;       **</div>**

&#x20;       **<div class="stat-box" style="text-align: right;">**

&#x20;           **<div class="stat-label">Accuracy</div>**

&#x20;           **<div class="stat-value"><span id="pctEl">0</span><span style="font-size:1rem">%</span></div>**

&#x20;           **<div class="stat-label" style="font-size:0.7rem"><span id="shotsEl">0</span> SHOTS</div>**

&#x20;       **</div>**

&#x20;   **</div>**

&#x20;   

&#x20;   **<div id="feedback">SWISH!</div>**

&#x20;   **<div id="instructions">Drag to aim, release to shoot</div>**

&#x20;   

&#x20;   **<div class="controls">**

&#x20;       **<button id="restartBtn">Reset Stats</button>**

&#x20;   **</div>**

**</div>**



**<script>**

**/\*\* \* Mobile Hoops - Physics \& Graphics Engine**

&#x20;**\*/**



**// --- DOM \& Setup ---**

**const canvas = document.getElementById('gameCanvas');**

**const ctx = canvas.getContext('2d');**

**let cw, ch;**



**// UI Elements**

**const scoreEl = document.getElementById('scoreEl');**

**const pctEl = document.getElementById('pctEl');**

**const shotsEl = document.getElementById('shotsEl');**

**const feedbackEl = document.getElementById('feedback');**

**const restartBtn = document.getElementById('restartBtn');**

**const instructionsEl = document.getElementById('instructions');**



**// --- Game State \& Constants ---**

**let score = 0;**

**let shots = 0;**

**let hasStarted = false;**

**let cameraShake = 0;**



**const GRAVITY = 0.45;**

**const FRICTION = 0.99;**

**const BOUNCE\_DAMPING = 0.75;**

**const RIM\_BOUNCE = 0.65;**

**const MAX\_DRAG\_DIST = 200;**

**const POWER\_MULTIPLIER = 0.16;**



**// --- Audio System (Web Audio API) ---**

**let audioCtx = null;**



**function initAudio() {**

&#x20;   **if (!audioCtx) {**

&#x20;       **audioCtx = new (window.AudioContext || window.webkitAudioContext)();**

&#x20;   **}**

&#x20;   **if (audioCtx.state === 'suspended') {**

&#x20;       **audioCtx.resume();**

&#x20;   **}**

**}**



**function playSound(type) {**

&#x20;   **if (!audioCtx) return;**

&#x20;   **const osc = audioCtx.createOscillator();**

&#x20;   **const gainNode = audioCtx.createGain();**

&#x20;   

&#x20;   **osc.connect(gainNode);**

&#x20;   **gainNode.connect(audioCtx.destination);**

&#x20;   

&#x20;   **const now = audioCtx.currentTime;**

&#x20;   

&#x20;   **if (type === 'bounce') {**

&#x20;       **osc.type = 'triangle';**

&#x20;       **osc.frequency.setValueAtTime(150, now);**

&#x20;       **osc.frequency.exponentialRampToValueAtTime(40, now + 0.1);**

&#x20;       **gainNode.gain.setValueAtTime(0.5, now);**

&#x20;       **gainNode.gain.exponentialRampToValueAtTime(0.01, now + 0.1);**

&#x20;       **osc.start(now);**

&#x20;       **osc.stop(now + 0.1);**

&#x20;   **} else if (type === 'rim') {**

&#x20;       **osc.type = 'sine';**

&#x20;       **osc.frequency.setValueAtTime(300, now);**

&#x20;       **osc.frequency.exponentialRampToValueAtTime(600, now + 0.05);**

&#x20;       **gainNode.gain.setValueAtTime(0.8, now);**

&#x20;       **gainNode.gain.exponentialRampToValueAtTime(0.01, now + 0.1);**

&#x20;       **osc.start(now);**

&#x20;       **osc.stop(now + 0.1);**

&#x20;   **} else if (type === 'score') {**

&#x20;       **osc.type = 'sine';**

&#x20;       **osc.frequency.setValueAtTime(400, now);**

&#x20;       **osc.frequency.exponentialRampToValueAtTime(800, now + 0.1);**

&#x20;       **osc.frequency.exponentialRampToValueAtTime(1200, now + 0.3);**

&#x20;       **gainNode.gain.setValueAtTime(0, now);**

&#x20;       **gainNode.gain.linearRampToValueAtTime(0.5, now + 0.05);**

&#x20;       **gainNode.gain.exponentialRampToValueAtTime(0.01, now + 0.4);**

&#x20;       **osc.start(now);**

&#x20;       **osc.stop(now + 0.4);**

&#x20;   **} else if (type === 'throw') {**

&#x20;       **// Noise burst for swoosh**

&#x20;       **const bufferSize = audioCtx.sampleRate \* 0.2;** 

&#x20;       **const buffer = audioCtx.createBuffer(1, bufferSize, audioCtx.sampleRate);**

&#x20;       **const data = buffer.getChannelData(0);**

&#x20;       **for (let i = 0; i < bufferSize; i++) {**

&#x20;           **data\[i] = Math.random() \* 2 - 1;**

&#x20;       **}**

&#x20;       **const noise = audioCtx.createBufferSource();**

&#x20;       **noise.buffer = buffer;**

&#x20;       **const filter = audioCtx.createBiquadFilter();**

&#x20;       **filter.type = 'lowpass';**

&#x20;       **filter.frequency.setValueAtTime(1000, now);**

&#x20;       **filter.frequency.linearRampToValueAtTime(100, now + 0.2);**

&#x20;       

&#x20;       **noise.connect(filter);**

&#x20;       **filter.connect(gainNode);**

&#x20;       

&#x20;       **gainNode.gain.setValueAtTime(0.3, now);**

&#x20;       **gainNode.gain.exponentialRampToValueAtTime(0.01, now + 0.2);**

&#x20;       

&#x20;       **noise.start(now);**

&#x20;   **}**

**}**



**// --- Entities ---**



**const hoop = {**

&#x20;   **x: 0, y: 0, width: 100, rimRadius: 5,**

&#x20;   **leftRim: {x: 0, y: 0},**

&#x20;   **rightRim: {x: 0, y: 0},**

&#x20;   **backboard: {x: 0, yTop: 0, yBot: 0, width: 10},**

&#x20;   **netPoints: \[]**

**};**



**const ball = {**

&#x20;   **x: 0, y: 0, vx: 0, vy: 0, radius: 25,**

&#x20;   **isDragging: false, isFlying: false, hasScored: false,**

&#x20;   **rotation: 0, vRot: 0,**

&#x20;   **startX: 0, startY: 0,**

&#x20;   **prevY: 0**

**};**



**const input = {**

&#x20;   **startX: 0, startY: 0,**

&#x20;   **currX: 0, currY: 0,**

&#x20;   **active: false**

**};**



**// --- Initialization \& Resizing ---**

**function resize() {**

&#x20;   **cw = canvas.width = window.innerWidth;**

&#x20;   **ch = canvas.height = window.innerHeight;**

&#x20;   

&#x20;   **// Position hoop based on screen size**

&#x20;   **hoop.x = cw / 2;**

&#x20;   **hoop.y = ch \* 0.3; // 30% down**

&#x20;   **hoop.width = Math.min(cw \* 0.35, 140);**

&#x20;   **hoop.rimRadius = hoop.width \* 0.05;**

&#x20;   

&#x20;   **hoop.leftRim.x = hoop.x - hoop.width / 2;**

&#x20;   **hoop.leftRim.y = hoop.y;**

&#x20;   **hoop.rightRim.x = hoop.x + hoop.width / 2;**

&#x20;   **hoop.rightRim.y = hoop.y;**

&#x20;   

&#x20;   **hoop.backboard.x = hoop.x + hoop.width / 2 + hoop.rimRadius \* 3;**

&#x20;   **hoop.backboard.yTop = hoop.y - hoop.width \* 0.8;**

&#x20;   **hoop.backboard.yBot = hoop.y + hoop.width \* 0.2;**

&#x20;   

&#x20;   **// Init net points (simple 3x3 grid simulation)**

&#x20;   **hoop.netPoints = \[];**

&#x20;   **for(let i=0; i<=4; i++) {**

&#x20;       **let px = hoop.leftRim.x + (hoop.width/4) \* i;**

&#x20;       **hoop.netPoints.push({ x: px, y: hoop.y, tx: px, ty: hoop.y + hoop.width\*0.8, vx: 0, vy: 0 });**

&#x20;   **}**



&#x20;   **if (!ball.isFlying \&\& !ball.isDragging) {**

&#x20;       **resetBall();**

&#x20;   **}**

**}**



**function resetBall() {**

&#x20;   **ball.radius = Math.min(cw \* 0.08, 35);**

&#x20;   **ball.x = cw / 2;**

&#x20;   **ball.y = ch - ball.radius - 120; // Above restart button**

&#x20;   **ball.startX = ball.x;**

&#x20;   **ball.startY = ball.y;**

&#x20;   **ball.vx = 0;**

&#x20;   **ball.vy = 0;**

&#x20;   **ball.vRot = 0;**

&#x20;   **ball.isFlying = false;**

&#x20;   **ball.isDragging = false;**

&#x20;   **ball.hasScored = false;**

**}**



**// --- Input Handling ---**

**function handleStart(x, y) {**

&#x20;   **initAudio();**

&#x20;   **if (instructionsEl.style.opacity !== '0') instructionsEl.style.opacity = '0';**

&#x20;   

&#x20;   **if (ball.isFlying) return;**

&#x20;   

&#x20;   **// Hitbox for ball grabbing (generous)**

&#x20;   **const dx = x - ball.x;**

&#x20;   **const dy = y - ball.y;**

&#x20;   **if (Math.sqrt(dx\*dx + dy\*dy) < ball.radius \* 3) {**

&#x20;       **input.active = true;**

&#x20;       **input.startX = x;**

&#x20;       **input.startY = y;**

&#x20;       **input.currX = x;**

&#x20;       **input.currY = y;**

&#x20;       **ball.isDragging = true;**

&#x20;   **}**

**}**



**function handleMove(x, y) {**

&#x20;   **if (!input.active) return;**

&#x20;   **input.currX = x;**

&#x20;   **input.currY = y;**

**}**



**function handleEnd() {**

&#x20;   **if (!input.active) return;**

&#x20;   **input.active = false;**

&#x20;   **ball.isDragging = false;**

&#x20;   

&#x20;   **const dx = input.startX - input.currX;**

&#x20;   **const dy = input.startY - input.currY;**

&#x20;   **const dist = Math.sqrt(dx\*dx + dy\*dy);**

&#x20;   

&#x20;   **if (dist > 10) {**

&#x20;       **// Launch**

&#x20;       **let pullDist = Math.min(dist, MAX\_DRAG\_DIST);**

&#x20;       **let angle = Math.atan2(dy, dx);**

&#x20;       

&#x20;       **ball.vx = Math.cos(angle) \* pullDist \* POWER\_MULTIPLIER;**

&#x20;       **ball.vy = Math.sin(angle) \* pullDist \* POWER\_MULTIPLIER;**

&#x20;       **ball.vRot = ball.vx \* 0.05;**

&#x20;       **ball.isFlying = true;**

&#x20;       **ball.prevY = ball.y;**

&#x20;       **shots++;**

&#x20;       **updateStats();**

&#x20;       **playSound('throw');**

&#x20;   **}**

**}**



**// Mouse**

**window.addEventListener('mousedown', e => handleStart(e.clientX, e.clientY));**

**window.addEventListener('mousemove', e => handleMove(e.clientX, e.clientY));**

**window.addEventListener('mouseup', handleEnd);**



**// Touch**

**window.addEventListener('touchstart', e => {**

&#x20;   **handleStart(e.touches\[0].clientX, e.touches\[0].clientY);**

**}, {passive: false});**

**window.addEventListener('touchmove', e => {**

&#x20;   **e.preventDefault(); // Prevent scrolling**

&#x20;   **handleMove(e.touches\[0].clientX, e.touches\[0].clientY);**

**}, {passive: false});**

**window.addEventListener('touchend', handleEnd);**



**restartBtn.addEventListener('click', () => {**

&#x20;   **score = 0;**

&#x20;   **shots = 0;**

&#x20;   **updateStats();**

&#x20;   **resetBall();**

&#x20;   **hasStarted = false;**

&#x20;   **instructionsEl.style.opacity = '1';**

**});**



**// --- Physics \& Logic ---**



**function resolveCircleCollision(ball, rimX, rimY, rimR) {**

&#x20;   **let dx = ball.x - rimX;**

&#x20;   **let dy = ball.y - rimY;**

&#x20;   **let dist = Math.sqrt(dx\*dx + dy\*dy);**

&#x20;   **let minDist = ball.radius + rimR;**



&#x20;   **if (dist < minDist) {**

&#x20;       **// Overlap resolution**

&#x20;       **let angle = Math.atan2(dy, dx);**

&#x20;       **let overlap = minDist - dist;**

&#x20;       **ball.x += Math.cos(angle) \* overlap;**

&#x20;       **ball.y += Math.sin(angle) \* overlap;**



&#x20;       **// Velocity bounce**

&#x20;       **let normalX = Math.cos(angle);**

&#x20;       **let normalY = Math.sin(angle);**

&#x20;       

&#x20;       **// Dot product**

&#x20;       **let dotProduct = ball.vx \* normalX + ball.vy \* normalY;**

&#x20;       

&#x20;       **ball.vx -= 2 \* dotProduct \* normalX;**

&#x20;       **ball.vy -= 2 \* dotProduct \* normalY;**

&#x20;       

&#x20;       **ball.vx \*= RIM\_BOUNCE;**

&#x20;       **ball.vy \*= RIM\_BOUNCE;**

&#x20;       

&#x20;       **ball.vRot -= normalX \* 0.2; // Spin on hit**

&#x20;       

&#x20;       **cameraShake = Math.max(cameraShake, 8);**

&#x20;       **playSound('rim');**

&#x20;       

&#x20;       **// Wiggle net**

&#x20;       **hoop.netPoints.forEach(p => p.vx += normalX \* 2);**

&#x20;   **}**

**}**



**function update() {**

&#x20;   **if (cameraShake > 0) cameraShake \*= 0.9;**

&#x20;   **if (cameraShake < 0.5) cameraShake = 0;**



&#x20;   **// Animate net**

&#x20;   **hoop.netPoints.forEach((p, i) => {**

&#x20;       **// Return to target**

&#x20;       **p.vx += (p.tx - p.x) \* 0.1;**

&#x20;       **p.vy += (p.ty - p.y) \* 0.1;**

&#x20;       **p.vx \*= 0.8;**

&#x20;       **p.vy \*= 0.8;**

&#x20;       **p.x += p.vx;**

&#x20;       **p.y += p.vy;**

&#x20;   **});**



&#x20;   **if (ball.isFlying) {**

&#x20;       **ball.prevY = ball.y;**

&#x20;       

&#x20;       **ball.vy += GRAVITY;**

&#x20;       **ball.vx \*= FRICTION;**

&#x20;       **ball.vy \*= FRICTION;**

&#x20;       

&#x20;       **ball.x += ball.vx;**

&#x20;       **ball.y += ball.vy;**

&#x20;       **ball.rotation += ball.vRot;**



&#x20;       **// Wall bounce**

&#x20;       **if (ball.x - ball.radius < 0) {**

&#x20;           **ball.x = ball.radius;**

&#x20;           **ball.vx = -ball.vx \* BOUNCE\_DAMPING;**

&#x20;           **playSound('bounce');**

&#x20;       **} else if (ball.x + ball.radius > cw) {**

&#x20;           **ball.x = cw - ball.radius;**

&#x20;           **ball.vx = -ball.vx \* BOUNCE\_DAMPING;**

&#x20;           **playSound('bounce');**

&#x20;       **}**



&#x20;       **// Floor bounce**

&#x20;       **if (ball.y + ball.radius > ch) {**

&#x20;           **ball.y = ch - ball.radius;**

&#x20;           **ball.vy = -ball.vy \* BOUNCE\_DAMPING;**

&#x20;           **ball.vx \*= 0.9; // Friction on floor**

&#x20;           **ball.vRot \*= 0.8;**

&#x20;           **if (Math.abs(ball.vy) > 2) playSound('bounce');**

&#x20;       **}**



&#x20;       **// Backboard collision (AABB mostly)**

&#x20;       **let bb = hoop.backboard;**

&#x20;       **if (ball.x + ball.radius > bb.x \&\& ball.x - ball.radius < bb.x + bb.width) {**

&#x20;           **if (ball.y > bb.yTop \&\& ball.y < bb.yBot) {**

&#x20;               **// Determine side**

&#x20;               **if (ball.vx > 0 \&\& ball.x < bb.x) {**

&#x20;                   **ball.x = bb.x - ball.radius;**

&#x20;                   **ball.vx = -ball.vx \* BOUNCE\_DAMPING;**

&#x20;                   **playSound('bounce');**

&#x20;                   **cameraShake = Math.max(cameraShake, 5);**

&#x20;               **}**

&#x20;           **}**

&#x20;       **}**



&#x20;       **// Rim collisions**

&#x20;       **resolveCircleCollision(ball, hoop.leftRim.x, hoop.leftRim.y, hoop.rimRadius);**

&#x20;       **resolveCircleCollision(ball, hoop.rightRim.x, hoop.rightRim.y, hoop.rimRadius);**



&#x20;       **// Scoring Detection**

&#x20;       **if (!ball.hasScored \&\& ball.vy > 0 \&\& ball.y > hoop.y \&\& ball.prevY <= hoop.y) {**

&#x20;           **// Crossed the hoop plane downwards**

&#x20;           **if (ball.x > hoop.leftRim.x \&\& ball.x < hoop.rightRim.x) {**

&#x20;               **score++;**

&#x20;               **ball.hasScored = true;**

&#x20;               **updateStats();**

&#x20;               **showFeedback();**

&#x20;               **playSound('score');**

&#x20;               

&#x20;               **// Animate net**

&#x20;               **hoop.netPoints.forEach(p => {**

&#x20;                   **p.vy += 15;**

&#x20;                   **p.vx += (cw/2 - p.x) \* 0.05; // Pull inward**

&#x20;               **});**

&#x20;           **}**

&#x20;       **}**



&#x20;       **// Auto reset if ball is dead or offscreen**

&#x20;       **if (ball.y > ch + 100 || (Math.abs(ball.vx) < 0.1 \&\& Math.abs(ball.vy) < 0.1 \&\& ball.y > ch - ball.radius - 10)) {**

&#x20;           **setTimeout(resetBall, 400); // Small delay before reset**

&#x20;           **ball.isFlying = false; // Prevent multiple timeouts**

&#x20;       **}**

&#x20;   **}**

**}**



**// --- Drawing ---**



**function drawCourt() {**

&#x20;   **// Floor area**

&#x20;   **ctx.fillStyle = '#db7a37'; // Hardwood color**

&#x20;   **ctx.fillRect(0, ch - 80, cw, 80);**

&#x20;   

&#x20;   **// Key**

&#x20;   **ctx.fillStyle = '#b65f29';**

&#x20;   **ctx.fillRect(cw/2 - 100, ch - 80, 200, 80);**

**}**



**function drawHoopBack() {**

&#x20;   **// Pole**

&#x20;   **ctx.fillStyle = '#444';**

&#x20;   **ctx.fillRect(hoop.backboard.x + 5, hoop.y, 20, ch);**

&#x20;   

&#x20;   **// Backboard**

&#x20;   **ctx.fillStyle = 'rgba(255,255,255,0.9)';**

&#x20;   **ctx.shadowColor = 'rgba(0,0,0,0.5)';**

&#x20;   **ctx.shadowBlur = 15;**

&#x20;   **ctx.fillRect(hoop.backboard.x, hoop.backboard.yTop, hoop.backboard.width, hoop.backboard.yBot - hoop.backboard.yTop);**

&#x20;   **ctx.shadowBlur = 0;**

&#x20;   

&#x20;   **// Backboard inner square**

&#x20;   **ctx.strokeStyle = varColor('--rim');**

&#x20;   **ctx.lineWidth = 4;**

&#x20;   **ctx.strokeRect(hoop.backboard.x + 2, hoop.y - hoop.width\*0.4, 6, hoop.width\*0.5);**

&#x20;   

&#x20;   **// Back Rim (drawn behind net)**

&#x20;   **ctx.beginPath();**

&#x20;   **ctx.ellipse(hoop.x, hoop.y, hoop.width/2, hoop.rimRadius\*1.5, 0, Math.PI, 0);**

&#x20;   **ctx.strokeStyle = varColor('--rim');**

&#x20;   **ctx.lineWidth = hoop.rimRadius \* 1.2;**

&#x20;   **ctx.stroke();**

**}**



**function drawNet() {**

&#x20;   **ctx.strokeStyle = '#fff';**

&#x20;   **ctx.lineWidth = 2;**

&#x20;   **ctx.lineCap = 'round';**

&#x20;   **ctx.lineJoin = 'round';**

&#x20;   

&#x20;   **ctx.beginPath();**

&#x20;   **// Vertical-ish lines**

&#x20;   **for(let i=0; i<hoop.netPoints.length; i++) {**

&#x20;       **let startX = hoop.leftRim.x + (hoop.width / (hoop.netPoints.length-1)) \* i;**

&#x20;       **ctx.moveTo(startX, hoop.y);**

&#x20;       **ctx.lineTo(hoop.netPoints\[i].x, hoop.netPoints\[i].y);**

&#x20;   **}**

&#x20;   

&#x20;   **// Horizontal zigzag**

&#x20;   **for(let j=1; j<=3; j++) {**

&#x20;       **ctx.moveTo(hoop.netPoints\[0].x, hoop.y + (hoop.width\*0.8/4)\*j);**

&#x20;       **for(let i=1; i<hoop.netPoints.length; i++) {**

&#x20;           **// Interpolate points**

&#x20;           **let px = hoop.netPoints\[i].x;**

&#x20;           **let py = hoop.y + ((hoop.netPoints\[i].y - hoop.y) / 3) \* j;**

&#x20;           **ctx.lineTo(px, py);**

&#x20;       **}**

&#x20;   **}**

&#x20;   **ctx.stroke();**

**}**



**function drawHoopFront() {**

&#x20;   **// Front Rim**

&#x20;   **ctx.beginPath();**

&#x20;   **ctx.ellipse(hoop.x, hoop.y, hoop.width/2, hoop.rimRadius\*1.5, 0, 0, Math.PI);**

&#x20;   **ctx.strokeStyle = varColor('--rim');**

&#x20;   **ctx.lineWidth = hoop.rimRadius \* 1.5;**

&#x20;   **ctx.stroke();**

&#x20;   

&#x20;   **// Rim highlight**

&#x20;   **ctx.beginPath();**

&#x20;   **ctx.ellipse(hoop.x, hoop.y-2, hoop.width/2, hoop.rimRadius\*0.8, 0, 0, Math.PI);**

&#x20;   **ctx.strokeStyle = '#ff7b85';**

&#x20;   **ctx.lineWidth = 1;**

&#x20;   **ctx.stroke();**



&#x20;   **// Rim nodes (connectors)**

&#x20;   **ctx.fillStyle = varColor('--rim');**

&#x20;   **ctx.beginPath(); ctx.arc(hoop.leftRim.x, hoop.leftRim.y, hoop.rimRadius, 0, Math.PI\*2); ctx.fill();**

&#x20;   **ctx.beginPath(); ctx.arc(hoop.rightRim.x, hoop.rightRim.y, hoop.rimRadius, 0, Math.PI\*2); ctx.fill();**

**}**



**function drawBall() {**

&#x20;   **ctx.save();**

&#x20;   **ctx.translate(ball.x, ball.y);**

&#x20;   **ctx.rotate(ball.rotation);**



&#x20;   **// Ball shadow**

&#x20;   **ctx.shadowColor = 'rgba(0,0,0,0.6)';**

&#x20;   **ctx.shadowBlur = 10;**

&#x20;   **ctx.shadowOffsetX = -5;**

&#x20;   **ctx.shadowOffsetY = 10;**



&#x20;   **// Base color**

&#x20;   **ctx.fillStyle = '#ff6b35';**

&#x20;   **ctx.beginPath();**

&#x20;   **ctx.arc(0, 0, ball.radius, 0, Math.PI\*2);**

&#x20;   **ctx.fill();**

&#x20;   

&#x20;   **ctx.shadowColor = 'transparent'; // Turn off shadow for details**

&#x20;   

&#x20;   **// Lighting gradient**

&#x20;   **let grad = ctx.createRadialGradient(-ball.radius/3, -ball.radius/3, ball.radius/10, 0, 0, ball.radius);**

&#x20;   **grad.addColorStop(0, 'rgba(255,255,255,0.3)');**

&#x20;   **grad.addColorStop(1, 'rgba(0,0,0,0.4)');**

&#x20;   **ctx.fillStyle = grad;**

&#x20;   **ctx.fill();**



&#x20;   **// Lines**

&#x20;   **ctx.strokeStyle = '#222';**

&#x20;   **ctx.lineWidth = ball.radius \* 0.08;**

&#x20;   **ctx.lineCap = 'round';**

&#x20;   

&#x20;   **ctx.beginPath(); ctx.moveTo(-ball.radius, 0); ctx.lineTo(ball.radius, 0); ctx.stroke(); // Horizontal**

&#x20;   **ctx.beginPath(); ctx.moveTo(0, -ball.radius); ctx.lineTo(0, ball.radius); ctx.stroke(); // Vertical**

&#x20;   

&#x20;   **// Curves**

&#x20;   **ctx.beginPath(); ctx.arc(-ball.radius, 0, ball.radius\*0.7, -Math.PI/2, Math.PI/2); ctx.stroke();**

&#x20;   **ctx.beginPath(); ctx.arc(ball.radius, 0, ball.radius\*0.7, Math.PI/2, Math.PI\*1.5); ctx.stroke();**



&#x20;   **ctx.restore();**

**}**



**function drawAimGuide() {**

&#x20;   **if (!ball.isDragging) return;**

&#x20;   

&#x20;   **const dx = input.startX - input.currX;**

&#x20;   **const dy = input.startY - input.currY;**

&#x20;   **const dist = Math.sqrt(dx\*dx + dy\*dy);**

&#x20;   

&#x20;   **if (dist < 10) return;**

&#x20;   

&#x20;   **let pullDist = Math.min(dist, MAX\_DRAG\_DIST);**

&#x20;   **let angle = Math.atan2(dy, dx);**

&#x20;   

&#x20;   **let pvx = Math.cos(angle) \* pullDist \* POWER\_MULTIPLIER;**

&#x20;   **let pvy = Math.sin(angle) \* pullDist \* POWER\_MULTIPLIER;**

&#x20;   

&#x20;   **ctx.beginPath();**

&#x20;   **ctx.setLineDash(\[8, 12]);**

&#x20;   **ctx.strokeStyle = 'rgba(255, 255, 255, 0.4)';**

&#x20;   **ctx.lineWidth = 3;**

&#x20;   

&#x20;   **let px = ball.x;**

&#x20;   **let py = ball.y;**

&#x20;   

&#x20;   **ctx.moveTo(px, py);**

&#x20;   **// Simulate trajectory**

&#x20;   **for(let i=0; i<30; i++) {**

&#x20;       **pvy += GRAVITY;**

&#x20;       **px += pvx;**

&#x20;       **py += pvy;**

&#x20;       **if(i % 2 === 0) ctx.lineTo(px, py); // Add point every other step for dashes**

&#x20;       **if(py > ch || px < 0 || px > cw) break;**

&#x20;   **}**

&#x20;   

&#x20;   **ctx.stroke();**

&#x20;   **ctx.setLineDash(\[]);**

**}**



**function draw() {**

&#x20;   **ctx.clearRect(0, 0, cw, ch);**

&#x20;   

&#x20;   **ctx.save();**

&#x20;   **if (cameraShake > 0) {**

&#x20;       **ctx.translate((Math.random()-0.5)\*cameraShake, (Math.random()-0.5)\*cameraShake);**

&#x20;   **}**

&#x20;   

&#x20;   **drawCourt();**

&#x20;   **drawHoopBack();**

&#x20;   

&#x20;   **// Draw ball behind front rim but in front of backboard/net based on Y \& vy**

&#x20;   **if (ball.y < hoop.y || ball.vy < 0) {**

&#x20;       **drawBall();**

&#x20;       **drawNet();**

&#x20;       **drawHoopFront();**

&#x20;   **} else {**

&#x20;       **drawNet();**

&#x20;       **drawHoopFront();**

&#x20;       **drawBall();**

&#x20;   **}**

&#x20;   

&#x20;   **drawAimGuide();**

&#x20;   

&#x20;   **ctx.restore();**

**}**



**function loop() {**

&#x20;   **update();**

&#x20;   **draw();**

&#x20;   **requestAnimationFrame(loop);**

**}**



**// --- UI Logic ---**

**function updateStats() {**

&#x20;   **scoreEl.innerText = score;**

&#x20;   **shotsEl.innerText = shots;**

&#x20;   **let pct = shots === 0 ? 0 : Math.round((score / shots) \* 100);**

&#x20;   **pctEl.innerText = pct;**

**}**



**function showFeedback() {**

&#x20;   **feedbackEl.innerText = \['SWISH!', 'NICE!', 'PERFECT!', 'SCORE!']\[Math.floor(Math.random() \* 4)];**

&#x20;   **feedbackEl.classList.add('show');**

&#x20;   **setTimeout(() => {**

&#x20;       **feedbackEl.classList.remove('show');**

&#x20;   **}, 1000);**

**}**



**function varColor(name) {**

&#x20;   **return getComputedStyle(document.documentElement).getPropertyValue(name).trim();**

**}**



**// Boot**

**window.addEventListener('resize', resize);**

**resize();**

**loop();**



**</script>**

**</body>**

**</html>**

