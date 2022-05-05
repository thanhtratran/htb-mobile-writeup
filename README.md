# Don't Overreact
Bài đầu tiên chủ yểu đọc được code, rồi tìm hidden in4 giấu trong client-side là ra được flag
Đầu tiên đọc trước file AndroidManifest.xml để biết Class nào sẽ chạy đầu tiên khi mở ap
```xml
<application android:theme="@style/AppTheme" android:label="@string/app_name" 
             android:icon="@mipmap/ic_launcher" **android:name="com.awesomeproject.MainApplication" **
             android:allowBackup="false" android:roundIcon="@mipmap/ic_launcher_round" 
             android:appComponentFactory="androidx.core.app.CoreComponentFactory">
    ...
</application>
```
Ta thấy `MainApplication` là điểm bắt đầu
Đọc 1 lượt code thì tới hàm `getBundleAssetName()`

![image](https://user-images.githubusercontent.com/46492646/166906138-783ca30d-333c-496d-b0b2-0e57c95229df.png)

nó return về file `index.android.bundle` trong assets

![image](https://user-images.githubusercontent.com/46492646/166906580-ccfa1808-f68f-45ff-ac6c-04c807366391.png)

Và phần quan trọng nằm ở cuối file:

![image](https://user-images.githubusercontent.com/46492646/166906765-c661ce80-f0fe-402a-9acf-feced176b3e0.png)

Deocde base64 ra lấy flag thôi:

![image](https://user-images.githubusercontent.com/46492646/166906928-34ca6f97-2e65-4e14-b72c-4a166558c33d.png)

# Cat
Đề cho 1 file `cat.ab`, search google thì biết đâu là file Android Backup, mình cần unpack nó ra để xem bên trong file có gì: https://stackoverflow.com/questions/18533567/how-to-extract-or-unpack-an-ab-file-android-backup-file

Cạy cmd trên linux: `java.exe -jar abe.jar unpack cat.ab cat.rar ""`
Sau khi chạy cmd bên trên thì unzip file `cat.rar` ra được 2 folder `app` với `shared`, tìm quanh 1 các tài nguyên để tìm flag:

![image](https://user-images.githubusercontent.com/46492646/166909219-b467325f-1456-4654-9e0e-e073e02d421c.png)

# Don't Overreact
Để làm được bài này, trước hết phải đọc Bài 4 trong series Android Pentest của anh tsu:
https://github.com/tsug0d/AndroidMobilePentest101

Đầu tiên dùng [jadx-gui](https://github.com/skylot/jadx) để reverse file apk

