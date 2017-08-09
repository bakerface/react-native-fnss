# react-native-fnss
[![npm version](https://badge.fury.io/js/react-native-fnss.svg)](http://badge.fury.io/js/react-native-fnss)
[![downloads](http://img.shields.io/npm/dm/react-native-fnss.svg)](https://www.npmjs.com/package/react-native-fnss)

This package is used to provide extensible, functional styling to your React
Native applications by wrapping the React Native components with
[fnss](https://www.npmjs.com/package/fnss).

``` javascript
import React from 'react';
import * as StyleSheet from 'fnss';
import { Text, View } from 'react-native-fnss';

// these are helper functions used to derive styles
// from props passed to the StyleSheet provider
const rem = (n = 1) => ({ rem = 16 }) => n * rem;
const primary = ({ primary = 'black' }) => primary;
const secondary = ({ secondary = 'white' }) => secondary;

const styles = StyleSheet.create({
  container: {
    // these are simple styles like you would use normally
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',

    // this will pull the `secondary` prop from the provider
    // and default to `white` if one is not provided
    backgroundColor: secondary
  },
  text: {
    // this will pull the `primary` prop from the provider
    // and default to `black` if one is not provided
    color: primary,

    // this will pull the `rem` prop from the provider
    // and default to `16` if one is not provided
    // then return twice the rem value
    fontSize: rem(2)
  }
});

export default class App extends React.Component {
  render() {
    return (
      <StyleSheet.Provider rem={10} primary="blue" secondary="gray">
        <View style={styles.container}>
          <Text style={styles.text}>
            Hello world
          </Text>
        </View>
      </StyleSheet.Provider>
    );
  }
}
```
