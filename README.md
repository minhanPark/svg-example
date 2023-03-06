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
