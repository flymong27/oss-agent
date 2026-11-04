# tools.py 함수 정리

`week09/tools.py`는 KOBIS(영화진흥위원회) 일별 박스오피스 API를 호출하는 함수 2개를 담고 있습니다.

## 공통 사항

- `requests`로 `BASE_URL`(`searchDailyBoxOfficeList.json`)을 호출합니다.
- 인증키 `API_KEY`는 `secret` 모듈에서 가져옵니다.
- 두 함수 모두 `targetDt` 파라미터로 날짜(8자리, 예: `"20261013"`)를 넘깁니다.

## 함수

### `get_boxoffice_rank_1(date)`

- **입력**: `date` (문자열, 8자리 날짜)
- **출력**: 그날 박스오피스 1위 영화 제목 (문자열)
- **동작**
  1. API를 호출하고 응답을 JSON으로 변환합니다.
  2. `boxOfficeResult.dailyBoxOfficeList`에서 목록을 꺼냅니다.
  3. 첫 번째 항목의 `movieNm`을 반환합니다.

### `get_movie_audience(date, title)`

- **입력**: `date` (문자열, 8자리 날짜), `title` (영화 제목 문자열)
- **출력**: 관객수 문자열 또는 "순위에 없음" 안내 문자열
- **동작**
  1. 같은 API를 호출하고 `dailyBoxOfficeList`를 꺼냅니다.
  2. 목록을 순회하며 `movieNm`이 `title`과 같은 영화를 찾습니다.
  3. 찾으면 `audiCnt`(관객수)를 천 단위 쉼표 형식으로 바꿔 `"-> 1,234명"` 형태로 반환합니다.
  4. 목록에 없으면 `"'제목' 은(는) 날짜 순위에 없습니다."`를 반환합니다.

## 참고

- 두 함수는 API 호출 코드(URL, 파라미터, 응답 파싱)가 똑같이 중복되어 있습니다. 공통 함수로 빼면 정리하기 좋습니다.
- `get_movie_audience`의 `movies[:]`는 리스트 복사본을 만들어 순회하는 것이라, 단순 순회인 `for movie in movies:`와 결과가 같습니다.
- 두 함수 모두 `timeout = 10`을 설정했지만, 응답 상태 코드(`response.status_code`)는 확인하지 않습니다. 오류 응답이 오면 `KeyError`가 날 수 있습니다.
