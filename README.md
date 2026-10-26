# 우리집 작은 습관 정원 | GitHub → Render 실시간 앱

## 구성
- `public/index.html` : 가족 습관 앱
- `public/kids.js` : 세 아이의 요일별 미션
- `render.yaml` : Render Static Site 자동 배포 설정
- `firestore.rules` : Firebase Firestore 보안 규칙 (공개 웹폴더 밖에 둠)

## Firebase 최초 설정 (앱을 실행하려면 필수)
1. https://console.firebase.google.com/ 에서 프로젝트 생성.
2. Authentication > Sign-in method > Email/Password 활성화.
3. Firestore Database 생성, Production mode 선택.
4. Firestore Database > Rules 화면에 `firestore.rules` 파일 내용 붙여 넣고 Publish. 테스트 규칙으로 운영하지 말 것.
5. Project settings > General > Your apps > Web app 등록 > Config의 `apiKey`, `authDomain`, `projectId`, `appId` 확인.
6. `public/index.html`에서 `PASTE_API_KEY`, `PASTE_PROJECT_ID`, `PASTE_APP_ID` 및 `authDomain` 자리를 실제 Config 값으로 변경하여 저장. 웹 클라이언트 설정값이며 서비스 계정 비공개 키는 절대 넣지 말 것.

## GitHub에 업로드
1. https://github.com/new 에서 **새 저장소** `family-habit-garden` 만들기. 기존 영어/역사 앱 저장소는 수정하지 않음.
2. 저장소에서 Add file > Upload files.
3. 압축을 푼 이 폴더의 내용(`public/`, `render.yaml`, `firestore.rules`, `README.md`)을 폴더 구조 그대로 업로드 후 Commit changes.
4. `public/index.html`과 `public/kids.js`가 **public 폴더 안**에 있는지 확인.

## Render에 연결
1. https://dashboard.render.com/ 접속 > New > Static Site.
2. GitHub에서 `family-habit-garden` 저장소를 선택해 연결.
3. Render가 `render.yaml`로 Blueprint 생성을 제안한다면 Blueprint 방식으로 생성 가능. 수동 Static Site를 만들 경우:
   - Name: `family-habit-garden` (중복되면 다른 이름)
   - Branch: `main`
   - Root Directory: 공란
   - Build Command: `echo "Static site"`
   - Publish Directory: `public`
   - Auto Deploy: On / commit
4. Deploy Static Site 선택. 배포 완료 후 제공되는 `https://실제사이트명.onrender.com` 주소 사용.
5. Firebase 콘솔 > Authentication > Settings > Authorized domains > Add domain에 **실제사이트명.onrender.com** 입력. https:// 없이 도메인만 입력.

## 부모/아이 최초 연결
1. 부모: 웹주소 접속 > 회원가입 > 새 가족 만들기 > 가족 ID 복사.
2. 아이 각자: 같은 웹주소 접속 > 별도 계정 가입 > 자신의 UID를 부모에게 전달.
3. 부모: 기기 연결 관리 > UID 붙여넣기 > 아이 지정 > 승인.
4. 아이: 가족 ID 입력 > 가족 연결 확인.
5. 한 기기에서 체크한 내용이 다른 기기 부모 대시보드에 나타나는지 확인.

## 관리 및 주의
- GitHub `main` 브랜치에 수정사항을 올리면 Render가 자동 재배포합니다.
- Render는 웹사이트 제공, Firebase는 인증·실시간 데이터 저장을 담당합니다.
- Firebase 연결 전에는 웹주소만 열리며 로그인·실시간 동기화는 작동하지 않습니다.
- 가족 기록이 브라우저의 이전 단독 앱(localStorage)에서 자동 이전되지는 않습니다.
- 아이의 실명이나 사적 정보를 저장소에 쓰지 말고, 가급적 저장소를 Private으로 설정하세요.
- 필요하면 Firebase의 비밀번호 재설정, 계정 관리, 개인정보 보호 기능을 추가하세요.
