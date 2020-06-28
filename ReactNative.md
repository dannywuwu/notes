# Views, Text, Styles

### `import { StyleSheet, Text, View } from 'react-native'`

### `<View>`

- `div` components

### `Text`

- Text components

### `style`

- Pass in as a prop to style components
- Set equal to an object containing CSS properties

```html
    <View style={styles.container}>
      ...
    </View>
```

```js
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});
```

- **Container styles will not be inherited**
    - ex. body container has font weight bold, text inside container are unaffected
    - however, nested `Text` components will inherit parent styles

# Text Input

```js
<TextInput 
  placeholder='name'
  onChangeText = {(val) => {setName(val)}}
  multiline
  keyboardType='numeric'
  ></TextInput>
```

- `placeholder` is the default text in input field
- `onChangeText` fires on input change and automatically takes in the value in the text field - `val` in this case
- `multiline` expands the text field on enter keypress
- `keyboardType` changes keyboard input type

# ScrollView + Lists

```html
<ScrollView>
  {people.map((person, index) => (
      <View key={index}>
        <Text style={styles.item}>{person.name}</Text>
      </View>
    )
  )}
</ScrollView>
```

- Output a list
- The list is very long so we need to wrap it with the `ScrollView` component in order to scroll down

## `FlatList`

```js
<FlatList 
    keyExtractor={(item) => item.id}
    data={people}
    renderItem={({item}) => (
      //jsx
      <Text style={styles.item}>{item.name}</Text>
    )}
/>
```

- `data` specifies output data
- `renderItem` is a function that returns JSX
    - Takes in a destructured item which represents the value in the array item we are outputting
- No key required: automatically checks for a `key` property in the object
- `keyExtractor` lets you choose which property will be used as the key (in this case we use the `id` property)
- All items are not immediately rendered, more load as you scroll down
- Best for lists of data

# Touchable Components

```js
<TouchableOpacity onPress={() => pressHandler(item.id)}>
  <Text style={styles.item}>{item.name}</Text>
</TouchableOpacity>
```
- Turn any component into a button and perform actions with `onPress`

# Alerts

```js
Alert.alert('Title', 'body', [
  {text: 'button', onPress: () => console.log('alert closed')}
]);
```

- Shows an alert popup

# Closing the keyboard

- Close the keyboard on touch the app body
- Wrap the entire container with a touchable component

```js
<TouchableWithoutFeedback onPress={() => Keyboard.dismiss()}>
    <View>
        main container view
    </View>
</TouchableWithoutFeedback>
```

- `keyboard.dismiss()` dismisses the keyboard


