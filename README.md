# iNaviMaps SDK for Android Demo
Android 플랫폼에서 아이나비 지도를 사용하기 위한 프로젝트 기본 설정 방법을 설명합니다.

## 사전 준비
- 아이나비 지도를 사용하기 위해서는 인증을 위한 **앱키**가 필요합니다.

### 서비스 활성화
- **[NHN Toast Console](https://console.toast.com/)** 에서 서비스 선택 후 Application Service > Maps를 클릭합니다

### 앱키 확인
- **앱키**는 **TOAST Console** 상단 **URL & Appkey** 메뉴에서 확인할 수 있습니다.


## Project 환경 구성
다음과 같이 Project 및 App 모듈 레벨의 build.gradle 파일에 아이나비 지도 저장소를 추가하고, 의존성을 설정합니다.
> SDK 0.6.1 버전부터 새로운 지도 저장소로 배포됩니다. 이전 지도 저장소를 이용하시는 경우 새로운 지도 저장소로 변경하셔야 합니다.
> - 기존 https://dl.bintray.com/inavi-systems/maps/
> - 신규 https://inavisystems.jfrog.io/artifactory/maps/

```gradle
/* Root Project build.gradle */

allprojects {
    repositories {
        google()
        ...
        // 아이나비 지도 저장소
        maven {
            url 'https://inavisystems.jfrog.io/artifactory/maps/'
        }
    }
}
```

```gradle
/* App Module build.gradle */

dependencies {
    implementation 'com.inavi.mapsdk:inavi-maps-sdk:0.6.1'
}
```


## 앱키 설정
발급받은 앱키를 설정할 수 있도록 아래의 두 가지 방법을 제공합니다. 

> `앱키가 설정되지 않으면 지도 초기화 단계에서 인증 오류가 발생합니다.`

### 1. AndroidManifest.xml에서 설정
`AndroidManifest.xml`에 `<meta-data>`를 추가하여 앱키를 설정할 수 있습니다.
```xml
<!-- AndroidManifext.xml -->

<manifest>
    <application>
        <meta-data
            android:name="com.inavi.mapsdk.AppKey"
            android:value="YOUR_APP_KEY" />
    </application>
</manifest>
```

### 2. InaviMapSdk API 호출로 설정
Application 생성 시점에 동적으로 [InaviMapSdk](https://inavi-systems.github.io/inavi-maps-sdk-reference/android/com/inavi/mapsdk/maps/InaviMapSdk.html) 싱글턴 객체의 함수를 호출하여 앱키를 설정할 수 있습니다.

```kotlin
// Kotlin
InaviMapSdk.getInstance(context).appKey = "YOUR_APP_KEY"
```


## 주요 iNavi Maps SDK 안내
추가적인 iNavi Maps SDK 사용법은 [iNavi Maps API 센터](http://imapsapi.inavi.com/)를 참고하시기 바랍니다.
- [사업 제휴 문의](mailto:hongspan@inavi.kr)
- [기술 문의](mailto:abskl@inavi.kr)


## License
© 2019-2021. iNavi Systems Corp. All rights reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
