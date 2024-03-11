---
title: React Tutorial - Creating a simple weather app using React and Material UI
published: true
Tags: ["programming","react"]
date: 2021-06-15
image: /images/images-wim-van-t.png
description: We'll make a weather app with the react js material UI framework in this article.
keywords: react,reactjs,React,weather,app,API,material,ui,tutorial,openweathermap,App.js,implemnentation,creating
---

# React Tutorial - Creating weather App using Material UI

In this article we will be building a weather app using react js material UI framework. We will also be using [openweathermap](https://openweathermap.org/) API for fetching the weather data from the site.

The idea is simple we are going to create a **Card** component which will consists of a **TextField** where the user can write the name of the city.

After getting the name of the city from input field we will then fetch this to our [openweathermap](https://openweathermap.org/) API. If every thing goes right this API will give respone of weatherReport in **json** format or else it will give error.

Then we will only take the values which we will be needing for our App from json respone. And finally we are going to diplay that value.

Now without further due let's build our App.

## Implementation

We will build three components :

- ` App.js` : This component will take input from the user and pass that value to `weatherAPI` components as prop.
- `weatherAPI.js` : This component will take the value from `App.js` and fetch it to [openweathermap](https://openweathermap.org/) API. After getting respone the json object is passed throung our `Display` components.
- `weatherReportDisplay` : This component simply dislay the weather information.

Now let's start by writing our first component:

**App.js**

```javascript
import React from "react";
import Grid from "@material-ui/core/Grid";
import Card from "@material-ui/core/Card";
import { makeStyles } from "@material-ui/core/styles";
import CardContent from "@material-ui/core/CardContent";
import TextField from "@material-ui/core/TextField";
import WeatherAPI from "./weatherAPI";
import bgImg from "./images/bg-img.jpg";

const style = makeStyles((theme) => ({
  root: {
    marginTop: 50,
    display: "flex",
    width: 550,
    height: 250,
  },
  cardcss: {
    backgroundImage: "url(" + bgImg + ")",
    backgroundPosition: "center",
  },
}));

function App() {
  const classes = style();
  const [city, setCity] = React.useState(null);

  return (
    <Grid className={classes.root} alignItems="center" container justify>
      <Card className={classes.cardcss}>
        <CardContent>
          <TextField
            autoFocus
            label="City Name"
            onChange={(e) => {
              setCity(e.target.value);
            }}
          />
          <WeatherAPI city={city} />
        </CardContent>
      </Card>
    </Grid>
  );
}

export default App;
```

This statless is simple. We are creating a state name `city` using new feature of react js called react hooks. Whenever user writes the value in input field the state of the function get's updated and passed it to weatherAPI component.

**weatherAPI.js**

```javascript

import React from 'react';
import LinearProgress from '@material-ui/core/LinearProgress';
import Display from './weatherReportDisplay';

const API_KEY = /* Your API key here */
const UNITS = "Metric"
const LANG = "en"

class WeatherAPI extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            weatherReport : null,
            isLoading : true,
            error : null
        }
    }
    componentDidUpdate() {
    var URL = "http://api.openweathermap.org/data/2.5/weather?q=" + this.props.city
                        + "&lang=" + LANG + "&appid=" + API_KEY + "&units="+ UNITS
    fetch(URL).then(response =>{
        if(response.ok) {return response.json() }
        else { throw new Error("SOMETHING WENT WRONG")}})
            .then(data => this.setState(
                { weatherReport : data,
                    isLoading: false }))
            .catch(error => this.setState( {error, isLoading : true }));
    }
    render() {

        if(this.state.isLoading) {
            if(this.props.city != null) {
                return (
                    <div>
                        <LinearProgress  />
                    </div>
                    )
            }
            else return null;
        }
        else {
            return(
                <Display weatherReport = {this.state.weatherReport}/>
            )
        }
    }
}

export default WeatherAPI;
```

For simplicity of our app here we have used statefull component. Here we have used `componentDidUpdate` method which will continusly update the state value of this component whenever input field changes.
The state of this component hold 3 value:

1. `weatherReport` Which will hold our json response.
2. `isLoading` Used for loading bar.
3. `error` If server respone with any error.

In `componentDidUpdate` method we are using javascript **promise** object.Which will contain some value either solved or unsolved when fetching data from website.The `.json()` method of promise object converts it into json format.

In the `render` method we first check that weather we have got response or not by checking `isLoading` state.Which only set to false whenever we get a response from server.

If everythings went fine `weatherReport` state is passed to `Display` component.

**weatherReportDisplay.js**

```javascript
import React from "react";
import Typography from "@material-ui/core/Typography";
import CardContent from "@material-ui/core/CardContent";
import Box from "@material-ui/core/Box";

function Display({ weatherReport }) {
  var lon = weatherReport.coord.lon;
  var lat = weatherReport.coord.lat;
  var weathermain = weatherReport.weather[0].main;
  var weatherdiscription = weatherReport.weather[0].description;
  var temp = weatherReport.main.temp;
  var pressure = weatherReport.main.pressure;
  var humidity = weatherReport.main.humidity;
  var wind = weatherReport.wind.speed;
  var country = weatherReport.sys.country;
  var city = weatherReport.name;

  return (
    <div>
      <CardContent>
        <Box display="flex" flexDirection="row">
          <Box p={1}>
            <Typography variant="h2" color="textPrimary">
              {city},{country}
            </Typography>
            <Typography variant="caption" color="textSecondary">
              {lon}, {lat}
            </Typography>
          </Box>
        </Box>
      </CardContent>
      <CardContent>
        <Box display="flex" flexDirection="row-reverse">
          <Box p={0}>
            <Typography variant="h4" color="textPrimary">
              Temp: {temp}
              <span>&#176;</span>
              {"C"}
            </Typography>
          </Box>
        </Box>
      </CardContent>
      <CardContent>
        <Box display="flex" flexDirection="row-reverse">
          <Box p={0}>
            <Typography variant="h6" color="textSecondary">
              {weatherdiscription}
            </Typography>
          </Box>
        </Box>
      </CardContent>
      <CardContent>
        <Box display="flex" flexDirection="row">
          <Box p={1}>
            <Typography variant="h6" color="textPrimary">
              Humidity: {humidity} %
            </Typography>
          </Box>
          <Box p={1}>
            <Typography variant="h6" color="textPrimary">
              pressure: {pressure} pa
            </Typography>
          </Box>
          <Box p={1}>
            <Typography variant="h6" color="textPrimary">
              wind: {wind} km/h
            </Typography>
          </Box>
        </Box>
      </CardContent>
    </div>
  );
}

export default Display;
```

This component displays weather information provided by `weatherAPI` component. Here from the json object we have chosen certain value for displaying such as temprature,humidity,pressure,etc. The `Box` component provided by material UI is used for manging layout.

That's it now try to implement the above app yourself.After successfull implemnentation try adding more feature such as weather icon or litter bit of animation.
