#Session 4a

##Flexbox & Transitions

Install [lite server](https://www.npmjs.com/package/lite-server) `$ npm install -g lite-server`

Run it: `$ lite-server`

Examine the final file - `http://localhost:3000/index-FINISHED.html`

Open index-START.html for editing.

Examine the DOM structure and CSS in the inspector.

###Editing

Flexbox formatting 
https://css-tricks.com/snippets/css/a-guide-to-flexbox/

```
.panel {
  background:#000;
  background-position: center;
  background-size: cover;
```

```
.panels {
  display: flex;
```

Each panel takes an equal width:

```
.panel {
  flex: 1;
```

```
.panel * { 
  border: 1px solid red;
```

Add each property (in this order)

```
.panel {
  display: flex;
  flex-direction: column;
  justify-content: center;
  <!-- align-items: center; --> 
```

Allow the outlined items to expand vertically:

```
.panel * {
  flex: 1 0 auto;
```

Note - [Default is 0 1 auto](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

Center the contents horizontally and vertically:

```
.panel * {
  display: flex;
  justify-content: center;
  align-items: center;
```

Setup for animation

```
.panel :first-child {
  transform: translateY(-100%);
}
```

```
.panel :last-child {
  transform: translateY(100%);
}
```

We are going to use JS to add classes that will animate the words in.


```
.panel.open-active :first-child {
  transform: translateY(0);
}
```

```
.panel * {
  transition:transform 0.5s;
```

Select a panel in the element inspector: `$0`

`$0.classList.add('open-active')`

Open panels take 3 times as much space:

```
.panel.open {
  flex: 3;
```

`$0.classList.add('open')`

Add transition to the panel

```
.panel {
  transition: font-size 0.7s linear, flex 0.7s linear;
```

The panels need to open before the words animate in.

###JavaScript

```
const panels = document.querySelectorAll('.panel');

function toggleOpen(){
  this.classList.toggle('open')
}
    
panels.forEach( (panel) => panel.addEventListener('click', toggleOpen))
```

In order to apply the second animation. NOT:

```
setTimeout(function(){
  console.log('boo')
}, 3000)
```

Use the transitionend event instead:

```
function openActive(e){
  console.log(e)
  // console.log(this)
  // console.log(e.propertyName)
  // this.classList.toggle('open-active')
}

panels.forEach( (panel) => panel.addEventListener('transitionend', openActive))
```

```
function openActive(e){
  if (e.propertyName === 'flex-grow'){
    this.classList.toggle('open-active')
  }
}
```

See comments in css re: Safari

```
function openActive(e){
  if(e.propertyName.includes('flex')){
    this.classList.toggle('open-active')
  }
}
```

```
.panel.open-active :last-child {
  transform: translateY(0);
}
```

Edit the transitions in the styles panel.

Copy the results to replace the linear timing functions.

`cubic-bezier(0.28, -0.3, 0.58, 1.21)`

Close panels on open

```
function closePanels(){
  panels.forEach( (panel) => panel.classList.remove('open'))
}
```

```
function toggleOpen(){
  closePanels()
  this.classList.toggle('open')
}
```





