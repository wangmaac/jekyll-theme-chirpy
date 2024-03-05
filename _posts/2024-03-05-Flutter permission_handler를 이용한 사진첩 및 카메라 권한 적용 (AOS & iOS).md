---
layout: post
title:  "Flutter permission_handler를 이용한 사진첩 및 카메라 권한 적용 (AOS & iOS)"
tags: [flutter, permission]
categories: [flutter]
author: frnd
---


## Flutter permission_handler를 이용한 사진첩 및 카메라 권한 적용 (AOS & iOS)

**목차**

1. 개요
2. Android 권한 적용 (33 버전 이전 & 이후)
3. iOS 권한 적용
4. 권한 요청 코드 예시
5. 참고자료

**1. 개요**

Flutter에서 사진첩 및 카메라 권한을 적용하기 위해서는 `permission_handler` 라이브러리를 사용하는 것이 일반적입니다. 이 라이브러리를 통해 플랫폼별 권한 요청 및 상태 확인 기능을 손쉽게 구현할 수 있습니다.

**2. Android 권한 적용**

**2.1. Android 33 버전 이전**

Android 33 버전 이전에는 다음 두 가지 권한이 필요했습니다.

- `READ_EXTERNAL_STORAGE`: 사진첩 접근 권한
- `CAMERA`: 카메라 사용 권한

**AndroidManifest.xml:**

XML

```yaml
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-feature android:name="android.hardware.camera" />
```

코드를 사용할 때는 [주의](https://gemini.google.com/faq#coding)가 필요합니다.

content_copy

**2.2. Android 33 버전 이후**

Android 33 버전부터 사진첩 접근 방식이 변경되어 새로운 권한 `MANAGE_EXTERNAL_STORAGE`가 도입되었습니다.

- `READ_EXTERNAL_STORAGE`: **더 이상 사진첩 접근 권한을 제공하지 않습니다.**
- `WRITE_EXTERNAL_STORAGE`: 앱 내부 저장소에 대한 쓰기 권한
- `MANAGE_EXTERNAL_STORAGE`: 모든 앱 데이터에 대한 읽고 쓰기 권한 (사진첩 포함)

따라서 **사진첩 접근**을 위해서는 `MANAGE_EXTERNAL_STORAGE` 권한을 요청해야 합니다.

**AndroidManifest.xml:**

XML

```yaml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.MANAGE_EXTERNAL_STORAGE" />
<uses-feature android:name="android.hardware.camera" />
```

코드를 사용할 때는 [주의](https://gemini.google.com/faq#coding)가 필요합니다.

content_copy

**3. iOS 권한 적용**

iOS에서는 다음 두 가지 권한이 필요합니다.

- `PHPhotoLibrary`: 사진첩 접근 권한
- `AVCaptureDevice`: 카메라 사용 권한

**Info.plist:**

XML

```
<key>NSPhotoLibraryUsageDescription</key>
<string>사진첩 접근 권한이 필요합니다.</string>
<key>NSCameraUsageDescription</key>
<string>카메라 사용 권한이 필요합니다.</string>
```

코드를 사용할 때는 [주의](https://gemini.google.com/faq#coding)가 필요합니다.

content_copy

**4. 권한 요청 코드 예시**

Dart

```dart
import 'package:permission_handler/permission_handler.dart';

Future<void> requestPermission() async {
  final status = await Permission.photos.request();
  if (status.isGranted) {
    // 권한 부여 시 처리
  } else {
    // 권한 거부 시 처리
  }

  final cameraStatus = await Permission.camera.request();
  if (cameraStatus.isGranted) {
    // 권한 부여 시 처리
  } else {
    // 권한 거부 시 처리
  }
}
```


**5. 참고자료**

- permission_handler 공식 문서: [https://pub.dev/packages/permission_handler](https://pub.dev/packages/permission_handler)
- Android 33 버전 권한 변경 내용: []
- iOS 권한 설정: []

#### 소스

[info](https://gemini.google.com/faq#citation)

1. [forum.mendix.com/link/questions/96273](https://forum.mendix.com/link/questions/96273)
    
2. [github.com/dmitryweiner/android-lectures](https://github.com/dmitryweiner/android-lectures)
    
3. [github.com/Ahmed-hussien90/Equation_Solver](https://github.com/Ahmed-hussien90/Equation_Solver)
    
4. [github.com/Ladro-Kim/saladDa](https://github.com/Ladro-Kim/saladDa)
