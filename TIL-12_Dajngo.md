### 2025-10-25

### 장고 실습

- venv는 터미널 단위로 유지된다.
- 폴더를 옮겨도, 터미널을 종료하지 않으면 유지된다.
- 새로운 프로젝트 (버전이 다른) 옮길때 종료 시키고
- 새로운 venv 만들어서 사용하면 된다.


- 프로젝트 폴더 / app폴더 / manage.py 이 구성이 한 폴더 안에 들어있는 구조가 맞다
  <a href="/../create_todo/"> 할일 추가 </a>
- html 링크 삽입, 경로 or 

- urls.py -> 바로 app의 views로 보내기
- 아니면 include로 각 app의 urls에서 관리하기
- 앱 새로 생성하면 settings에 추가

- 뷰함수에서
- return reder(request, '파일')

# 우리가 작성하는 코드
params_dict = {'query': 'python', 'sort': 'accuracy'}
requests.get('http://example.com/search', params=params_dict)

# 실제로 인터넷으로 전송되는 최종 URL
# -> http://example.com/search?query=python&sort=accuracy

# Django views.py 코드
def search_view(request):
    # 누군가 'http://내서버/search?query=python&sort=accuracy'로 접속하면

    # request.GET 에서 값을 꺼내 사용
    search_keyword = request.GET.get('query') # 'python'이 담김
    sort_option = request.GET.get('sort')    # 'accuracy'가 담김

    # ... 이 값들을 이용해 로직 처리 ...