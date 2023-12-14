# h12api

# Running api

1. Import env variable (npm install dotenv --save)
   - only have to do, first time you download project
2. run application in dev mode (npm run start)

# API Endpoints

1. Create Library Location (no impact on map locations)

   POST /library/api/v2.0/locations

- Body Params:

  - MapLocId: String, required, has to be unique
  - PhoneNumber: String, required, expected format 888.888.8888
  - OperatingHours: String, required, expected format 8am - 8pm PST
  - NameLocation: String, required

- Response:

  - Success: status code 200, Body of response JSON data
  - Failure: status code 400, JSON Body errorMessage with Object Body

         {
            "errorMessage": {
               "PhoneNumber": "Required field",
               "OperatingHours": "Required field",
               "NameLocation": "Required field"
             }
         }

         {
            "errorMessage": {
               "MapLocId": "Has to be unique (not a duplicate)"
            }
         }


         {
            "errorMessage": {
               "PhoneNumber": "Phone# not string"
            }
         }

2. Get all library locations
   GET /library/api/v2.0/locations/

- Response:

  - Success: status code 200, Body of response JSON data

          * If no records exist:

          []

          * If records exist:
            [
               {
                  "_id": "657a74374b095bfcc6fba2a9",
                  "MapLocId": "1",
                  "PhoneNumber": "5035886315",
                  "OperatingHours": "8am - 8pm PST",
                  "NameLocation": "Salem Public Library",
                  "__v": 0
               },
               {
                  "_id": "657a772fce9a67477a22affe",
                  "MapLocId": "2",
                  "PhoneNumber": "5035886315",
                  "OperatingHours": "8am - 8pm PST",
                  "NameLocation": "Salem Public Library",
                  "__v": 0
               },
            ]

  - Failure: status code 400, JSON Body errorMessage with Object Body

3.  Get a specic library's location data using MapLocId field
    GET /library/api/v2.0/locations/:\_MapLocId

    - Response:

      - Success: status code 200, Body of response JSON data

      * if location not found
        []

      * if location found

             [
                {
                   "_id": "657a860d73f708da246b2bb2",
                   "MapLocId": "1",
                   "PhoneNumber": "5035886315",
                   "OperatingHours": "8am - 8pm PST",
                   "NameLocation": "Salem Public Library",
                   "__v": 0
                }
             ]
