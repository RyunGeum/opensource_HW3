# opensource-HW3

오픈소스 개발프로젝트 과제#3

1. 개발 내용

● 공공데이터 포털의 서울특별시 버스 위치 정보 조회 서비스의 api를 이용해 간단한 웹을 개발한다.

1-1. 공공데이터 포털의 api 데이터를 요청함으로써 버스 노선 번호, 위치 정보를 받아온다.
1-2. 그 정보를 바탕으로 웹에 접속하면, “버스 위치 조회” 버튼을 클릭할 수 있게 설정한다. (버튼이 눌리기 전까지는 아무 정보도 표시되지 않는다.)
1-3. 웹에 접속한 사용자가 “버스 위치 조회” 버튼을 누르면 서울특별시의 지도가 로드된다. 
1-4. 요청한 api 정보에 따른 버스 번호와 그 버스의 위치를 X축, Y축으로 구분해 파란색 핀으로 표시되게 한다.

2. 동작 원리

● 개발 환경: PyCharm, html 이용

2-1. 웹 환경 구축
![image](https://github.com/2022039078/opensource-HW3/assets/131639123/e6a4b9a8-b387-45c6-88e3-30936e68afd7)

2-2. 공공데이터 api 받아오기
![image](https://github.com/2022039078/opensource-HW3/assets/131639123/b2e30d9a-c82f-469a-8ec2-836017487c2c)
![image](https://github.com/2022039078/opensource-HW3/assets/131639123/106cf489-1b66-43d0-ac85-0cc997279522)

2-3. 지도 호출 및 핀 나타내기
![image](https://github.com/2022039078/opensource-HW3/assets/131639123/9e4c5d5e-39e7-41d2-806d-ab87111a1cb8)
![image](https://github.com/2022039078/opensource-HW3/assets/131639123/021f08c8-6390-42b6-8a6e-117b9a00e9ce)

3. 컴파일 및 실행 방법

● Ph/charm의 코드를 작성한 후 Pycharm 개발 환경 자체에서 미리보기 형식을 지원한다. 이 형태로 실행을 해도 결과를 할 수 있다.
또 다른 결과인 웹에서 띄우는 형식을 통해 확인할 수 있다. 실행 결과는 2단계로 나누어지며, 그 절차는 다음과 같다.

3-1. 사용자가 웹에 접속
![image](https://github.com/2022039078/opensource-HW3/assets/131639123/1e33f316-4696-4250-8d6f-a3c5aa20aee4)

3-2. 사용자가 "버스 위치 조회" 버튼을 클릭
![image](https://github.com/2022039078/opensource-HW3/assets/131639123/ec086779-3a96-40a8-bfde-e34d00c1aa64)

이와 같이 1, 2단계에 거쳐 정상적으로 프로그램이 실행된 것을 확인할 수 있다.
