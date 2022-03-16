# Install software for Unity and AR
## Install Unity 2020+, VuforiaEngine package, Visual Studio 2019, MRTK and URDF Importer
* Download and install Microsoft Visual Studio 2019
* Install Vuforia Engine from Official Website (Note: you should manually install this package because in other cases it will freeze during installation)
* Install Mixed Reality Toolkit (MRTK). It’s required for proper work of the camera.
* In case of any doubts occur, you can refer to the official website of Vuforia, where there is a detailed instruction on how to set up your scene in Unity for HoloLens ([https://library.vuforia.com/articles/Solution/Working-with-the-HoloLens-sample-in-Unity.html](https://library.vuforia.com/articles/Solution/Working-with-the-HoloLens-sample-in-Unity.html))
## Setup your scene
* Create an empty Unity Project
* Click `Edit` - `Project` - `XR Plugin Management`
  - Install **Windows Mixed Reality** and enable **Holographic Remoting** in the `Project settings`
* Click `File` - `Build Settings` - `Player Settings` - `Player`
* Navigate to `Publishing Settings` and under `Capabilities` select **Internet Client**, **WebCam** and **Microphone**. Under `Supported Device Families` select **Holographic**
* Navigate to `Resolution and Presentation` disable **Run in Background** and in `Default Orientation` select **Landscape Left**
* Close `Project Settings`
* Add the MRTK to each scene using `Mixed Reality Toolkit` - `Add to Scene and Configure`, from the top menu
* In the **MixedRealityToolkit GameObject**, in each scene, set the configuration profile to the **DefaultXRSDKConfigurationProfile** (Or **Default HoloLens2**, depending on with which device are you going to work)
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
* 
