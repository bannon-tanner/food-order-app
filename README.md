# Food Order App

This project is a practice project from [React - The Complete Guide (incl Hooks, React Router, Redux)](https://www.udemy.com/course/react-the-complete-guide-incl-redux/)

## Building the Header

- Need actual header (with cart icon) and the image below
  - Has a Page Title and the cart icon (as a button) - header section
  - Has the image below - img section (within div)
- Problem with the supplied `.header` styling, pushes button off screen
  - Seems that the `position: fixed` css rule along with `top: 0; left: 0` and `padding: 0 10%` is causing the header element to compensate the padding width into a negative `right` position
  - This was caused by starting my own project and not copying over the `index.css` stylings from the starting-project
    - The actual rule that fixed it was
    ```css
    * {
      box-sizing: border-box;
    }
    ```
    - Without this rule, the padding on a fixed element causes the position to compensate
- Can use spans inside of buttons to add multiple content

## Adding Meals section

- Created AvailableMeals first as the dummy-meals information was supplied
- Created MealItem which holds the information from the dummy-meals.js and also the form for each item to add things to the cart
- Created MealItemForm which holds the input/label and a button to add things to cart
  - Set defaultValue for input to 1
- Created Input component for the amount/label that is needed in each meal
  - This component is also built to be reusable if another part of the app would need it, not sure at time of creation if that is needed
- Created Card component to add styling provided and used AvailableMeals as child
- Too big of a space on the name/description/price in MealItem component
  - Seems as if semantically the structure is wrong
  - Changing the `<p></p>` tags to `<div></div>` seemed to do the trick
- Added Meals.js as recommended by instructor
  - This really just causes one less import in App.js

## Adding Checkout / Order Form

- clicking order button expands modal with form for user information
- has confirm and cancel buttons
  - cancel closes modal
  - confirm orders food
- validate user input
  - show errors on invalid input
  - submit to server on valid submission

## Submit Orders to Backend Server (Http)

- send the checkout form data back to the cart
- should always validate incoming data on the server as well, because the JS on the client can be edited and validation bypassed
- send order to firebase passing the submitOrderHandler to the Checkout component
- show different JSX depending on submission state
- clear cart when order is submitted, by adding a new action to the CartProvider

## Fetch Meals Data

- Manually added meals dummy data to the firebase realtime database
- in AvailableMeals component, fetch the data from firebase
- use useEffect with a custom async function inside of it to be able to await the data
  - then set the state for the meals
- added logic/jsx for loading data
- moved cumbersome meals list out of JSX into a constant
- added error handling, that displays error instead of JSX
- moved the call to fetchMeals into a try/catch block
  - actually chain `.catch()` to the end of the function call so that don't have to wrap that function in another async call
