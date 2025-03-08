# SCSS

### Nesting (중첩)

> `Nesting`은 '중첩'이라는 뜻을 가진 단어로, 중첩 기능을 지원함으로써 좀 더 직관적이고 편하게 요소의 구조를 확인할 수 있다는 장점이 있다


```css
.title {
	font-size: 20px;
	font-weight: 900;
	margin-left: 10px
}

.title a {
	color: #000;
	text-decoration: none;
}
```

```scss
.title {
	font-size: 20px;
	font-weight: 900;
	margin-left: 10px

	a {
		color: #000;
		text-decoration: none;
	}
}
```

> `SCSS`에서는 `&` 기호를 사용하여 중첩 내부에서 부모 요소를 더 쉽게 참조할 수 있다
> 

```css
.item {
	font-size: 20px;
	font-weight: 900;
	margin-left: 10px
}

.item:last-child {
	color: #000;
	text-decoration: none;
}
```

```scss
.title {
	font-size: 20px;
	font-weight: 900;
	margin-left: 10px;

	&:last-child {
		color: #000;
		text-decoration: none;
	}
}
```

<br/>

### Variables (변수)

> 자주 사용되고 값이 변하지 않는 상수들을 변수에 값을 선언하여 예를 들어 이전엔 어렵게 컬러코드명으로 자주 사용하는 색상을 반복해서 찾아 썻다면 변수의 등장으로 인해 편하게 변수명으로 그 값을 불러와 세팅할 수 있음 !


```scss
// _variables.scss
$bg: #e7473c;
$title: 32px;

// styles.scss
@import "_variables";

body {
  background: $bg;
}
h1 {
  color: $bg;
  font-size: $title;
}
```

<br/>


### @Mixin

> 함수와 비슷한 동작을 하는 문법이며 CSS 스타일 시트에서 반복적으로 **재 사용할 CSS 스타일 그룹 선언을 정의**하는 기능을 의미한다.

- **매개변수를 이용하여 값을 set 할 수 있음 (물론 매개변수 없이도 사용 가능 !)**
    
    ```scss
    @mixin link($color) {
      text-decoration: none;
      display: block;
      color: $color;
    }
    
    a {
    	&:nth-child(odd) {
    	  @include link(yellow);
    	}
    	&:nth-child(even) {
    	  @include link(green);
    	}
    }
    ```
    
- **mixin 함수 내에 조건문(@if / @else)으로 분기처리도 가능**
    
    ```scss
    @mixin link2($word) {
      text-decoration: none;
      display: block;
      @if $word == "odd" {
        color: yellow;
      }
      @else {
        color: green;
      }
    }
    
    a {
    	&:nth-child(even) {
    	  @include link2(even);
    	}
    }
    ```
    
- **정해진 함수를 그대로 사용하는 것 뿐만 아니라 사용하는 곳에서 `@content`로 선언된 함수 내부에 커스텀하게 값을 사용하는 곳에 맞춰서 바꿔가면서 사용할 수 있다.**
    
    ```scss
    $minIphone: 500px;
    $maxIphone: 690px;
    $minTablet: $minIphone + 1;
    $maxTablet: 1120px;
    
    @mixin responsive2($device) {
      @if $device == "iphone" {
        @media screen and (min-width: $minIphone) and (max-width: $maxIphone) {
          @content;
        }
      } @else if $device == "tablet" {
        @media screen and (min-width: $minTablet) and (max-width: $maxTablet) and (orientation: landscape) {
          @content;
        }
      }
    }
    
    h1 {
      color: red;
      @include responsive2("iphone"){
        color: yellow;
      }
      @include responsive2("tablet"){
        font-size: 40px;
      }
    }
    ```
    
<br/>


### @extends

> extends는 말그대로 이미 선언된 scss 묶음을 그대로 가져와 필요하면 내가 그 세팅에서 값을 더 추가하여 (확장하여) 스타일을 선언할 수 있는 것

```scss
// _extends.scss
%button {
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  border-radius: 7px;
  font-size: 12px;
  text-transform: uppercase;
  padding: 5px 10px;
  background-color: peru;
  color: white;
  font-weight: 500;
}

// styles.scss
@import "_extends";

a {
  @extend %button;
  text-decoration: none;
}

button {
  @extend %button;
  border: none;
}
```
