# Flex-box

> Flexbox는 layout을 위해 box 자체에 스타일을 부여하는 것이 아닌 box를 감싸고 있는 container에 layout을 지정하는 방식
Flexbox의 container는 다른 것의 부모가 될 수 없고 바로 붙어있는 부모여야 한다.

---

### 🔹 `flex-direction` : 자식들의 정렬 방향 지정
- `row (default)` : 가로 방향으로 자식들을 정렬
- `column` : 세로 방향으로 자식들을 정렬
- `row-reverse` : 가로 방향으로 자식들을 정렬하되 맨 뒤 자식이 제일 앞에 오도록 정렬
- `column-reverse` : 세로 방향으로 자식들을 정렬하되 맨 뒤 자식이 제일 앞에 오도록 정렬

💡 **`row-reverse` / `column-reverse`는 `justify-content: center`가 기본으로 세팅됩니다.**  
필요할 시 조정해서 마크업해야 합니다.

---

### 🔹 `justify-content` : 수평축에서 자식들의 위치 조정 (wrapper에 부여)
- `center` : 가운데 정렬
- `space-between` : box들의 간격을 균일하게 띄움
- `space-around` : box 주변 옆 공간을 같게 만듦

---

### 🔹 `align-items` : 세로축에서 자식들의 위치 조정 (wrapper에 부여)
- `flex-start (default)` : 세로축 상단 정렬
- `center` : 세로축 기준으로 가운데 정렬
- `stretch`  
  - `row` : wrapper의 높이까지 가득 채움 (box 높이 지정 시 무효)  
  - `column` : wrapper의 너비까지 가득 채움 (box 너비 지정 시 무효)

💡 `flex-direction`이 `column`이면 `align-items`와 `justify-content`의 역할이 서로 반대로 적용됩니다.

---

### 🔹 `align-self` : 개별 자식의 세로축 정렬 설정 (child에 부여)
- `flex-start` : 상단 정렬 (default)
- `center` : 중앙 정렬
- `flex-end` : 하단 정렬

💡 **`align-self`는 부모의 높이가 자식의 높이보다 커야 제대로 동작합니다.**

---

### 🔹 `order` : 자식 요소의 순서를 지정하는 속성 (child에 부여)
- 기본 값 : `0`
- `order` 값이 클수록 뒤로 이동, 작을수록 앞으로 이동

```css
.children:nth-child(2) {
    order: 1; /* 세 개의 요소 중 가장 마지막으로 위치 */
}

.children:nth-child(3) {
    order: -1; /* 가장 앞에 위치 */
}
```

---

### 🔹 `flex-wrap` : 한 줄에 모든 자식을 포함할 것인지를 선택하는 속성 (wrapper에 부여)
- `nowrap (default)` : 자식들의 너비를 줄여서라도 한 줄에 전부 포함시킴
- `wrap` : 자식들의 너비를 유지하면서 공간이 모자라면 줄바꿈
- `wrap-reverse` : wrap과 같지만 맨 뒷줄이 가장 앞으로 배치

---

### 🔹 `flex-flow` : flex-direction과 flex-wrap을 함께 설정할 수 있음
```css
flex-flow: row wrap;
```

---

### 🔹 `align-content` : 여러 줄로 구성된 Flex 아이템들의 정렬 방식 (wrapper에 부여)
- `flex-start` : 줄 간격 없이 바짝 붙음
- `center` : 세로축 기준으로 가운데 정렬
- `space-between` : 양쪽 끝에 배치하고, 줄 간격을 균일하게 설정
- `space-around` : 바깥 여백을 동일하게 배치

---

## 🔹 `flex-grow` : 자식 요소의 남은 공간 비율 지정 (child에 부여)
- 기본 값 : 0
- 값이 클수록 남은 공간을 더 많이 차지함

```css
.children:nth-child(2) {
    flex-grow: 2;
}
.children:nth-child(3) {
    flex-grow: 1;
}
```

> 위 경우 남은 공간을 3등분해 2번째 자식이 2/3을 차지하고, 3번째 자식이 1/3을 차지합니다.
 
--- 

### 🔹 `flex-shrink` : 요소의 너비가 줄어들 때 자식 요소의 너비 감소 비율 지정 (child에 부여)
- 기본 값 : 1
- 값이 클수록 더 많이 줄어듦

```css
.children:nth-child(2) {
    flex-shrink: 2; /* 다른 자식들보다 2배 더 많이 줄어듦 */
}
```

---

### 🔹 `flex-basis` : 요소의 초기 너비 설정 (child에 부여)
> width와 비슷하지만, 요소의 초기 크기를 지정하는 속성
> flex-direction: column일 경우 height의 초기 값으로 설정됨

```css
.children {
    flex-basis: 200px;
}
```
