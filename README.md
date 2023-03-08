# SVG 강의 따라하기

## SVG의 크기 설정하기

기본적으로 svg에는 width와 height를 전달할 수 있다.

```html
<svg width="500" height="500">
  <rect x="0" y="0" width="100" height="100"></rect>
</svg>
```

> css로도 전달이 가능

중요한건 svg는 viewBox라는 속성을 기준으로 그리게 된다.

```html
<svg width="500" height="500" viewBox="0 0 1000 1000">
  <rect x="0" y="0" width="100" height="100"></rect>
</svg>
```

위와 같이 있을 때 rect는 50/50 만큼 그리게 된다. 왜냐면 viewBox가 1000이고 width 및 height가 100이니 1/10의 크기가 되어야 하고, 실제 svg의 크기는 500이니 거기의 1/10으로 그려지는 것이다.

> svg에 width 및 height를 따로 주지 않고 viewBox만 주면 전체 크기에서 반응형처럼 동작한다

## css 적용하기

svg 태그 등에 클래스를 주고 css를 적용할 수 있다.

```html
<svg>
  <style>
     {
      ....;
    }
  </style>
</svg>
```

svg 태그 내부에도 style 태그를 사용할 수 있다

## js 적용하기

dom 똑같이 사용가능하다.  
위에처럼 내부에 스크립트를 쓸 수도 있다.

```html
<svg>
  <style>
     {
      ....;
    }
  </style>
  <script>
    {.....}
  </script>
</svg>
```

> 순서 바꿔보니 밑에 태그에 넣으려고 하면 script도 맨 마지막에 사용해야하는 듯 하다.

## 기본도형

```html
<rect x="10" y="20" width="200" height="100"></rect>
<rect x="10" y="20" width="200" height="100" />
```

x가 10px, y가 20px인 위치부터 width가 200, height가 100인 인 사각형을 그림

```html
<rect x="50" y="170" rx="10" ry="30" width="100" height="100"></rect>
```

사각형인데 round를 가진(rx, ry) 사각형을 그림

```html
<circle cx="350" cy="250" r="30"></circle>
```

원은 센터와 반지름을 통해서 그린다. (cx = centerX, cy=centerY, r = radius)

```html
<ellipse cx="200" cy="200" rx="100" ry="50" fill="red"></ellipse>
```

타원은 ellipse를 통해서 그린다. rx는 x의 반지름 ry는 y의 반지름으로 타원이기때문에 각각 주게됨

```html
<line x1="10" x2="400" y1="30" y2="300" stroke="red"></line>
```

(10, 30) 에서 (400, 300)으로 직선을 긋는다.

```html
<polyline
  points="0 0, 200 100, 150 300"
  stroke="red"
  stroke-width="10"
></polyline>
```

polyline은 point를 찍어나가면 연결해서 선을 그어준다.

```html
<polygon
  points="0 0, 200 100, 150 300"
  stroke="red"
  stroke-width="10"
></polygon>
```

폴리곤은 폴리라인과 똑같이 만들지만 도형으로 만들어준다(첫번째 점과 마지막 점을 이어준다).

```html
<path d="M 300 200 L 500 100 H 50 V 300 Z"></path>
```

path는 자유 그리기이다
M은 이동, x좌표 y좌표를 적어주면 된다. L은 직선 그리기, H는 가로선 그리기이다(Horizontal). V는 세로선 그리기이다(Vertical) Z는 폴리곤때처럼 도형을 합쳐준다.

```html
<path d="M 100 150 C 100 150, 300 50, 500 250"></path>
```

C는 곡선을 그린다. 300 50은 각도를 정하는 점, 500 250은 도착선이다. Z를 붙이면 또 연결해준다.

## stroke 모양 조정하기

```css
path {
  stroke-linecap: round;
  /* stroke-linecap: butt; */
  /* stroke-linecap: square; */
  stroke-linejoin: round;
}
```

path애 stroke-linecap과 stroke-linejoin으로 stroke의 모양을 조절할 수 있다.  
선의 끝 부분을 처리할 때는 stroke-linecap(모자씌운다는 의미인가?)에 값을 주면 되고, 선끼리 만난 부분을 처리할 때는 stroke-linejoin(조인)에 값을 주면 된다.

## 그룹 지정하기

그룹을 지정해서 같은 효과를 줄 수 있다.

```html
<g fill="blue" stroke-width="20" stroke="red">
  <rect x="10" y="20" width="200" height="100"></rect>
  <rect x="50" y="170" rx="10" ry="10" width="100" height="100"></rect>
</g>
```

위와 같이 g로 묶고 효과를 주면 rect에 똑같이 적용되는 것을 확인 가능  
g에 class를 주고 그 클래스에 css를 줘도 된다.

## text

text 태그를 사용하면 글자를 쓸 수 있다.

```html
<svg class="shapes">
  <text x="20" y="50">Hello, RW!</text>
</svg>
```

(x, y) 부터 글씨를 쓰기 시작한다. 다른 css에서 텍스트에 효과를 주듯이 주면되지만 color 대신에 fill을 줘야 글씨 색이 바뀜

## 곡선을 따라 글쓰기

defs는 참조를 위한 태그를 담는 태그이다.

```html
<svg class="shapes">
  <defs>
    <path
      id="text-curve"
      d="M 50 400 C 50 400, 300 500, 400 400 C 400 400, 600 170, 700 300"
    ></path>
  </defs>
  <text x="20" y="50">
    <textPath href="#text-curve">
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Cupiditate fugit
      unde accusamus voluptate aspernatur alias?
    </textPath>
  </text>
</svg>
```

path를 참조하기 위해 defs 태그 안에 넣고, path의 아이디 값을 주었다.  
text안에 textPath를 주고 href와 path의 id를 맞춰주면 우리가 그린 path를 따라서 글씨가 써진다.

텍스트에 부분을 강조하려면 어떻게 해야할까?  
일반적인 html에서는 span태그를 쓰듯이 svg안에서는 tspan을 쓰면 된다

```html
<text x="20" y="50">
  <textPath href="#text-curve">
    Lorem
    <tspan>ipsum dolor</tspan>
    sit amet consectetur adipisicing elit. Cupiditate fugit unde accusamus
    voluptate aspernatur alias?
  </textPath>
</text>
```

위에 tspan에 클래스를 주든지 하면됨.

## 그라디언트 주기

defs안에 gradiant태그를 정의한다.

```html
<defs>
  <linearGradient id="hair-color">
    <stop offset="0%" stop-color="yellow" />
    <stop offset="50%" stop-color="hotpink" />
    <stop offset="100%" stop-color="deepskyblue" />
  </linearGradient>
  <!--radialGradient-->
  <style>
    .hair {
      fill: url("#hair-color");
    }
  </style>
</defs>
```

원형일때는 radialGradient이고, 직선일때는 linearGradient으로 감싸면 된다.

중요한건 id와 url로 연결시키는 것이다.(곡선따라 글 쓸때도 href로 주었음)  
클래스 hair에 fill(색)을 그라디언트(id-url로 연결)로 주었음

## 패턴

패턴도 defs에 정의한 다음 fill에 연결시켜주면 된다.

```html
<defs>
  <pattern id="bg-pattern" x="0" y="0" width="0.1" height="0.1">
    <circle cx="25" cy="25" r="25" class="pattern-circle"></circle>
  </pattern>
</defs>
```

pattern의 width와 height는 비율을 나타낸다. 즉 0.1이기 때문에 1/10로 나눠서 패턴이 들어간다는 의미이다.  
그리고 x, y는 비율에서 나눠진 부분들에서 시작점을 뜻한다. 즉 밑에 circle은 나눠진 칸에서 각 (0, 0)을 기준으로 반복될 것이다.  
전체 svg가 크기가 얼마일지 예상이 안간다면 svg에 viewBox를 안에 기준점을 바꿔주면 된다.

## 마스크

마스크라는 기능을 통해서 부분적으로 보이도록 설정할 수 있다.

```html
<svg class="shapes">
  <defs>
    <mask id="mask-circle">
      <circle cx="900" cy="70" r="40"></circle>
    </mask>
    <style>
      #mask-circle circle {
        fill: #fff;
      }
    </style>
  </defs>
  <g mask="url(#mask-circle)">
    <text x="10" y="100">
      Lorem ipsum dolor sit, amet consectetur adipisicing elit. Saepe
      consectetur quod sequi temporibus hic. Reiciendis.
    </text>
  </g>
</svg>
```

defs 안에 mask태그를 쓰고, mask 태그안에 형태(사각형이든 원이든)를 잡아준다. 이때 **반드시 fill을 하얀계열**로 채운다.  
밑에 작성한 텍스트 부분을 그룹(g)로 감싸고 mask를 연결해주면 마스크에 설정된 부분만 텍스트가 보이게 된다.
