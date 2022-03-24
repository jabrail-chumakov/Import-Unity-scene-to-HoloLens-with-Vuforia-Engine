# Install software for Unity and Augmented Reality (AR)
## Install Unity 2020+, Vuforia Engine package, Visual Studio 2019 and MRTK
* Download and install [Unity 2020](https://unity3d.com/get-unity/download) or newer. During installation check `IL2CPP Scripting Backend`
* Download and install [Microsoft Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) (16.8 or higher)
* Install Mixed Reality Toolkit (MRTK). It’s required for proper work of the camera. It's better to use [Mixed Reality Feature Tool](https://www.microsoft.com/en-us/download/details.aspx?id=102778) for installation because it's easier. 
  - Just extract folder from zip file and run **MixedRealityFeatureTool.exe**. 
  - Click **Start** and enter the location of your Unity project. After that click **Discover Features**
  - From `Discover Features`, click **Select All** from **Mixed Reality Toolkit** and click **Get Features**
  - Click **Import** - **Approve** - **Exit**
  - Note that it may take some time for importing package into Unity, so be patient **:)**
  - Now MRTK is ready for use. 
  - If you will navigate to Unity you may notice that `MRTK Project Configurator` appeared. Just close this window 
* Install [Vuforia Engine](https://developer.vuforia.com/downloads/sdk) from Official Website (Note: you should manually install this package in case it freezes during installation)
  - You will get file with **.unitypackage** extension. Just double-click on it
  - In Unity `Import Unity Package` window will pop-up
  - Click **All** and **Import**
  - Note that it may take some time for importing package into Unity, so be patient **:)**
  - During importing it may ask to update your project. Click **Update** for that
  - Now Vuforia is ready for use
## Setup your scene
* Run **Unity Hub** and click on **New project** button
* In the appeared window, find **AR** template and click on it. Name your project (e.g., **Franka-HL**), specify the installation path and click on **Create project** button
* In the newly appeared window, you will see **SampleScene** in the `Hierarchy` tab. For our project, we need to create our own scene, but let's change some settings before
* Click `Edit` - `Project Settings` - `XR Plug-in Management`
  - Click on **Universal Windows Platform settings** and check **Windows Mixed Reality** (Unity will install it) and enable **Holographic Remoting** from the dropdown menu of `XR Plug-in Management` in the left. Now you can close `Project Settings`
* Click `File` - `Build Settings` 
  - From left navigate to **Universal Windows Platform (UWP)** 
  - In the `Target Device` select **HoloLens**, `Architecture` to **ARM64** (ARM64 is used for HoloLens 2, while x86 for HoloLens 1), `Build Type` to **D3D project**, `Target SDK Version` to **Latest installed**, `Minimum Platform Version` to **Your lowest version**, `Visual Studio Version` to **Latest installed**, `Build and Run on` to **Local machine** and `Build Configuration` to **Release**. Other options remain unchanged
  - Click `Switch Platform`. Unity icon should appear next to **UWP**
  - Click `Player Settings` - `Player`
  - Navigate to `Publishing Settings` and under `Capabilities` select **Internet Client**, **WebCam**, **Microphone** and **Spatial Perception**. Under `Supported Device Families` select **Holographic**
  - Navigate to `Resolution and Presentation` disable **Run in Background** and in `Default Orientation` select **Landscape Left**
  - Now you can close `Project Settings`
* In **Project** tab right click on **Scenes** folder and then **Create** - **Scene**. Name your scene as **Holemika** and open it.
* Now you have an empty scene with only **Main Camera** and **Directional Light** objects
* Click on **Holemika** in `Hierarchy` tab and add the MRTK to each scene by using `Mixed Reality` - `Toolkit` - `Add to Scene and Configure...`, from the top menu
* Now you will have only 4 parent objects under your **Holemika** scene
* Click on the **MixedRealityToolkit** object and set the configuration profile to the **DefaultHoloLens2ConfigurationProfile** (Or **DefaultHoloLens1ConfigurationProfile**, depending on with which device are you going to work) in **MixedReality Toolkit** component
* Expand **MixedRealityPlayspace** object and in dropdown menu select the **Main Camera**. Click **Add Component** in the `Inspector` tab. Type **VuforiaBehaviour** and select this component. 
  - Click **Open Vuforia Engine configuration** 
  - **IMPORTANT**: In the `Inspector` tab, next to **App Licence Key** enter your licence key. It's free and will be given to you after your registration
## Import URDF model of Franka Emika manipulator
* Go to [URDF Importer](https://github.com/Unity-Technologies/URDF-Importer) webpage and copy git URL for the lasted version of URDF Importer
* In Unity navigate to `Window` - `Package Manager`
  - Click on **+** and in dropdown menu select **Add package from git URL**
  - Paste git URL and click **Add**
* In this repository you may notice **URDF_Franka** folder. It contains URDF model for Franka Emika manipulator
* Place this folder under the `Assets` in `Project` tab of your Unity project and open it
* Inside you will find **panda_arm_hand.urdf** file
* Right click on it and in the appeared list click `Import Robot from Selected URDF file`
  - In `URDF Importer Settings` for `Select Axis Type` choose **Y Axis**, while for `Mesh Decomposer` choose **VHACD**. Let **Overwrite Existing Prefabs** remain unchecked
  - Click **Import URDF**
  - Your model will appear in `Hierarchy` window as a **panda** object
## Vuforia Engine
* In Hierarchy window Right Mouse click in empty space and in the appeared list click **Vuforia Engine** - **Image Target**. This will create **ImageTarget** game object in your scene
* Place your **panda** object under **ImageTarget**, so it becomes subcomponent of it
* Click on **ImageTarget** and in the `Inspector` window navigate to `Image Target Behaviour (Script)`
* Next to `Type` choose **From Database**. New window will appear asking to Import a default database. Click **Import**
* Now it's time to upload your own database. Go to Vuforia Engine developer portal and add your own database. Service will evaluate and rate your mark depending on its features. After that, download createad database and import it to Unity as a Custom Package (or double click on it). The size of imported mark should be exactly the same as of a real one since it affects on tracking features!
* Click **All** and **Import** in Unity. It will import your database inside Unity
* After that, nagiate to your **ImageTarget** object and under **Image Target Behaviour** component next to `Database` choose your imported mark
* You can now adjust position of your mark relative to your panda robot
## Build scene
* Click `File` - `Build settings`
* Click **Add Open Scenes** (Note: there should be only one scene that you’re building)
* Verify that everythings is correct. It should look like this: **place photo**
* Click **Build**
* Now, name a folder in the appeared window and save it (e.g., name folder as “App”)
## Build app
* Open the **.sln** file in a saved folder and wait until Visual Studio will be opened
* On the top of VS, select **Release** and **ARM64** (or x86) and then **Start without Debugging** (Note: at that moment you should connect HoloLens (HL) device to your computer via USB cable. HL should be turned-on at that moment)
* Now wait until it will be fully built into the HL device, it will take some time
* Vuforia Engine logo should appear on a display of your HL and after that, you will observe your scene
