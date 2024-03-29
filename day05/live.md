# Image Background Example

```js
import React from 'react';
import { ImageBackground, StyleSheet, Text, View , Button} from 'react-native';

const image = {
  uri: 'https://cdn.pixabay.com/photo/2016/06/02/02/33/triangles-1430105_1280.png',
};

const App = () => (
  <View style={styles.container}>
    <ImageBackground source={image} resizeMode="cover" style={styles.image}>
      <View style={styles.insideContainer}>
        <Text style={styles.text}>App With background Image</Text>
        <View style={{flexDirection:'row', justifyContent:'center', gap:20}}>
         <Button title="Ok" /> <Button title="Cancel" /> 
        </View>
      </View>
    </ImageBackground>
  </View>
);

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  insideContainer:{
    backgroundColor: '#000000c0',
    padding:40
  },
  image: {
    flex: 1,
    justifyContent: 'center',
  },
  text: {
    color: 'white',
    fontSize: 42,
    lineHeight: 84,
    fontWeight: 'bold',
    textAlign: 'center',

  },
});

export default App;
```
# Linking Example

```js
import React, { useCallback } from 'react';
import { Alert, Button, Linking, StyleSheet, View } from 'react-native';

const supportedURL =
  'https://play.google.com/store/apps/details?id=com.Slack&hl=en&gl=US';
  const whatsAppUrl = "https://wa.me/+919999988888?text=Hi, Contacting from your app"

const unsupportedURL = 'slack://open?team=123456';

const OpenURLButton = ({ url, children }) => {
  const handlePress = useCallback(async () => {
    // Checking if the link is supported for links with custom URL scheme.
    const supported = await Linking.canOpenURL(url);

    if (supported) {
      // Opening the link with some app, if the URL scheme is "http" the web link should be opened
      // by some browser in the mobile
      await Linking.openURL(url);
    } else {
      Alert.alert(`Don't know how to open this URL: ${url}`);
    }
  }, [url]);

  return <Button title={children} onPress={handlePress} />;
};

const App = () => {
  return (
    <View style={styles.container}>
      <OpenURLButton url={supportedURL}>Please Rate Us</OpenURLButton>
      <OpenURLButton url={whatsAppUrl}>Whats app us</OpenURLButton>
      <OpenURLButton url={unsupportedURL}>Open Unsupported URL</OpenURLButton>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
});

export default App;
```

# FlatList Example

```js
import React from 'react';
import {
  SafeAreaView,
  View,
  FlatList,
  StyleSheet,
  Text,
  StatusBar,
} from 'react-native';

const DATA = [
  {
    id: 'bd7acbea-c1b1-46c2-aed5-3ad53abb28ba',
    title: 'First Item',
  },
  {
    id: '3ac68afc-c605-48d3-a4f8-fbd91aa97f63',
    title: 'Second Item',
  },
  {
    id: '58694a0f-3da1-471f-bd96-145571e29d72',
    title: 'Third Item',
  },
  {
    id: '58694a0f-3da1-471f-bd96-145571e29d72',
    title: 'Fourth Item',
  },
  {
    id: '58694a0f-3da1-471f-bd96-145571e29d72',
    title: 'Fifth Item',
  },
  {
    id: '58694a0f-3da1-471f-bd96-145571e29d72',
    title: 'Sixth Item',
  },
  {
    id: '58694a0f-3da1-471f-bd96-145571e29d72',
    title: 'Seventh Item',
  },
  {
    id: '58694a0f-3da1-471f-bd96-145571e29d72',
    title: 'Eighth Item',
  },
  {
    id: '58694a0f-3da1-471f-bd96-145571e29d72',
    title: 'Nineth Item',
  },
  {
    id: '58694a0f-3da1-471f-bd96-145571e29d72',
    title: 'Tenth Item',
  },
  {
    id: '58694a0f-3da1-471f-bd96-145571e29d72',
    title: 'Eleventh Item',
  },
  {
    id: '58694a0f-3da1-471f-bd96-145571e29d72',
    title: 'Tweleveth Item',
  },
  {
    id: '58694a0f-3da1-471f-bd96-145571e29d72',
    title: 'Thirteenth Item',
  },
  {
    id: '58694a0f-3da1-471f-bd96-145571e29d72',
    title: 'Fourteenth Item',
  },
];

const Data1 = [];

const Item = ({ title }) => (
  <View style={styles.item}>
    <Text style={styles.title}>{title}</Text>
  </View>
);

const App = () => {
  return (
    <SafeAreaView style={styles.container}>
      <FlatList
        data={DATA}
        numColumns={3}
        ItemSeparatorComponent={() => (
          <View
            style={{
              height: 10,
              width: '100%',
              backgroundColor: 'green',
            }}></View>
        )}
        ListHeaderComponent={() => (
          <View
            style={{
              width: '100%',
              padding: 30,
              backgroundColor: 'green',
            }}>
            <Text style={{ color: '#FFFFFF', fontSize: 45, textAlign:'center' }}>
              This is Header
            </Text>
          </View>
        )}
        ListEmptyComponent={() => (
          <View
            style={{
              width: '100%',
              padding: 30
            }}>
            <Text style={{ color: 'red', fontSize: 45, textAlign:'center' }}>
              List is Empty 
            </Text>
          </View>
        )}
        renderItem={({ item }) => <Item title={item.title} />}
        keyExtractor={(item) => item.id}
      />
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    marginTop: StatusBar.currentHeight || 0,
  },
  item: {
    flex:1,
    backgroundColor: '#f9c2ff',
    padding: 10,
    marginVertical: 8,
    marginHorizontal: 16,
  },
  title: {
    fontSize: 15,
  },
});

export default App;
```

## Section List With Columns

```js
import React from 'react';
import {
  StyleSheet,
  Text,
  View,
  SafeAreaView,
  SectionList,
  StatusBar,
  FlatList,
} from 'react-native';

const DATA = [
  {
    title: 'Main dishes',
    data: [{ list: ['Pizza', 'Burger', 'Risotto'] }],
  },
  {
    title: 'Sides',
    data: [{ list: ['French Fries', 'Onion Rings', 'Fried Shrimps'] }],
  },
  {
    title: 'Drinks',
    data: [{ list: ['Water', 'Coke', 'Beer'] }],
  },
  {
    title: 'Desserts',
    data: [{ list: ['Cheese Cake', 'Ice Cream'] }],
  },
];

const App = () => (
  <SafeAreaView style={styles.container}>
    <SectionList
      sections={DATA}
      keyExtractor={(item, index) => item + index}
      renderItem={({ item }) => (
        <FlatList
          data={item.list}
          numColumns={2}
          renderItem={({ item }) => (
            <Text
              style={{
                flex: 1,
                backgroundColor: 'red',
                padding: 10,
                marginHorizontal: 10,
                marginVertical: 2,
              }}>
              {item}
            </Text>
          )}
        />
      )}
      renderSectionHeader={({ section: { title } }) => (
        <Text style={{ textAlign: 'center', fontSize: 24, color: 'green' }}>
          {title}
        </Text>
      )}
    />
  </SafeAreaView>
);

const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: StatusBar.currentHeight,
    marginHorizontal: 16,
  },
});

export default App;
```

