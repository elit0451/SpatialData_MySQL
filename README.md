# Spatial data <img src="https://geodiscover.alberta.ca/geoportal/catalog/images/icon-layers-pin.png" height="45" align="center"> with MySQL <img src="https://pngimg.com/uploads/mysql/mysql_PNG9.png" height="40" align="center">

The following exercises are based on data taken from http://wfs-kbhkort.kk.dk 🇩🇰. 

<br/>

_The Copenhagen data is in Danish, so here are references to the ones we used_ <img src="https://cdn4.iconfinder.com/data/icons/file-types-5/96/document_file_extension_format_type_csv-512.png" height="20" align="center">:  
&nbsp;&nbsp;&nbsp; [Parks](http://wfs-kbhkort.kk.dk/k101/ows?service=WFS&version=1.0.0&request=GetFeature&typeName=k101:parkregister&maxFeatures=50&outputFormat=csv) <img src="https://www.emoji.co.uk/files/emoji-one/travel-places-emoji-one/1795-national-park.png" height="20" align="center"> , [Trees along road](http://wfs-kbhkort.kk.dk/k101/ows?service=WFS&version=1.0.0&request=GetFeature&typeName=k101:gadetraer&maxFeatures=50&outputFormat=csv) <img src="https://hotemoji.com/images/dl/b/deciduous-tree-emoji-by-google.png" height="20" align="center">, [Exposed areas](http://wfs-kbhkort.kk.dk/k101/ows?service=WFS&version=1.0.0&request=GetFeature&typeName=k101:f_udsatte_byomraader&maxFeatures=50&outputFormat=csv) <img src="https://bit.ly/2G7f63b" height="20" align="center">&nbsp;, [Bike racks](http://wfs-kbhkort.kk.dk/k101/ows?service=WFS&version=1.0.0&request=GetFeature&typeName=k101:cykelstativ&maxFeatures=50&outputFormat=csv) <img src="https://static.thenounproject.com/png/40463-200.png" height="25" align="center">&nbsp;, [Heavy traffic](http://wfs-kbhkort.kk.dk/k101/ows?service=WFS&version=1.0.0&request=GetFeature&typeName=k101:tungvognsnet&maxFeatures=50&outputFormat=csv) <img src="https://cdn3.iconfinder.com/data/icons/transportation-vehicles-2/128/car-traffic-two-lanes-512.png" height="25" align="center">

<br/>

----
## Excercise 1 
### How many parks are located in exposed areas? :fountain: <img src="https://bit.ly/2Kto0fF" height="25" align="center">

```sql
SELECT id AS exp_area_id, byomraade AS area_name, delomraade AS subregion, COUNT(areal_id) AS nr_parks 
FROM exposedAreas, parkRegister
WHERE ST_Within(parkRegister.wkb_geometry, exposedAreas.wkb_geometry)
GROUP BY exp_area_id;
```

> RESULTS

| exp_area_id | area_name | subregion |nr_parks |
| :----:|:----:|:----:|:----:|
|	9 |Valby/Sydhavnen| Sydhavnen |3|
|	13|Valby/Sydhavnen| Ved Folehaven|1|
|	10|Amager/Sundby| Urbanplanen mv.|1|
|	6|Nørrebro| Ved Bispeengbuen|1|
|	3|Nordvest/Ryparken| Ryparken|1|
|	4|Nordvest/Ryparken| Nordvest|1|

</br>

### How many trees are located in exposed areas? :deciduous_tree::evergreen_tree:
```sql
SELECT exposedAreas.id AS exp_area_id, byomraade AS area_name, delomraade AS subregion, COUNT(roadTrees.id) AS nr_trees 
FROM exposedAreas, roadTrees
WHERE ST_Within(roadTrees.wkb_geometry, exposedAreas.wkb_geometry)
GROUP BY exp_area_id;
```

> RESULTS

| exp_area_id | area_name | subregion |nr_trees |
| :----:|:----:|:----:|:----:|
|	4 |Nordvest/Ryparken| Nordvest |3|
|	6|Nørrebro| Ved Bispeengbuen|2|
|	12|Nørrebro| Indre Nørrebro|1|
|	3|Nordvest/Ryparken| Ryparken|2|
<br/>

----
## Excercise 2 
### How many bike racks are places along routes for heavy traffic? :parking: :bike:

_Unfortunatelly, we couldn't figure out how to check if a bike rack POINT is part of a heavy traffic LINESTRING/MULTILINESTRING_ :frowning: Any suggestions are welcomed! :nerd_face: :mortar_board:

<img src="https://bit.ly/2YVAgIY" width="50%"><img src="https://bit.ly/2VzLMHX" width="50%">


<br/>

___
> #### Assignment made by:   
`David Alves 👨🏻‍💻 ` :octocat: [Github](https://github.com/davi7725) <br />
`Elitsa Marinovska 👩🏻‍💻 ` :octocat: [Github](https://github.com/elit0451) <br />
> Attending "Databses for Developers" course of Software Development bachelor's degree

