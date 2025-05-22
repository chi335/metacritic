# 🎮 Game Review Website

게임 정보를 확인하고, 유저들이 리뷰를 작성할 수 있는 웹 애플리케이션입니다. React와 PHP 기반으로 구축되었으며, 사용자는 회원가입을 통해 리뷰를 남기고, 다양한 게임 정보를 확인할 수 있습니다.

---

## 🗂 프로젝트 구조

project-root/
├── frontend/ # React 프론트엔드 코드
│ ├── src/
│ │ ├── components/ # 재사용 가능한 UI 컴포넌트
│ │ ├── pages/ # 페이지 단위 컴포넌트
│ │ └── ...
│ └── public/ # 정적 파일
└── backend/ # PHP 백엔드 코드
├── api/ # RESTful API 엔드포인트
├── config/ # 데이터베이스 및 설정 파일
└── db/ # 데이터베이스 스키마 및 연결 설정

yaml
복사
편집

---

## ⚙️ 주요 기능

- 🎲 게임 목록 보기
- 🕹️ 개별 게임 상세 정보 확인
- 📝 리뷰 작성 및 조회
- 👤 사용자 회원가입 및 로그인 (이메일 인증 포함)

---

## 📦 설치 방법

### 1. 리포지토리 클론

```bash
git clone https://github.com/yourusername/game-review-website.git
cd game-review-website
```


### 2. 백엔드 설정

1. MySQL 데이터베이스를 생성합니다.
2. `backend/db/schema.sql` 파일에 포함된 SQL 명령어로 테이블을 생성합니다.
3. `backend/config/db_connect.php` 파일에서 데이터베이스 연결 정보를 본인의 환경에 맞게 설정합니다.  
   (데이터베이스 호스트, 이름, 사용자명, 비밀번호 등을 수정해야 합니다.)

### 3. 프론트엔드 설정

```bash
cd frontend
npm install
npm start```

### 3 ```bash.htaccess``` 파일로 라우팅 설정
