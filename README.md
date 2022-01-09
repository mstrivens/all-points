# all-points

## Current progress

Pulled Google map api in using @point-hub/vue-google-maps - https://github.com/point-hub/vue-google-maps/blob/main/src/vue-google-maps/MapLoader.vue
Created method to get user location

Trying to implement refreshing map once user location found.
Currently not able to do this
Usually done using gmap or built in keyword

# Project Planning

## Modelling

As a user
So that I can visualize the location of a charger point
I would like to be able to view a map

As a user
So that I can see where my closest charger is
I would like to be able to see the charger points on the map

As a user
So that I can see all the closest points to me
I would like to be able to see the closest points on a carousel

## Architecture

Vue uses App.vue and main.js to pull in components are create the app instance.

I want to bring in a Google maps api into a maps component
I want to bring in the charging points into a charging-points component and assign each point to a pin using it's location
I want to also iterate through each position and show the closest x number on cards in a carousel

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Lints and fixes files
```
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
