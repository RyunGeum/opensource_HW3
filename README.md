# opensource_HW3 오픈소스 개발프로젝트 과제#3

## 1. 개발 내용


### ● 공공데이터 포털의 서울특별시 버스 위치 정보 조회 서비스 api를 이용해 간단한 웹을 개발한다.



1-1. 공공데이터 포털의 api 데이터를 요청함으로써 버스 노선 번호, 위치 정보를 받아온다.

1-2. 그 정보를 바탕으로 웹에 접속하면, “버스 위치 조회” 버튼을 클릭할 수 있게 설정한다.

(버튼이 눌리기 전까지는 아무 정보도 표시되지 않는다.)

1-3. 웹에 접속한 사용자가 “버스 위치 조회” 버튼을 누르면 서울특별시의 지도가 로드된다. 

1-4. 요청한 api 정보에 따른 버스 번호와 그 버스의 위치를 X축, Y축으로 구분해 파란색 핀으로 표시되게 한다.


## 2. 동작 원리


### ● 개발 환경: PyCharm, html 이용

2-1. 웹 환경 구축
![image](https://github.com/2022039078/opensource-HW3/assets/131639123/e6a4b9a8-b387-45c6-88e3-30936e68afd7)

2-2. 공공데이터 api 받아오기
![image](https://github.com/2022039078/opensource-HW3/assets/131639123/b2e30d9a-c82f-469a-8ec2-836017487c2c)
![image](https://github.com/2022039078/opensource-HW3/assets/131639123/106cf489-1b66-43d0-ac85-0cc997279522)

2-3. 지도 호출 및 핀 나타내기
![image](https://github.com/2022039078/opensource-HW3/assets/131639123/9e4c5d5e-39e7-41d2-806d-ab87111a1cb8)
![image](https://github.com/2022039078/opensource-HW3/assets/131639123/021f08c8-6390-42b6-8a6e-117b9a00e9ce)


## 3. 컴파일 및 실행 방법


### ● Phycharm의 코드를 작성한 후 Pycharm 개발 환경 자체에서 미리보기 형식을 지원한다.
### 이 형태로 실행을 해도 결과를 할 수 있다.

또 다른 결과인 웹에서 띄우는 형식을 통해 결과를 확인할 수 있다.

실행 결과는 2단계로 나누어지며, 그 절차는 다음과 같다.

3-1. 사용자가 웹에 접속
![image](https://github.com/2022039078/opensource-HW3/assets/131639123/1e33f316-4696-4250-8d6f-a3c5aa20aee4)

3-2. 사용자가 "버스 위치 조회" 버튼을 클릭
![image](https://github.com/2022039078/opensource-HW3/assets/131639123/ec086779-3a96-40a8-bfde-e34d00c1aa64)


이와 같이 1, 2단계에 거쳐 정상적으로 프로그램이 실행된 것을 확인할 수 있다.

# 전체 코드
```<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>서울시 버스 위치 조회</title>
    <link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
    <style>
        #map {
            height: 500px;
        }
    </style>
</head>
<body>
    <h1>서울시 버스 위치 조회</h1>
    <button onclick="getBusLocations()">버스 위치 조회</button>
    <div id="map"></div>

    <script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
    <script>
        let map;

        function getBusLocations() {
            // 서울시 버스 위치 조회 API 호출
            // API 호출에 필요한 키, 요청 파라미터 등을 설정

            // 서비스 키 입력
            const serviceKey = 'gDz%2F4X9zkedy2m3MtJBiOsnQDPXQu%2F1ux37CGNG6RMazax26QtOKv%2BIwiusd1ePMd34NwmuDHZ12%2FcB14Twj3w%3D%3D';
            const busRouteId = '100100118'; // 버스 노선 ID 입력
            const startOrd = '1';
            const endOrd = '10';

            const corsAnywhere = 'https://cors-anywhere.herokuapp.com/';
            const url = corsAnywhere + 'http://ws.bus.go.kr/api/rest/buspos/getBusPosByRouteSt';
            const queryParams = `?serviceKey=${serviceKey}&busRouteId=${busRouteId}&startOrd=${startOrd}&endOrd=${endOrd}`;

            // AJAX를 사용하여 서버에 요청을 보냄
            const xhr = new XMLHttpRequest();
            xhr.open('GET', url + queryParams);

            // 헤더 추가
            xhr.setRequestHeader('Accept', '*/*');

            xhr.onreadystatechange = function () {
                if (xhr.readyState == 4) {
                    if (xhr.status == 200) {
                        // alert(xhr.responseText);
                        parser = new DOMParser();
                        xmlDoc = parser.parseFromString(xhr.responseText, "text/xml");
                        // alert(xmlDoc);

                        // const response = JSON.parse(xhr.responseText);
                        const response = xmlDoc;
                        displayBusLocations(response);
                    } else {
                        console.error('Failed to fetch bus locations. Status:', xhr.status);
                    }
                }
            };

            xhr.send();
        }

        function displayBusLocations(data) {
            // Leaflet을 사용하여 지도 초기화
            if (!map) {
                map = L.map('map').setView([37.5665, 126.9780], 13);

                // OpenStreetMap 타일 레이어 추가
                L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
                    attribution: '© OpenStreetMap contributors'
                }).addTo(map);
            }

            // 받아온 데이터를 이용하여 마커 표시
            const foo = data.querySelectorAll('itemList');

            foo.forEach(bus => {
                const tmY = bus.querySelector('tmY').textContent;
                const tmX = bus.querySelector('tmX').textContent;
                const plainNo = bus.querySelector('plainNo').textContent;
                const posX = bus.querySelector('posX').textContent;
                const posY = bus.querySelector('posY').textContent;

                const marker = L.marker([Number(tmY), Number(tmX)]).addTo(map);
                marker.bindPopup(`<b>버스 번호:</b> ${plainNo}<br><b>위치:</b> ${posX}, ${posY}`).openPopup();
            });
            /*
            data.ServiceResult.msgBody.itemList.forEach(bus => {
                const marker = L.marker([bus.tmY, bus.tmX]).addTo(map);
                marker.bindPopup(`<b>버스 번호:</b> ${bus.plainNo}<br><b>위치:</b> ${bus.posX}, ${bus.posY}`);
            });
            */
        }
    </script>
</body>
</html> ```
