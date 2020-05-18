# CamView

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
                    .setCameraFlash(CameraFlash.ALL) // ALL,AUTO,ON,OFF
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
