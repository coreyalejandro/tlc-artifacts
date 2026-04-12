# I'm Just A Build!

## ✅ OPTION 1: Complete 5-Part Script Set

**Files to save and run in order:**

### **setup-part-1.sh** (Core files)
```bash
#!/bin/bash
set -e
echo "🎬 Part 1: Core Setup..."
mkdir -p im-just-a-build/src/{characters,components,scenes,lib}
mkdir -p im-just-a-build/scripts
mkdir -p im-just-a-build/{public,verification,dist}
cd im-just-a-build

cat > package.json << 'EOF'
{"name":"im-just-a-build","version":"1.0.0","scripts":{"dev":"remotion studio","render":"remotion render src/index.tsx ImJustABuild dist/im-just-a-build.mp4"},"dependencies":{"@remotion/cli":"^4.0.0","react":"^18.0.0","react-dom":"^18.0.0","remotion":"^4.0.0"},"devDependencies":{"@types/react":"^18.0.26","typescript":"^5.1.3"}}
EOF

cat > tsconfig.json << 'EOF'
{"compilerOptions":{"target":"ES2020","module":"commonjs","jsx":"react-jsx","strict":true,"noEmit":true,"esModuleInterop":true,"skipLibCheck":true,"lib":["es2020","dom","dom.iterable"]},"include":["src"]}
EOF

cat > remotion.config.ts << 'EOF'
import{Config}from'@remotion/cli/config';Config.setVideoImageFormat('jpeg');Config.setOverwriteOutput(true);
EOF

cat > src/lib/colors.ts << 'EOF'
export const Colors={midnightBase:'#0D0221',burgundyPower:'#4A0E0E',burntOrange:'#CC5500',oliveGold:'#B5A642',cyanDigital:'#00CED1',creamPaper:'#F5F5DC',deepPurple:'#1A0A2E',goldBright:'#FFD700',shadowBlack:'#0A0A0A',highlightWhite:'#FFF8DC',stepUncertainty:'#4A4A4A',stepRegulation:'#8B7355',stepProof:'#D4AF37',stepLegitimacy:'#FFD700',guardianArchitect:'#9B59B6',guardianAuditor:'#3498DB',guardianAdvocate:'#E74C3C',guardianCustodian:'#27AE60',guardianWitness:'#F39C12',guardianScribe:'#ECF0F1',guardianSentinel:'#34495E',guardianCounsel:'#16A085',guardianChronicler:'#D35400',guardianSeal:'#FFD700'}as const;export const Timing={fps:12,duration:720,bpm:84,framesPerBeat:7,act1End:180,act2End:360,act3End:540,act4End:720};
EOF

cat > src/lib/deterministic.ts << 'EOF'
export const createSeededRandom=(seed:number)=>()=>{let t=seed+=0x6D2B79F5;t=Math.imul(t^(t>>>15),t|1);t^=t+Math.imul(t^(t>>>7),t|61);return((t^(t>>>14))>>>0)/4294967296};export const seededRandom=(frame:number,seed:number=0):number=>createSeededRandom(frame+seed*10000)();export const interpolate=(value:number,inputRange:[number,number],outputRange:[number,number],extrapolate:'clamp'|'extend'='clamp'):number=>{const[inMin,inMax]=inputRange;const[outMin,outMax]=outputRange;let result=(value-inMin)*(outMax-outMin)/(inMax-inMin)+outMin;if(extrapolate==='clamp'){result=Math.max(outMin,Math.min(outMax,result))}return result};export const Easing={linear:(t:number)=>t,easeIn:(t:number)=>t*t,easeOut:(t:number)=>1-(1-t)*(1-t),easeInOut:(t:number)=>t<0.5?2*t*t:1-Math.pow(-2*t+2,2)/2};export const swaggerWalk=(frame:number,startFrame:number,duration:number,intensity:number=1)=>{const progress=(frame-startFrame)/duration;if(progress<0||progress>1)return{x:0,y:0,rotation:0,bounce:0};const sway=Math.sin(progress*Math.PI*4)*5*intensity;const bounce=Math.abs(Math.sin(progress*Math.PI*4))*8*intensity;const rotation=Math.sin(progress*Math.PI*2)*3*intensity;const x=progress*100;return{x,y:-bounce,rotation,bounce}};export const generateSpeedLines=(frame:number,centerX:number,centerY:number,count:number=20)=>{const lines=[];const rand=seededRandom(frame);for(let i=0;i<count;i++){const angle=(i/count)*Math.PI*2+rand*0.5;const length=50+seededRandom(frame+i)*100;lines.push({x1:centerX+Math.cos(angle)*30,y1:centerY+Math.sin(angle)*30,x2:centerX+Math.cos(angle)*length,y2:centerY+Math.sin(angle)*length,opacity:0.3+seededRandom(frame+i+100)*0.5})}return lines};
EOF

echo "✅ Part 1 complete"
```

### **setup-part-2.sh** (Characters)
```bash
#!/bin/bash
cd im-just-a-build 2>/dev/null || cd ~/im-just-a-build

cat > src/characters/Build.tsx << 'EOF'
import React from'react';import{interpolate,swaggerWalk}from'../lib/deterministic';import{Colors}from'../lib/colors';interface B{frame:number;x?;y?;scale?;rotation?;state?;intensity?}export const Build:React.FC<B>=({frame,x=540,y=540,scale=1,rotation=0,state='idle',intensity=1})=>{const breathe=Math.sin(frame*0.1)*2*intensity;const swagger=state==='walking'?swaggerWalk(frame,0,60,intensity):null;const blink=frame%120<3?0.1:1;const eyeSquint=0.8+Math.sin(frame*0.05)*0.1;const unrollProgress=state==='presenting'?interpolate(frame,[0,30],[0,1],'clamp'):state==='unrolled'?1:0;const glowIntensity=state==='validated'?0.5+Math.sin(frame*0.2)*0.3:0;const transformX=swagger?swagger.x:0;const transformY=swagger?swagger.y+breathe:breathe;const swaggerRotation=swagger?swagger.rotation:0;return(<g transform={`translate(${x+transformX},${y+transformY})rotate(${rotation+swaggerRotation})scale(${scale})`}style={{filter:glowIntensity>0?`drop-shadow(0 0 ${20+glowIntensity*30}px ${Colors.goldBright})`:'none'}}><ellipse cx="0"cy="85"rx="40"ry="10"fill={Colors.shadowBlack}opacity={0.4}/><g transform={`translate(-25,60)rotate(${swagger?Math.sin(frame*0.3)*10:0})`}><rect x="-12"y="0"width="24"height="25"fill="#8B4513"rx="3"/><rect x="-14"y="20"width="28"height="10"fill={Colors.shadowBlack}rx="2"/></g><g transform={`translate(25,60)rotate(${swagger?-Math.sin(frame*0.3)*10:0})`}><rect x="-12"y="0"width="24"height="25"fill="#8B4513"rx="3"/><rect x="-14"y="20"width="28"height="10"fill={Colors.shadowBlack}rx="2"/></g><g transform={`scale(${1+unrollProgress*0.3},1)`}><rect x="-30"y="-60"width="60"height="120"rx="5"fill={Colors.creamPaper}stroke={Colors.shadowBlack}strokeWidth="2"/><g opacity="0.3">{[...Array(6)].map((_,i)=><line key={`h-${i}`}x1="-25"y1={-50+i*20}x2="25"y2={-50+i*20}stroke={Colors.cyanDigital}strokeWidth="0.5"/>)}{[...Array(3)].map((_,i)=><line key={`v-${i}`}x1={-20+i*20}y1="-55"x2={-20+i*20}y2="55"stroke={Colors.cyanDigital}strokeWidth="0.5"/>)}</g><text x="-28"y="-20"fontSize="8"fill={Colors.burgundyPower}fontFamily="cursive"transform="rotate(-90,-28,-20)"opacity="0.7">C-RSP</text>{state==='validated'&&<circle cx="0"cy="40"r="12"fill={Colors.goldBright}stroke={Colors.oliveGold}strokeWidth="2"/>}<g transform="translate(0,-70)rotate(-15)"><ellipse cx="0"cy="0"rx="35"ry="12"fill={Colors.burntOrange}/><path d="M-30 0Q0-25 30 0"fill={Colors.burntOrange}stroke={Colors.shadowBlack}strokeWidth="1"/><rect x="-8"y="-15"width="16"height="15"fill={Colors.burntOrange}rx="3"/></g></g><g transform={`translate(0,-20)scale(${eyeSquint},${blink})`}><g transform="translate(-12,0)"><ellipse cx="0"cy="0"rx="8"ry="6"fill={Colors.creamPaper}stroke={Colors.shadowBlack}strokeWidth="1.5"/><circle cx="2"cy="0"r="3"fill={Colors.shadowBlack}/><circle cx="3"cy="-1"r="1"fill="white"/><path d="M-8-2Q0-8 8-2"fill="none"stroke={Colors.shadowBlack}strokeWidth="2"strokeLinecap="round"/></g><g transform="translate(12,0)"><ellipse cx="0"cy="0"rx="8"ry="6"fill={Colors.creamPaper}stroke={Colors.shadowBlack}strokeWidth="1.5"/><circle cx="-2"cy="0"r="3"fill={Colors.shadowBlack}/><circle cx="-1"cy="-1"r="1"fill="white"/><path d="M-8-2Q0-8 8-2"fill="none"stroke={Colors.shadowBlack}strokeWidth="2"strokeLinecap="round"/></g><path d="M-18-8L-6-6"stroke={Colors.shadowBlack}strokeWidth="2.5"strokeLinecap="round"/><path d="M18-8L6-6"stroke={Colors.shadowBlack}strokeWidth="2.5"strokeLinecap="round"/></g><path d={state==='walking'||state==='validated'?"M-8 15Q0 20 10 12":"M-5 18Q0 15 5 18"}fill="none"stroke={Colors.shadowBlack}strokeWidth="2"strokeLinecap="round"/><g><path d={state==='presenting'?"M-30-20Q-50-10-45 20":"M-30-20Q-45 0-40 30"}fill="none"stroke={Colors.creamPaper}strokeWidth="8"strokeLinecap="round"/><path d={state==='presenting'?"M-30-20Q-50-10-45 20":"M-30-20Q-45 0-40 30"}fill="none"stroke={Colors.shadowBlack}strokeWidth="2"strokeLinecap="round"/><path d={state==='presenting'||state==='validated'?"M30-20Q50-30 55-10":"M30-20Q45 0 40 30"}fill="none"stroke={Colors.creamPaper}strokeWidth="8"strokeLinecap="round"/><path d={state==='presenting'||state==='validated'?"M30-20Q50-30 55-10":"M30-20Q45 0 40 30"}fill="none"stroke={Colors.shadowBlack}strokeWidth="2"strokeLinecap="round"/></g>{state==='validated'&&<g><path d="M-20-50Q0-30 20-50"fill="none"stroke={Colors.goldBright}strokeWidth="3"/><circle cx="0"cy="-35"r="5"fill={Colors.goldBright}stroke={Colors.oliveGold}strokeWidth="1"/><text x="0"y="-33"textAnchor="middle"fontSize="4"fill={Colors.shadowBlack}fontFamily="monospace">GIT</text></g>}</g>)};
EOF

cat > src/characters/Guardians.tsx << 'EOF'
import React from'react';import{interpolate}from'../lib/deterministic';import{Colors}from'../lib/colors';const GUARDIANS=[{id:1,name:'Architect',color:Colors.guardianArchitect,symbol:'◈',x:-400,y:0},{id:2,name:'Auditor',color:Colors.guardianAuditor,symbol:'⊕',x:-300,y:-100},{id:3,name:'Advocate',color:Colors.guardianAdvocate,symbol:'⚖',x:-150,y:-150},{id:4,name:'Custodian',color:Colors.guardianCustodian,symbol:'⚘',x:0,y:-200},{id:5,name:'Witness',color:Colors.guardianWitness,symbol:'◉',x:150,y:-150},{id:6,name:'Scribe',color:Colors.guardianScribe,symbol:'✍',x:300,y:-100},{id:7,name:'Sentinel',color:Colors.guardianSentinel,symbol:'⛨',x:400,y:0},{id:8,name:'Counsel',color:Colors.guardianCounsel,symbol:'☯',x:300,y:100},{id:9,name:'Chronicler',color:Colors.guardianChronicler,symbol:'◷',x:150,y:150},{id:10,name:'Seal',color:Colors.guardianSeal,symbol:'✦',x:0,y:0}];interface G{frame:number;centerX?;centerY?;activatedGuardians?;allActivated?;intensity?}export const Guardians:React.FC<G>=({frame,centerX=540,centerY=300,activatedGuardians=[],allActivated=false,intensity=1})=>(<g transform={`translate(${centerX},${centerY})`}>{GUARDIANS.map((guardian,index)=>{const isActivated=activatedGuardians.includes(guardian.id)||allActivated;const activationDelay=index*5;const activationProgress=isActivated?interpolate(frame-activationDelay,[0,20],[0,1],'clamp'):0;const glowRadius=activationProgress*30*intensity;const opacity=0.3+activationProgress*0.7;const floatY=Math.sin((frame+index*10)*0.05)*5;return(<g key={guardian.id}transform={`translate(${guardian.x},${guardian.y+floatY})`}opacity={opacity}>{activationProgress>0&&<circle cx="0"cy="0"r={60+glowRadius}fill={guardian.color}opacity={activationProgress*0.2}style={{filter:`blur(${20+activationProgress*10}px)`}}/>}<g transform={`scale(${0.8+activationProgress*0.2})`}><path d={guardian.id===10?"M-40 80L-30-20L0-60L30-20L40 80Z":"M-25 60L-20-10L0-40L20-10L25 60Z"}fill={guardian.color}stroke={Colors.highlightWhite}strokeWidth={isActivated?3:1}/><ellipse cx="0"cy={guardian.id===10?-40:-30}rx={guardian.id===10?25:18}ry={guardian.id===10?30:22}fill={guardian.color}stroke={Colors.highlightWhite}strokeWidth={isActivated?2:1}/>{isActivated&&<><ellipse cx={guardian.id===10?-10:-7}cy={guardian.id===10?-35:-25}rx="6"ry="8"fill={Colors.highlightWhite}/><ellipse cx={guardian.id===10?10:7}cy={guardian.id===10?-35:-25}rx="6"ry="8"fill={Colors.highlightWhite}/></>}<text x="0"y={guardian.id===10?20:15}textAnchor="middle"fontSize={guardian.id===10?40:30}fill={isActivated?Colors.goldBright:Colors.highlightWhite}fontFamily="serif"fontWeight="bold">{guardian.symbol}</text><text x="0"y={guardian.id===10?100:80}textAnchor="middle"fontSize="12"fill={Colors.highlightWhite}fontFamily="sans-serif"letterSpacing="2"opacity={activationProgress}>{guardian.name.toUpperCase()}</text></g><rect x={guardian.id===10?-50:-35}y="80"width={guardian.id===10?100:70}height="200"fill="#3A3A3A"stroke={guardian.color}strokeWidth={isActivated?4:2}opacity={0.8}/></g>)})}</g>);
EOF

echo "✅ Part 2 complete"
```

### **setup-part-3.sh** (Components)
```bash
#!/bin/bash
cd im-just-a-build 2>/dev/null || cd ~/im-just-a-build

cat > src/components/Steps.tsx << 'EOF'
import React from'react';import{interpolate,seededRandom}from'../lib/deterministic';import{Colors}from'../lib/colors';interface S{frame:number;progress:number;showCrack?;intensity?}export const Steps:React.FC<S>=({frame,progress,showCrack=false,intensity=1})=>{const steps=[{level:0,label:'UNCERTAINTY',color:Colors.stepUncertainty,glitch:true},{level:1,label:'UNCERTAINTY',color:Colors.stepUncertainty,glitch:true},{level:2,label:'UNCERTAINTY',color:Colors.stepUncertainty,glitch:true},{level:3,label:'REGULATION',color:Colors.stepRegulation,glitch:false},{level:4,label:'REGULATION',color:Colors.stepRegulation,glitch:false},{level:5,label:'REGULATION',color:Colors.stepRegulation,glitch:false},{level:6,label:'PROOF',color:Colors.stepProof,glitch:false},{level:7,label:'PROOF',color:Colors.stepProof,glitch:false},{level:8,label:'PROOF',color:Colors.stepProof,glitch:false},{level:9,label:'LEGITIMACY',color:Colors.stepLegitimacy,glitch:false}];return(<g transform="translate(540,800)">{steps.map((step,index)=>{const stepProgress=(progress*10)-index;const isActive=stepProgress>0;const isCurrent=stepProgress>0&&stepProgress<=1;const glitchOffset=step.glitch&&isActive?(seededRandom(frame+index)-0.5)*5*intensity:0;const glowOpacity=isActive?0.3+(stepProgress%1)*0.4:0.1;const showStepCrack=showCrack&&index===6&&isActive;return(<g key={index}transform={`translate(${glitchOffset},${-index*25})`}><rect x={-200-index*20}y="0"width={400+index*40}height="20"fill={isActive?step.color:Colors.stepUncertainty}stroke={isActive?Colors.highlightWhite:Colors.shadowBlack}strokeWidth={isCurrent?3:1}opacity={0.9}/>{step.glitch&&isActive&&<g opacity={0.3}><rect x={-200-index*20+(seededRandom(frame)-0.5)*10}y="2"width="50"height="4"fill={Colors.cyanDigital}/><rect x={(seededRandom(frame+1)-0.5)*100}y="10"width="30"height="3"fill={Colors.burgundyPower}/></g>}{isActive&&<rect x={-200-index*20}y="-2"width={400+index*40}height="24"fill={step.color}opacity={glowOpacity}style={{filter:'blur(8px)'}}/>}{showStepCrack&&<path d="M-50 0L-30 10L-10 5L10 15L30 8"fill="none"stroke={Colors.shadowBlack}strokeWidth="2"/>}{isActive&&stepProgress>0.5&&<text x="0"y="-5"textAnchor="middle"fontSize="10"fill={Colors.highlightWhite}fontFamily="sans-serif"letterSpacing="3"opacity={Math.min(1,stepProgress-0.5)}>{step.label}</text>}</g>})}<g transform="translate(0,-250)"><ellipse cx="0"cy="0"rx="300"ry="60"fill={Colors.stepLegitimacy}stroke={Colors.goldBright}strokeWidth="4"opacity={progress>=1?1:0.3}/><ellipse cx="0"cy="0"rx="280"ry="50"fill="none"stroke={Colors.highlightWhite}strokeWidth="2"opacity={progress>=1?0.8:0.2}strokeDasharray="10 5"/></g></g>)};
EOF

cat > src/components/Effects.tsx << 'EOF'
import React from'react';import{seededRandom,generateSpeedLines}from'../lib/deterministic';import{Colors}from'../lib/colors';export const SpeedLines:React.FC<{frame:number;centerX:number;centerY:number;intensity?;count?}>=({frame,centerX,centerY,intensity=1,count=30})=>{const lines=generateSpeedLines(frame,centerX,centerY,count);return(<g opacity={0.6*intensity}>{lines.map((line,i)=><line key={i}x1={line.x1}y1={line.y1}x2={line.x2}y2={line.y2}stroke={Colors.highlightWhite}strokeWidth={1+seededRandom(frame+i)*2}opacity={line.opacity*intensity}/>)}</g>)};export const GraffitiTitle:React.FC<{frame:number;text:string;subtext?;x?;y?;revealProgress?}>=({frame,text,subtext,x=540,y=540,revealProgress=1})=>{const chars=text.split('');const revealedChars=Math.floor(chars.length*revealProgress);return(<g transform={`translate(${x},${y})`}><ellipse cx="0"cy="10"rx={text.length*25*revealProgress}ry="60"fill={Colors.burgundyPower}opacity={0.3}style={{filter:'blur(20px)'}}/><text x="0"y="0"textAnchor="middle"fontSize="80"fill={Colors.creamPaper}fontFamily="Impact,sans-serif"fontWeight="900"letterSpacing="8"stroke={Colors.shadowBlack}strokeWidth="3">{chars.map((char,i)=><tspan key={i}opacity={i<revealedChars?1:0}fill={i<revealedChars?Colors.creamPaper:'transparent'}>{char}</tspan>)}</text><text x="0"y="0"textAnchor="middle"fontSize="80"fill="none"stroke={Colors.burntOrange}strokeWidth="1"strokeDasharray="5 5"opacity={0.5}fontFamily="Impact,sans-serif"fontWeight="900"letterSpacing="8">{text}</text>{subtext&&<text x="0"y="50"textAnchor="middle"fontSize="24"fill={Colors.oliveGold}fontFamily="cursive"letterSpacing="4"opacity={revealProgress}>{subtext}</text>}</g>)};
EOF

echo "✅ Part 3 complete"
```

### **setup-part-4.sh** (Scenes)
```bash
#!/bin/bash
cd im-just-a-build 2>/dev/null || cd ~/im-just-a-build

cat > src/scenes/Act1Concept.tsx << 'EOF'
import React from'react';import{interpolate}from'../lib/deterministic';import{Colors,Timing}from'../lib/colors';import{Build}from'../characters/Build';import{GraffitiTitle}from'../components/Effects';export const Act1Concept:React.FC<{frame:number}>=({frame})=>{const progress=frame/Timing.act1End;const titleProgress=interpolate(frame,[0,60],[0,1],'clamp');const buildEntrance=interpolate(frame,[60,120],[0,1],'clamp');const buildY=800-buildEntrance*300;const buildScale=0.5+buildEntrance*0.5;const devEntrance=interpolate(frame,[90,150],[0,1],'clamp');const devX=1200-devEntrance*500;const interaction=interpolate(frame,[120,180],[0,1],'clamp');return(<g><rect x="0"y="0"width="1080"height="1080"fill={Colors.midnightBase}/>{frame<80&&<GraffitiTitle frame={frame}text="I'M JUST A BUILD"subtext="A Constitutional Remix"x={540}y={400}revealProgress={titleProgress}/>}<rect x="100"y="600"width="880"height="40"fill="#444"stroke="#222"strokeWidth="2"/><line x1="100"y1="610"x2="980"y2="610"stroke="#666"strokeWidth="1"/>{frame>=60&&<Build frame={frame}x={400}y={buildY}scale={buildScale}state={interaction>0.5?'presenting':'idle'}intensity={1}/>}{frame>=90&&<g transform={`translate(${devX},580)`}opacity={devEntrance}><ellipse cx="0"cy="40"rx="30"ry="50"fill="#4A90E2"/><circle cx="0"cy="-10"r="25"fill="#8B4513"/><path d="M-30 20Q0 60 30 20L30 80L-30 80Z"fill="#2C3E50"/><circle cx="-8"cy="-15"r="3"fill="white"/><circle cx="8"cy="-15"r="3"fill="white"/><circle cx="-8"cy="-15"r="1.5"fill="black"/><circle cx="8"cy="-15"r="1.5"fill="black"/><text x="40"y="-30"fontSize="40"fill={Colors.goldBright}fontFamily="serif">?</text></g>}{frame>=120&&<g transform="translate(540,1000)"opacity={interaction}><text x="0"y="0"textAnchor="middle"fontSize="28"fill={Colors.creamPaper}fontFamily="cursive">"I'm just a build, yes I'm only a build..."</text></g>}</g>)};
EOF

cat > src/scenes/Act2Mechanism.tsx << 'EOF'
import React from'react';import{interpolate}from'../lib/deterministic';import{Colors,Timing}from'../lib/colors';import{Build}from'../characters/Build';import{Steps}from'../components/Steps';import{SpeedLines}from'../components/Effects';export const Act2Mechanism:React.FC<{frame:number}>=({frame})=>{const localFrame=frame-Timing.act1End;const progress=localFrame/(Timing.act2End-Timing.act1End);const climbProgress=interpolate(localFrame,[0,160],[0,1],'clamp');const currentStep=Math.floor(climbProgress*10);const buildX=540;const buildY=750-climbProgress*500;const ownsItMoment=localFrame>=60&&localFrame<=90;const ownsItIntensity=ownsItMoment?interpolate(localFrame,[60,75,90],[0,1,0],'clamp'):0;const shakeX=ownsItIntensity*(Math.sin(localFrame*0.8)*5);const shakeY=ownsItIntensity*(Math.cos(localFrame*0.8)*5);const showSpeedLines=ownsItMoment||currentStep>=7;return(<g transform={`translate(${shakeX},${shakeY})`}><rect x="0"y="0"width="1080"height="1080"fill={Colors.midnightBase}/><g opacity={0.2}>{[...Array(5)].map((_,i)=><rect key={i}x={100+i*220}y="100"width="60"height="800"fill={Colors.deepPurple}/>)}</g>{showSpeedLines&&<SpeedLines frame={localFrame}centerX={buildX}centerY={buildY}intensity={ownsItIntensity+0.5}count={40}/>}<Steps frame={localFrame}progress={climbProgress}showCrack={ownsItMoment}intensity={1+ownsItIntensity}/><Build frame={frame}x={buildX}y={buildY}state={ownsItMoment?'walking':climbProgress>0.8?'presenting':'walking'}intensity={1+ownsItIntensity*0.5}scale={1+ownsItIntensity*0.1}/>{currentStep<10&&<g transform={`translate(200,${buildY})`}opacity={0.8}><text fontSize="20"fill={Colors.oliveGold}fontFamily="sans-serif"letterSpacing="4">{currentStep<3?'UNCERTAINTY':currentStep<6?'REGULATION':currentStep<9?'PROOF':'LEGITIMACY'}</text></g>}{ownsItMoment&&ownsItIntensity>0.5&&<g transform="translate(540,200)"><text x="0"y="0"textAnchor="middle"fontSize="60"fill={Colors.goldBright}fontFamily="Impact,sans-serif"fontWeight="900"stroke={Colors.shadowBlack}strokeWidth="3"opacity={ownsItIntensity}>OWNS IT</text></g>}<g transform="translate(50,50)"><rect x="0"y="0"width="200"height="10"fill={Colors.shadowBlack}rx="5"/><rect x="0"y="0"width={200*climbProgress}height="10"fill={Colors.oliveGold}rx="5"/></g></g>)};
EOF

cat > src/scenes/Act3Pillars.tsx << 'EOF'
import React from'react';import{interpolate}from'../lib/deterministic';import{Colors,Timing}from'../lib/colors';import{Build}from'../characters/Build';import{Guardians}from'../characters/Guardians';import{SpeedLines}from'../components/Effects';export const Act3Pillars:React.FC<{frame:number}>=({frame})=>{const localFrame=frame-Timing.act2End;const arrivalProgress=interpolate(localFrame,[0,40],[0,1],'clamp');const buildY=500-arrivalProgress*100;const activatedGuardians:number[]=[];for(let i=1;i<=10;i++){const activationStart=40+(i-1)*15;if(localFrame>=activationStart)activatedGuardians.push(i)}const allActivated=localFrame>160;const presenting=localFrame>20&&localFrame<160;const presentingIntensity=presenting?interpolate(localFrame,[20,40,140,160],[0,1,1,0],'clamp'):0;const zoomProgress=interpolate(localFrame,[160,180],[1,1.3],'clamp');return(<g transform={`translate(540,300)scale(${zoomProgress})translate(-540,-300)`}><rect x="0"y="0"width="1080"height="1080"fill={Colors.midnightBase}/><defs><radialGradient id="throneLight"cx="50%"cy="30%"r="50%"><stop offset="0%"stopColor={Colors.goldBright}stopOpacity="0.3"/><stop offset="100%"stopColor="transparent"/></radialGradient></defs><rect x="0"y="0"width="1080"height="1080"fill="url(#throneLight)"/><ellipse cx="540"cy="900"rx="400"ry="100"fill={Colors.deepPurple}opacity="0.5"/>{localFrame>40&&localFrame<160&&<SpeedLines frame={localFrame}centerX={540}centerY={400}intensity={0.7}count={25}/>}<Guardians frame={localFrame}activatedGuardians={activatedGuardians}allActivated={allActivated}intensity={1}/><Build frame={frame}x={540}y={buildY}state={presenting?'presenting':allActivated?'validated':'idle'}intensity={1+presentingIntensity*0.3}scale={1+arrivalProgress*0.2}/>{presenting&&<g opacity={presentingIntensity}><line x1="540"y1={buildY-50}x2="540"y2="200"stroke={Colors.cyanDigital}strokeWidth="3"strokeDasharray="10 5"/></g>}<g transform="translate(50,50)"><text fontSize="24"fill={Colors.creamPaper}fontFamily="sans-serif"letterSpacing="2">GUARDIANS:{activatedGuardians.length}/10</text></g>{allActivated&&localFrame>170&&<g transform="translate(540,150)"opacity={interpolate(localFrame,[170,180],[0,1],'clamp')}><text x="0"y="0"textAnchor="middle"fontSize="48"fill={Colors.goldBright}fontFamily="Impact,sans-serif"fontWeight="900"stroke={Colors.shadowBlack}strokeWidth="2">PROOF ACCEPTED</text></g>}</g>)};
EOF

cat > src/scenes/Act4Validation.tsx << 'EOF'
import React from'react';import{interpolate,seededRandom}from'../lib/deterministic';import{Colors,Timing}from'../lib/colors';import{Build}from'../characters/Build';import{Guardians}from'../characters/Guardians';import{GraffitiTitle,SpeedLines}from'../components/Effects';export const Act4Validation:React.FC<{frame:number}>=({frame})=>{const localFrame=frame-Timing.act3End;const sealProgress=interpolate(localFrame,[0,30],[0,1],'clamp');const goldProgress=interpolate(localFrame,[30,90],[0,1],'clamp');const standProgress=interpolate(localFrame,[90,120],[0,1],'clamp');const cameraPullBack=interpolate(localFrame,[120,150],[1.3,1],'clamp');const titleProgress=interpolate(localFrame,[150,180],[0,1],'clamp');const particles=[...Array(30)].map((_,i)=>{const angle=(i/30)*Math.PI*2;const distance=goldProgress*(100+seededRandom(i)*200);return{x:540+Math.cos(angle)*distance,y:400+Math.sin(angle)*distance,size:5+seededRandom(i+100)*10,opacity:goldProgress>0.5?1-(goldProgress-0.5)*2:goldProgress*2}});return(<g><rect x="0"y="0"width="1080"height="1080"fill={Colors.midnightBase}/><defs><radialGradient id="goldBurst"cx="50%"cy="40%"r="60%"><stop offset="0%"stopColor={Colors.goldBright}stopOpacity={goldProgress*0.5}/><stop offset="50%"stopColor={Colors.oliveGold}stopOpacity={goldProgress*0.3}/><stop offset="100%"stopColor="transparent"/></radialGradient></defs><rect x="0"y="0"width="1080"height="1080"fill="url(#goldBurst)"/><g opacity={standProgress}transform={`scale(${cameraPullBack})`}>{[...Array(10)].map((_,i)=><g key={i}transform={`translate(${100+i*100},0)`}><rect x="0"y="0"width="60"height="1080"fill={Colors.deepPurple}opacity={0.2}/><rect x="0"y="0"width="60"height="100"fill={Colors.oliveGold}opacity={0.5}/></g>)}</g>{goldProgress>0&&<g>{particles.map((p,i)=><circle key={i}cx={p.x}cy={p.y}r={p.size}fill={Colors.goldBright}opacity={p.opacity}/>)}</g>}{sealProgress>0&&sealProgress<1&&<SpeedLines frame={localFrame}centerX={540}centerY={400}intensity={sealProgress}count={50}/>}<g opacity={0.3+standProgress*0.3}><Guardians frame={localFrame}allActivated={true}intensity={0.5}/></g>{sealProgress<1&&<g transform={`translate(540,${200+sealProgress*200})`}><ellipse cx="0"cy="0"rx="80"ry="100"fill={Colors.guardianSeal}opacity={0.8}/><text x="0"y="10"textAnchor="middle"fontSize="60"fill={Colors.shadowBlack}>✦</text></g>}<g transform={`translate(540,${400-standProgress*50})scale(${1+goldProgress*0.3})`}><Build frame={frame}state="validated"intensity={1+goldProgress}/>{standProgress>0&&<g transform="translate(0,-120)"opacity={standProgress}><path d="M-40 0L-20-30L0-10L20-30L40 0L30 20L-30 20Z"fill={Colors.goldBright}stroke={Colors.oliveGold}strokeWidth="3"/></g>}</g>{titleProgress>0&&<GraffitiTitle frame={localFrame}text="C-RSP"subtext="Constitutional Responsive System Protocol"x={540}y={200}revealProgress={titleProgress}/>}{goldProgress>0.5&&<g transform="translate(540,600)"opacity={interpolate(goldProgress,[0.5,1],[0,1],'clamp')}><text x="0"y="0"textAnchor="middle"fontSize="72"fill={Colors.goldBright}fontFamily="Impact,sans-serif"fontWeight="900"stroke={Colors.shadowBlack}strokeWidth="3">LEGITIMATE</text></g>}</g>)};
EOF

cat > src/index.tsx << 'EOF'
import React from'react';import{Composition}from'remotion';import{ImJustABuild}from'./Composition';import{Timing}from'./lib/colors';export const RemotionRoot:React.FC=()=>(<Composition id="ImJustABuild"component={ImJustABuild}durationInFrames={Timing.duration}fps={Timing.fps}width={1080}height={1080}/>);
EOF

cat > src/Composition.tsx << 'EOF'
import React from'react';import{useCurrentFrame}from'remotion';import{Timing}from'./lib/colors';import{Act1Concept}from'./scenes/Act1Concept';import{Act2Mechanism}from'./scenes/Act2Mechanism';import{Act3Pillars}from'./scenes/Act3Pillars';import{Act4Validation}from'./scenes/Act4Validation';export const ImJustABuild:React.FC=()=>{const frame=useCurrentFrame();const getCurrentAct=()=>{if(frame<Timing.act1End)return 1;if(frame<Timing.act2End)return 2;if(frame<Timing.act3End)return 3;return 4};const currentAct=getCurrentAct();return(<svg viewBox="0 0 1080 1080"style={{width:'100%',height:'100%',backgroundColor:'#0D0221'}}>{currentAct===1&&<Act1Concept frame={frame}/>}{currentAct===2&&<Act2Mechanism frame={frame}/>}{currentAct===3&&<Act3Pillars frame={frame}/>}{currentAct===4&&<Act4Validation frame={frame}/>}</svg>)};
EOF

echo "✅ Part 4 complete"
```

### **setup-part-5.sh** (GitHub Push)
```bash
#!/bin/bash
set -e
echo "🚀 Part 5: Pushing to GitHub..."
echo "Target: https://github.com/coreyalejandro/tlc-artifacts"
echo ""

if ! command -v git &> /dev/null; then
    echo "❌ Git not installed. Install from: https://git-scm.com/downloads"
    exit 1
fi

if [ ! -f "package.json" ]; then
    echo "❌ Error: Not in im-just-a-build folder"
    echo "Run: cd im-just-a-build"
    exit 1
fi

if [ ! -d ".git" ]; then
    echo "📦 Initializing Git..."
    git init
fi

if ! git config user.email &> /dev/null; then
    read -p "Git email: " email
    git config user.email "$email"
fi

if ! git config user.name &> /dev/null; then
    read -p "Git name: " name
    git config user.name "$name"
fi

cat > .gitignore << 'EOF'
node_modules/
dist/
out/
*.log
.DS_Store
.vscode/
.idea/
EOF

echo "✅ .gitignore created"

git add .
git commit -m "Initial: I'm Just a Build - Neo-soul constitutional animation"

git remote add origin https://github.com/coreyalejandro/tlc-artifacts.git 2>/dev/null || git remote set-url origin https://github.com/coreyalejandro/tlc-artifacts.git

echo "☁️  Pushing to GitHub..."
echo "   You will be prompted for GitHub credentials"
echo "   Use your Personal Access Token as the password"
echo ""

git push -u origin main 2>/dev/null || git push -u origin master

echo ""
echo "✅ PUSHED TO GITHUB!"
echo "📍 https://github.com/coreyalejandro/tlc-artifacts"
```

---

## ✅ OPTION 2: Single Master Script

**Save as: `setup-everything.sh`**

```bash
#!/bin/bash
# ═══════════════════════════════════════════════════════════════════
# MASTER SCRIPT: Setup + GitHub Push
# Run: bash setup-everything.sh
# ═══════════════════════════════════════════════════════════════════

set -e

echo "🎬 ============================================================"
echo "🎬  I'M JUST A BUILD - COMPLETE SETUP"
echo "🎬 ============================================================"
echo ""

# PART 1: Create project
echo "📦 Creating project structure..."
mkdir -p im-just-a-build/src/{characters,components,scenes,lib}
mkdir -p im-just-a-build/scripts
mkdir -p im-just-a-build/{public,verification,dist}

cd im-just-a-build

# Create all files (content abbreviated for space - use parts 1-4 above)
echo "📝 Creating source files..."

# [Insert all the cat > file << 'EOF' commands from parts 1-4 here]

echo "✅ All files created"

# PART 2: Install and build
echo ""
echo "📥 Installing dependencies (this takes 5-10 minutes)..."
npm install

echo ""
echo "🎥 Rendering video (this takes 15-30 minutes)..."
npm run render

# PART 3: GitHub push
echo ""
echo "☁️  Pushing to GitHub..."

if ! command -v git &> /dev/null; then
    echo "⚠️  Git not installed. Skipping push."
    exit 0
fi

git init
git add .
git commit -m "Initial: I'm Just a Build"

cat > .gitignore << 'EOF'
node_modules/
dist/
EOF

git remote add origin https://github.com/coreyalejandro/tlc-artifacts.git 2>/dev/null || true
git push -u origin main 2>/dev/null || git push -u origin master

echo ""
echo "✅ ============================================================"
echo "✅  COMPLETE!"
echo "✅ ============================================================"
echo ""
echo "📺 Video: dist/im-just-a-build.mp4"
echo "📍 GitHub: https://github.com/coreyalejandro/tlc-artifacts"
```

---

## ✅ OPTION 3: GitHub Authentication Instructions

### **Method A: Personal Access Token (Recommended)**

**Step 1: Create Token on GitHub**
1. Go to https://github.com/settings/tokens
2. Click **"Generate new token (classic)"**
3. Give it a name: "I'm Just a Build Push"
4. Select scopes: **repo** (full control of private repositories)
5. Click **Generate token**
6. **COPY THE TOKEN IMMEDIATELY** (you can't see it again)

**Step 2: Use Token When Pushing**
When the script asks for password, paste your token instead.

---

### **Method B: SSH Key (More Secure)**

**Step 1: Generate SSH Key**
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
# Press Enter 3 times (accept defaults, no passphrase)
```

**Step 2: Add to GitHub**
1. Copy the public key:
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```
2. Go to https://github.com/settings/keys
3. Click **"New SSH key"**
4. Paste the key, give it a title
5. Click **Add SSH key**

**Step 3: Use SSH URL**
```bash
git remote set-url origin git@github.com:coreyalejandro/tlc-artifacts.git
```

---

## 🎯 Quick Command for Cursor Agent

**Tell your Cursor agent:**

> "Run these 5 commands in order:
> 1. Save setup-part-1.sh, setup-part-2.sh, setup-part-3.sh, setup-part-4.sh, setup-part-5.sh
> 2. bash setup-part-1.sh && bash setup-part-2.sh && bash setup-part-3.sh && bash setup-part-4.sh
> 3. cd im-just-a-build && npm install
> 4. npm run render
> 5. bash setup-part-5.sh (I'll provide GitHub credentials)"

**Or use the single script:**
> "Save and run: bash setup-everything.sh"

