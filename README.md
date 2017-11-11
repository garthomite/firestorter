<h1 align="center">
  <img src="./logo.jpg"/><br>
  Firestorter
</h1>


Simple & super fast Firestore bindings for React, using Mobx observables.

- **Simple**, easy to use API, get up & running in minutes
- **Fast**, only query and re-render data when needed
- **No clutter**, no complex stores/providers/actions/reducers, just go

![this-thing-really-moves](./this-thing-really-moves.gif)

Because, React `+` Firestore `+` Mobx `===` ❤️


- [Installation](#installation)
- [Usage](#usage)
- [Examples](#examples)
- [Documentation](./docs/API.md)


## Work in progress

*Thank you for checking out this repo in its early stages. This project was 
previously known as `react-firestore-mobx` and is under active development.
Its API may therefore still change a bit as I work out the kinks.
This message will disappear when I feel the API is solid.*


## Installation

	yarn add firestorter
	
*This will automatically install `mobx` and `mobx-react`*

## Usage

```js
import firebase from 'firebase';
import 'firebase/firestore';
import {setFirebaseApp, Collection} from 'firestorter';
import {observer} from 'mobx-react';

// Initialize firebase app
firebase.initializeApp({...});

// Initialize `firestorter`
setFirebaseApp(firebase);

// Create collection and listen for real-time updates
const todos = new Collection('todos');
// note, you can also use references if you like:
// new Collection(firebase.firestore().collection('todos'));

// Observe collection and only re-render when
// documents are added/removed/moved in it.
// Rendering this component automatically causes
// the `todos` collection to start real-time updating.
@observer class Todos extends Component {
	render() {
		return <div>
			{todos.docs.map((doc) => (
				<TodoItem
					key={todo.id}
					doc={doc} />
			))}
		</div>;
	}
}

// Observe doc and re-render when finished or text change.
// Does not re-render when other docs are
// added/removed/updated in the collection.
const TodoItem = observer(({doc}) => {
	const {finished, text} = doc.data;
	return <div>
		<input type='checkbox' checked={finished} />
		<input type='text' value={text} />
	</div>;
});

ReactDOM.render(<Todos />, document.getElementById('root'));
```

## Examples

- [TodoApp](https://rawgit.com/IjzerenHein/firestorter/master/examples/todoApp/build/index.html) ([source](./examples/todoApp/src))


## Documentation

- [API Reference](./docs/API.md)


## Work in progress

Firestoreter is being build as you read this. The essentials are done 
but more functionality and testing is still needed.

Still Todo:

- [ ] Per document fetching
- [ ] Per document real time updates
- [ ] Sub-collections in documents
- [ ] Revise Collection.add
- [ ] Collection.delete()
- [ ] Blobs
- [ ] GeoPoint ?
- [ ] Custom Documents ?
- [ ] Batch updates
- [ ] More testing


## License

[MIT](./LICENSE.txt)
