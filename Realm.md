# Realm Tour Seoul
Realm 모바일 데이터베이스 & 플랫폼 개발자 서울모임 참가내용 정리

## Realm
모바일 데이터 베이스
Apache 2.0 License
쓰고 싶고, 동작속도 빠르고, 다양한 기능을 제공하고, 오픈소스이며 무료인

realm news - 다양한 컨텐츠 제공



## Ralm 기본, 데모
Live Object - 실시간 최신화
객체    -    쿼리
 |           |
트랜젝션 - 노티피케이션

### 객체
class Dog: Object {
  dynamic var age: Int = 0
  dynamic var owner: Person?
}

-> 이 자체가 데이터베이스에 올라감 - 매서드까지 자유롭게 사용

### 쿼리
let puppies = realm
.object(Dog.self)
.fillter("age < 2")

디스크에서 읽어서 메모리에 넣지 않고 리스트 뷰에 넣던지 설정
디스크에 대한 동적 뷰를 만든다고 생각하면 됨

### 노티피케이션
UI설정 -

let token = puppies.addNotificationBlock { change in
  self.updateUI....
}

### 트렌젝션
쓰기때만 트렌젝션이 발생

try realm.write {
  dog.onwer = Person(name:"me")
}



## 네트워크를 이용한 realm (RMP)
restful API의 한계
SQL의 한계

-> realm object server / realm mobile database
only realm으로 가능
realdatabase 로만 통신 - 실시간으로 자동적으로 동기확가 가능해줌

var Realm - require('realm');

var results = realm.ob..

write...

 무료
 인증
 암호화
 실시간 동기화

 유료
 이벤트 핸들링
 수평 스케일링
 지속적인 백업


#RMP

##Scanner
사진 찍기 -> 로컬 디비 -> 서버 디비와 동기화 -> 서버 이벤트핸들러 -> 왓슨에 이미지를 전달 -> 왓은은 분석 -> 처리 결과 이벤트 핸들러 -> 서버 디비 업데이트 -> 로컬 디비 동기화 -> UI에 변경

=> restful 에서 많은 축약이 가능

##realm pop

###Realm Object Server

Realm Mobile Platform = Realm Object Server
 + Realm Mobile Database

각 사이드에 이벤트 핸드러가 있음

관리자는 접근할 수 있는 토큰
웹상에서 관리가 가능

Java (Android):
플러그인으로 등록 -> 디펜던시 등록 -> 버전 관리
매니피스트에 세팅

Swift -> Cocoapod으로 설치

* 객체
class Scan: Object {
  scanId = "" //널을 허용 x
  scan....: ? //널을 허용시 ?
}

* 모델
기본키
primarKey() //기본기 지정

쓰레드 하나에 램 인스턴스가 하나

* 인증
로그인 / 패스워드
등등

* 쓰기
변경 리스너를 통해 클라이언트에서도 볼 수 있음 Key-Value Observation

* 읽기

* 변경 알림
UI갱신

QnA
파시얼 싱크로 클라이언트에게는 부분별 정보만 제공이 가능함

컴플릭스 상황에서는 저의된 룰에 따라 진행됨 -> 유료 기능으로 변경할 수 있음

# 좌충우돌 realm 사용기
할일 관리 목록

데이터 베이스에 등록 -> realm를 선택

렘을 사용하면서 느낀 점

좋았던 점
* 편리함
* 빠른 디비 구성 가능
로컬 디비 : 10% 정도 개발 기간
서버 동기화 : 10% 정도 개발 기간

* 개발자 지원
* 렘 브라우저

- 오브젝트 서버
* macOS 설치
* 간편한 설치
* 편리한 사용자 인증 제공
* 개발자 지원
* 렘 브라우저

아쉬운 점
* 큰 용량 / 긴 빌드시간 : 많은 용량을 차지
* 귀찮은 마이그레이션
* 노티피케이션 : 콜백 핸들러의 아쉬움 -> 트렌젝션이 끝날 때 알수가 없음?
* 공식 예제코드
* 예외 처리 : 위험한 코드가 좀 있었음
* 구조화되지 않은 문서
* 렘 브라우저 : 굉장히 예민함 -> 익셉션이 굉장히 많이 발생 -> 오류 메세지에 대한 구조화 되지 않는 문서, Mac에서만 사용이 가능

- 오브젝트 서버
* 오류의 문서화 부재
* 관리자 페이지
* 동기화 타이밍 잡기: 완료 되었을 때 알려주는 노티가 필요
* 로컬 렘 -> 동기화 렘 미지원
* API 구성 유료


여러대의 클라이언트가 있다면 서버에서 쿼리해서 뽑아쓰는 방식이라 생각
그러나
-> 오브젝트 서버에서도 각자의 사용자 마다 렘 파일을 생성을해서 사용

오프라인 사용자가 서버를 사용하고 싶다 -> 복사가 되어 서버에 올라갈 줄 알았는데
-> 실제로는 서버에서 렘이 생성이 되어 클라이언트에 렘이 또 생성이 됨

로컬에 있는 렘을 최초에 서버에 등록은 불가능
그렇기에 서버에서 마든 렘을 복사해서 넣어줘야 함

생산성은 굉장히 좋아짐
쿼리가 없는 상황에서 좋은 생산성을 제공


빌드 타임 - 스위프트 빌드 타임에 문제가 있음
브라우저 - 멀티 플랫폼으로 다시 만드는 중 / 안드로이드 애드온

노드제에에스에서 렘 블로그 만들기 튜토리얼
다양한 시나리오를 커버

유료기능 - 장벽을 낮추기위한 일

#Welcome to the Real Reactive World

Erik Meijer - Reactive
When you want to stay up to date push

Pull driven - 사용자가 데이터를 요청 - 리프레시
버스 확인할 때 - 시점의 문제가 있음

Push driven - Push Notification - 서버사이드에서 변경시 클라이언트에게 알려준다.


Realm mobile Platform

Google Firebase...


* Clients
인증
설정
동기화

Realm
로그인을 만들어 인증서버를 구현
컨피그를 변경해서 싱크 서버 요청
워퍼를 구성 후 호출하게 됨
로그인을 호출해서 인증된 사용자인 경우에 만듦

Notification(realm, Collection, Object)

Firebase
절차는 realm 동일
