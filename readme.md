#Session 4a

##Flexbox & Transitions

Install [lite server](https://www.npmjs.com/package/lite-server) `$ npm install -g lite-server`

Run it: `$ lite-server`

Examine the final file - `http://localhost:3000/index-FINISHED.html`

Open index-START.html for editing.

Examine the DOM structure and CSS in the inspector.

###Editing

```
.panel {
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

```
.panel * {
  flex: 1 0 auto;
```

```
.panel * {
  display: flex;
  justify-content: center;
  align-items: center;
```

https://css-tricks.com/snippets/css/a-guide-to-flexbox/

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

We are going to use JS to animate the words in.


```
.panel.open-active :first-child {
  transform: translateY(0);
}
```

Select a panel in the element inspector: `$0`

`$0.classList.add('open-active')`

Open panels take 5 times as much space:

```
.panel.open {
  flex: 5;
```

`$0.classList.add('open')`

Add transition to the panel

```
.panel {
  transition: font-size 0.7s linear, flex 0.7s linear;
```

###JavaScript

```
const panels = document.querySelectorAll('.panel');

function toggleOpen(){
  this.classList.toggle('open')
}
    
panels.forEach( (panel) => panel.addEventListener('click', toggleOpen))
```

In order to apply the second animation

```
setTimeout(function(){
  console.log('boo')
}, 3000)
```

```
function openActive(e){
  console.log(e)
  console.log(this)
  console.log(e.propertyName)
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

Edit the transitions in the styles panel.

Copy the results to replace the linear timing functions.

`cubic-bezier(0.28, -0.3, 0.58, 1.21)`





