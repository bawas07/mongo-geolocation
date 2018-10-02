# How to title?

How to find location using geonear with mongodb

# Created by ?

Bayu Waskita, Backend Programmer Divisi Web
PT. GITS Indonesia

# Created at ?

02 Okt 2018

# Type ? 

Tutorial

# Description ?

How - To Setup => Mongodb have a function to find collection based on location,
but in order to use this function, we have to do some set-up, 

# How - to?

## How-to-use ?

### How-to-setup schema

```JS
const mongoose = require('mongoose')

const position = new mongoose.Schema({
    name: {type:String, required:true},
    location:{
        type: {
            type: String,
            required: true,
            default: 'Point'
        },
        coordinates: [Number]
    }
})

reportAccidentSchema.index({'location.coordinates': '2dsphere'})

module.exports = mongoose.model('Position', position)
```

This code define a mongodb schema. In here we can find at location.coordinate 
is an array that contain value [longitute, latitude]

### How-to-query near me

To get the data we need to add an option like this : 

```
const longlat = [ parseFloat(longitude), parseFloat(latitude) ];
// distance are in meters
const distance = parseInt(req.query.distance, 10);
const query = {
    'location.coordinates': {
        $near: {
            $geometry: {
                type: 'Point',
                coordinates: longlat
            },
            $maxDistance: distance
        }
    },
};
```