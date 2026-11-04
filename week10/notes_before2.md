# tools.py 함수 정리 (2)

`week09/tools.py`에는 KOBIS(영화진흥위원회) 일별 박스오피스 API를 호출하는 함수가 2개 있습니다.

## 공통 사항

- `requests.get`으로 `BASE_URL`(`searchDailyBoxOfficeList.json`)을 호출합니다.
- 인증키 `API_KEY`는 `secret` 모듈에서 가져옵니다.
- 두 함수 모두 `targetDt` 파라미터에 8자리 날짜(예: `"20261013"`)를 넘깁니다.
- 요청 제한 시간은 `timeout = 10`(10초)입니다.

## 함수

### `get_boxoffice_rank_1(date)`

- **입력**: `date` (문자열, 8자리 날짜)
- **출력**: 그날 박스오피스 1위 영화 제목 (문자열, 예: `"오디세이"`)
- **동작**
  1. API를 호출하고 응답 본문을 딕셔너리로 변환합니다.
  2. `boxOfficeResult` → `dailyBoxOfficeList` 순서로 영화 목록을 꺼냅니다.
  3. 목록의 첫 번째(1위) 항목에서 `movieNm`을 반환합니다.

### `get_movie_audience(date, title)`

- **입력**: `date` (문자열, 8자리 날짜), `title` (영화 제목 문자열)
- **출력**: 관객수 문자열(`"-> 1,234명"`) 또는 "순위에 없음" 안내 문자열
- **동작**
  1. 같은 API를 호출하고 `dailyBoxOfficeList`를 꺼냅니다.
  2. 목록을 돌면서 `movieNm`이 `title`과 같은 영화를 찾습니다.
  3. 찾으면 `audiCnt`(관객수)를 `int`로 바꾼 뒤 천 단위 쉼표를 붙여 반환합니다.
  4. 끝까지 못 찾으면 `"'제목' 은(는) 날짜 순위에 없습니다."`를 반환합니다.

## 참고

- 두 함수는 API 호출과 응답 파싱 코드(URL, 파라미터, JSON 변환, 목록 추출)가 똑같이 중복되어 있습니다. 공통 함수로 빼면 정리하기 좋습니다.
- `get_movie_audience`의 `movies[:]`는 목록 복사본을 만들어 순회하지만, 결과는 `for movie in movies:`와 같습니다.
- 응답 상태 코드(`response.status_code`)는 확인하지 않습니다. 오류 응답이 오면 `data['boxOfficeResult']`에서 `KeyError`가 날 수 있습니다.
- `get_movie_audience`는 `get_boxoffice_rank_1`을 호출하지 않고, 같은 API를 직접 다시 호출합니다. 같은 날짜에 두 번 요청하는 셈입니다.
