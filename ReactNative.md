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
    renderItem={({ item }) => (
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


# React Native Flexbox

- `View` components use flexbox under the hood

`flex: 1` - the "growth" rate, how much space the items take up

- Everything inside the flex container is now a flex item, taking up all available width

# Expo Async

```js
const [fontsLoaded, setFontsLoaded] = useState(false);

if(fontsLoaded) {
  return (
    <Home />
  )
} else {
  return (
    <AppLoading
    startAsync={getFonts}
    onFinish={() => setFontsLoaded(true)}
  )
}
```

- A smart way to deal with asynchronous code using the `useState` hook
- In this example, we are waiting for fonts to load through `getFonts`
- Until the fonts are loaded, we use the Expo `AppLoading` component which `onFinish` loads the desired `Home` component

# Global Styles

- Create styles in modules

```js
// styles/global.js
import { StyleSheet } from 'react-native';

export const globalStyles = StyleSheet.create({
    // styles here
})
```

```js
import { globalStyles } from '...'
```

# [React Navigation](https://reactnavigation.org/docs/getting-started)

## Stack Navigation

- Push/pop screens on a stack

```js
import { NavigationContainer } from '@react-navigation/native'
import { createStackNavigator } from '@react-navigation/stack';
// ... imports for Home, About

const Stack = createStackNavigator();

export const Routes = () => {
    return (
        <NavigationContainer>
                <Stack.Navigator>
                // renders home by default - on top of stack
                    <Stack.Screen name="Home" component={Home} />
                    <Stack.Screen name="About" component={About} />
                </Stack.Navigator>
        </NavigationContainer>
    );
};

export default Routes;
```

## Navigating between screens

- Every screen we configure automatically gets a navigation prop

```js
const { navigation } = props;

navigation.navigate('Home');
navigation.push('Home');

navigation.goBack();
```

- In this example, we want to navigate to whatever component `Home` has as its screen

### `.push` 

- Always pushes the route on top of the stack

### `.navigate`

-  Will pop back to earlier in the stack if a component is already mounted there

### `.goBack()`

- Pops screen of the stack

## Passing data between screens

```js
navigation.navigate('Home', {name: 'danny', cool: true})
```

- Can send parameters of data as a second parameter

### `route.params`

```js
// component takes in { route } as a prop
const { name, cool } = route.params;
<Text>{ navigation.getParam('name')}</Text>
```

- Pass in the key that you want to access from the passed in parameters

# Drawer Navigation

```js
import { createDrawerNavigator } from '@react-navigation/drawer';
import { NavigationContainer } from '@react-navigation/native';

const Drawer = createDrawerNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Drawer.Navigator initialRouteName="Home">
        <Drawer.Screen name="Home" component={HomeScreen} />
        <Drawer.Screen name="About" component={AboutScreen} />
      </Drawer.Navigator>
    </NavigationContainer>
  );
}
```

# Custom Card Components

```js
export default function Card(props) {
  return (
    <View style={styles.card}>
        <View style={styles.cardContent}>
            { props.children }
        </View>
    </View>
  )
}
```

```html
<Card>
    <Text>hello</Text>
    <Text>hey there</Text>
</Card>
```

- `props.children` are similar to slots in Vue
    - It passes in the nested elements into the Native component

# Images

```html
<Image source={require('url')} />
<Image source={image} /> - image variable

<ImageBackground source={require('url')}>
    Wrapped Components
</ImageBackground>
```

# Modals

- Pop up windows

```js
<Modal visible={modalOpen} animationType='slide'>
    <Button onPress={() => setModalOpen(false)} />
    Wrapped Components
</Modal>
```

- Visibility is bound to `modalOpen` state boolean
    - Combined with the `useState` hook, we can use `setModalOpen` to open/close the modal
- Animation is set to `slide`

# Formik Forms

```js
import { Formik } from 'formik';

<Formik
    initialValues={{ title: '', body: '' }}
    onSubmit={(values, actions) => {
      actions.resetForm();
      function(values);
    }}
>
    {(formikProps) => (
      <View>
        <TextInput 
            placeholder="Title"
            onChangeText={formikProps.handleChange('title')}
            value={formikProps.values.title}
        />
        <Button title="Submit"onPress={formikProps.handleSubmit} />
      </View>
    )}
</Formik>
```

- The `values` parameter represents the values in the form fields as an object
- Inside the `<Formik>` tags we create the form fields inside a `render` function returning JSX
- `formikProps` include helpful functions provided by Formik
- `.handleChange()` takes in the value we want to change
    - In the `values` prop for `onSubmit`, we update 
- The `value` of the `<TextInput>` is also `values.title` (2 way binding)
- `formikProps.handleSubmit` runs the `onSubmit` function for us
- `actions.resetForm()` resets fields
