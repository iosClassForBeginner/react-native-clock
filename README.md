# react-native-clock
<h2>shows clock with background changer</h2>

<img src="https://media.giphy.com/media/3ohhwG0IaQkhD0YvJu/giphy.gif" />
<br>

code 
★ It's preferable to write following code yourself. It will help you to understand code more.

``` Style sheet
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center'
  },
  imageBackground: {
    flex: 1,
    width: '100%',
    justifyContent: 'space-around',
    alignItems: 'center'
  },
  btnContainer: {
    width:200,
    flex: 1,
  },
  timer: {
    flex: 1,
    backgroundColor: 'transparent',
    fontSize: 30,
    marginTop: 150,
    alignSelf: 'center'
  },
  botton: {
    color: "#841584",
    marginTop: 50,
    height: 100,
    borderRadius: 30
  }
});



``` code
```
import React from 'react';
import { StyleSheet, Text, View, Image} from 'react-native';
 //add momentjs to our app
import moment from 'moment'
//add button component to our app
import Button from 'react-native-button';

// make an object of images 
const image ={
  sunny: require('./images/sunny.jpg'),
  night: require('./images/bg.jpg')
}


export default class App extends React.Component {
//intiallizer
  constructor () {
    super();
    this.state = {
      backgroundName: 'sunny',
      time: moment().format('LTS'),
      color: true
    };
  }
  // funtion for changing background 
  handlePress () {
    console.log(this.state.backgroundName);
    if (this.state.backgroundName === 'sunny') {
      this.setState({backgroundName: 'night', color: false});
    } else {
      this.setState({backgroundName: 'sunny', color: true});
    }
  }
  
  // react life cicle component this function will excute when the application is run 
  componentDidMount(){
    setInterval(()=>{
      this.setState({ time: moment().format('LTS')  })

    }),1000
  }
  
  render () {
  
    const fontColor = this.state.color == true ? "black" : "white"
    // Destructuring time 
    const time = moment().format('LTS')
    return (
      <View style={styles.container}>
        <Image
          style={styles.imageBackground}
          source={image[this.state.backgroundName]}
          >
          <View style={{flex: 1}}>
                <Text style= {styles.timer}>
                  {this.state.time}
                </Text>
          </View>
          <View style={styles.btnContainer}>
            <Button
              style={styles.button}
              containerStyle={{padding:10, height:45, overflow:'hidden', borderRadius:4, backgroundColor: 'white'}}
              onPress={() => this.handlePress()}
              >
                  change background
              </Button>
          </View>
        </Image>

      </View>
    );
  }
}

