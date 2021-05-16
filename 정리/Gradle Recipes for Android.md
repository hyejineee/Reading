# 그레이들 레시피

## 1. 안드로이드를 위한 그레이들 기초 

### 안드로이드를 위한 그레이들 파일

* setting.gradle 

  * 안드로이드 프로젝트는 멀티 프로젝트 구조이다.
  * Settings.gradle 파일에 하위 프로젝트(모듈)이 담겨있다. 
  * Include ':app' -> 하위 모듈을 포함하는 방법
  * 안드로이드 라이브러리 프로젝트를 추가한다면 settings.gradle 파일에도 추가

* build.gradle 

  * 프로젝트 build.gradle 파일

  * 프로젝트 build,gradle 파일의 buildscript 블록에는 안드로이드 플러그인을 어디서 다운로드할지 지정한다.

    * 안드로이드 플러그인 : 안드로이드 스튜디오에서 그레이들을 사용하여 앱을 빌드하기 위해 반드시 필요한 플러그인

    * 안드로이드 스튜디오는 그레이들을 기반으로 프로젝트를 빌드함.

    * 안드로이드 스튜디오에서는 안드로이드를 위해 기능이 추가된 android gradle plugin이라는 라이브러리를 사용한다.

    * 기본 값으로 플러그인은 Jcenter에서 다운로드 함.

    * ~~jcenter 앞으로 지원 중단함.~~

      [jcenter 지원 중단 안내](https://developer.android.com/studio/build/jcenter-migration)

  * allprojects 블록 : 최상위 프로젝트와 하위 모듈이 공통으로 사용할 내용을 지정한다. 

* App/build.gradle

  * apply : 안드로이드 플러그인을 지정 
    * 그레이들 플럭그인 : 안드로이드 환경을 위한 DSL를 구현함.

### SDK 버전과 그 외 기본값 설정하기 



