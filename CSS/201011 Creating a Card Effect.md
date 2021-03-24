tags: #JavaScript #CSS #english

## Creating a Card with CSS

이번에 [도서관](https://github.com/jioneeu/library)을 만들면서 사용한 CSS.
아래의 코드를 사용해서 카드와 같은 느낌이 나도록 만들수있다.

```css
/* Add shadows to create the "card" effect */
.card {
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
    transition: 0.3s;
    border-radius: 10%;
}
```

`:hover`할 때 `scale`을 조정하므로써 마치 카드를 집어 올리는 듯한 느낌이 들도록 효과를 줘봤다
(전혀 그런 느낌이 안나지만...)

```css 
.card:hover {
  transform: scale(1.05);
}
```