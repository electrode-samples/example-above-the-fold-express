# example-above-the-fold-express
* This repo is an example express.js app with [Above-the-fold-only-server-render] module fully integrated
* The step-by-step instructions on building it from scratch can be found below

## <a name="express-server"></a>Express Server
* Let's use the [express-react-redux-starter] repo to scaffold our app.
* Create a hapi app using the following commands:

```bash
git clone https://github.com/electrode-samples/express-react-redux-starter.git expressApp
cd expressApp
npm install
```

## <a name="above-the-fold-only-server-render"></a>Above The Fold Only Server Render

[above-the-fold-only-server-render] is a React component for optionally skipping server side rendering of components 
outside above-the-fold (or inside of the viewport). This component helps render your components on the server that are 
above the fold and the remaining components on the client.

[above-the-fold-only-server-render] helps increase performance both by decreasing the load on renderToString and sending
 the end user a smaller amount of markup.

By default, the [above-the-fold-only-server-render] component is an exercise in simplicity; it does nothing and only 
returns the child component.

### Install

* Add the `above-the-fold-only-server-render` component:

```bash
npm install above-the-fold-only-server-render --save
```

* Add the `expressApp/source/components/above-the-fold/above-the-fold.js` file: 

```jsx
import React, { Component } from "react";
import { AboveTheFoldOnlyServerRender } from "above-the-fold-only-server-render";

class AboveTheFold extends Component {
  render() {
    return (
      <div>
        <h3>Above-the-fold-only-server-render: Increase Your Performance</h3>
        <AboveTheFoldOnlyServerRender skip={true}>
          <div className="renderMessage" style={{color: "blue"}}>
            <p>This will skip server rendering if the 'AboveTheFoldOnlyServerRender'
              lines are present, or uncommented out.</p>
            <p>This will be rendered on the server and visible if the 'AboveTheFoldOnlyServerRender'
              lines are commented out.</p>
            <p>Try manually toggling this component to see it in action</p>
            <p>
              <a href="https://github.com/electrode-io/above-the-fold-only-server-render"
                 target="_blank">Read more about this module and see our live demo
              </a>
            </p>
          </div>
        </AboveTheFoldOnlyServerRender>
      </div>
    );
  }
}

export default AboveTheFold;
```

* Add the `above-the-fold` route in `expressApp/source/routes.js`: 

```jsx
import AboveTheFold from "./components/above-the-fold/above-the-fold";

<Route path="above-the-fold" component={AboveTheFold} />
```

* You can tell the component to skip server side rendering either by passing a property: `skip={true}` or by setting up 
`skipServerRender` in your app context and passing the component a `contextKey` `prop`.

* The easiest way to demo this component is actually going to be in your `node_modules` folder. Navigate to 
`expressApp/node_modules/above-the-fold-only-server-render/lib/components/above-the-fold-only-server-render.js` line 29:

```javascript
var SHOW_TIMEOUT = 50;
```

* You are going to change line 29 to slow down the SHOW_TIMEOUT so you can see the component wrapper in action. 
Change this to:

```javascript
var SHOW_TIMEOUT = 3000;
```

* Run the commands below and test it out in your app:

```bash
NODE_ENV=development npm start
```

* Navigate to `localhost:3000/above-the-fold`

* The code in the `<h3>` tag that are above the 
`<AboveTheFoldOnlyServerRender skip={true}></AboveTheFoldOnlyServerRender>` will render first. The contents of 
`<AboveTheFoldOnlyServerRender>` should render on the client side after the `SHOW_TIMEOUT` delay.

[express-react-redux-starter]: https://github.com/electrode-samples/express-react-redux-starter
[Above-the-fold-only-server-render]: https://github.com/electrode-io/above-the-fold-only-server-render