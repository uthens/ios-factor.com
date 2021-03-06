앱의 설정이라 함은, 기본 코드는 변경되지 않고 배포(App Store, TestFlight, 로컬 환경) 또는 시간이 지남에 따라 변경될 가능성이 있는 모든 것을 뜻합니다. 다음과 같은 것들이 설정에 포함됩니다.

- 백엔드 서비스를 위해 필요한 API 키 (내부 서비스 뿐만 아니라 외부 서비스까지)
- 원격 리소스를 위한 URL (앱이 사용하는 API 주소)
- 기능 토글을 위한 플래그

앱들은 가끔씩 설정을 상수처럼 코드에 저장하곤 합니다. 이것은 iOS-factor에서는 있을 수 없는 일이며, **엄격하게 설정을 코드에서 분리하는** 규칙을 위반하는 경우입니다. 설정은 대체로 배포에 따라 바뀌며, 코드에 따라 바뀌진 않습니다.

앱이 설정을 올바르게 분리했는지 알아보기 위한 가장 확실한 방법은 코드를 지금 당장 어떠한 타협도 없이 오픈 소스화 할 수 있는지를 생각해보는 것입니다.

빌드할 때 설정 값을 건드릴 수 있는 방법은 아주 다양합니다.

- 설정 파일 (예를 들어, JSON 또는 YAML 파일들)
- [cocoapods-keys](https://github.com/orta/cocoapods-keys)를 사용하여 빌드하는 동안 iOS 앱에 보안 키를 안전하게 적용
- 커스텀으로 빌드된 솔루션 (예를 들어, build phase를 사용)

iOS 플랫폼에서 배포하는 것은 서버 배포에 비해서 현저하게 느립니다. 여러분은 이슈에 빨리 대응하기 위해 설정을 OTA(over the air)로 업데이트하길 원하실 수 있습니다.

OTA 설정 업데이트는 강력하고 여러분에게 즉시 다음과 같은 일을 할 수 있게 해줍니다.

- 특정 기능에서 A/B 테스트나 UI 변경을 일부 유저에게만 오픈하기
- API 키 변경하기
- 새로 바뀌는 웹 호스트나 다른 URL을 업데이트하기
- 원격으로 기능이나 버튼을 숨기기

OTA 업데이트가 없다면 앱이 업데이트 되는 것을 며칠동안 기다려야 합니다. 모든 심사 제출은 리젝되어 긴급한 릴리즈를 잠재적으로 연기하는 위험을 포함하고 있습니다.

동시에, 여러분은 반대로도 작동하기를 원할 수도 있습니다. 무슨 뜻이냐면, 최신 iOS 버전으로 업데이트하지 못하는 사용자가 여러분의 앱 업데이트도 설치할 수 없게 만드는 것을 원할 것이란 뜻입니다. OTA에 대한 몇가지 업데이트만 제공하면 과거 버전들에 대한 지원도 유지할 수 있을 것입니다.

설정에서 OTA 업데이트를 구현할 때 잠재적인 접근 방식은 다음과 같습니다.

- 자신만의 솔루션을 구현하는 방법
- [Firebase 원격 설정](https://firebase.google.com/docs/remote-config/)과 같은 웹 서비스를 이용하는 방법
