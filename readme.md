# Welcome to the source code of `yaqinhasan.com`

This is the current repository for the source code for `yaqinhasan.com`
The previous repository containing abandoned approaches and alpha versions has been made private and deprecated to avoid confusion. 

# CSS Tree
Most sites have one gigantic `styles.css` file, I didn't want to do this because, while this does improve site performance by reducing `HTTP GET` requests, this makes the development process much more tedious. 

Having the css split into global and page files means that you can change the css for global components (found on one or more pages) and page components (found in a certain html page) separately. 

Additionally, having separate files means that each file is actually manageable and reduces the amount of code repetition, incentivizing shorter class names, increased used of polymorphism and code modularity. 

Lastly, once the site is done (or in a release stable state), there is a chance of me integrating some pre-deployment processing, using `CS` and `JavaScript` aggregators to make a single `styles.css` and `main.js` for deployment. 

# JavaScript documentation (because I will definitely forget)
### How the site handles cross-page shortcuts
So a common user flow is to go from one page to specific point in another, this becomes a problem because the site has a lot of collapsible elements that are closed by default. 
So there needs to be a way for the one page to communicate to the other that the specific element it is redirecting to needs to be opened when the user gets there. 
Ideally, this would also only happen when the user uses this link, and not in any other cases. (no permanence)

How this is implemented: 

functions within `shortcutsHandler.js`: 

- `gotoElement(<element_id>)` is for local shortcuts (same page), where the collapsible being linked to is opened and scrolled to. 

- `openPageElement(<page_name>, <element_id>)` is for the source page to call. 
<br>For example `pageA.html` will call `openPageElement('pageB', 'element0')` and a sessionStorage item will be created to store the information that `pageB_element0_opened` should be `true`. 

- `handleShortcuts(<page_name>)` is for the destination page to call (or more accurately, be bound to onload). 
<br> For example `pageB.html` will have a file called `pageB.js` which has a function `pageBShortcuts()` that calls `handleShortcuts('pageB')`.
<br>`handleShortcuts(<page_name>)` will then go iterate through session storage and try to match the `page_name` with an `_opened` item in sessionStorage. 
<br>Then it will extract the element_id from it and try to open the corresponding element. 
It should then finish off by deleting the sessionStorage item. 



### The rest of this readme file is just notes for where I can get the resources used in the site. 
- The .svg Icons of other companies are from https://icons.getbootstrap.com, this is mainly used for the contact box in contact.html and index.html. 

- The favicon was made with a favicon generator using an svg generated from https://danmarshall.github.io/google-font-to-svg-path/

- The font used globally is JetBrains Mono, obtainable from https://www.jetbrains.com/lp/mono/ or through google's font API https://fonts.google.com/specimen/JetBrains+Mono

