Matisse(V0.5.3-beta3)+Ucrop(V2.2.6)的整合。支持所有Matisse的方法。UCrop没有使用native版本的，太大了，不喜欢。
UCrop开放的三个方法也在Matisse里使用:
`ableCrop:Boolean                 是否开启裁剪（该功能必须是Matisse的maxSelectable为1）`
`isCircleCrop:Boolean             是否显示圆形的裁剪框`
`isHideBottomControls:Boolean     是否关闭Ucrop的底部操作栏`


## 下载
Gradle:

```groovy
repositories {
    jcenter()
}

dependencies {
    implementation 'com.github.BeiHaiCoding:MatisseUcrop:1.0.3'
}
```


## 如何使用?
#### 权限
该库需要使用三个权限:
- `android.permission.READ_EXTERNAL_STORAGE`
- `android.permission.WRITE_EXTERNAL_STORAGE`
- `<uses-permission android:name="android.permission.CAMERA"/>`



#### 使用事例
------


```java
Matisse.from(MainActivity.this)
        .choose(MimeType.ofImage())
        .theme(R.style.Matisse_Dracula)
        .countable(flase)
        .maxSelectable(1)
        .ableCrop(true)
        .isCircleCrop(true)
        .isHideBottomControls(true)
        .restrictOrientation(ActivityInfo.SCREEN_ORIENTATION_UNSPECIFIED)
        .imageEngine(new GlideEngine())
        .showPreview(false) // Default is `true`
        .forResult(REQUEST_CODE_CHOOSE);
```

关于Matisse的更多用法请移步至[Matisse](https://github.com/zhihu/Matisse)

 
没有使用UCrop，获取返回值
```java
List<Uri> mSelected;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (requestCode == REQUEST_CODE_CHOOSE && resultCode == RESULT_OK) {
        mSelected = Matisse.obtainResult(data);
        Log.d("Matisse", "mSelected: " + mSelected);
    }
}
```

使用UCrop，获取返回值
```java
 @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == REQUEST_CODE_CHOOSE && resultCode == RESULT_OK) {
            Uri uri = UCrop.getOutput(data);
            Log.e("OnActivityResult ", String.valueOf(uri));
        }
    }
```


## License

    Copyright 2017 Zhihu Inc.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.


