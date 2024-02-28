API Data for Indonesian Regions

This repository contains the source code to generate a static (REST) API containing data for Indonesian regions and commands to deploy it to static hosting Github Page.

Demo: https://emsifa.github.io/api-wilayah-indonesia


What is meant by a static API?

A static API is an API whose endpoints consist of static files.
Advantages of a static API?

Can be hosted on static file hosting services such as Github Page, Netlify, etc.
Faster process because it does not require server-side scripting.

How does it work?

Lists of provinces, districts/cities, districts, and villages are stored in the data folder in CSV files (for easy editing).
Then the generate.php script is executed. This script will read the CSV files inside the data folder and then generate thousands of endpoints (files) into the static/api folder.
The API is ready to be served.

I want to host it on my own Github, how can I do that?

Click fork in the top right corner.
On the forking page, UNCHECK "Copy the master branch only".
Click "Create Fork".
After forking is done, click Settings (not account settings, but repository settings).
Click the "Pages" menu to enter the GitHub Pages settings menu.
In the GitHub Pages settings menu:
  Choose Source: Deploy from a Branch
  Branch: gh-pages
  Directory: /root
  Click Save
Wait a few minutes (5-10 minutes), go back to the repository's home page (https://github.com/yourusername/api-wilayah-indonesia).
If the page has been deployed, on the right side of the page, you will see "Environments" information. If not, wait a few more minutes, then refresh.
Once the Environments information appears, click on "🚀 github-pages".
On the Deployments page, click "View Deployment" to see the successfully deployed page.

## ENDPOINTS

#### 1. Get List of Provinces

```
GET https://imitasi11.github.io/IndonesianRegion-API/static/api/provinces.json
```

Example Response:

```
[
  {
    "id": "11",
    "name": "ACEH"
  },
  {
    "id": "12",
    "name": "SUMATERA UTARA"
  },
  ...
]
```

#### 2. Get List of Districts/Cities in a Certain Province

```
GET https://imitasi11.github.io/IndonesianRegion-API/static/api/regencies/{provinceId}.json
```

Example to get a list of districts/cities in Aceh province (ID = 11)

```
GET https://imitasi11.github.io/IndonesianRegion-API/static/api/regencies/11.json
```

Example Response:

```
[
  {
    "id": "1101",
    "province_id": "11",
    "name": "KABUPATEN SIMEULUE"
  },
  {
    "id": "1102",
    "province_id": "11",
    "name": "KABUPATEN ACEH SINGKIL"
  },
  ...
]
```

#### 3. Get List of Districts in a Certain District/City

```
GET https://imitasi11.github.io/IndonesianRegion-API/static/api/districts/{regencyId}.json
```

Example to get a list of districts in South Aceh (ID = 1103):

```
GET https://imitasi11.github.io/IndonesianRegion-API/static/api/districts/1103.json
```

Example Response:

```
[
  {
    "id": "1103010",
    "regency_id": "1103",
    "name": "TRUMON"
  },
  {
    "id": "1103011",
    "regency_id": "1103",
    "name": "TRUMON TIMUR"
  },
  ...
]
```

#### 4. Get List of Villages in a Certain District

```
GET https://imitasi11.github.io/IndonesianRegion-API/static/api/villages/{districtId}.json
```

Example to get a list of villages in Trumon (ID = 1103010):

```
GET https://imitasi11.github.io/IndonesianRegion-API/static/api/villages/1103010.json
```

Example Response:

```
[
  {
    "id": "1103010001",
    "district_id": "1103010",
    "name": "KUTA PADANG"
  },
  {
    "id": "1103010002",
    "district_id": "1103010",
    "name": "RAKET"
  },
  ...
]
```

#### 5. Get Province Data based on Province ID

```
GET https://imitasi11.github.io/IndonesianRegion-API/static/api/province/{provinceId}.json
```

Example to get data for Aceh province (ID = 11):

```
GET https://imitasi11.github.io/IndonesianRegion-API/static/api/province/11.json
```

Example Response:

```
{
  "id": "11",
  "name": "ACEH"
}
```

#### 6. Get District/City Data based on District/City ID

```
GET https://imitasi11.github.io/IndonesianRegion-API/static/api/regency/{regencyId}.json
```

Example to get data for South Aceh district (ID = 1103):

```
GET https://imitasi11.github.io/IndonesianRegion-API/static/api/regency/1103.json
```

Example Response:

```
{
  "id": "1103",
  "province_id": "11",
  "name": "KABUPATEN ACEH SELATAN"
}
```

#### 7. Get District Data based on District ID

```
GET https://imitasi11.github.io/IndonesianRegion-API/static/api/district/{districtId}.json
```

Example to get data for East Trumon district (ID = 1103011):

```
GET https://imitasi11.github.io/IndonesianRegion-API/static/api/district/1103011.json
```

Example Response:

```
{
  "id": "1103011",
  "regency_id": "1103",
  "name": "TRUMON TIMUR"
}
```

#### 8. Get Village Data based on Village ID

```
GET https://imitasi11.github.io/IndonesianRegion-API/static/api/village/{villageId}.json
```

Example to get data for Jambo Dalem village (ID = 1103011010):

```
GET https://imitasi11.github.io/IndonesianRegion-API/static/api/village/1103011010.json
```

Example Response:

```
{
  "id": "1103011010",
  "district_id": "1103011",
  "name": "JAMBO DALEM"
}
```

## LIMITATION

Since this API is hosted on Github Page, Github Page itself provides a bandwidth limit of 100GB/month. 

Because this limitation, its recomended to make your own github page -API.

For more information you can check this(https://help.github.com/en/articles/about-github-pages#usage-limits).
