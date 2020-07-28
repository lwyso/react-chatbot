# React Simple Chatbot How-to Guide

If you are a React developer and what to add some sparks to your web site, why not add a chatbot to interact with your users?


This how-to guide will show you how to create your first react chatbot.

## What you will be creating

In this tutorial, we will use React Simple Chabot to build a simple donut order chatbot.

The final chatbot will look like this:
![Chatbot demo](/donutchatbot-demo.gif)

__In this how-to guide:__

* [Section 1: Create a new react app](#section1)
* [Section 2: Installation](#section2)
* [Section 3: Create a simple chatbot - "Hello World](#section3)
* [Section 4: Design the flow](#section4)
* [Section 5: Steps](#section5)
* [Section 6: Adding Order component](#section6)

---

### <a name="section1"></a> Section 1: Create a new react app

Let's create a new react project using `create-react-app`, in your terminal run:
```bash
# Create a new react app
npx create-react-app donut-chatbot

# Change directory to donut-chatbot
cd donut-chatbot

# Start the project
npm start
```

Once you have run `npm start`, you should see the default React page.

![React App](/react-app.png)

There is an `App.js` file inside the `src` folder. This file contains everything that runs this default react page. Update the content of this file to include a title of our chatbot app.

```javascript
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
      <h1>Donut Chatbot</h1>
    </div>
  );
}

export default App;
```
![React Header](/react-step1.png)

---

### <a name="section2"></a>Section 2: Installation

Two packages are required for this project, `react-simple-chatbot` and `styled-component`, as the styling used for the chatbot are imported from `styled-component`.

To install all dependencies needed to create a simple chatbot, run the following command in your terminal:
```bash
npm install react-simple-chatbot styled-components --save
```
You can check if these are installed by looking through the `dependencies` list in `package.json`.

---

### <a name="section3"></a>Section 3: Create a simple chatbot - "Hello World"

In the `src` folder, create a new folder called `components`. All React components we are going to create will be stored here. In this folder, create two files titled `Donutchatbot.js` and `Order.js`.

`Donutchatbot.js` will handle the chatbot, `Order.js` will handle the order preview.

In `Donutchatbot.js`, create a class component as below:
```javascript
import React, { Component } from 'react';

class Donutchatbot extends Component{

  /* state to be added here */

  render(){

    return(
        <div>
            {/* code to be added here */}
        </div>
    )
  }
}

export default Donutchatbot;
```
__Import required modules__

We need to import `ChatBot` and `ThemeProvider` to get the structure needed for this chatbot, add these to `Donutchatbot.js`.
```javascript
import ChatBot from 'react-simple-chatbot';
import { ThemeProvider } from 'styled-components';
```
__Adding state__

Two pieces of information required to run the chatbot, we specify these in the state. Create a state as below:

```javascript
state = {
    theme : {
        background: '#f5f8fb',
        fontFamily: 'Courier',
        headerBgColor: '#007FFF',
        headerFontColor: '#fff',
        headerFontSize: '15px',
        botBubbleColor: '#007FFF',
        botFontColor: '#fff',
        userBubbleColor: '#fff',
        userFontColor: '#4a4a4a',
    },
      steps : [
        {
          id: '1',
          message: 'Hello World',
          end: true,
        }
    ]
}
```
`theme` sets out the styling for the chatbot such as the colours and font, you can amend these as you wish.

`steps` sets out the flow of the chatbot conversation, you must have an `id` as an identifier for each step. 

`id`, `message`, `end` are keywords which cannot be changed, we will explore other keywords later in this tutorial.

At this stage, we have a message `Hello World`, and then `end` the chatbot.

__Adding components__

Now add `ThemeProvider` and `ChatBot` components in our `return`:
```javascript
return(
    <div>
        <ThemeProvider theme = {this.state.theme}>
            <ChatBot steps = {this.state.steps} />
        </ThemeProvider>
    </div>
)
```

This will take the `theme` we set in the `state` for the styling and `steps` for the flow of the chatbot.

This is how the `Donutchatbot.js` should look like:

<details><summary>expend to see the code</summary>
<p>

```javascript
import React, { Component } from 'react';
import ChatBot from 'react-simple-chatbot';
import { ThemeProvider } from 'styled-components';

class Donutchatbot extends Component{

  state = {
    theme : {
      background: '#f5f8fb',
      fontFamily: 'Courier',
      headerBgColor: '#007FFF',
      headerFontColor: '#fff',
      headerFontSize: '15px',
      botBubbleColor: '#007FFF',
      botFontColor: '#fff',
      userBubbleColor: '#fff',
      userFontColor: '#4a4a4a',
    },
    steps : [
      {
        id: '1',
        message: 'Hello World',
        end: true,
      }
    ]
  }

  render(){

    return(
        <div>
            <ThemeProvider theme = {this.state.theme}>
                <ChatBot steps = {this.state.steps} />
            </ThemeProvider>
        </div>
    )
  }
}

export default Donutchatbot;
```
</p>
</details>

<br>

__Import to App.js__

In App.js, add the following:

```javascript
import Donutchatbot from './components/Donutchatbot';
```

This will import the `Donutchatbot.js` module from `src/components` as `Donutchatbot`.

Call this component by adding `<Donutchatbot />` underneath the title.

This is what `App.js` should look like:

<details><summary>expend to see the code</summary>
<p>

```javascript
import React from 'react';
import './App.css';
import Donutchatbot from './components/Donutchatbot';

function App() {
  return (
    <div className="App">
      <h1>Donut Chatbot</h1>
      <Donutchatbot />
    </div>
  );
}

export default App;
```

</p>
</details>

<br>

__Styling__

Let's add some styling by updating the default `App.css` file.
```css
.App {
  text-align: center;
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
```

__Hello world chatbot__
You have now created a simple chatbot!
![Hello world](/helloworld.png)

---
### <a name="section4"></a>Section 4: Design the flow

Imagine the conversation with the chatbot you are about to create. This is a simplified version of the flow:

![Flow Diagram](/flow-diagram.png)

Once the flow is designed, we can start thinking about the steps following this flow. 

---

### <a name="section5"></a>Section 5: Steps
We must have an `id` for each step, and to identify whether we expect the user to provide some values (e.g. name), check if the user is giving you valid value, or simply provide a list of options for the user to choose from.

Each step will need a `trigger` to identify the next step, this refers to the step `id`.

These `steps` are added to the `state`:
```javascript
state = {
  theme : {/*theme code here*/},
  steps : [/*steps code to be added here*/]
}
```

__Welcome, ask for name__

```javascript
steps: [
  {
    id: '1',
    message: 'What is your name?',
    trigger: 'name',
  },
  {
    id: 'name',
    user: true,
    trigger: '3',
  }, 
  ...
]

```
This will print a message `What is your name?`, once the message is shown, it will trigger the step `id` called `name`. 

In the step with id `name`, we expect the user to provide an input value `name`. This can only be done by setting `user` to `true` to allow user input. Once a name is provided, it will be stored, and then trigger the next step, with an id `3`. 

__Give a selection of donuts to choose from__

```javascript
steps: [
  ...,
  {
    id: '3',
    message: 'Hi {previousValue}! Which donut would you like?',
    trigger: 'selection',
  },
  {
    id: 'selection',
    options: [
      { value: 'original', label: 'Original', trigger: '5' },
      { value: 'chocolate', label: 'Chocolate', trigger: '5' },
      { value: 'jam', label: 'Jam', trigger: '5' },
      { value: 'special', label: 'Special', trigger: '5' },
    ],
  },
  ...
]
```
This will take the user's name as `{previousValue}`, display this as part of the message.

We want to be in control of the available selection of donuts. `options` are used here for the user to choose from. The `trigger` for all options are the same in this case, as this will continue with our flow.

__Ask how many to order__

```javascript
steps: [
  ...,
  {
    id: '5',
    message: 'How many would you like?',
    trigger: 'quantity',
  },
  {
    id: 'quantity',
    user: true,
    trigger: '7',
    validator: (value) => {
        if (isNaN(value)) {
          return 'Please give me a number';
        } else if (value < 1) {
          return 'Minimum order is 1';
        } else if (value > 60) {
          return `${value}? Maximum order is 60!`;
        }
      return true;
    },
  },
  ...
]
```
Once a message is displayed `How many would you like?`, we expect the user to provide a number. `validator` is used here for this purpose. 

A few conditions are set here to ensure that:
* this is a number
* minimum value of 1
* maximum value of 60

Note that it will not trigger step id `7` until a valid number is provided.

__Show order__

```javascript
steps: [
  ...,
  {
    id: '7',
    message: 'Great! This is your order',
    trigger: 'order',
  },
  {
    id: 'order',
    component: <Order/>,
    asMessage: true,
    trigger: 'update',
  },
  ...
]
```
Once all questions are answered, the values will be stored and show the `Order` component, we will set up this component later (in section 6).

__Check order__

```javascript
steps: [
  ...,
  {
    id: 'update',
    message: 'Would you like to update your order?',
    trigger: 'update-question',
  },
  {
    id: 'update-question',
    options: [
      { value: 'yes', label: 'Change order', trigger: 'update-yes' },
      { value: 'no', label: 'Place my order!', trigger: 'end-message' },
    ],
  },
  ...
]
```
This allows the user to update their order if they wish, depending on the `options` chosen, will have a different `trigger`.

__Update order__

```javascript
steps: [
  ...,
  {
    id: 'update-yes',
    message: 'What would you like to update?',
    trigger: 'update-fields',
  },
  {
    id: 'update-fields',
    options: [
      { value: 'selection', label: 'Donut Selection', trigger: 'update-selection' },
      { value: 'quantity', label: 'Quantity', trigger: 'update-quantity' },
    ],
  },
  {
    id: 'update-selection',
    update: 'selection',
    trigger: '7',
  },
  {
    id: 'update-quantity',
    update: 'quantity',
    trigger: '7',
  },
  ...
]
```

Give further `options` of which one to update, once selected, it will `trigger` to the chosen option: `update-selection` or `update-quantity`.

The key `update` will update that value stored, once updated, it will go back to trigger `7`, which we have set above to ask the user to check their order again.

__Complete order__

```javascript
steps: [
  ...,
  {
    id: 'end-message',
    message: 'Thanks! Your order is on its way!',
    end: true,
  }
]
```

This is the final step, with a message and set the `end` to be `true` so the chatbot will no longer be active.

Looking back to our flow diagram to make sure that we have covered every steps:

![Flow Diagram](/flow-diagram-id.png)

This is how the `Donutchatbot.js` should look like:

<details><summary>expend to see the code</summary>
<p>

```javascript
import React, { Component } from 'react';
import ChatBot from 'react-simple-chatbot';
import { ThemeProvider } from 'styled-components';

class Donutchatbot extends Component{

  state = {
    theme : {
      background: '#f5f8fb',
      fontFamily: 'Courier',
      headerBgColor: '#007FFF',
      headerFontColor: '#fff',
      headerFontSize: '15px',
      botBubbleColor: '#007FFF',
      botFontColor: '#fff',
      userBubbleColor: '#fff',
      userFontColor: '#4a4a4a',
    },
    steps : [
      {
        id: '1',
        message: 'What is your name?',
        trigger: 'name',
      },
      {
        id: 'name',
        user: true,
        trigger: '3',
      },
      {
        id: '3',
        message: 'Hi {previousValue}! Which donut would you like?',
        trigger: 'selection',
      },
      {
        id: 'selection',
        options: [
          { value: 'original', label: 'Original', trigger: '5' },
          { value: 'chocolate', label: 'Chocolate', trigger: '5' },
          { value: 'jam', label: 'Jam', trigger: '5' },
          { value: 'special', label: 'Special', trigger: '5' },
        ],
      },
      {
        id: '5',
        message: 'How many would you like?',
        trigger: 'quantity',
      },
      {
        id: 'quantity',
        user: true,
        trigger: '7',
        validator: (value) => {
            if (isNaN(value)) {
              return 'Please give me a number';
            } else if (value < 1) {
              return 'Minimum order is 1';
            } else if (value > 60) {
              return `${value}? Maximum order is 60!`;
            }
          return true;
        },
      },
      {
        id: '7',
        message: 'Great! This is your order',
        trigger: 'order',
      },
      {
        id: 'order',
        component: <Order/>,
        asMessage: true,
        trigger: 'update',
      },
      {
        id: 'update',
        message: 'Would you like to update your order?',
        trigger: 'update-question',
      },
      {
        id: 'update-question',
        options: [
          { value: 'yes', label: 'Change order', trigger: 'update-yes' },
          { value: 'no', label: 'Place my order!', trigger: 'end-message' },
        ],
      },
      {
        id: 'update-yes',
        message: 'What would you like to update?',
        trigger: 'update-fields',
      },
      {
        id: 'update-fields',
        options: [
          { value: 'selection', label: 'Donut Selection', trigger: 'update-selection' },
          { value: 'quantity', label: 'Quantity', trigger: 'update-quantity' },
        ],
      },
      {
        id: 'update-selection',
        update: 'selection',
        trigger: '7',
      },
      {
        id: 'update-quantity',
        update: 'quantity',
        trigger: '7',
      },
      {
        id: 'end-message',
        message: 'Thanks! Your order is on its way!',
        end: true,
      }
    ] 
}

  render(){

    return(
        <div>
            <ThemeProvider theme = {this.state.theme}>
                <ChatBot steps = {this.state.steps} />
            </ThemeProvider>
        </div>
    )
  }
}

export default Donutchatbot;

```
</p>
</details>

<br>

This app is not yet working until `Order` component is added.

---

### <a name="section6"></a>Section 6: Adding Order component

Previously, we added `<Order />` component in step `order`, this component doesn't exist, so we need to create it.
```javascript
steps: [
  ...,
  {
    id: '7',
    message: 'Great! This is your order',
    trigger: 'order',
  },
  {
    id: 'order',
    component: <Order/>,
    asMessage: true,
    trigger: 'update',
  },
  ...
]
```

There are three steps: 
* store the values, 
* display the order, 
* import `Order.js` to `Donutchatbot.js`.

__Order Component__

Earlier, you have created an `Order.js` file inside the `components` directory. This needs to be a class component as we will be storing a `state`.

```javascript
import React, { Component } from 'react';

class Order extends Component{

  /* state and lifecycle to be added here */

  render(){

    return (
      <div style = {{ width: '100%' }}>
        {/* code to be added here */}
      </div>
    );
  }
}

export default Order;
```
__Setting state__

The values we need for the order are `name`, `selection` and `quantity`, set these as `state`:

```javascript
state = {
        name: '',
        selection: '',
        quantity: '',
}
```

__Lifecycle: Component Did Mount__

Lifecycle is used here in `Order.js` before `render()` to mount the `steps` and the values `name`, `selection` and `quantity` when this component is rendered. We also use `setState()` method to add/update the values in due course.

```javascript
componentDidMount() {
  const { steps } = this.props;
  const { name, selection, quantity } = steps;

  this.setState({ name, selection, quantity });
}
```

`this.props` refers to the steps defined in `DonutChatbot.js`. When `Order.js` is rendered, this will `setState` to add the values of `name`, `selection` and `quantity` to the `state`.

If you want to know more about lifecycle, you can read more [here](https://reactjs.org/docs/state-and-lifecycle.html#adding-lifecycle-methods-to-a-class).

__Rendering__

To display all information in a table as below:

```javascript

render(){

  const { name, selection, quantity } = this.state;

  return (
    <div style={{ width: '100%' }}>
        <h3>Your order</h3>
        <table>
            <tbody>
                <tr>
                    <td>Name</td>
                    <td>{name.value}</td>
                </tr>
                <tr>
                    <td>Selection</td>
                    <td>{selection.value}</td>
                </tr>
                <tr>
                    <td>Quantity</td>
                    <td>{quantity.value}</td>
                </tr>
            </tbody>
        </table>
    </div>
  );
}
```

We set `name`, `selection` and `quantity` from `this.state`, and then display these in the table by referring to `name.value`, `selection.value` and `quantity.value` respectively.

`Order.js` should now look like this:

<details><summary>expend to see the code</summary>
<p>

```javascript
import React, { Component } from 'react';

class Order extends Component{

  state = {
    name: '',
    selection: '',
    quantity: '',
  }
  componentDidMount() {
    const { steps } = this.props;
    const { name, selection, quantity } = steps;

    this.setState({ name, selection, quantity });
  }

  render(){

    const { name, selection, quantity } = this.state;

    return (
      <div style = {{ width: '100%' }}>
        <h3>Your order</h3>
        <table>
            <tbody>
                <tr>
                    <td>Name</td>
                    <td>{name.value}</td>
                </tr>
                <tr>
                    <td>Selection</td>
                    <td>{selection.value}</td>
                </tr>
                <tr>
                    <td>Quantity</td>
                    <td>{quantity.value}</td>
                </tr>
            </tbody>
        </table>
      </div>
    );
  }
}

export default Order;
```

</p>
</details>
<br>

__Import Order Component__

`Order.js` is all set, this must now to be imported to `Donutchatbot.js`:

```javascript
import Order from './Order';
```

`Donutchatbot.js` should now look like this:

<details><summary>expend to see the code</summary>
<p>

```javascript
import React, { Component } from 'react';
import ChatBot from 'react-simple-chatbot';
import { ThemeProvider } from 'styled-components';
import Order from './Order';

class Donutchatbot extends Component{

  state = {
    theme : {
      background: '#f5f8fb',
      fontFamily: 'Courier',
      headerBgColor: '#007FFF',
      headerFontColor: '#fff',
      headerFontSize: '15px',
      botBubbleColor: '#007FFF',
      botFontColor: '#fff',
      userBubbleColor: '#fff',
      userFontColor: '#4a4a4a',
    },
    steps : [
      {
        id: '1',
        message: 'What is your name?',
        trigger: 'name',
      },
      {
        id: 'name',
        user: true,
        trigger: '3',
      },
      {
        id: '3',
        message: 'Hi {previousValue}! Which donut would you like?',
        trigger: 'selection',
      },
      {
        id: 'selection',
        options: [
          { value: 'original', label: 'Original', trigger: '5' },
          { value: 'chocolate', label: 'Chocolate', trigger: '5' },
          { value: 'jam', label: 'Jam', trigger: '5' },
          { value: 'special', label: 'Special', trigger: '5' },
        ],
      },
      {
        id: '5',
        message: 'How many would you like?',
        trigger: 'quantity',
      },
      {
        id: 'quantity',
        user: true,
        trigger: '7',
        validator: (value) => {
            if (isNaN(value)) {
              return 'Please give me a number';
            } else if (value < 1) {
              return 'Minimum order is 1';
            } else if (value > 60) {
              return `${value}? Maximum order is 60!`;
            }
          return true;
        },
      },
      {
        id: '7',
        message: 'Great! This is your order',
        trigger: 'order',
      },
      {
        id: 'order',
        component: <Order/>,
        asMessage: true,
        trigger: 'update',
      },
      {
        id: 'update',
        message: 'Would you like to update your order?',
        trigger: 'update-question',
      },
      {
        id: 'update-question',
        options: [
          { value: 'yes', label: 'Change order', trigger: 'update-yes' },
          { value: 'no', label: 'Place my order!', trigger: 'end-message' },
        ],
      },
      {
        id: 'update-yes',
        message: 'What would you like to update?',
        trigger: 'update-fields',
      },
      {
        id: 'update-fields',
        options: [
          { value: 'selection', label: 'Donut Selection', trigger: 'update-selection' },
          { value: 'quantity', label: 'Quantity', trigger: 'update-quantity' },
        ],
      },
      {
        id: 'update-selection',
        update: 'selection',
        trigger: '7',
      },
      {
        id: 'update-quantity',
        update: 'quantity',
        trigger: '7',
      },
      {
        id: 'end-message',
        message: 'Thanks! Your order is on its way!',
        end: true,
      }
    ] 
}

  render(){

    return(
        <div>
            <ThemeProvider theme = {this.state.theme}>
                <ChatBot steps = {this.state.steps} />
            </ThemeProvider>
        </div>
    )
  }
}

export default Donutchatbot;

```

</p>
</details>
<br>

---

### Final app

All done. This is the complete app.

![Chatbot demo](/donutchatbot-demo.gif)

### What's next?

There are more you can do with this chatbot, for example:
* Store the steps in a JSON and fetch this via an API call
* Add Speech Recognition to support user accessibility.
* Connect to the server and database so you can actually place an order.
* and many more.


---

__Checkout their documentation:__ [Chatbot documentation](https://lucasbassetti.com.br/react-simple-chatbot/#/)