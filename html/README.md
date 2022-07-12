# janus - vp9svctest 실행 방법

1. settings.js에서 server 주소를 기입합니다.
   1. ex) http://192.168.5.5:8088/janus // http는 8088, s는 8089
2. chrome 브라우저 실행 프로그램의 바로가기를 생성해서 다음과 같이 대상 옵션을 변경합니다.
   1. "C:\Program Files\Google\Chrome\Application\chrome.exe" --user-data-dir="C:\Users\reborn\.chromedata" --unsafely-treat-insecure-origin-as-secure="http://192.168.5.55:8080"
   2. 빈 폴더를 c드라이브 등에 생성해서 user-data-dir에 경로를 줍니다. 개발용 크롬 실행시 폴더 내부는 자동으로 초기화 됩니다.
   3. unsafely-treat-insecure-origin-as-secure는 live-server를 실행한 컴퓨터의 ipv4 주소와 실행된 포트번호를 기입합니다. 이유는 카메라 권한이 http로 실행 시 localhost로 한정되기 때문에 외부에서 192.168.5.55로 접속 시 카메라 권한이 거부되어 작동하지 않기 때문입니다.