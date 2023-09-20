
# Goals

  * What does browser know: What computer languages can our browser understand? [#](#what-does-browser-know)
  * Enhanced languages: Why do we use other langugage that needs to be transpiled to those computer languages? [#](#enhanced-languages)
  * Create a React+Vite project: Project development environment using Vite + ReactJS [#](#create-a-reactvite-project)

# What does browser know? 

[Foodpanda example](https://www.foodpanda.com.tw/restaurant/ag3m/liang-she-han-pai-gu-san-xia-min-sheng-dian)

Consists of three parts:

  * Front-end: HTML, CSS, JavaScript

HTML
```html
<button data-testid="menu-product-button-overlay-id" class="product-button-overlay" aria-label="炸雞腿飯,  $ 168 - 放入購物車"></button>
```

CSS
```css
.dish-card .product-button-overlay {
    border-radius: 4px;
    bottom: 0;
    cursor: pointer;
    display: block;
    height: calc(100% - 2px);
    left: 1px;
    outline: none!important;
    position: absolute;
    right: 0;
    top: 1px;
    width: calc(100% - 2px);
    z-index: 2
}
```

JavaScript
```javascript
const product_buttons = document.getElementsByClassName("product-button-overlay")
```


Most of the time, css are saved in a .css file, js are saved in a .js file, and html are saved in a .html file. And somewhere inside html, there is a link to the css file and a link to the js file through `<link>` and `<script>` tags.

# Enhanced languages

We wish we can do:
```javascript
function ProductButton(arialLabel){
    return (
        <button data-testid="menu-product-button-overlay-id" class="product-button-overlay" aria-label={arialLabel}></button>
    )
}

ProductButton("炸雞腿飯,  $ 168 - 放入購物車")
ProductButton("炸排骨飯,  $ 148 - 放入購物車")
```

Unfortunately we can not.  

But we can develop under such an environment with the help of [ReactJS](https://reactjs.org/), which allows you to mix javascript with html. We call this html in javascript as JSX.

> ReactJS gives us flexibility to use JSX. (There are other frameworks that also allow us to use JSX, such as VueJS and AngularJS.)

Browser can not understand JSX. In addition, ReactJS comes with a lot of features browser can not understand directly. So we need to translate JSX and ReactJS into something browser can understand. This is called **transpiling**.

A good development environment has to be able to transpile JSX and ReactJS into something browser can understand. We use some development management tools to help us do that, which is [Vite](https://vitejs.dev/)


# Create a React+Vite project

We are going to create a React project with Vite development environment.


First create a project folder, and open it in vscode.

## Create projects 


  1. Open project in your vscode. 
  2. Click ![](../img/toggle%20panels.png) and navigate to terminal, type:  
  3. 
```
npm create vite@latest . -- --template react
```

 * There will be questions to answer. Just press enter to accept the default value.

After creation, it also said: Now run

```
  npm install
  npm run dev
```

  * line 1: install the project dependencies

  * line 2: run the developing result.

You should see what the app looks like in your browser.

## File structure

![](../img/project%20structure.png)

  * `package.json` is for npm to manage the project.  
  * `vite.config.js` is for vite to manage the project.

## NPM script

![](../img/npm%20scripts.png)

If this function does not show up, click your `package.json` file to trigger it.

  * `npm run dev` is the same as clicking **dev**  
  * `npm run build` is the same as clicking **build**  

**build** will create a folder called **dist**. 
  * transpiled results.
  * This is the folder we will deploy to the server.

> `package.json` is a configuration file for npm. It contains the name of the project, the version of the project, the dependencies of the project, and the scripts of the project.

Difference between `dev` and `build` is that `dev` will keep watching your code and transpile it whenever you change your code. `build` will only transpile your code once.

## .js and .jsx

JS that has jsx element should have an extension `.jsx`. However, use `.js` will work. But in a strict environment setting you must use `.jsx`.

# Card example

  * [Card](https://www.w3schools.com/howto/howto_css_cards.asp)