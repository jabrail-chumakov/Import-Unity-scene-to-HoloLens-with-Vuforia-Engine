# Install software for Unity and AR
## Install Unity 2020+, VuforiaEngine package, Visual Studio 2019, MRTK and URDF Importer
* Download and install [Unity 2020](https://unity3d.com/get-unity/download) or newer. During installation check `IL2CPP Scripting Backend`
* Download and install [Microsoft Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) (16.8 or higher)
* Install Mixed Reality Toolkit (MRTK). It’s required for proper work of the camera. It's better to use [Mixed Reality Feature Tool](https://www.microsoft.com/en-us/download/details.aspx?id=102778) for installation because it's easier. 
  - Just extract folder from zip file and run **MixedRealityFeatureTool.exe**. 
  - Click **Start** and enter the location of your Unity project. After that click **Discover Features**
  - From `Discover Features`, click **Select All** from **Mixed Reality Toolkit** and click **Get Features**
  - Click **Import** - **Approve** - **Exit**
  - Now MRTK is ready for use (Note: it may take some time for importing package into Unity, so be patient **:)**)
* Install [Vuforia Engine](https://developer.vuforia.com/downloads/sdk) from Official Website (Note: you should manually install this package in case it freezes during installation)
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
* Add the MRTK to each scene by using `Mixed Reality Toolkit` - `Add to Scene and Configure`, from the top menu
* In the **MixedRealityToolkit GameObject**, in each scene, set the configuration profile to the **DefaultHoloLens2ConfigurationProfile** (Or **DefaultHoloLens1ConfigurationProfile**, depending on with which device are you going to work)
* Select the **Main Camera** found as a child of the MixedRealityPlaySpace GameObject and add the **VuforiaBehaviour** component to it from the `Inspector` tab in the right
* **IMPORTANT**: don't forget to enter your licence code in vuforia component
## Import URDF model of Franka Emika manipulator
* Place your URDF model into the `Assets` folder of your Unity project. It will appear automatically in the `Project window` in Unity
* Right Mouse click on your URDF model and in the appeared list click `Import Robot from Selected URDF` file. Your model will appear in `Hierarchy` window.
## Vuforia Engine
* In Hierarchy window Right Mouse click in empty space and in the appeared list click **Vuforia Engine** - **Image Target**. This will create Image Target game object
* Place your **panda** under **ImageTarget** object as a child, so it becomes subcomponent of it.
* Click on **ImageTarget** and in the `Inspector` window navigate to `Image Target Behaviour`, Select `Type` - `From Database`, `Database` - `“Your database”` and `Image Target` - `“Your Image Target”` (Note that before that, you need to import your mark on the Vuforia website. Create an account there and import your mark. It will evaluate and rate your mark depending on its features. After that, download createad database and import it to Unity as a Custom Package. The size of imported mark should be exactly the same as of a real one since it affects on tracking feature!)
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
