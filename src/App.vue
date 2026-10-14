<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

const show = ref(null);
const showP = ref(null);


function closeSection() {
  show.value = '00'; 
}

// Close sections on escape key press
function handleKeyPress(event) {
  if (event.key === 'Escape'){
  if (showP.value){
	showP.value = false;
  } 
  else{
    closeSection();
  }
}
}
function handleClickOutside(event){
 const navDiv = document.querySelector('.nav');
 const dimDiv = document.querySelector('.lower');
 const resumeDiv = document.querySelector('.resume');
 const projectDiv = document.querySelector('.projects');
 const contactDiv = document.querySelector('.contact');
 const clickTarget = event.target;
 const clickTargetZ = window.getComputedStyle(clickTarget).zIndex;
			
	if(parseInt(clickTargetZ) < 1){
	if(showP.value){
	showP.value= false;
	}
	else{
		closeSection();
	}
	}
}

onMounted(() => {
  // Add an event listener for key presses when the component is mounted
  window.addEventListener('keydown', handleKeyPress);
  document.addEventListener('click', handleClickOutside);
});

onBeforeUnmount(() => {
  // Remove the event listener when the component is about to be destroyed
  window.removeEventListener('keydown', handleKeyPress);
  document.removeEventListener('click', handleClickOutside);
  clearInterval(intervalID);
});
</script>

<template>
	<div class = header>William Langley - Data Analyst</div>
	<hr class = "divide" style = "opacity:.25; color:inherit">	
	<div class = "nav">
		<button class = "btn" @click="show = 'A'">Projects</button>
		<button class = "btn" @click="show = 'B'">Resume</button>
		<button class = "btn" @click="show = 'D'">Contact</button>
		<a href="https://github.com/willisxyz/" 
		   target="_blank" rel = "noopener noreferrer"><button class =
				   "btn GitHub">GitHub</button></a>
	</div>
	<Transition name="nest" mode="out-in">
		<div v-if="show==='A'">
			<div class = projects>
				<div class = "mouse">
					<button class = "btn" @click = "showP = 'A1'">UM Assessments</button>
					<transition name = "fade">
					<span v-if="showP==='A1'"> 
						<div class = "Assessments">
							<p>
							<img src = "./assets/pbi_1.png" class = "servetrackgif">
							<img src = "./assets/pbi_2.png" class = "servetrackgif">
							PowerBI report created to audit staff timeliness, form errors, and other metrics
							by utilization management team.
							</p>
						</div>
					</span>
					</transition>
				</div>
				<div class = "think">
					<button class = "btn" @click = "showP = 'B1'">Batch Details Report</button>
					<transition name = "fade">
						<span v-if="showP==='B1'"> 
						<div class = "BDR">
							<p>
							<img src = "./assets/cr_1.png" class = "BDR_1">
							<br>Crystal Reports report used by management services team to retrieve
							organized batch details for export.
							</p>
						</div>
						</span>
					</transition>
				</div>
				<div class = "serveP">
					<button class = "btn" @click = "showP = 'C1'">servetrack</button>
					<transition name = "fade">
					<span v-if="showP==='C1'"> 
						<div class = "servetrack">
							<button class = "close" @click="showP = false">close</button>
							<p>
							<img src = "./assets/track78.gif" class = "servetrackgif">
							<a href="https://github.com/wlangley512/servetrack" 
						    target="_blank" rel = "noopener noreferrer">
							<img src="./assets/github-mark.png" alt = "repository" width = "24" height = "24">
							</a>
							Servetrack is an object tracking script that utilizes the Python 
							library OpenCV to track and anaylyze a volleyball serve. Coded back in 2023 with very minimal AI assisstance.
							</p>
						</div>
						</span>
					</transition>
				</div>
				<div class = "vb">
				</div>
		</div>
	</div>
	<div v-else-if="show==='B'" style="height:0px;">
		<div class = "resume">	
			<iframe src="https://docs.google.com/document/d/e/2PACX-1vSGEWk4qb5FHlKd32V_4qNmbU7_Q3-FMPKQgH0z_HrZH-cBlLqjfo-Br6vZmaymho04N6Fwqrbu1mZA/pub?embedded=true"
				width="100%"
				frameBorder="0"
				></iframe>
			<button class = "close" 
					style="left: -740px;
						   top: 5px;"
					@click="show = 'F'">close</button>
		</div>
	</div>
	<div v-else-if="show==='D'" style="height:0px">
		<div class = "contact">
			<button class = "close" @click="show = 'F'">close</button>
			<p>Email: wlangley512@gmail.com</p>
			<p>LinkedIn: 
			<a href ="https://www.linkedin.com/in/william-langley/"
			   target="_blank" rel="noopener noreferrer">https://www.linkedin.com/in/william-langley/</a></p>
		</div>
	</div>
</Transition>
<div class = lower>
	<div class = "setup"><img src="./assets/me.jpg" width = "375" height = "375"/>	
		<div class = "LFW">
			<p>currently looking for work!</p>
		</div>
	<div class = "blurb">
		<p>Heya. I'm a data analyst/DBA. Check out my resume!</p> 
		
		<p>From 04/24 to 10/26 I worked for Integral Care as a <span class = "jobtitle">Data Analyst 
			<span class = "jobtitletip">"Quality Systems Database Administrator"</span>
			</span>	I created reports in <em1>PowerBI</em1> and <em1>Crystal Reports</em1> 
		using <em1>T-SQL</em1>, <em1>InterSystems Cache</em1>, and <em1>Intersystems IRIS</em1> 
		as backend languages. Also automated stored procedures using <em1>Python</em1> scripting.</p> 
		
		<p>I also have experience with <em2>HTML</em2>/<em2>CSS</em2>/<em2>JS</em2> 
		and various <em2>JS frameworks</em2>. I made this site originally 
		using <em2>jQuery</em2> but have since switched it over to <em2>VueJS</em2>.</p>
		<p>I am looking for work as a data analyst or DBA anywhere in the US or the UK.</p>
		
	</div>
</div>
<Transition name="dark" mode="in-out">
	<div v-if="show==='A' || show==='B' || show==='C' || show === 'D' || showP === 'A1'
		|| showP === 'B1'" @click="closeSection">
		<div class = "dim"></div>
	</div>
</Transition>
</div>
</template>

<style>
.nav{
	z-index: 3;
	position: absolute;
	text-align: center;
	left:50%;
	transform: translateX(-50%);
	top: 55px;
}
.header{
	z-index: 0;
	position: absolute;
	left:50%;
	transform: translateX(-50%);
	font-family: Roboto;
	font-size: 25px;
	font-weight:500;
	text-align:center;
	top:5px;
}
.divide{
	z-index: 1;
	border:solid 1px;
	margin-top:45px;
	width: 800px;
}
.lower{
	z-index: -1;
	font-family: Roboto;
	font-weight: 500;
	font-size: 25px;
	text-align: center;
	position: fixed;
	top:0;
	left:0;
	width: 100%;
	height: 100%;
	background: rgb(237,223,202, 1);
}
.setup{
	position: absolute;
	top: 100px;
	z-index: -1;
	left: 0;
	right: 0;
	margin-left: auto;
	max-width: 850px;
	margin-right: auto;
	display: flex;
}
.setup img{
	z-index: -1;
	max-height: 375px;
	border: 2px solid grey;
	max-width: 375px;
}
.setup em1{
	color: #0058ab;
	font-style: normal;
}
.setup em2{
	color: #2bab00;
	font-style:normal;
}
.LFW{
	z-index: -1;
	position: absolute;
	left: -50px; 
	height: 60px;
	rotate: -28deg;
	text-align: left;
	font-size: 15px;
	color: #f4fc03;
	text-shadow: -1px -1px 0 #000, 1px -1px 0 #000, -1px 1px 0 #000, 1px 1px 0 #000;
	animation: LFW 2s infinite;
}
@keyframes LFW{
	50%{font-size:20px}
}
.jobtitle{
	position: relative;
	display: inline-block;
	font-style:normal;
	cursor:pointer;
	border-bottom: .05px dotted black;
}
.jobtitletip{
	visibility: hidden;
	width: 200px;
	background-color: #5c7178E6;
	color: #fff;
	text-align: center;
	border-radius: 6px;
	padding: 1px 0;
	position: absolute;
	z-index: 1;
}
.jobtitle:hover .jobtitletip{
	visibility:visible;
}

.blurb{
	font-size: 16px;
	z-index: -1;
	margin-left: 10px;
	margin-top: 50px;
}
.blurb p{
	z-index: -1;
}
.btn {
	z-index: 3;
	position: relative;
	font-size: 17px;
	border: none;
	background-color: inherit;
	font-family: Roboto; 
	cursor: pointer;
	text-align: center;
	text-decoration: underline;
}
.close{
	z-index: 0;
	border: none;
	position:absolute;
	top:0;
	right:0;
	background-color: inherit;
	font-family: Roboto;
	cursor: pointer;
	text-decoration: underline;
}
.resume {
	z-index: 3;
	top:40px;
	display: flex;
	position: relative;
	margin: auto;
	justify-content: center;
	overflow: hidden;
	width: 800px;
	height: 935px; 
	background: rgb(255, 245, 230, 1);
	border: 2px solid grey;
}
.projects {
	text-align: center;
	display: flex;
	justify-content: center;
	flex-wrap: wrap;
	height: 0px;
}
.projects .btn{
	position: static;
}
.projects div{
	z-index:3;
	margin: 0 10px 20px 10px;
	padding:5px; 
	float:left;
}
.mouse, .serveP, .think, .vb{
	z-index: 0;
	text-align: center;
	position: relative;
	margin: auto;
	margin-bottom: 2px;
	top: 70px;
	width: 175px;
	height: 21px;
	background: rgb(255, 245, 230, 1);
	border: 2px solid grey;
}
.Assessments{
	z-index: 3;
	font-family: Roboto;
	display: flex;
	justify-content: center;
	align-items:center;
	position: static;
	width: 1100px;
	height: 400px;
	border: 2px solid grey;
	background: rgb(255,245,230,1);
}
.BDR{
	z-index: 3;
	font-family: Roboto;
	display: flex;
	justify-content: center;
	align-items:center;
	position: static;
	width: 900px;
	height: 450px;
	border: 2px solid grey;
	background: rgb(255,245,230,1);
}
.servetrack{
	z-index: 3;
	font-family: Roboto;
	display: flex;
	justify-content: center;
	align-items:center;
	position: static;
	width: 600px;
	height: 400px;
	border: 2px solid grey;
	background: rgb(255,245,230,1);
}
.servetrackgif{
	z-index: 5;
	border: 2px solid grey;
	margin: 10px;
	height:306px;
	width:513px;
}
.BDR_1{
	z-index: 5;
	border: 2px solid grey;
	margin: 10px;
	height:358px;
	width:736px;
}
.contact{
	font-family:Roboto;
	z-index: 3;
	text-align: center;
	font-size:17px;
	position: relative;
	margin:auto;
	top: 70px;
	width:40%;
	border: 2px solid grey;
	background: rgb(255,245,230,1);
}
.about{
	font-family: Roboto;
	z-index: 3;
	font-size: 17px;
	text-align: center;
	position: relative;
	margin: auto;
	padding: 5px;
	top: 70px;
	width: 50%;
	height: 66%;
	border: 2px solid grey;
	background: rgb(255,245,230, 1);
}	
.warning{
	position: absolute;
	color: #ab0000;
	text-align: center;
	top: -38px;
	left: -87px;
	width: 120px;
}
.dim{
	position:relative;
	z-index: -1;
	box-shadow: 0 0 0 100vmax rgba(0,0,0,.3);
}
.fade-enter-active, .fade-leave-active{
	transition: opacity 0.5s;
}
.fade-enter-from, .fade-leave-to{
	opacity: 0;
}
.nest-enter-active, .nest-leave-active{
	transition: all .4s ease-in-out;
}
.dark-enter-from, .dark-leave-to{
	transition: all .7s ease-in-out;
}
.nest-leave-active {
	transition-delay: .2s;
}
.nest-enter-from, 
.nest-leave-to{
	transform: translateX(10px);
	opacity: 0.001;
}
.nest-enter-active .mouse, 
.nest-leave-active .mouse, 
.nest-enter-active .serveP, 
.nest-leave-active .serveP, 
.nest-enter-active .think,
.nest-leave-active .think,
.nest-enter-active .vb,
.nest-leave-active .vb{
	transition:  .3s ease-in-out;
}
.nest-enter-from .mouse,
.nest-leave-to .mouse,
.nest-enter-from .serveP,
.nest-leave-to .serveP,
.nest-enter-from .think,
.nest-leave-to .think,
.nest-enter-from .vb,
.nest-leave-to .vb{
	transform: translateX(10px);
	opacity: 0.001;
}
.nest-leave-active .mouse{
	transition-delay: .3s;
}
.nest-leave-active .serveP{
	transition-delay: .2s;
}
.nest-leave-active .think{
	transition-delay: .1s;
}
.nest-enter-active .serveP{
	transition-delay: .1s;
}
.nest-enter-active .think{
	transition-delay: .2s;
}
.nest-enter-active .vb{
	transition-delay: .3s;
}
/* NEW ANIMATION LATER
@keyframes bugger {
	0%{
		top: 0px;
		transform: scaleX(1.0);
	}
	100%{
		top: 200px;
		transform: scaleX(0.1);
	}
}
*/
.shake {
  animation: shake 0.3s cubic-bezier(0.4, 0.2, 0.8, 0.1) both;
  transform: translate3d(0, 0, 0);
  display: inline-block;
  
}
@keyframes shake {
	10%,20%,30%,40%,50%,60%,70%,80%,90%{
		transform: rotate(-3deg);
	}
	15%,25%,35%,45%,55%,65%,75%,85%,95%{
		transform: rotate(3deg);
	}
}
</style>
