---
layout: post
title:      "Reverse Geocoding"
date:       2018-11-29 13:15:45 +0000
permalink:  reverse_geocoding
---


You visit one of your favorite websites, and a wild popup appears. It says “https://nedditt.herokuapp.com/ wants to know your location”. Did you ever wonder what happens If you allow access, and also, how and why would I want to use this in my own website? I was curious on how to do so, so I included this feature in my website.
  
The sparknotes version is once you click “yes”, allowing the website access to your location, it gathers your latitude and longitude coordinates. The website will then take those coordinates, and then use Reverse Geocoding in order to take the coordinates you just allowed the site to have into human readable format. This can be done using the Google Maps Reverse Geocoding API. After the site does the API call, the site will then have the information such as the city, state, and country that you are currently in. 

HTML5 Geolocation gets your longitude and latitude coordinates from a few factors such as your pubic IP address, cell tower IDs, GPS information, list of wifi access points, signal strengths, and MAC IDs. 

In order to have your site ask your users for their location, you need to add the following: 

```
if ("geolocation" in navigator) {
  navigator.geolocation.getCurrentPosition(
   function success(position) {
     console.log('latitude', position.coords.latitude, 
                 'longitude', position.coords.longitude);
   }
```
This will provide you with the Longitude and Latitude data that you need. After you gather the Longitude and Latitude data, you can then use those values into an asynchronous request for the Reverse Geocoding. Before you begin making the api request, you need to make sure that you get an API key for the Google Maps Platform. Once you get your API key, and include it into your .env file, you are good to go. 
In my application, I used React and Redux, and I will show you how I did it. There are many ways to skin a horse, so if your site is a little different, you can still achieve the same results. 

When I asked permission for location, I created an arrow function in the App.js, and ran the function in ComponentDidMount()

```
class App extends Component {

  getCoords = () => {
    if (navigator.geolocation) { //check if geolocation is available
              navigator.geolocation.getCurrentPosition(position =>{
                this.props.fetchLocation( position.coords.latitude, position.coords.longitude);
              });
          }
  }
  componentDidMount() {
    this.getCoords()
  }
…
```

I also mapped the dispatch to props. 

```
const mapDispatchToProps = (dispatch) => {
  return {
    fetchLocation: bindActionCreators(fetchLocation, dispatch)
  }
}

export default connect(mapStateToProps, mapDispatchToProps)(App);
```

My location-actions.js file is where I did the fetch request for the reverse geocoding. 

```
import dotenv from 'dotenv'
dotenv.config()
export const FETCH_LOCATION = 'FETCH_LOCATION';
const mapsApiKey = process.env.REACT_APP_KEY;
export const fetchLocation = (latitude, longitude) => {
return (dispatch) => {
  fetch("https://maps.googleapis.com/maps/api/geocode/json?latlng="+ latitude + "," + longitude +"&sensor=false&key=" +  mapsApiKey)
    .then(res => res.json())
    .then(location => {
      dispatch({
        type: FETCH_LOCATION,
        payload: location
      })
    })
}
}
```

You need to be sure to include your API key, in order to have your function come out to be a success. After this function runs, it is sending the payload to my reducer. 

```
import initialState from './initialState';
import {FETCH_LOCATION} from '../actions/location-actions'


export default (state = initialState.locations, action) => {
  switch(action.type) {

    case FETCH_LOCATION:
      return [ action.payload.results[0].address_components];

    default:
      return state
    }
}
```

You then have all of the location data in the application’s store, and can use it for many different things. Websites will use this data to help the user locate the nearest store location to them, gather data on where their visitor traffic is coming from, or even to help display where a user is commenting from. After adding this feature to my own site, as cool as it was, I also realized how much information you provide when you allow a website access to your location. The data that is returned from the Google Maps Reverse Geocoding gives you everything up to the address you are currently located at. For being on a laptop with no GPS signal, it was able to pinpoint my location, and it was only one block off where I was located. When you give a site access to your location, you truly are letting them know exactly where you are. 



