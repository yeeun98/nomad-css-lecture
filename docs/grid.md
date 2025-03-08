# GRID의 필요성
~~~
grid없이 사용하면 grid 형태로 자식들을 분류하기가 매우 어려웠다.

만약 현재 화면이 줄어들어 첫째줄에 세 개, 두 번째줄에 두 박스가 위치한다고 가정하자.
첫 째줄을 박스끼리 간격있게 배치하기 위해서 justify-content를 space-between로 지정하였는데 그러면 줄바꿈된 부분은 두 개가 완전히 서로 양끝으로 찢어지게 되어 grid로 만들고 싶었던 의도와 벗어나게 되고 줄끼리의 간격을 위해서도 아래줄의 박스들에게 margin-top을 줘야해서 불편하고 화면크기의 변화가 생기면 또 의도하지 않은 화면이 될 수 있기에 적합하지 않다.

이를 개선하기 위해 우리는 grid를 배워 익혀야 한다!
~~~

---

### `grid-template-columns`
> 같은 세로라인에 있는 박스들이 적힌 값만큼의 너비를 가지는 column을 생성함
    
```css
.father {
  display: grid;
  grid-template-columns: 200px 55px 100px;
  grid-template-rows: 100px 100px 100px; // grid-template-rows: repeat(3, 100px);
}
```

### `grid-template-rows`
> 같은 수평선에 있는 박스들이 적힌 값만큼의 높이를 가지는 column을 생성함

```css
.father {
  display: grid;
  grid-template-columns: 250px 250px 250px; /** grid-template-columns: repeat(3, 250px); */
  grid-template-rows: 100px 150px 100px;
}
```

### `column-gap`
> 세로줄끼리의 간격을 지정

```css
.father {
  display: grid;
  grid-template-columns: 250px 250px 250px;
  grid-template-rows: 100px 150px 100px;
  column-gap: 10px;
}
```

### `row-gap`
> 가로줄끼리의 간격을 지정하는 속성

```css
.father {
  display: grid;
  grid-template-columns: 250px 250px 250px;
  grid-template-rows: 100px 150px 100px;
  row-gap: 10px;
}
```

### `gap`
> column-gap과 row-gap을 이 속성으로 동시에 적용할 수 있다.

```css
.father {
  display: grid;
  grid-template-columns: 250px 250px 250px;
  grid-template-rows: 100px 150px 100px;
  gap: 10px;
}
```


### `grid-template-areas`
> 직관적으로 어떻게 grid가 배치되어야 하는지 볼 수 있게 해준다. (wrapper)

```css
.grid {
  display: grid;
  grid-template-columns: repeat(4, 200px);
  grid-template-rows: 100px repeat(2, 200px) 300px;
  grid-template-areas: 
    "header header header header"
    "content content content nav"
    "content content content nav"
    "footer footer footer footer"
  ;
}

.header {
  background-color: #2ecc71;
  grid-area: header;
}
.content {
  background-color: #3498db;
  grid-area: content;
}
.nav {
  background-color: #8e44ad;
  grid-area: nav;
}
.footer{
  background-color: orange;
  grid-area: footer;
}
```

> 💡 grid-temlplate-area를 쓸 때엔 자식들에게 grid-area를 사용해 본인이 어떤 grid인지 지정을 해줘야 부모 grid가 알아 챌 수 있다


### `grid-row-start` / `grid-row-end`
> 줄을 기준으로 start의 값부터 grid-row-end의 값까지 row를 차지하는 것. 이것을 이용해 html 이동 없이 element의 앞 뒤 순서를 바꾸는 것이 가능하다.

### `grid-column-start` / `grid-column-end`
> grid를 나누고 있는 줄을 기준으로 어떤 줄 부터 어디줄까지 grid를 채울건지 지정하는 속성

```css
.header {
  background-color: #2ecc71;
  grid-column-start: 1;
  grid-column-end: 5;
}
```

**💡 꼭 end 값이 start 보다 커야 하는 건 아니다**

### `grid-row` : `start value / end value`
> grid-row-start, grid-row-end 축약 속성

### `grid-column` : `start value / end value`
> grid-column-start, grid-column-end 축약 속성

```css
.header {
  background-color: #2ecc71;
  grid-column: 1 / 5;
	grid-row: span 2;
}
```

> 💡 위처럼도 가능한데 한 줄 한 줄 계산하기 힘들 때, 앞에서부터 줄을 셀 때 1,2,3...이렇겠지만 뒤에서부터 줄을 셀 땐 맨 뒤부터 -1,-2,-3 이렇게 되기 때문에 end 값을 -1로하면 마지막 줄까지 차지한다고 할 수 있다.
> 그리고 줄로 계산하기 싫다면 span을 사용해서 셀의 갯수로 지정하는 것도 가능하다

```css
.header {
  background-color: #2ecc71;
  grid-column: 1 / -1; 
	grid-row: span 2; // 셀 두개를 차지
	/**
		 grid-column: 2 / span 2; 
		라고 한다면 2번째 줄부터 시작해서 그것을 기준으로 두 개의 셀을 내가 차지하는 것을 의미할 수 있다
	*/
}
```

### `grid-area`
> `/` (슬래쉬)로 구분지어 `grid-row-start`, `grid-column-start`, `grid-row-end`, `grid-column-end`순으로 입력 가능

### `grid-template`
> 축약형의 제일 꼭데기에 있는 속성이라고 생각하면 됨

> grid-template-areas처럼 한 눈에 어떻게 그리드가 위치할지 볼 수 있고 그 옆에 값을 통해
> grid-template-rows와 grid-template-columns의 값을 지정할 수 있다.

**🚨 단, grid-template에서는 repeat 함수를 쓸 수 없으니 이점은 유의!**
그리고 grid-template-areas처럼 사용하기 때문에 grid-area를 통해 자식들이 본인의 이름을 정해놔야 이를 알고 배치할 수 있음


### `justify-item`
> 셀 한 칸 크기 안에서 element를 수평축에서 어떻게 정렬할건지 정하는 속성 ( default :: `stretch` )

### `align-item`
> 셀 한 칸 크기 안에서 element를 수직축에서 어떻게 정렬할건지 정하는 속성( default :: `stretch` )

### `place-item`
> `justify-item`와 `align-item` 한줄로 작성 가능
> place-item: align-items justify-items;

```css
place-item : stretch center;
```

> 💡 grid는 기본적으로 셀이 지정한 너비와 높이를 가득채우는 것이 기본으로 되어있다.
> 하지만 start, center, end를 사용하게 되면 셀 안에 있는 element의 너비 혹은 높이는 셀의 콘텐츠를 감싸는 정도로만 줄어들게 되고 줄어든 셀이 정해 놓은 값으로 정렬된다.

### `justify-content`
> 수평선에 있는 모든 items를 정해놓은 값으로 수평 정렬하는 것

### `align-content`
> 모든 줄들을 정해놓은 값으로 서로 떨어트리거나 붙혀놓는 등 이동시킬 수 있음

### `place-content`
> `justify-content`와 `align-content` 한줄로 작성 가능
> place-content : align-content  justify-content;

```css
place-content  :  stretch center;**
```

### `justify-self`
> 셀 한 칸 크기 안에서 element를 수평축에서 어떻게 정렬할건지 정하는 속성( default :: `stretch` )

### `align-self`
> 셀 한 칸 크기 안에서 element를 수직축에서 어떻게 정렬할건지 정하는 속성( default :: `stretch` )

### `place-self`
> `justify-self`와 `align-self` 한줄로 작성 가능
> place-self : align-self justify-self;

### `grid-auto-flow`
> grid-template-colums에서 지정한 한 줄에 있을 수 있는 셀의 갯수보다 더 많은 셀들이 존재할 때, grid-auto-flow를 column으로 선언하면 direction이 column으로 변해 옆으로 긴 형태로 변한다
> wrapper ( default : `row` )

### `minmax()`
> 셀의 너비나 높이를 지정하는 곳에 함수를 사용하면, 지정한 최솟값 최댓값 만큼까지만 셀의 크기가 변화한다

```scss
.grid {
  display: grid;
  gap: 5px;
  grid-template-columns: repeat(5, minmax(100px, 1fr));
  grid-template-rows: repeat(4, 100px);
}
```

### `auto-fill` / `auto fit`
- `auto-fill` :: 우리가 준 사이즈 안에 최대한 많은 공간을 만든다
- `auto fit` :: 우리가 준 사이즈 안에 최대한 fit하게 다 차도록 한다.

```html
<head>
  .....
  <style>
    .grid {
      display: grid;
      gap: 5px;
      grid-template-columns: repeat(5, minmax(100px, 1fr));
      grid-template-rows: 100px;
    }
    
    .grid:first-child {
      grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
    }

    .grid:last-child {
      grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
    }

    .item:nth-child(odd) {
      background-color: #2ecc71;
    }

    .item:nth-child(even) {
      background-color: blue;
    }
  </style>
</head>
<body>
  <div class="grid">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
    <div class="item">4</div>
    <div class="item">5</div>
  </div>

  <div class="grid">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
    <div class="item">4</div>
    <div class="item">5</div>
  </div>
</body>
```

### `min-content` / `max-content`
- `min-content` : 작아질 수 있는 크기 중 가장 작은 크기
- `max-content` : 셀이 안에 content를 다 덮는 크기 중 최소 크기

```html
<head>
  <style>
    .grid {
      display: grid;
      gap: 5px;
      grid-template-columns: repeat(5, minmax(max-content, 1fr));
      grid-auto-rows: 100px;
    }

    .item:nth-child(odd) {
      background-color: #2ecc71;
    }

    .item:nth-child(even) {
      background-color: blue;
    }
  </style>
</head>
<body>
  <div class="grid">
    <div class="item">This is a very long text</div>
    <div class="item">This is a very long text</div>
  </div>
</body>
```
