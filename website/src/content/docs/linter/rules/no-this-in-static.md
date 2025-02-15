---
title: noThisInStatic (since vnext)
---

**Diagnostic Category: `lint/nursery/noThisInStatic`**

:::caution
This rule is part of the [nursery](/linter/rules/#nursery) group.
:::

Disallow `this` and `super` in `static` contexts.

In JavaScript, the `this` keyword in static contexts refers to the class (the constructor) instance,
not an instance of the class. This can be confusing for developers coming from other languages where
`this` typically refers to an instance of the class, not the class itself.

Similarly, `super` in static contexts refers to the parent class, not an instance of the class.
This can lead to unexpected behavior if not properly understood.

This rule enforces the use of the class name itself to access static methods,
which can make the code clearer and less prone to errors. It helps to prevent
misunderstandings and bugs that can arise from the unique behavior of `this` and `super` in static contexts.

Source: https://github.com/mysticatea/eslint-plugin/blob/master/docs/rules/no-this-in-static.md

## Example

### Invalid

```jsx
 class A {
    static CONSTANT = 0;

    static foo() {
        this.CONSTANT;
    }
 }
```

<pre class="language-text"><code class="language-text">nursery/noThisInStatic.js:5:9 <a href="https://biomejs.dev/lint/rules/no-this-in-static">lint/nursery/noThisInStatic</a> <span style="color: #000; background-color: #ddd;"> FIXABLE </span> ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

<strong><span style="color: Orange;">  </span></strong><strong><span style="color: Orange;">⚠</span></strong> <span style="color: Orange;">Using </span><span style="color: Orange;"><strong>this</strong></span><span style="color: Orange;"> in a </span><span style="color: Orange;"><strong>static</strong></span><span style="color: Orange;"> context can be confusing.</span>
  
    <strong>4 │ </strong>    static foo() {
<strong><span style="color: Tomato;">  </span></strong><strong><span style="color: Tomato;">&gt;</span></strong> <strong>5 │ </strong>        this.CONSTANT;
   <strong>   │ </strong>        <strong><span style="color: Tomato;">^</span></strong><strong><span style="color: Tomato;">^</span></strong><strong><span style="color: Tomato;">^</span></strong><strong><span style="color: Tomato;">^</span></strong>
    <strong>6 │ </strong>    }
    <strong>7 │ </strong> }
  
<strong><span style="color: lightgreen;">  </span></strong><strong><span style="color: lightgreen;">ℹ</span></strong> <span style="color: lightgreen;"><strong>this</strong></span><span style="color: lightgreen;"> refers to the class.</span>
  
<strong><span style="color: lightgreen;">  </span></strong><strong><span style="color: lightgreen;">ℹ</span></strong> <span style="color: lightgreen;">Unsafe fix</span><span style="color: lightgreen;">: </span><span style="color: lightgreen;">Use the class name instead.</span>
  
    <strong>3</strong> <strong>3</strong><strong> │ </strong>  
    <strong>4</strong> <strong>4</strong><strong> │ </strong>      static foo() {
    <strong>5</strong>  <strong> │ </strong><span style="color: Tomato;">-</span> <span style="color: Tomato;"><span style="opacity: 0.8;">·</span></span><span style="color: Tomato;"><span style="opacity: 0.8;">·</span></span><span style="color: Tomato;"><span style="opacity: 0.8;">·</span></span><span style="color: Tomato;"><span style="opacity: 0.8;">·</span></span><span style="color: Tomato;"><span style="opacity: 0.8;">·</span></span><span style="color: Tomato;"><span style="opacity: 0.8;">·</span></span><span style="color: Tomato;"><span style="opacity: 0.8;">·</span></span><span style="color: Tomato;"><span style="opacity: 0.8;">·</span></span><span style="color: Tomato;"><strong>t</strong></span><span style="color: Tomato;"><strong>h</strong></span><span style="color: Tomato;"><strong>i</strong></span><span style="color: Tomato;"><strong>s</strong></span><span style="color: Tomato;"><strong>.</strong></span><span style="color: Tomato;"><strong>C</strong></span><span style="color: Tomato;"><strong>O</strong></span><span style="color: Tomato;"><strong>N</strong></span><span style="color: Tomato;"><strong>S</strong></span><span style="color: Tomato;"><strong>T</strong></span><span style="color: Tomato;"><strong>A</strong></span><span style="color: Tomato;"><strong>N</strong></span><span style="color: Tomato;"><strong>T</strong></span><span style="color: Tomato;">;</span>
      <strong>5</strong><strong> │ </strong><span style="color: MediumSeaGreen;">+</span> <span style="color: MediumSeaGreen;"><span style="opacity: 0.8;">·</span></span><span style="color: MediumSeaGreen;"><span style="opacity: 0.8;">·</span></span><span style="color: MediumSeaGreen;"><span style="opacity: 0.8;">·</span></span><span style="color: MediumSeaGreen;"><span style="opacity: 0.8;">·</span></span><span style="color: MediumSeaGreen;"><span style="opacity: 0.8;">·</span></span><span style="color: MediumSeaGreen;"><span style="opacity: 0.8;">·</span></span><span style="color: MediumSeaGreen;"><span style="opacity: 0.8;">·</span></span><span style="color: MediumSeaGreen;"><span style="opacity: 0.8;">·</span></span><span style="color: MediumSeaGreen;"><strong>A</strong></span><span style="color: MediumSeaGreen;"><strong>.</strong></span><span style="color: MediumSeaGreen;"><strong>C</strong></span><span style="color: MediumSeaGreen;"><strong>O</strong></span><span style="color: MediumSeaGreen;"><strong>N</strong></span><span style="color: MediumSeaGreen;"><strong>S</strong></span><span style="color: MediumSeaGreen;"><strong>T</strong></span><span style="color: MediumSeaGreen;"><strong>A</strong></span><span style="color: MediumSeaGreen;"><strong>N</strong></span><span style="color: MediumSeaGreen;"><strong>T</strong></span><span style="color: MediumSeaGreen;">;</span>
    <strong>6</strong> <strong>6</strong><strong> │ </strong>      }
    <strong>7</strong> <strong>7</strong><strong> │ </strong>   }
  
</code></pre>

```jsx
 class B extends A {
    static bar() {
        super.CONSTANT;
    }
 }
```

<pre class="language-text"><code class="language-text">nursery/noThisInStatic.js:3:9 <a href="https://biomejs.dev/lint/rules/no-this-in-static">lint/nursery/noThisInStatic</a> <span style="color: #000; background-color: #ddd;"> FIXABLE </span> ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

<strong><span style="color: Orange;">  </span></strong><strong><span style="color: Orange;">⚠</span></strong> <span style="color: Orange;">Using </span><span style="color: Orange;"><strong>super</strong></span><span style="color: Orange;"> in a </span><span style="color: Orange;"><strong>static</strong></span><span style="color: Orange;"> context can be confusing.</span>
  
    <strong>1 │ </strong> class B extends A {
    <strong>2 │ </strong>    static bar() {
<strong><span style="color: Tomato;">  </span></strong><strong><span style="color: Tomato;">&gt;</span></strong> <strong>3 │ </strong>        super.CONSTANT;
   <strong>   │ </strong>        <strong><span style="color: Tomato;">^</span></strong><strong><span style="color: Tomato;">^</span></strong><strong><span style="color: Tomato;">^</span></strong><strong><span style="color: Tomato;">^</span></strong><strong><span style="color: Tomato;">^</span></strong>
    <strong>4 │ </strong>    }
    <strong>5 │ </strong> }
  
<strong><span style="color: lightgreen;">  </span></strong><strong><span style="color: lightgreen;">ℹ</span></strong> <span style="color: lightgreen;"><strong>super</strong></span><span style="color: lightgreen;"> refers to a parent class.</span>
  
<strong><span style="color: lightgreen;">  </span></strong><strong><span style="color: lightgreen;">ℹ</span></strong> <span style="color: lightgreen;">Unsafe fix</span><span style="color: lightgreen;">: </span><span style="color: lightgreen;">Use the class name instead.</span>
  
    <strong>1</strong> <strong>1</strong><strong> │ </strong>   class B extends A {
    <strong>2</strong> <strong>2</strong><strong> │ </strong>      static bar() {
    <strong>3</strong>  <strong> │ </strong><span style="color: Tomato;">-</span> <span style="color: Tomato;"><span style="opacity: 0.8;">·</span></span><span style="color: Tomato;"><span style="opacity: 0.8;">·</span></span><span style="color: Tomato;"><span style="opacity: 0.8;">·</span></span><span style="color: Tomato;"><span style="opacity: 0.8;">·</span></span><span style="color: Tomato;"><span style="opacity: 0.8;">·</span></span><span style="color: Tomato;"><span style="opacity: 0.8;">·</span></span><span style="color: Tomato;"><span style="opacity: 0.8;">·</span></span><span style="color: Tomato;"><span style="opacity: 0.8;">·</span></span><span style="color: Tomato;"><strong>s</strong></span><span style="color: Tomato;"><strong>u</strong></span><span style="color: Tomato;"><strong>p</strong></span><span style="color: Tomato;"><strong>e</strong></span><span style="color: Tomato;"><strong>r</strong></span><span style="color: Tomato;"><strong>.</strong></span><span style="color: Tomato;"><strong>C</strong></span><span style="color: Tomato;"><strong>O</strong></span><span style="color: Tomato;"><strong>N</strong></span><span style="color: Tomato;"><strong>S</strong></span><span style="color: Tomato;"><strong>T</strong></span><span style="color: Tomato;"><strong>A</strong></span><span style="color: Tomato;"><strong>N</strong></span><span style="color: Tomato;"><strong>T</strong></span><span style="color: Tomato;">;</span>
      <strong>3</strong><strong> │ </strong><span style="color: MediumSeaGreen;">+</span> <span style="color: MediumSeaGreen;"><span style="opacity: 0.8;">·</span></span><span style="color: MediumSeaGreen;"><span style="opacity: 0.8;">·</span></span><span style="color: MediumSeaGreen;"><span style="opacity: 0.8;">·</span></span><span style="color: MediumSeaGreen;"><span style="opacity: 0.8;">·</span></span><span style="color: MediumSeaGreen;"><span style="opacity: 0.8;">·</span></span><span style="color: MediumSeaGreen;"><span style="opacity: 0.8;">·</span></span><span style="color: MediumSeaGreen;"><span style="opacity: 0.8;">·</span></span><span style="color: MediumSeaGreen;"><span style="opacity: 0.8;">·</span></span><span style="color: MediumSeaGreen;"><strong>A</strong></span><span style="color: MediumSeaGreen;"><strong>.</strong></span><span style="color: MediumSeaGreen;"><strong>C</strong></span><span style="color: MediumSeaGreen;"><strong>O</strong></span><span style="color: MediumSeaGreen;"><strong>N</strong></span><span style="color: MediumSeaGreen;"><strong>S</strong></span><span style="color: MediumSeaGreen;"><strong>T</strong></span><span style="color: MediumSeaGreen;"><strong>A</strong></span><span style="color: MediumSeaGreen;"><strong>N</strong></span><span style="color: MediumSeaGreen;"><strong>T</strong></span><span style="color: MediumSeaGreen;">;</span>
    <strong>4</strong> <strong>4</strong><strong> │ </strong>      }
    <strong>5</strong> <strong>5</strong><strong> │ </strong>   }
  
</code></pre>

### Valid

```jsx
class B extends A {
    static ANOTHER_CONSTANT = A.CONSTANT + 1;

    static foo() {
        A.CONSTANT;
        B.ANOTHER_CONSTANT;
    }

    bar() {
        this.property;
    }
}
```

```jsx
class A {
   static foo() {
       doSomething()
   }

   bar() {
     A.foo()
   }
}
```

## Related links

- [Disable a rule](/linter/#disable-a-lint-rule)
- [Rule options](/linter/#rule-options)
