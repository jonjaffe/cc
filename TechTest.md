## General CS Question
>Every day a new frog is born weight 0grams and grows at a rate of 10grams/day, maxing out at 100grams in 10 days
### On day n, what is the total weight of the frog community?

| 13  | 12  | 11  | 10 | 9  | 8  | 7  | 6  | 5  | 4  | 3  | 2  | 1 |
|-----|-----|-----|----|----|----|----|----|----|----|----|----|---|
| 100 | 100 | 100 | 90 | 80 | 70 | 60 | 50 | 40 | 30 | 20 | 10 | 0 |
| 100 | 100 | 90  | 80 | 70 | 60 | 50 | 40 | 30 | 20 | 10 | 0  |   |
| 100 | 90  | 80  | 70 | 60 | 50 | 40 | 30 | 20 | 10 | 0  |    |   |
| 90  | 80  | 70  | 60 | 50 | 40 | 30 | 20 | 10 | 0  |    |    |   |
| 80  | 70  | 60  | 50 | 40 | 30 | 20 | 10 | 0  |    |    |    |   |
| 70  | 60  | 50  | 40 | 30 | 20 | 10 | 0  |    |    |    |    |   |
| 60  | 50  | 40  | 30 | 20 | 10 | 0  |    |    |    |    |    |   |
| 50  | 40  | 30  | 20 | 10 | 0  |    |    |    |    |    |    |   |
| 40  | 30  | 20  | 10 | 0  |    |    |    |    |    |    |    |   |
| 30  | 20  | 10  | 0  |    |    |    |    |    |    |    |    |   |
| 20  | 10  | 0   |    |    |    |    |    |    |    |    |    |   |
| 10  | 0   |     |    |    |    |    |    |    |    |    |    |   |
| 0   |     |     |    |    |    |    |    |    |    |    |    |   |


```javascript
function totalWeight(n) {
  if (n <= 1) {
    total = 0;
  }
  if (n <= 10) {
    total = n * (n -1) * 5;
  }
  else {
    total = (n-10) * 100 + (10*9*5);
  }
  return total;
}
```
### On day n, what is the average weight of the average frog?
```javascript
function averageWeightOfFrog(n) {
  return totalWeight(n) / n;
}
```
### How might we redesign the model to allow for new frogs to be born on a manually set schedule?
```javascript
function totalWeight(n, interval) {
  let total = 0;
  let numFrogs = (n-1) / interval + 1;
  for (let i = 1; i <= numFrogs; i++) {
    total += weight(n)
    n -= interval;
  }
  return total;
}

function weight(n) {
  if (n > 10) {
    return 100;
  }
  return 10 * (n-1);
}
```

## Android Questions
### 1	Object row of type FrameLayout is defined, with its corresponding OnTouchListener:
```java
row.setOnTouchListener(new View.OnTouchListener() {
  int count = 0;
  @Override
  public boolean onTouch(View view, MotionEvent event) {
    count++;
    return true;
  }
});
```
>What is the value of count after two short taps?
```
2
```
### 2	MainActivity starts TextActivity with a call to startActivityForResult. String "Hello World!" is entered in TextActivity's EditText object and Button object is clicked. Button's onClick method:
```java
public void onClick(View v) {
  Intent intent = new Intent(getApplicationContext(), MainActivity.class);
  intent.putExtra("string", edit.getText().toString());
  setResult(Activity.RESULT_OK, data);
  startActivity(intent);
}
  ```
MainActivity's onActivityResult method:
```java
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
  super.onActivityResult(requestCode, resultCode, data);
  text = data.getStringExtra("string");
}
```
>What will the content of the text object be?

```
"Hello World!"
```


## Typescipt / JavaScript Questions
### 1	Write a function appendRow that appends a table row to the table with ID "tbl". The appended row should have the same number of cells as the last row in that table. For example, after appending a row to the table below, the table should have 2 rows where each row has 2 cells.
```html
<table id="tbl" border="1">
  <tbody>
    <tr>
      <td></td>
      <td></td>
    </tr>
  </tbody>
</table>
```
```javascript
function appendRow() {
  let cells = document.getElementById("tbl").firstElementChild.lastElementChild.childElementCount;
  let newRow = document.createElement("TR");
  for (let i = 0; i < cells; i++) {
    newRow.appendChild(document.createElement("TD"));
  }
  document.getElementById("tbl").firstElementChild.appendChild(newRow);
}
```

### 2	Write an addClickHandler function that registers a click handler and implements the following logic:
>When a button with id "btn" is clicked, it disappears.
>1 second after the click, it reappears.

```javascript
function addClickHandler() {
  const button = document.getElementById("btn");
  button.addEventListener("click", function() {
    button.style.visibility = "hidden";
    setTimeout(function() { button.style.visibility = "initial" }, 1000)
  });
}
```

### 3	Write a function that removes all items that are not numbers from the array. The function should modify the existing array, not create a new one.															
>For example, if the input array contains values [1, 'a', 'b', 2], after processing, the array will contain only values [1, 2].
```javascript
function removeNonNumbers(array) {
  for (let i = array.length-1; i >= 0; i--) {
    if (isNaN(array[i])) {
      array.splice(i, 1);
    }
  }
  return array;
}
```


## HTML Questions
### 1	Add necessary HTML attributes so that paragraph editor has the following properties:
>When mouse is on paragraph, tooltip with text "Click for editing" should be shown.
>When user clicks on paragraph, paragraph should be editable.
>Spell checking should be enabled with default language "en".
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Paragraph editor</title>
  </head>
  <body>
    <p id="editor" title="Click for editing" onclick="changeParagraphToTextArea()">
      Hello, I should be editable if you click on me!
    </p>
    <script>
      function changeParagraphToTextArea() {
        let textArea = document.createElement("TEXTAREA");
        let editor = document.getElementById("editor");
        textArea.placeholder = "Write something";
        textArea.spellcheck = true;
        let parent = editor.parentNode
        parent.replaceChild(textArea, editor);
      }
    </script>
  </body>
</html>
```

## CSS Questions
### 1	Write CSS which implements the following rules for all tables:
>The text in the table header should be gray (HEX: 808080).
>The text in the first column should be bold.
>Odd rows in the table body (1, 3, 5, etc.) should have white text (HEX: FFFFFF) on a gray background (HEX: 808080).
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Format table</title>
    <style type="text/css">
    thead { color: 808080; }
    td:first-child { font-weight: bold; }
    tbody > tr:nth-child(odd) { color: FFFFFF; background-color: 808080; }
    </style>
  </head>
  <body>
    <table>
      <thead>
        <tr><th>Rank</th><th>Name</th></tr>
      </thead>
      <tbody>
        <tr><td>1.</td><td>New York</td></tr>
        <tr><td>2.</td><td>Los Angeles</td></tr>
        <tr><td>3.</td><td>Chicago</td></tr>
        <tr><td>4.</td><td>Houston</td></tr>
      </tbody>
    </table>
  </body>
</html>
```
