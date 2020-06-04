![Kropper](https://i.imgur.com/lstHevl.png)
Kropper is a android library,which is used to cropping feature for your mobile app, This app cloned from **Android-Image-Cropper** & I redesigned cropping view as per WhatsApp's croping view that's all.
# Demo

# Setup
##### 1. Provide the gradle dependency
Add it in your root build.gradle at the end of repositories:
``` gradle
	allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}
```

Add the gradle dependency to your `app` module `build.gradle` file:

``` gradle
	dependencies {
	        implementation 'com.github.ajithvgiri:kropper:v1.0'
	}
```

Add permissions to manifest

``` xml
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```

Add this line to your Proguard config file
``` gradle
-keep class androidx.appcompat.widget.** { *; }
```
##### 2. Initialization

##### Kotlin
Start CropImageActivity using builder pattern from your activity
``` kotlin
    // start cropping activity for pre-acquired image saved on the device
    CropImage.activity(imageUri).start(this)
    
        override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
        super.onActivityResult(requestCode, resultCode, data)
        if (requestCode == CropImage.CROP_IMAGE_ACTIVITY_REQUEST_CODE) {
            val result = CropImage.getActivityResult(data)
            if (resultCode == Activity.RESULT_OK) {
                imageView.setImageURI(result.uri)
                textView.visibility = View.GONE
            } else if (resultCode == CropImage.CROP_IMAGE_ACTIVITY_RESULT_ERROR_CODE) {
                val error = result.error
                Toast.makeText(this, "$error", Toast.LENGTH_SHORT).show()
            }
        }
    }
```

#### Java
add below code in your activity
``` java
`   // start cropping activity for pre-acquired image saved on the device
CropImage.activity(imageUri).start(this);

@Override
public void onActivityResult(int requestCode, int resultCode, Intent data) {
  if (requestCode == CropImage.CROP_IMAGE_ACTIVITY_REQUEST_CODE) {
    CropImage.ActivityResult result = CropImage.getActivityResult(data);
    if (resultCode == RESULT_OK) {
      Uri resultUri = result.getUri();
    } else if (resultCode == CropImage.CROP_IMAGE_ACTIVITY_RESULT_ERROR_CODE) {
      Exception error = result.getError();
    }
      }
    }
```
### Screenshots
![Screenshots](https://i.imgur.com/tKvW5cA.png)

# Credits
This library is cloned from [Android Image Cropper](https://github.com/ArthurHub/Android-Image-Cropper).
Library name credit goes to Arthur.

License
----
Copyright 2020 Ajith v

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.