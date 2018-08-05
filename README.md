# Pick image from Gallery and camera.
# Developed by 
Manasvi Pundir

# Features

Easy in Implementation. 
No run time permissions required. 
Allow Cropping image.
Compress image.
No manually handling of image path.


# Installation

Add repository url and dependency in application module gradle file:

allprojects {
	repositories {
		...
		maven { url 'https://jitpack.io' }
	}
}

dependencies {
        compile 'com.github.himangipatel:ImagePickerUtil:0.1.8'
}

# Usage

1. Start by creating an instance of ImagePicker and ImageCallBackManager can be called in onCreate().

  ImagePicker imagePicker = new ImagePicker(this, onFileChoose);;
  ImageCallBackManager callBackManager = imagePicker.getCallBackManager();
  
  
2. Callback listener

  private ImagePicker.OnFileChoose onFileChoose = new ImagePicker.OnFileChoose() {
    @Override public void onFileChoose(String fileUri, int requestCode) {
     //  here you will get captured or selected image...
    }
  };
  
  
  
  
3. Call below lines on onRequestPermissionsResult and onActivityResult

 @Override
public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
  super.onRequestPermissionsResult(requestCode, permissions, grantResults);
  if (callBackManager != null) {
    callBackManager.onRequestPermissionsResult(requestCode, permissions, grantResults);
  }
}

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
  super.onActivityResult(requestCode, resultCode, data);
  if (callBackManager != null) {
    callBackManager.onActivityResult(requestCode, resultCode, data);
  }
}


4. Open Camera picker. 

  imagePicker.requestImageCamera(CAMERA_PERMISSION, true, true); // pass false if you dont want to allow image crope
  
5. Open gallery picker. 

 imagePicker.requestImageGallery(STORAGE_PERMISSION_IMAGE, true, true);
 
 
6. Add below code to your manifest 

<provider
       android:name="android.support.v4.content.FileProvider"
       android:authorities="add your package name"
       android:exported="false"
       android:grantUriPermissions="true">
     <meta-data
         android:name="android.support.FILE_PROVIDER_PATHS"
         android:resource="@xml/provider_paths"/>
   </provider>
   
   
7. @xml/provider_paths

  <?xml version="1.0" encoding="utf-8"?>
<paths xmlns:android="http://schemas.android.com/apk/res/android">
    <external-path
        name="external_files"
        path="."/>
</paths>

