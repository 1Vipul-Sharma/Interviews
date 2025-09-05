1. What is ReactJS - A JS library used for building Single Page Application

   The five main building blocks of React are

   Components: These are reusable blocks of code that return HTML.
   JSX: It stands for JavaScript and XML and allows you to write HTML in React.
   Props and State: props are like function parameters and State is similar to variables.
   Context: This allows data to be passed through components as props in a hierarchy.
   Virtual DOM: It is a lightweight copy of the actual DOM which makes DOM manipulation easier.

2. Props vs State
   Props -

   - The data that is passed from one component to another.Allows us to send data in a component
   - It is immutable
     State -
   - The data that is within the component only
   - It is mutable

3. Virtual DOM -
   It is an in-memory representation of the actual DOM.
   React compares the curr and previous virtual DOM and then make upates in patches to the real DOM

4. JSX(JS XML) -
   BAsically it is a syntax extension for JS used in React . We can return html in jsx file
   before sending to browser it gets converted to JS using Babel.

5. Components -
   These are basically the part of UI . Ui made up of multiple reusable components.
   2 types - functional and class

6. setState() is a method used to update the state of a component. When the state is updated, React re-renders the component and its child components to reflect the changes.
