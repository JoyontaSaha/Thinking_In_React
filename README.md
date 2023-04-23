# React App: Thinking in React

This project is a sample app to demonstrate the thinking process behind building a React app. The steps to build the app are as follows:

Step 1: Break the UI into a component hierarchy
![Alt Text](https://react.dev/images/docs/s_thinking-in-react_ui_outline.png)

Step 2: Build a static version in React
Either build “top down” by starting with building the components higher up in the hierarchy (like FilterableProductTable) or “bottom up” by working from components lower down (like ProductRow). In simpler examples, it’s usually easier to go top-down, and on larger projects, it’s easier to go bottom-up.

Step 3: Find the minimal but complete representation of UI state
The most important principle for structuring state is to keep it DRY (Don’t Repeat Yourself). Figure out the absolute minimal representation of the state your application needs and compute everything else on-demand. For example, if you’re building a shopping list, you can store the items as an array in state. If you want to also display the number of items in the list, don’t store the number of items as another state value—instead, read the length of your array.

All of the pieces of data in this example application:

The original list of products
The search text the user has entered
The value of the checkbox
The filtered list of products
Which of these are state? Identify the ones that are not:

Does it remain unchanged over time? If so, it isn’t state.
Is it passed in from a parent via props? If so, it isn’t state.
Can you compute it based on existing state or props in your component? If so, it definitely isn’t state!
What’s left is probably state.

Let’s go through them one by one again:

The original list of products is passed in as props, so it’s not state.
The search text seems to be state since it changes over time and can’t be computed from anything.
The value of the checkbox seems to be state since it changes over time and can’t be computed from anything.
The filtered list of products isn’t state because it can be computed by taking the original list of products and filtering it according to the search text and value of the checkbox.
This means only the search text and the value of the checkbox are state!

Step 4: Identify where your state should live
For each piece of state in the application:

Identify every component that renders something based on that state.
Find their closest common parent component—a component above them all in the hierarchy.
Decide where the state should live:
Often, you can put the state directly into their common parent.
You can also put the state into some component above their common parent.
If you can’t find a component where it makes sense to own the state, create a new component solely for holding the state and add it somewhere in the hierarchy above the common parent component.
In the previous step, you found two pieces of state in this application: the search input text, and the value of the checkbox. In this example, they always appear together, so it makes sense to put them into the same place.

Now let’s run through our strategy for them:

Identify components that use state:
ProductTable needs to filter the product list based on that state (search text and checkbox value).
SearchBar needs to display that state (search text and checkbox value).
Find their common parent: The first parent component both components share is FilterableProductTable.
Decide where the state lives: We’ll keep the filter text and checked state values in FilterableProductTable.
So the state values will live in FilterableProductTable.e.

## Step 5: Add Inverse Data Flow

Finally, you need to add inverse data flow to allow child components to update the state of their parent components. In this app, the state is owned by the FilterableProductTable component, so only it can update the state. To allow the SearchBar component to update the state, you need to pass the setFilterText and setInStockOnly functions down to the SearchBar component.

This project was bootstrapped with Create React App. To run the app in development mode, run `npm start` in the project directory. This will open the app in your browser at http://localhost:3000. To launch the test runner in interactive watch mode, run `npm test`. To build the app for production, run `npm run build`. This will create a production-ready version of the app in the `build` directory. If you're not satisfied with the build tool and configuration choices, you can eject at any time using `npm run eject`. Note that this is a one-way operation, and once you eject, you can't go back.
