## **CSS Combinators**
https://www.w3schools.com/css/css_combinators.asp

A combinator is something that explains the relationship between the selectors.

## Descendant Selector

The descendant selector matches all elements that are descendants of a specified element.

```scss
//selects all <p> elements inside <div> elements
div p {
  background-color: yellow;
}
```
---
## Child Selector (>)
The child selector selects all elements that are the children of a specified element.**Only within**
Doesnot select if element is a children of another element

```scss
//selects all <p> elements that are children of a <div> element. 
div > p {
  background-color: yellow;
}
```
---
## Adjacent Sibling Selector (+)
The adjacent sibling selector is used to select an element that is directly after another specific element.

Sibling elements must have the same parent element, and "adjacent" means "immediately following".


```scss
// selects the first <p> element that are placed immediately after <div> elements
div + p {
  background-color: yellow;
}
```
---
## General Sibling Selector (~)
The general sibling selector selects all elements that are next siblings of a specified element.

```scss
//  selects all <p> elements that are next siblings of <div> elements
div + p {
  background-color: yellow;
}
```

For Children use Descendant and child >
For siblings use Adjacent Sibling + and  General Sibling ~

