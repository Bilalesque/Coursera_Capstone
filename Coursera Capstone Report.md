# Finding Pharmacy Close To Your Neighborhood

*Data Science Capstone - IBM Data Science Professional Certificate on Coursera*

## Introduction

In these unfortunate times of global pandemic due to the novel coronavirus-19 or covid-19, we aim to compare different cities in the US
and analyze what city in the US is better equipped to provide for its population, the much needed medical supplies. The pandemic has not only caused suffering to those that have been directly affected by it, but also, those patients that have been suffering from various other illnesses and medical problems are also being affected by it in the form of lockdowns and unavailibilty/shortage of medicines.
Therefore, we will analyze the pharmacy density of each city that we are analyzing in our final project. Our main target are the local population and our aim is to find which city has the highest number of pharmacies in its neighborhoods. The city with the highest density of pharmacies in its neighborhoods will be considered to be better equipped as more people would have a higher chance of getting the vital medicines and medical supplies. 

## Data section 

I will use the FourSquare API to collect data about locations of pharmacies in 5 major US cities which are: New York,NY, San Francisco, CA, Jersey City, NJ,  Boston, MA and Chicago,IL. These are one of the most populated US cities and I am hopeful that they will contain the best and highest number of pharmacies in the US. One sample JSON data from the Foursquare API is as follows:
```yaml
{
  "reasons":{
     "count":0,
     "items":[
        {
           "summary":"This spot is popular",
           "type":"general",
           "reasonName":"globalInteractionReason"
        }
     ]
  },
  "venue":{
     "id":"4e034363b61ce80e5d67d09f",
     "name":"Duane Reade",
     "location":{
        "address":"40 Wall St",
        "crossStreet":"btwn Nassau & William St",
        "lat":40.7071871,
        "lng":-74.0095394,
        "labeledLatLngs":[
           {
              "label":"display",
              "lat":40.7071871,
              "lng":-74.0095394
           }
        ],
        "distance":1134,
        "postalCode":"10005",
        "cc":"US",
        "city":"New York",
        "state":"NY",
        "country":"United States",
        "formattedAddress":[
           "40 Wall St (btwn Nassau & William St)",
           "New York, NY 10005",
           "United States"
        ]
     },
     "categories":[
        {
           "id":"4bf58dd8d48988d10f951735",
           "name":"Pharmacy",
           "pluralName":"Pharmacies",
           "shortName":"Pharmacy",
           "icon":{
              "prefix":"https:\/\/ss3.4sqi.net\/img\/categories_v2\/shops\/pharmacy_",
              "suffix":".png"
           },
           "primary":true
        }
     ],
     "photos":{
        "count":0,
        "groups":[

        ]
     }
  },
  "flags":{
     "outsideRadius":true
  },
  "referralId":"e-0-4e034363b61ce80e5d67d09f-8"
}
```
The data above is extracted from the Foursquare API using venues and categories parameters. The data shows the name of the pharmacy, its geolocation, distance from the pharmacy, its postal address, its street address as well as the state and city it belongs to.
We will use such data for finding the pharamcy density in the neighborhoods of our 5 subject cities.
