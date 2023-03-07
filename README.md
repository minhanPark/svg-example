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
