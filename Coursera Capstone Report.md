# Finding Pharmacy Close To Your Neighborhood

**_Data Science Capstone - IBM Data Science Professional Certificate on Coursera_**

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

## Methodology

My main target here is to asses which city would have the highest pharmacy density. I used the FourSquare API through the venues channel. I used the near query to get venues in the cities. Also, I use the CategoryID to set it to show only pharmacies. An Example of my requests:

https://api.foursquare.com/v2/venues/explore?&client_id=&client_secret=&v=20180605&near=New%20York,%20NY&limit=100&categoryId=4bf58dd8d48988d10f951735

That 4bf58dd8d48988d10f951735 is the Id of the Pharmacy Category. Also, FourSquare limits us to maximum of 100 venues per query.

Moreover, I repeated this request for the 5 studied cities and got their top 100 venues. I saved the name and coordinate data only from the result and plotted them on the map for visual inspection.

Next, to get an indicator of the density of pharmacies, I calculated a center coordinate of the venues to get the mean longitude and latitude values. Then I calculated the mean of the Euclidean distance from each venue to the mean coordinates. That was my indicator; mean distance to the mean coordinate.

## Results

For our initial visual inspection we see that they all have multiple pharmacies and often more than FourSquare would like to supply us. The following here are the pictures of the geoplot generated with folium:

**New York:**

![alt text](https://github.com/Bilalesque/Coursera_Capstone/blob/master/docs/NY.PNG "New York")

**Chicago**

![alt text](https://github.com/Bilalesque/Coursera_Capstone/blob/master/docs/Chicago.PNG "Chicago")

**New Jersey**

![alt text](https://github.com/Bilalesque/Coursera_Capstone/blob/master/docs/NJ.PNG "New Jersey")

**San Francisco**

![alt text](https://github.com/Bilalesque/Coursera_Capstone/blob/master/docs/SF.PNG "San Francisco")

**Boston**

![alt text](https://github.com/Bilalesque/Coursera_Capstone/blob/master/docs/Boston.PNG "Boston")


Upon first inspection we see that New York, Jersey City and San Francisco are the most dense cities. In the next phase we calculate the mean coordinate and the mean distance to mean coordinate(MDMC). We represent the mean coordinate with a big green circle and distances with green lines.


**New York**

MDMC: 0.02298
![alt text](https://github.com/Bilalesque/Coursera_Capstone/blob/master/docs/NY%20MDMC.PNG "New York MDMC")

**Chicago**

MDMC: 0.05963
![alt text](https://github.com/Bilalesque/Coursera_Capstone/blob/master/docs/Chicago%20MDMC.PNG "Chicago MDMC")

**New Jersey**

MDMC: 0.018859
![alt text](https://github.com/Bilalesque/Coursera_Capstone/blob/master/docs/NJ%20MDMC.PNG "New Jersey MDMC")

**San Francisco**

MDMC: 0.028948
![alt text](https://github.com/Bilalesque/Coursera_Capstone/blob/master/docs/SF%20MDMC.PNG "San Francisco MDMC")

**Boston**

MDMC: 0.038830
![alt text](https://github.com/Bilalesque/Coursera_Capstone/blob/master/docs/Boston%20MCDC.PNG "Boston MDMC")


Therefore our results are :

1. Jersey City
2. New York
3. San Francisco
4. Boston
5. Chicago

## Discussion

One thing I noticed in the figure is that there is a really far away pharmacy in New York that is probably giving it a higher MDMC. So I cheched what if I removed it, it would not harm anyone to try 99 pharmacies than 100 and New Jersey is just at the other shore.

The new MDMC was lower than the MDMC of New Jersey, putting it at the top place on the list replacing New Jersey.

One consideration to do further work on is to move the location of the FourSquare API query until we get all the pharmacies in each city and do the calculations again.

## Conclusion

Now there is no doubt that New Jersey is the most equipped place to fullfil your medical and pharmaceutical needs in the US. Also, if our person cannot find his required medicines in New Jersey, he can cross to New York City and can find it in 100 other pharmacies in New York.

Also, we would recommend that our a person should look at the pharmacies close to the mean coordinate if he cannot find his medicines at his nearest local store as there is a higher chance that he would find it near the mean coordinate due to higher number of pharmacies.
