# Notes App
- Start view
![1](https://user-images.githubusercontent.com/77986239/222265365-1997463c-fe48-4d4a-b5e4-26725078214a.PNG)

- Edit View
![2](https://user-images.githubusercontent.com/77986239/222265380-2e909ce6-5a93-4567-975f-33d78d251f5c.PNG)

- Preview View
![3](https://user-images.githubusercontent.com/77986239/222265395-e21f2f53-6180-4ae5-a68c-fb45fcbaf3e2.PNG)

## Quick Setup
1. Fork then clone the project into local machine 🍴
1. run 'npm install' in the root folder to install all the necessary packages 👩‍💻
1. Might have to run **npm install react-mde --force**  since it refuses to install
1. Happy coding 💻

* Dependencies used: react-mde, nanoid, showdown, react-split

### Check if an element exists before accessing its property
- initialize the state either as the id of the very first note or an empty string and ensure notes at index of 0 exists before i try to access the id property of that note.
```jsx
    const [currentNoteId, setCurrentNoteId] = React.useState(
        (notes[0] && notes[0].id) || ""
    )
```

### Lazy state initilaization
- How we are initializing from state when we pull from local storage since it is expensive to get item from localstorage every time state changes then triggering a re-render. It takes more effort for browser to dip into local storgae and get something every single state change, so react has implemented a way  for us to easily make it so that any expensive code that might be running inside our state initialization can happen only once - this is called lazy state initialization.
- With every change, every code is run again even if the component doesn't use the value so with lazy state initialization we can prevent some codes from running with every render.
- With it instead of providing a value, I can  provide a function that returns a value
```jsx
    //If this code is added in App.jsx 
    //not lazy would run with every minor change e,g creating new note, editing etc
    const [state, setState] = (React.useState(console.log("State initialization")))

    // lazy state initialization will run only once not when chnages are made
    const [state, setState] = (React.useState(()=>(console.log("State initialization"))))

    // Lazy State initialization - will only reach into localStorage the first time the app loads
    const [notes, setNotes] = React.useState(()=>(JSON.parse(localStorage.getItem("notes")) || []))
```

> Connect to db
