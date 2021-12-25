# scss

## **Variables**

**Deffination**

```scss
$variableName: value;
```

**usage**

```scss
color: $variable;
```

> compile to its original value not to css variable .

---

## **Map**

like js obj

**Deffination**

```scss
$mapVariableName: (
  "key": value,
);
```

variableName
**To get value from a map use map-get function**

```scss
font-weight: map-get($map: $font-weight, $key: bold);
```

---

## **Nesting**

https://css-tricks.com/the-sass-ampersand/

```scss
//basic nesting
.parent {
  .child {
  }
}
```

You can nest as deep as you’d like, but it’s a good practice to keep it only a level or two to prevent overly specific selectors.

> & always refer to the parent class

1- adding another class

```scss
.some-class {
  &.another-class {
  } // .some-class .anotherclass
}
```

2-Using the & with pseudo classes

```scss
.button {
  &:visited {
  } //.button:visited
  &:hover {
  }
  &:active {
  }
}
```

3-Using the & with >, +, and ~
Using the & with the

- child combinator >
- adjacent sibling combinator +
- general sibling combinator ~
