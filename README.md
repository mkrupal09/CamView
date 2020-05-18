# CamView - Capture Image/Video Easily

<img alt="RecyclerView Adapter Library" src="https://github.com/mkrupal09/CamView/blob/master/demo.JPEG" width = "300" height = "633"/>&nbsp;<img alt="RecyclerView Adapter Library" src="https://github.com/mkrupal09/CamView/blob/master/capture.JPEG" width="300" height = "633"/>&nbsp;<img alt="RecyclerView Adapter Library" src="https://github.com/mkrupal09/CamView/blob/master/preview.JPEG" width="300" height="633">
  
# Use Case
1. To capture Image/Video From Camera (Custom Camera) so it'll have many features as native camera provide for intent
2. To Record video for specific length
3. Can customize camera layout/feautres by downloading library
4. Can control some settings for camera. either you only want front camera capture, or need flashed image, or enable sound for capture/ grid showing and many more..

Download
--------

Grab via Maven:
```xml
<dependency>
  <groupId>com.hb.camview</groupId>
  <artifactId>camview</artifactId>
  <version>1.0</version>
  <type>pom</type>
</dependency>
```
or Gradle:
```groovy
implementation 'com.hb.camview:camview:1.0'
```

# How it works?
  ```java
  //Build camera config object by providing customization
  val cameraConfig = CameraConfig.Builder()
                    .setCameraFacing(CameraFacing.BACK_FRONT) // BACK,FRONT,BACK_FRONT
                    .setCameraFlash(CameraFlash.MANUAL) // MANUAL,AUTO,ON,OFF
                    .setCameraType(CameraType.PHOTO) // PHOTO,VIDEO,PHOTO_VIDEO
                    .setVideoLength(45) // Provide length of video
                    .setShowGrid(true) // To show preview grid or not
                    .setPlaySounds(false) // To enable/disable sounds
                    .build()
                    
startActivityForResult(CameraActivity.createIntent(this, cameraConfig,
                    object : CameraActivity.OnCameraCaptureResult {
                        override fun onCameraResult(files: List<File>) {
                            //Load Image/video into your view
                            Glide.with(this).load(files[0]).into(binding.ivImagePick)
                        }
                    }), 123)
```
  
  - and override onActivityResult on Activity/Fragment and write following

```java
  override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
        super.onActivityResult(requestCode, resultCode, data)
         if(requestCode==123) {
            CameraActivity.provideResult(requestCode, resultCode, data)
        }
    }
```

<h2 id="social">Social Media :fire:</h2>

If you like this library, please tell others about it :two_hearts: :two_hearts:

(https://github.com/mkrupal09/PinLView/blob/master/twitter_icon.png)
(https://github.com/mkrupal09/PinLView/blob/master/facebook_icon.png)

[![Share on Twitter](https://github.com/mkrupal09/PinLView/blob/master/twitter_icon.png)]
[![Share on Facebook](https://github.com/mkrupal09/PinLView/blob/master/facebook_icon.png)]

# License

```
Copyright 2017 HiddenBrains

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
