# JCHS-Classmate-Server

> 학생용 시간표 앱 Classmate 서버, 컴시간·리로스쿨·NEIS 연동 (Spring Boot)

제천고등학교 코딩 동아리 코딩연구소에서 2023년에 만든 학생용 시간표 앱 Classmate(개발 당시 이름 School Helper)의 백엔드 서버다. 제천고 학생의 학년·반·번호를 받아 그날의 시간표와 급식을 돌려준다.

## 주요 기능
- 학생 시간표 조회 (`GET /timetable?grade=&class=&id=`, 날짜는 `year`, `month`, `day`로 선택)
- 컴시간알리미의 반 시간표를 기본으로 쓰고, 2·3학년은 리로스쿨에서 학생별 수업을 가져와 같은 교시를 덮어쓴다
- 리로스쿨 세션이 만료되면 다시 로그인한다
- NEIS Open API로 급식 조회 (`GET /meal`, 날짜는 `year`, `month`, `day`로 선택)
- 날짜·학생별 시간표와 급식을 메모리에 캐시하고, 주말은 빈 시간표를 돌려준다

## 기술 스택
| 영역 | 기술 |
|---|---|
| 언어 | Java 17 |
| 프레임워크 | Spring Boot 3.1.0-SNAPSHOT (Web), Lombok |
| 외부 연동 | 컴시간알리미, 리로스쿨, NEIS Open API (OkHttp, Jsoup, Gson) |

## 구조
```
src/main/java/com/github/ioloolo/schoolhelper/
  SchoolHelperApplication.java
  controllers/   /timetable, /meal
  services/      시간표 병합, 급식 조회
  api/           ComciganApi, RiroSchoolApi, NeisApi
  cache/         시간표·급식 메모리 캐시
  data/          TimeTable, Meal, Student
```

## 실행
```bash
./gradlew bootRun
```
`src/main/resources/application.yaml`(저장소에 없음)에 리로스쿨 계정 `app.riroschool.id`, `app.riroschool.pw`를 넣어야 한다.

## 관련 저장소
- [JCHS-Classmate-Client](https://github.com/son-daehyeon/JCHS-Classmate-Client) — Apple Watch 앱
- [JCHS-Teacher-Plan-Server](https://github.com/son-daehyeon/JCHS-Teacher-Plan-Server) — 교사용 앱 서버

---
2023 · 개인 프로젝트 · 보관됨
