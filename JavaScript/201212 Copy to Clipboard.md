tags: #JavaScript #copy #clipboard

I used below codes to copy CSS codes into the clipboard for [this](https://github.com/bugxvii/border-radius-previewer) project.

```js
   let dummy = document.getElementById('dummy');
    dummy.innerText = `{
    ${css}
    ${firefox}
    ${safari}
}`;

    var selection = window.getSelection();
    var range = document.createRange();
    range.selectNodeContents(dummy);
    selection.removeAllRanges();
    selection.addRange(range);

    document.execCommand('copy');
    selection.removeAllRanges();
```

Seems like their are other solutions like ...
```js
let dummy = document.getElementById('dummy');
    dummy.innerText = `{
    ${css}
    ${firefox}
    ${safari}
}`;

    dummy.select(); // this caused an error
    document.execCommand('copy');
```

I got an error saying that `.select()` is not a funciton.. so I had used the first solution.

### Reference
- [Copy output of a JS variable to the clipboard](https://stackoverflow.com/questions/33855641/copy-output-of-a-javascript-variable-to-the-clipboard)