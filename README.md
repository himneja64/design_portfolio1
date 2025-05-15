<div align="center">
	<h1>Design portfolio</h1>
	<h3><a href=https://himneja64.github.io/design_portfolio1>💻사이트 이동하기💻</a></h3>
	<p>HTML, CSS, Emmit, Js Libraries를 활용하여 작업한 반응형 웹페이지입니다.</p>
</div>
<br/>
<div align="end">

</div>

<br/>

## 📌주요 기능
- 창 너비 체크 및 메뉴 초기화
- 메뉴 버튼 클릭 시 메뉴 열고 닫기
- GNB 항목 클릭/마우스 이벤트 처리
- 슬라이드 이미지 경로 설정
- 디바이스 종류 확인 및 GSAP 타이포 효과 설정
- 요소에 스크롤 트리거 효과

## 🧩사용 기술
|기술|설명|
|---|---|
|![HTML](https://img.shields.io/badge/-HTML-F05032?style=flat-square&logo=html5&logoColor=ffffff)|HTML5 웹표준 준수|
|![CSS](https://img.shields.io/badge/-CSS-007ACC?style=flat-square&logo=css3)|반응형 처리 및 디자인|
|![JavaScript](https://img.shields.io/badge/-JavaScript-dc8d2d?style=flat-square&logo=javascript&logoColor=ffffff)|웹 요소의 제어 및 라이브러리 연동|
|![Swiper](https://img.shields.io/badge/Swiper-6332F6?logo=swiper&logoColor=white&style=flat-square) |슬라이더 구현|
|![GSAP](https://img.shields.io/badge/GSAP-88CE02?logo=greensock&logoColor=white&style=flat-square)|부드럽고 가벼운 애니메이션 구현|

### 1. 화면 사이즈💻
<details>
	<summary>💛적용 구간 보기</summary>
	|: 동작 이전 :|: 동작 이후 :|
	|***************|***************|
	| ![](https://github.com/user-attachments/assets/b069f0a6-38fb-4ae4-9b81-97178c28e63d) | ![](https://github.com/user-attachments/assets/3ad59cb0-abe9-4665-867f-4396e9f45327) |
</details>

```javascript
	let desktopFlag;

	function checkWindowSize(){
		let winw=window.innerWidth;

		if(winw >= 1240){
			desktopFlag=true;
		}
		else{
			desktopFlag=false;
		}

		if(header.classList.contains("menu-open")){
			header.classList.remove("menu-open");
		}

		Array.from(gnbList).forEach(function(item){
			if(item.classList.contains("open")){
				item.classList.remove("open");
			}
		});
	}

	checkWindowSize();
```

> [!NOTE]  
>`winw` 변수 생성으로 브라우저 넓이를 분기했습니다.  
해당 함수는 브라우저의 넓이에 변화가 발생하는 시점에 실행됩니다.  
>
>이때 menu와 gnb를 닫음으로써 어색하게 느껴질 수 있는 그리드 변화가 사용자에게 노출되는 것을 차단하는 동시에 사이드 이펙트의 발생 가능성을 예방합니다.
>
> 또한 함수를 호출하여 최초 로드시 강제로 1회 실행시킵니다.

<br>

### 2. GNB 2depth 📂
<details>
	<summary>💛적용 구간 보기</summary>
	|: 동작 이전 :|: 동작 이후 :|
	|***************|***************|
	| ![](https://github.com/user-attachments/assets/71f8fc4e-bb01-4e27-a64c-6f01e772b108) | ![](https://github.com/user-attachments/assets/aed3da53-6b0b-4175-bd75-4ced48a1a992) |
</details>

```javascript
	Array.from(gnbList).forEach(function(item1, i){
		item1.addEventListener("click", function(e){
			e.preventDefault();

			if(desktopFlag) return;

			if(item1.classList.contains("no-depth")) return;

			if(!item1.classList.contains("open")){
				Array.from(gnbList).forEach(function(item2, j){
					if(j == i){
						item2.classList.add("open");
					}
					else{
						item2.classList.remove("open");
					}
				});
			}
			else{
				item1.classList.remove("open");
			}
		});

	// (중략)…

	});
```

> [!NOTE]  
> GNB 메뉴를 조정하는 코드로, 동작되기 위해서는 두 가지의 조건이 먼저 충족되어야 합니다.  
> 1. `if(desktopFlag) return` : 브라우저의 너비가 1240px 미만일 것.
> 1. `if(item1.classList.contains("no-depth")) return;` : 2depth가 존재할 것.
>
> 두 조건이 충족되었다면, 2depth를 가진 gnblist(item1)가 열려있는지 확인합니다.
>
> 이때 클릭한 아이템만 열고 나머지는 모두 닫도록 합니다.  
> 반대로 열려 있었다면 닫도록합니다. (토글 기능 구현)

<br>

### 3. 중복 요소 가변적으로 처리하기 ⛓

```javascript
	const imageData=[
		{
			pc: "visual_pc1.jpg",
			mobile: "visual_mobile1.jpg"
		},
		{
			pc: "visual_pc2.jpg",
			mobile: "visual_mobile2.jpg"
		}
	];

	let swiperSlides=document.querySelectorAll(".main-slider .swiper-slide");

	swiperSlides.forEach(function(item, i){
		let pc=item.querySelector(".pc");
		let mobile=item.querySelector(".mobile");

		pc.style.backgroundImage=`url(images/${imageData[i].pc})`;
		mobile.style.backgroundImage=`url(images/${imageData[i].mobile})`;
	});
```

> [!NOTE]  
> 해당 부분은 Template Literal방식을 사용하여 작성했습니다.  
> 유사한 이름을 가진 요소들을 배열로 묶을 처리 한 후, 적용할 부분에 작성했습니다.

<br>

### 4. custom mouse 🖱
<details>
	<summary>💛적용 구간 보기</summary>
	|: 동작 :|
	|***************|
	| https://github.com/user-attachments/assets/029d4194-50df-4f3b-bf20-0e6085fd4d6d |
</details>

```javascript
	let customHover=document.querySelectorAll(".custom-hover");
	let pageTop=document.querySelector("#page-top");

	document.body.addEventListener("mousemove", function(e){
		gsap.to("#custom-cursor, #custom-cursor-text", {
			x: e.clientX,
			y: e.clientY,
			duration: 1.2,
			ease: Power3.easeOut
		});
	});

	customHover.forEach(function(item){
		item.addEventListener("mouseenter", function(){
			gsap.to(".custom-hover-circle, .custom-hover-text", {
				width: "100%",
				height: "100%",
				opacity: 1,
				duration: 0.3,
				ease: Power3.easeOut
			});
		});

		item.addEventListener("mouseleave", function(){
			gsap.to(".custom-hover-circle, .custom-hover-text", {
				width: 0,
				height: 0,
				opacity: 0,
				duration: 0.3,
				ease: Power3.easeOut
			});
		});
	});
```

> [!NOTE]  
> 위의 코드는 커스텀 마우스에 대한 코드로,  
> 기본적으로 사용자의 마우스를 느긋하게 따라오되 `ease: Power3.easeOut` 값을 주어 부드러운 움직임을 나타내도록 했습니다.
>
> 평소에는 위의 기본값이 드러나지 않지만, 특정 위치(customHove)에서는 마우스의 형태가 변화함과 더불어 시각적으로도 효과가 드러나도록 했습니다.


![Footer](https://capsule-render.vercel.app/api?type=waving&color=auto&height=200&section=footer)
