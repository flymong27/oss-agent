작성: Claude Code / 확인: 정준영

# tools.py 함수 정리

- 대상: `week09/tools.py`
- 목적: KOBIS(영화진흥위원회) 일별 박스오피스 API를 호출하는 함수 Ⅱ개 정의
- 함수 목록
  - `get_boxoffice_rank_1(date)`
  - `get_movie_audience(date, title)`

## 공통 사항

- `requests`로 `BASE_URL`(`searchDailyBoxOfficeList.json`) 호출
- 인증키 `API_KEY`는 `secret` 모듈에서 import
- 두 함수 모두 `targetDt` 파라미터에 Ⅷ자리 날짜 문자열을 전달
- 두 함수 모두 `timeout = Ⅹ`(Ⅹ초) 설정
- 두 함수 모두 API 응답의 `boxOfficeResult.dailyBoxOfficeList` 목록을 사용

## 함수별 설명

### `get_boxoffice_rank_1(date)`

- 입력: `date` (문자열, Ⅷ자리 날짜)
- 출력: 해당 날짜 박스오피스 Ⅰ위 영화 제목 (문자열)
- 동작
  Ⅰ. API 호출 후 응답을 JSON(딕셔너리)으로 변환
  Ⅱ. `dailyBoxOfficeList`에서 목록 추출
  Ⅲ. 목록의 첫 번째 항목(`movies[0]`)에서 `movieNm` 반환
- 특징: 목록이 비어 있으면 `IndexError`가 발생할 수 있음

### `get_movie_audience(date, title)`

- 입력: `date` (문자열, Ⅷ자리 날짜), `title` (영화 제목 문자열)
- 출력: 관객수 문자열 또는 순위 없음 안내 문자열
- 동작
  Ⅰ. 같은 API를 호출하고 `dailyBoxOfficeList` 추출
  Ⅱ. 목록을 순회하며 `movieNm`이 `title`과 같은 영화 탐색
  Ⅲ. 일치하는 영화가 있으면 `audiCnt`(관객수)를 천 단위 쉼표 형식으로 변환해 `"-> X,XXX명"` 형태로 반환
  Ⅳ. 일치하는 영화가 없으면 `"'제목' 은(는) 날짜 순위에 없습니다."` 반환
- 특징: `movies[:]`는 리스트 복사본을 만들어 순회하며, 단순 순회 `for movie in movies:`와 결과가 같음

## 참고 사항

- 두 함수에 API 호출 코드(URL, 파라미터, 응답 파싱)가 중복됨
  - 공통 함수로 분리하면 유지보수가 쉬워짐
- 두 함수 모두 `response.status_code`를 확인하지 않음
  - 오류 응답이 오면 `KeyError`가 발생할 수 있음
- `secret` 모듈이 없으면 import 단계에서 실패함
