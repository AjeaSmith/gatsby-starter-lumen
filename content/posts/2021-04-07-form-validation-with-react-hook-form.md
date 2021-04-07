---
template: post
title: Form validation with React-Hook-Form
slug: validation-with-react-hook-form
socialImage: /media/reactjs.png
draft: false
date: 2021-04-07T00:33:59.379Z
description: "I've created many projects and during that time I can't remember a
  time when I didn't use some sort of form and had to add validation. "
category: react
tags:
  - frontend
  - react
  - webdev
---
dI've created many projects and during that time I can't remember a time when I didn't use some sort of form and had to add validation. Adding this manually every time can be cumbersome, especially if you have multiple fields. I found a helpful form validation package name React Hook Form, and yes it's based on using hooks since that is commonly used in React. 

We'll create a basic React project to start, then we'll set up a basic login form.

1. Create a basic react app template using `npx create-react-app react-hook-form` and save it to your desired location. It should look bare-bones at the start. 

   ```jsx
   import logo from './logo.svg';
   import './App.css';

   function App() {
     return (
       <div className="App">
         <header className="App-header">
           <img src={logo} className="App-logo" alt="logo" />
           <p>
             Edit <code>src/App.js</code> and save to reload.
           </p>
           <a
             className="App-link"
             href="https://reactjs.org"
             target="_blank"
             rel="noopener noreferrer"
           >
             Learn React
           </a>
         </header>
       </div>
     );
   }

   export default App;
   ```
2. Add the 2 packages we'll need `react-hook-form` , `react-bootstrap`, and `bootstrap`(for quick styling) -> `npm i react-hook-form react-bootstrap bootstrap`
3. Next add the bootstrap css file in your `App.js` file. 

   ```jsx
   import logo from './logo.svg';
   // Added css
   import "bootstrap/dist/css/bootstrap.min.css";
   import './App.css';

   function App() {
     ...
   }
   ```
4. Remove all the content inside `App.js` file and add the form elements (BTW I'm using react bootstrap so you can find these components from the [docs](https://react-bootstrap.netlify.app/components/forms/#forms))

   ```jsx
   import "bootstrap/dist/css/bootstrap.min.css";
   import { Form, Button, Container } from "react-bootstrap";
   import "./App.css";

   function App() {
     return (
       <Container className="App">
         <h2 style={{ marginBottom: "10px", textAlign: "center" }}>Login</h2>
         <Form>
           <Form.Group controlId="formBasicEmail">
             <Form.Label>Email address</Form.Label>
             <Form.Control type="email" placeholder="Enter email" />
             <Form.Text className="text-muted">Error Message</Form.Text>
           </Form.Group>
           <Form.Group controlId="formBasicPassword">
             <Form.Label>Password</Form.Label>
             <Form.Control type="password" placeholder="Password" />
             <Form.Text className="text-muted">Error Message</Form.Text>
           </Form.Group>
           <Button variant="primary" type="submit">
             Submit
           </Button>
         </Form>
       </Container>
     );
   }

   export default App;
   ```

   Be sure to clear everything from the `App.css` file and add

   ```css
   .App {
     margin-top: 50px;
   }
   ```

   Now, it should look like this

   ![](/media/screen-shot-2021-04-04-at-5.54.14-pm.png)

   Let's get to the fun part which is validation :) 

   ```jsx
   // ... other imports
   import { useForm } from "react-hook-form";

   function App() {
     const { register, handleSubmit, formState: {errors} } = useForm({ mode: "onBlur" });
     // ... other code
   }
   ```

   Here we're importing the package. The `useForm` method is a hook and we're extracting all the functions/pieces we need for our form.

   1. **register**, register validations(rules and error messages) to our inputs
   2. **handleSubmit**, function that handles our data when we submit form
   3. **formState: {errors}**, stores our error messages so we can render them later
   4. **mode: "onBlur"** `useForm` method takes optional param which gives us an option to whether we want to handle the validation on form submit or `onBlur`. In my case, I always choose `onBlur`. If you don't pass anything the default is on form submit. 

   Let's add the validation to the email and password inputs.

   ```jsx
   // ... other imports
   import { useForm } from "react-hook-form";

   function App() {
     const { register, handleSubmit, formState: { errors } } = useForm({ mode: "onBlur" });
     return (
       <Container className="App">
         <h2 style={{ marginBottom: "10px", textAlign: "center" }}>Login</h2>
         <Form>
           <Form.Group controlId="formBasicEmail">
             <Form.Label>Email address</Form.Label>
             {/* Added validation*/}
             <Form.Control
               type="email"
               placeholder="Enter email"
               {...register("email", {
                 required: {
                   value: true,
                   message: "Please enter your email address",
                 },
                 pattern: {
                   value: /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$/,
                   message: "Please enter valid email",
                 },
               })}
             />
             <Form.Text className="text-muted">Error Message</Form.Text>
           </Form.Group>
           <Form.Group controlId="formBasicPassword">
             <Form.Label>Password</Form.Label>
             {/* Added validation*/}
             <Form.Control
               type="password"
               placeholder="Password"
               {...register("password", {
                 required: { value: true, message: "Please enter your password" },
                 minLength: {
                   value: 8,
                   message: "Password must be at least 8 characters",
                 },
               })}
             />
             <Form.Text className="text-muted">Error Message</Form.Text>
           </Form.Group>
           <Button variant="primary" type="submit">
             Submit
           </Button>
         </Form>
       </Container>
     );
   }

   export default App;
   ```

   Here, the **register** method has 2 params: a name used to reference the input (helpful when we show error messages), and object where we declare validation rules. --> `register('name', {rules go here})`

   There are many validation rules you can use, but in our case we want the `required` and `pattern` rules for the email input. With each rule, we can add a `value` and `message` prop. 

   For the pattern rule, the `value` prop holds the regex of a valid email address. The `message` prop will hold the error message if the email is invalid. Same process with the password input as well.

   We won't see anything yet because we're not handling the errors if the inputs are invalid.

   ```jsx
   // ... other imports
   import { useForm } from "react-hook-form";

   function App() {
     const {
       register,
       handleSubmit,
       formState: { errors },
     } = useForm({ mode: "onBlur" });
     return (
       <Container className="App">
         <h2 style={{ marginBottom: "10px", textAlign: "center" }}>Login</h2>
         <Form>
           <Form.Group controlId="formBasicEmail">
             <Form.Label>Email address</Form.Label>
             <Form.Control
               type="email"
               placeholder="Enter email"
               {...register("email", {
                 required: {
                   value: true,
                   message: "Please enter your email address",
                 },
                 pattern: {
                   value: /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$/,
                   message: "Please enter valid email",
                 },
               })}
             />
             {/* Added error message */}
             {errors.email && (
               <Form.Text style={{ color: "red" }}>
                 {errors.email.message}
               </Form.Text>
             )}
           </Form.Group>
           <Form.Group controlId="formBasicPassword">
             <Form.Label>Password</Form.Label>
             <Form.Control
               type="password"
               placeholder="Password"
               {...register("password", {
                 required: { value: true, message: "Please enter your password" },
                 minLength: {
                   value: 8,
                   message: "Password must be at least 8 characters",
                 },
               })}
             />
             {/* Added error message */}
             {errors.password && (
               <Form.Text style={{ color: "red" }}>
                 {errors.password.message}
               </Form.Text>
             )}
           </Form.Group>
           <Button variant="primary" type="submit">
             Submit
           </Button>
         </Form>
       </Container>
     );
   }

   export default App;
   ```

   Here, we added the error message (if any) below the inputs. If there is an error from our `errors` object (`errors.email` or `errors.password`), then we render that inputs error message(`errors.password.message`or `errors.email.message`) 

   ![](/media/screen-shot-2021-04-06-at-7.54.47-pm.png)

   ![](/media/screen-shot-2021-04-06-at-7.55.30-pm.png)

   This is what it looks like when the inputs are invalid based on the rules you set for the inputs (on blur). Not only will the error messages will disappear when inputs are valid, they also wont submit if there are invalid as well. The react-hook-form package handles that behind the scenes (awesome). 

   Now that we have validation working, let's see how to handle the submitted data.  

   ```jsx
   function App() {
     const {
       register,
       handleSubmit,
       formState: { errors },
     } = useForm({ mode: "onBlur" });
     {/* Added this */}
     const submitForm = (data) => {
       // submit to DB in real world 
       console.log(data)
     };
     return (
       <Container className="App">
         <h2 style={{ marginBottom: "10px", textAlign: "center" }}>Login</h2>
         {/* Added this */}
         <Form onSubmit={handleSubmit(submitForm)}>
           <Form.Group controlId="formBasicEmail">
             <Form.Label>Email address</Form.Label>
             <Form.Control
               type="email"
               placeholder="Enter email"
               {...register("email", {
                 required: {
                   value: true,
                   message: "Please enter your email address",
                 },
                 pattern: {
                   value: /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$/,
                   message: "Please enter valid email",
                 },
               })}
             />
             {errors.email && (
               <Form.Text style={{ color: "red" }}>
                 {errors.email.message}
               </Form.Text>
             )}
           </Form.Group>
           <Form.Group controlId="formBasicPassword">
             <Form.Label>Password</Form.Label>
             <Form.Control
               type="password"
               placeholder="Password"
               {...register("password", {
                 required: { value: true, message: "Please enter your password" },
                 minLength: {
                   value: 8,
                   message: "Password must be at least 8 characters",
                 },
               })}
             />
             {errors.password && (
               <Form.Text style={{ color: "red" }}>
                 {errors.password.message}
               </Form.Text>
             )}
           </Form.Group>
           <Button variant="primary" type="submit">
             Submit
           </Button>
         </Form>
       </Container>
     );
   }

   export default App;
   ```

   We pass in our function (`submitForm`) to the `handleSubmit` method to handle the data. The `handleSubmit` method formats are data for us behind the scenes, which is awesome. We have access to that formatted data within our function (`submitForm`). At this point we could send it to the backend, in our case we just `console.log` it. 

   ![](/media/screen-shot-2021-04-06-at-8.23.56-pm.png)

Final code: 

```jsx
import "bootstrap/dist/css/bootstrap.min.css";
import { Form, Button, Container } from "react-bootstrap";
import "./App.css";
import { useForm } from "react-hook-form";

function App() {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm({ mode: "onBlur" });
  const submitForm = (data) => {
    console.log(data)
  };
  return (
    <Container className="App">
      <h2 style={{ marginBottom: "10px", textAlign: "center" }}>Login</h2>
      <Form onSubmit={handleSubmit(submitForm)}>
        <Form.Group controlId="formBasicEmail">
          <Form.Label>Email address</Form.Label>
          <Form.Control
            type="email"
            placeholder="Enter email"
            {...register("email", {
              required: {
                value: true,
                message: "Please enter your email address",
              },
              pattern: {
                value: /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$/,
                message: "Please enter valid email",
              },
            })}
          />
          {errors.email && (
            <Form.Text style={{ color: "red" }}>
              {errors.email.message}
            </Form.Text>
          )}
        </Form.Group>
        <Form.Group controlId="formBasicPassword">
          <Form.Label>Password</Form.Label>
          <Form.Control
            type="password"
            placeholder="Password"
            {...register("password", {
              required: { value: true, message: "Please enter your password" },
              minLength: {
                value: 8,
                message: "Password must be at least 8 characters",
              },
            })}
          />
          {errors.password && (
            <Form.Text style={{ color: "red" }}>
              {errors.password.message}
            </Form.Text>
          )}
        </Form.Group>
        <Button variant="primary" type="submit">
          Submit
        </Button>
      </Form>
    </Container>
  );
}
export default App;
```

Resources: [react-hook-form](https://react-hook-form.com/) [react-bootstrap](https://react-bootstrap.netlify.app/)

Thats all for this one folks :) Enjoy!