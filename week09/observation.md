실습 2
1.수락 / 명령을 잘 수행함
2. 거절 / read를 해달라고 했는데 write 일 뿐만 아니라 내용도 틀림
3. 거절 / 코드만 봐도 해석이 가능한데 저명령을 실행할 이유가 없음
4. 다르게 지시 / 폴더 안에 tool.py 가 없을 경우 혹은 인식하지 못한 경우 이런 일이 발생할수 있음 절대 경로를 지정해주면 해결된다
5. 승인 / 오타를 잘 고친것으로 추정
6. 다르게 지시 / 코드를 잘못 짜서 main.py를 실제로 사용하고 있지 않을수 있음 정확하게 구조를 보고 분석해달라고 하면된다.


순서 / 도구 이름 / 대상
1 Read c:\projects\oss-week9\readme.md
2 Read c:\projects\oss-week9\실습폴더.txt
3 Read c:\projects\oss-week9\check.py
4 Read c:\projects\oss-week9\average_pandas.py
5 Read c:\projects\oss-week9\average_plain.py
6 Read c:\projects\oss-week9\scores.csv

맡기기 5단계
파일               o/x
check.py:           o
average_pandas.py:  o
average_plain.py:   o
scores.csv:         o


비교항목                   원본                         사본
받는값의 형식              date                         date
예시값                    20261013                    20260101
돌려주는것     그 날짜 박스오피스 1위 영화의 제목 | 해당 날짜 1위 영화의 제목 문자열
틀리거나 애매한 부분     박스오피스 정보가 빠졌다.