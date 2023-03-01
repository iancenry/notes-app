# Notes App
npm install showdown react-split nanoid showdown
npm install react-mde --force  - use this since refuses to install

### Dependencies
react mde  - a markdown editor
nanoid - generate ids
showdown - transform markdown to html on client-side

### Check if an element exists before accessing its property
- initialize the state either as the id of the very first note or an empty string and ensure notes at index of 0 exists before i try to access the id property of that note.
```jsx
    const [currentNoteId, setCurrentNoteId] = React.useState(
        (notes[0] && notes[0].id) || ""
    )
```

### Lazy state initilaization
- Without it
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

> Connect with db


    function updateNote(text) {
 
        // setNotes(oldNotes => {
        //     let newNotesArray = [];
        //     for (const note of oldNotes) {
        //         if(note.id === currentNoteId){
        //             newNotesArray.unshift({ ...note, body: text })
                    
        //         }else{
        //             newNotesArray.push(note)
        //         }
                
        //     }
        //     return newNotesArray            

        // })

        setNotes(oldNotes => oldNotes.map(oldNote => {
            return oldNote.id === currentNoteId
                ? { ...oldNote, body: text }
                : oldNote
        }))
    }
