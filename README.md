# Interactive Data Visualization and Augmented Reality of Urban Photovoltaic
The same repository is also backed up at ETH Arch Chair's repo: 
https://github.com/architecture-building-systems/FCL-Exhibition-2023-ARUnity

## Introduction  
This project is an iPad mobile app created for the Future Cities Lab Exhibition 2023 at ETH Zurich, aiming to visualize influential data of photovoltaic power usage using augmented reality. It utilizes 3D printed models of two sites, Zurich and Singapore, and is composed of three key modules: energy demand(cooling and heating), mobility flow (both vehicle and non-vehicle), and social economics(energy trading within these regions). 
By inputting these data in a specific format, the project creates a virtual overlay on the physical 3D models, providing a direct and clear view of the real situations in the designated areas.

## Environment and dependencies  

The `ARFoundationAllBackup` branch represents the final version of this repository. It is compatible with [Unity](https://unity.com/download) 2021.2 and later.  

This project is developed based on [AR Foundation 5.1](https://docs.unity3d.com/Packages/com.unity.xr.arfoundation@5.1/manual/index.html) and its demonstration example [AR Foundation Sample Project](https://github.com/Unity-Technologies/arfoundation-samples).

It depends on 2 Unity packages:  
* [AR Foundation](https://docs.unity3d.com/Packages/com.unity.xr.arfoundation@5.1/manual/index.html)  
* [Apple ARKit XR Plug-in](https://docs.unity3d.com/Packages/com.unity.xr.arkit@5.1/manual/index.html) on iOS  
To check the packages in unity editor, go to Windows > Packages manager  

To build on iOS mobile devices, it requires an external development environment:    
* [Xcode](https://developer.apple.com/documentation/xcode) available on macOS and developer account  


## How to use 

### case1: Directly run on device without modification

This project can be directly built to iOS device providing input data in specific formats.   
In this case, Unity is not required. Follow the steps below:   

**Xcode part**     
(See [tutorial video](https://www.youtube.com/watch?v=Z-gija1aAhw) that demonstrates the following steps.)    
1. Clone this repository and go to `1610FinalBuild` folder, open `Unity-iPhone.xcodeproj` using Xcode 14.0 or later.

2. Plug in your iOS device (with [developer mode](https://docs.expo.dev/guides/ios-developer-mode/#) enabled) to the compmuter, and select this device on top of the window in Xcode.

3. In Xcode, click on "Unity-iPhone" on folder hierarchy on the top left, and then "Signing & Capabilities" in the middle.

4. In "Signing & Capabilities" page, check "automatically manages signing"

5. "Add an account" under "Team" selection options, and then choose your account for Team.

6. Run the project by clicking the triangle "run" button on top left. This way Xcode builds the app to your device. 

**Device part**    

7. On your iOS device, sign in to the Apple developer account the same as "Team"

8. "[Verify](https://www.youtube.com/watch?v=vsi2MsEW764)" this app in Settings > General > VPN & Device Management 

9. Transfer the data for visualization to the device under App document folder(Example file formats are described [below](#Data-Format)). There are many ways to do this. For example, use 3rd-party iOS file explorers, such as [iMazing](https://imazing.com) or [iExplorer](https://macroplant.com/iexplorer). Navigate to ../Apps/FCL AR Visualization/Developer/Documents, and copy-paste the folder `PersistantFilePath` including the files in it to this path (i.e., the whole file path can be: ../Apps/FCL AR Visualization/Developer/Documents/PersistantFilePath/ZurichEnergyTrade.json). For the app document file path, see [Unity Persistant File Path](https://docs.unity3d.com/ScriptReference/Application-persistentDataPath.html).

12. The app is ready to use. 


### case 2: Modify project before building to device  

To modify project on models, scenes, scripts,...,etc, follow the steps below:   

**Unity part**    
1. Install [Unity Hub](https://unity.com/download). In Unity Hub, go to "Install" to install Unity 2021.2 or later, add 2 modules: "Visual Studio for Mac" and "iOS Build Support".  

2. Clone this repository and open the Unity project at the root of this repository.

3. Modify the projects as needed.

4. Go to [Build Settings](https://docs.unity3d.com/Manual/BuildSettings.html), select a target platform([iOS](https://docs.unity3d.com/Manual/iphone-BuildProcess.html) in this sample), and build this project in a new folder. In this way, unity automatically build a Xcode project. 

**Xcode part**    

5. After finishing building, go to that new folder and open `Unity-iPhone.xcodeproj` using Xcode 14.0 or later.

6. Follow the steps of [case1](#case1:-Directly-run-on-device-without-modification)


## Data Format   
Sample data can be found in this repository under folder `PersistantFilePath`. To customize data to visualize, prepare new data in the following format, update the file name in code,and follow step#9 of previous section [case1](#case1:-Directly-run-on-device-without-modification).   

### Energy Demand   

{  
"houses":  
[  
    {  
        "id": "B6327",  
        "load": "227630.1"  
    },  
    {  
        "id": "B117045",  
        "load": "0"  
    },...  
    ]}  
    
### Mobility   

{  
"type": "FeatureCollection",  
"features": [  
{ "type": "Feature", "properties": { "uid": 0.0, "Time": "2023-07-31T02:23:32.083", "Lat": 1.3906850104627779, "Lon": 103.89404394884859, "is_vehicle": 0.0 }, "geometry": { "type": "Point", "coordinates": [ 103.894043948848591, 1.390685010462778 ] } },  
{ "type": "Feature", "properties": { "uid": 0.0, "Time": "2023-07-31T02:23:32.083", "Lat": 1.3906829774271761, "Lon": 103.89404762958823, "is_vehicle": 0.0 }, "geometry": { "type": "Point", "coordinates": [ 103.894047629588229, 1.390682977427176 ] } },  
...]}  

### Energy Trade   

{  
"DataEnergyTrade":[  
    {  
        "From": "B1082_demand.csv",  
        "To": "B1030_demand.csv",    
        "Transmission": "4",  
        "T": "12"  
    },  
    {  
        "From": "B1108_demand.csv",  
        "To": "B1047_demand.csv",  
        "Transmission": "1",  
        "T": "12"  
    },  
    ...]}  

# Table of Contents   

| Sample scene(s) | Location in project |
| :----------------------------- | :------------------ |
| [Menu](#Menu) | ../Asset/Scenes/ImageTracking/Menu |
| [Images](#Scenes) | ../Asset/Scenes/ImageTracking/Images |
| [Energy Demand Module](#Energy-Demand-Module) | ../Asset/Scenes/ImageTracking/ImageTrackingWithMultiplePrefabs|
| [Mobility Flow Module](#Mobility-Flow-Module) | ../Asset/Scenes/ImageTracking/ImageTrackingWithMultiplePrefabs |
| [Social Economics (Energy Trade) Module](#Social-Economics-(Energy-Trade)-Module) | ../Asset/Scenes/ImageTracking/ImageTrackingWithMultiplePrefabs |
| [Debug Image Tracking](#Debug-Image-Tracking) | ../Asset/Scenes/ImageTracking/BasicImageTracking |

## Menu   

 ../Asset/Scenes/ImageTracking/Menu   

 **Menu**   
 ![Menu](RESULTS/Menu.gif)  
 
The menu scene is the start page of the app. It allows users (1)select the city, then (2)select the data module.   

## Image   

 ../Asset/Scenes/ImageTracking/Images   
 
`ReferenceImageLibrary.asset` manages the images that can be detected in physical world. Use this to modify or add new images.   
After modifying images, add the cooresponding prefabs that will be instantiated when the new image is detected under: (A module's scene, eg., EnergyDemandScene.unity) > Hierarchy > gameobject `ARF XR Origin Set Up` > gameobject `XR Origin` > Inspector > component `PrefabImagePairManager(Script)` > `PrefabList`.

 
### Instantiate module prefabs   

The matched prefabs are instantiated in the virtual world when the corresponding image is detected in physical world. The location and rotation are set by function`AssignPrefab` in the script`PrefabImagePairManager.cs`.    

Detailed explanation can be found in [AR Foundation Image Tracking package documentation](https://docs.unity3d.com/Packages/com.unity.xr.arfoundation@5.1/manual/features/image-tracking.html).   

   
## Data Visualization Modules   

Prefabs location: ../Asset/Scenes/ImageTracking/Prefabs    
Scenes location: ../Asset/Scenes/ImageTracking/ImageTrackingWithMultiplePrefabs    
Scripts location: ../Asset/Scenes/ImageTracking/Scripts    

### Energy Demand Module   

**Zurich Cooling Demand**    
![Zurich Cooling Demand](RESULTS/ZurichCooling.gif)    

**Zurich Heating Demand**    
![Zurich Heating Demand](RESULTS/ZurichHeating.gif)    

**Singapore Cooling Demand**    
![Singapore Cooling Demand](RESULTS/SingaporeCooling.gif)   

The annual energy demand is measured in kWh, and it's represented by a color bar on the right. This bar uses different shades of blue(for cooling)/red(for heating) to indicate the level of demand. Darker shades of blue/red represent higher demand. The darkest level matches the highest demand within the area of study. Each building displays its annual demand on top of the model, and its color corresponds to the color scale bar to show the level of demand. The annual cooling demand data is visualized on both Zurich and Singapore models; the annual heating demand data is visualized only on Zurich model.   

The following table summarizes the code for Zurich case, the Singapore case shares the same structure.   
| Scripts | Function | Description |
| :------------ | :--------- |:---------- | 
| `ColorManager.cs` | `Start` | Set the file path: `string path = Application.persistentDataPath + "/PersistantFilePath/" + "Zurich_QH_total.json"` , and call all functions. | 
|                   | `Loadjson` | Read and load the data from energy demand json file.  Store the data into dictionary with building id as Key and cooling load as Value. | 
|                   |`AssignLoad`| Assign the cooling load on the attached building gameobject.  | 
|                   |`AssignColor`| Assign the color according to the level of demand of the attached building gameobject. | 
|                   |`LoadOnText`| Show cooling demand on top of the building gameobject by changing the text of its children gameobject: TextMeshPro  | 
|   `Colorbar.cs `  |`SetColorbar`| Set the color bar that indicates the level of demand. The highest demand value in this area is rounded to the nearest whole number. This number matches the darkest color, and 0 demand value matches the white color. The color gradient in between shows the interpolation between min and max values of demand. | 
|                   |`LoadOnText`| Display the interpolated figures beside color bar.|
|`House.cs`         |class `Root`| Transferred data from json files using [JSON2CSHARP](https://json2csharp.com) online tool.| 

| Unity Assets | Zurich Heating | Zurich Cooling | Singapore Cooling |
| :--------- | :------------- |:-------------- |:----------------- |
| Scene |`EnergyDemandScene.unity`|`QCEnergyDemandScene.unity`|`QCSingaporeEnergyDemandScene.unity`| 
| Prefabs |`ZRHmodel2809.prefab`|`ZRHModel_QC.prefab`|`Qc_SingaporeEnergyDemand.prefab`|
| Scripts |`ColorManager.cs`,`Colorbar.cs`|`QCColorManager.cs`,`QCColorbar.cs`|`QCSingColorManager.cs`,`QCSingColorbar.cs`|
| Data Scripts|`House.cs`|`House.cs`|`House.cs`|
| Data Files|`Zurich_QH_total.json`| `Zurich_QC_total.json`| `Sing_QC_total.json`|


### Mobility Flow Module   

**Zurich Mobility Flow**       
![Zurich Mobility Flow](RESULTS/ZurichMobility.gif)     

**Singapore Mobility Flow**   
![Singapore Mobility Flow](RESULTS/SingaporeMobility.gif)    

The mobility flow of vehicles and non-vehicles is demonstrated on virtual models which include the terrain and buildings within areas of study. Given the location(latitude, longitude) and time, each user(a person/a vehicle) is represented by one dot(a sphere prefab) showing on the models according to time sequence. Based on real-time records, the mobility flow is speeded up by `timeSpeedupFactor`, which default value is 1000 times faster than real-time.    

The following table summarizes the code for the Zurich case, the Singapore case shares the same structure.   
| Scripts | Function | Description |
| :------------ | :--------- |:---------- | 
| `MobilityFlow.cs` | `Start` | Set the file path: `string path = Application.persistentDataPath + "/PersistantFilePath/" + "Zurich_Mobility.geojson"` , and call all functions. | 
|                   |`LoadJsonFlat`| Read and load the data from a mobility json file, store the data `uid`, `time`, `lon`, `lat` into the list `dataList`, and sort out by time from the earliest to the oldest time. | 
|                   |IEnumerator `InstantiateSpheresWithTimeDelay`| fetches the data from dataList and instantiates sphere prefabs that represent the users according to time. The waiting time is the difference between the previous time spot and the current time spot.| 
|                   |`MapCoordinatesToUnitySpace`| Map latitude and longitude to their corresponding locations on the model using reference points and their respective coordinates from Google Maps, allowing the calculation of new points on the model. | 
|                   |`ShowTime`| Display time on the progress bar.  | 
|`ZurichMobilityJson.cs`|class `ZurichMobilityJson`| Transferred data from json files using [JSON2CSHARP](https://json2csharp.com) online tool according to json file structure.|


| Unity Assets | Zurich | Singapore |
| :-------- | :------------- |:-------------- |
| Scene |`MobilityScene.unity`|`SingMobilityScene.unity`| 
| Prefabs |`ZurichModel0210_buildingterrain.prefab`|`SingaporeMobility.prefab`|
| Scripts |`MobilityFlow.cs`|`SingMobilityFlow.cs`|
| Data Scripts |`ZurichMobilityJson.cs`|`ZurichMobilityJson.cs`|
| Data Files |`Zurich_Mobility.geojson`|`Singapore_Mobility.json`|

### Social Economics (Energy Trade) Module   

**Zurich Energy Trade**     
![Zurich Energy Trade](RESULTS/ZurichEnergyTrade.gif)   

**Singapore Energy Trade**   
![Singapore Energy Trade](RESULTS/SingEnergyTrade.gif)   

The social economics module illustrates energy trading among buildings in the area over the course of a day. When a building's PV panel generates surplus electricity, it trades it with neighboring buildings. Buildings turn blue when selling excess energy, displaying the amount in kWh above them, while those purchasing electricity turn yellow, showing the electricity they receive. Arrows indicate the trading direction and amount (indicated by arrow width).   

The following table summarizes the code for Zurich case, the Sinagpore case shares the same structure.   
| Scripts | Function | Description |
| :------------ | :--------- |:---------- | 
| `EnergyTrade.cs`| `Start` | Set the file path: `string jsonFilePath = Application.persistentDataPath + "/PersistantFilePath/" + "ZurichEnergyTrade.json"` , and call all functions. | 
|                 |`LoadJson`| Read and load data from the energy trade json file. `FromBuilding` sells `transmission` amount of electricity to `ToBuilding` at hour `T`, and these data are stored in a list. | 
|                |IEnumerator `StartLaunchLineRenderers`| Fetch data from dataList and assign corresponding building on the model, and then pass the data to initiate `TEMPChangeBuildingColor`| 
|                |IEnumerator `TEMPChangeBuildingColor`| Assign "from building" location as the start point of the arrow(line renderer) and "to building" as end point. Change the color to blue for "from building" and yellow for "to building". The arrow width is scaled to fit the model size and indicates the amount of transmission electricity. The arrows are destroyed after `prefabStayTime` | 
|                   |`ShowTime`| Display time on progress bar(slider) | 
|`ZurichMobilityJson.cs`|class `ZurichMobilityJson`| Transferred data from json files using [JSON2CSHARP](https://json2csharp.com) online tool according to json file structure.|

| Unity Assets | Zurich | Singapore |
| :------ | :------------- |:-------------- |
| Scene |`EnergyTradeScene.unity`|`EnergyTradeSingaporeScene.unity`| 
| Prefabs |`ZRHmodelEnergyTrade.prefab`|`EnergyTradeSingapore.prefab`|
| Scripts |`EnergyTrade.cs`|`SingEnergyTrade.cs`|
| Data Scripts |`DataEnergyTrade.cs`|`DataEnergyTrade.cs`|
| Data Files | `ZurichEnergyTrade.json` | `EnergyTradeSingapore.json` |

## Debug Image Tracking   
 ../Asset/Scenes/ImageTracking/BasicImageTracking    
This scene is used for checking the image detection works. It is disabled by default. To enable this function, go to `menu.unity` scene, find Debug button under Canvas, and check the box in Inspector.    

| Unity Assets | Content | Description |
| :----- | :------------- | :------------- |
| Scene |`BasicImageTracking.unity`| When an image in the `ReferenceImageLibrary.asset` is detected, the information of this image is displayed in virtual space. |
| Scripts |`TrackedImageInfoManager.cs`||
