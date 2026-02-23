# 📦 DJL Tokenizers 인텔 맥(x86_64) 라이브러리 연동 가이드

본 라이브러리는 공식 DJL 서버에서 더 이상 배포되지 않는 **인텔 맥(x86_64)** 환경의 정상 작동을 위해, DJL 공식 Rust 소스 코드를 바탕으로 직접 빌드한 결과물입니다.

---

### 1. 전달 파일 정보
* **파일명**: `libtokenizers.dylib`
* **빌드 타겟**: `osx-x86_64` (Intel Mac 전용)
* **소스 출처**: [DJL Official Extensions (Rust)](https://github.com/deepjavalibrary/djl/tree/master/extensions/tokenizers/rust)

---

### 2. 파일 배치 경로 (수동 설치)
서버 다운로드 대신 로컬 파일을 우선 참조하도록 프로젝트 루트 하위의 **jnilib** 폴더에 아래 구조로 파일을 배치해 주세요.

**[파일 배치 경로]**
`[프로젝트 루트] / jnilib / [사용 중인 DJL 버전] / osx-x86_64 / cpu / libtokenizers.dylib`

* **예시**: DJL 0.21.0 버전을 사용하는 경우
  `jnilib/0.21.0/osx-x86_64/cpu/libtokenizers.dylib`

---

### 3. build.gradle.kts 수정 사항
Gradle 빌드 시 인텔 맥 환경에서 해당 파일을 리소스로 인식하도록 매핑 코드를 한 줄 추가해야 합니다.

**수정 위치**: `tasks { processResources { doLast { val files = mapOf(...) } } }`

**추가할 코드 (기존 osx-aarch64 설정 아래에 추가):**
```kotlin
"osx-x86_64/cpu/libtokenizers.dylib" to "$tokenizersVersion/jnilib/$djlVersion"