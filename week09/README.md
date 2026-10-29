# 주간 박스오피스 조회 (week09)

KOBIS(영화진흥위원회) 일별 박스오피스 API로 특정 날짜의 1위 영화와 영화별 관객 수를 조회하는 코드입니다.

## 설치

Python 3과 아래 패키지가 필요합니다.

```bash
pip install -r requirements.txt
```

같은 폴더에 `secret.py`를 만들고 KOBIS에서 발급받은 API 키를 넣어야 합니다.

```python
API_KEY = "발급받은_키"
```

## 실행

```bash
python main.py
```

`main.py`는 2026년 8월 24일 기준 `3오디세이`의 관객 수를 출력합니다. 다른 날짜나 영화를 보려면 `main.py`의 인자를 바꾸세요. 날짜는 `YYYYMMDD` 형식입니다.
