<script>
	var rolLength = 6;

	const rRandom = () => {
	var min = Math.ceil(0);
	var max = Math.floor(rolLength - 1);
	return Math.floor(Math.random() * (max - min)) + min;
	};

	const rRotate = () => {
	var panel = document.querySelector(".rouletter-wacu");
	var btn = document.querySelector(".rouletter-btn");
	var deg = [];
	for (var i = 1, len = rolLength; i <= len; i++) {
		deg.push((360 / len) * i);
	}

	var num = 0; //회전을 시킬 횟수
	var ani = setInterval(() => {
		num++; //인터벌 수치만큼 증가
		panel.style.transform = "rotate(" + 360 * num + "deg)";
		// 버튼 이벤트 막기
		btn.disabled = true; //button,input
		btn.style.pointerEvents = "none"; //a 태그
		
		// 횟수 50에 다달았을때,
		if (num === 50) {
		clearInterval(ani); //회전 삭제
		panel.style.transform = "rotate(" + deg[rRandom()] + "deg)"; //랜덤숫자로 멈춤
		} 
	}, 50);
	};

	document.addEventListener("click", function (e) {
	var target = e.target;
	if (target.tagName === "BUTTON") {
		rRotate();
		
		// transition-timing-function 를 ease-in-out로 적용 햇기때문에 잔여초 이후 버튼활성화
		setTimeout(() => {
		target.disabled = false;
		target.style.pointerEvents = "auto";
		console.log("이벤트가 끝남");
		}, 5500);
	}
	});
</script>

<main>
	<div class="rouletter">
		<div class="rouletter-bg"><div class="rouletter-wacu"></div></div>
		<div class="rouletter-arrow"></div>
		<button class="rouletter-btn">start</button>
	</div>
	
</main>

<style>
	.rouletter{
		position: relative;
		width:400px;
		height:400px;
	}
	.rouletter-bg{
		position: absolute;
		top:50%;
		left:50%;
		transform:translate(-50%,-50%);
		width:350px;
		height:350px;
		border-radius:350px;
		overflow:hidden;
	}
	.rouletter-wacu{
		width:100%;height:100%;
		background:#f5f5f2 url('https://m.lifeplanet.co.kr:444/commons/slink/administrator/openInnovation/img/MO)%20360%ED%94%8C%EB%9E%98%EB%8B%9B_%EB%A3%B0%EB%A0%9B%ED%8C%90_476x476_201026.png') no-repeat;
		background-size:100%;
		transform-origin: center;
	}
	.rouletter-arrow{
		position: absolute;
		top:0;
		left:50%;
		transform:translateX(-50%);
		width:1px;
		height:1px;
		border-right:10px solid transparent;
		border-left:10px solid transparent;
		border-top:40px solid red;
		border-bottom:0px solid transparent;
	}
	.rouletter-btn{
		position: absolute;
		top:50%;
		left:50%;
		transform:translate(-50%,-50%);
		width:80px;
		height:80px;
		border-radius:80px;
		background:#fff;
		border-image: linear-gradient(to right, #fbfcb9be, #ffcdf3aa, #65d3ffaa);
		border: 2px solid;
	}

	.onq{
		animation-name: ani;
		animation-duration: 0.1s;
		animation-fill-mode: forwards;  
		animation-iteration-count: infinite;
	}

	@keyframes ani{
		0% { 
			transform: rotate(0deg); 
			transition-timing-function: ease-out;
		}
		100%{ 
			transform: rotate(360deg); 
		}
	}
</style>