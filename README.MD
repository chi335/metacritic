# 🎮 Game Review Website

게임 정보를 확인하고, 유저들이 리뷰를 작성할 수 있는 웹 애플리케이션입니다. React와 PHP 기반으로 구축되었으며, 사용자는 회원가입을 통해 리뷰를 남기고, 다양한 게임 정보를 확인할 수 있습니다.

---

## 🗂 프로젝트 구조

```bash
project-root/
├── frontend/ # React 프론트엔드 코드
│ ├── src/
│ │ ├── components/
│ │ ├── pages/
│ │ └── ...
│ └── public/
└── backend/       # PHP 백엔드 코드
├── api/           # API 엔드포인트
├── config/        # 설정 파일
└── db/            # 데이터베이스 관련
```

---

## ⚙️ 주요 기능

- 🎲 게임 목록 보기
- 🕹️ 개별 게임 상세 정보 확인
- 📝 리뷰 작성 및 조회
- 👤 사용자 회원가입 및 로그인 

---

## 기술스택
---
### 프론트엔드

- React
- React Router
- Css

## 백엔드
- PHP
- MySQL

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
npm start
```

### 3 ```bash.htaccess``` 파일로 라우팅 설정


## 🔌 API 엔드포인트
---
```bashGET /api/get_games.php``` - 모든 게임 목록 조회

```bashGETGET /api/get_game.php?id=<id>``` - 특정 게임 정보 조회

```bashGETPOST /api/add_review.php``` - 리뷰 추가

```bashGETGET /api/get_reviews.php?game_id=<id>``` - 특정 게임의 리뷰 조회

```bashGETPOST /api/signup_manual.php``` - 일반 회원가입

```bashGETPOST /api/signup_email.php``` - 이메일 인증 회원가입


# 🎮 GameReview Hub - React Application
This repository contains the source code for GameReview Hub, a React application for browsing and reviewing games.

## 📋 Table of Contents
- Core Files

- Components

 - Pages

# 🧩 Core Files
---
## APP.js
```bash
import React from 'react';
import { Routes, Route } from 'react-router-dom';

import Home from './pages/Home/Home';
import GameList from './pages/GameList/GameList';
import GameDetail from './pages/GameDetail/GameDetail';
import Login from './pages/Login/Login';
import Signup from './pages/Signup/Signup';

import Header from './components/Header/Header';

const App = () => {
  return (
    <>
      <Header />
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/games" element={<GameList />} />
        <Route path="/games/:id" element={<GameDetail />} />
        <Route path="/login" element={<Login />} />
        <Route path="/signup" element={<Signup />} />
        <Route path="*" element={<div>페이지를 찾을 수 없습니다.</div>} />
      </Routes>
    </>
  );
};

export default App;
```

## index.js
```bash
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import { BrowserRouter } from 'react-router-dom';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <BrowserRouter basename='/reactproject'>		
    <App />
  </BrowserRouter>
);
```

## App.css
```bash
body {
  margin: 0;
  font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
  background-color: #1b1b1b;
  color: #eee;
}

a {
  color: #4fc3f7;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

.container {
  max-width: 1000px;
  margin: 0 auto;
  padding: 20px;
}

.card {
  background-color: #2a2a2a;
  border-radius: 8px;
  padding: 15px;
  margin-bottom: 15px;
  box-shadow: 0 0 5px rgba(0,0,0,0.5);
}

.score-badge {
  padding: 5px 10px;
  border-radius: 5px;
  color: white;
  font-weight: bold;
}

.score-high {
  background-color: #66bb6a;
}

.score-medium {
  background-color: #fdd835;
}

.score-low {
  background-color: #ef5350;
}
```

## 🎨 Components
---
## Header Component
### Header.jsx

```bash
import React from 'react';
import { Link } from 'react-router-dom';
import './Header.css';

function Header() {
  return (
    <header className="site-header">
      <div className="logo">🎮 GameReview Hub</div>
      <nav className="nav-links">
        <Link to="/">Home</Link>
        <Link to="/games">Games</Link>
        <button className="register-button">Register</button>
      </nav>
    </header>
  );
}

export default Header;
```

### Header.css

```bash
.site-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 20px;
  background-color: #000;
  color: white;
}
.logo { font-size: 1.5rem; font-weight: bold; }
.nav-links { display: flex; align-items: center; gap: 1rem; }
.nav-links a { color: #ffc107; text-decoration: none; font-weight: 500; }
.register-button {
  background-color: #ffc107;
  color: black;
  border: none;
  padding: 6px 12px;
  border-radius: 4px;
  font-weight: bold;
  cursor: pointer;
}
.register-button:hover { background-color: #e0a800; }
```

## GameCard Component
---
### GameCard.jsx

```bash
import React from 'react';
import './GameCard.css';
import { Link } from 'react-router-dom';

function getScoreClass(score) {
  if (score >= 75) return 'high';
  if (score >= 50) return 'mid';
  return 'low';
}

function GameCard({ game }) {
  return (
    <div className="game-card">
      <Link to={`/games/${game.id}`}>
        <img src={game.image_url} alt={game.title} className="game-image" />
        <h3 className="game-title">{game.title}</h3>
      </Link>
      <p className="description">
        {game.description ? game.description.slice(0, 100) + '...' : ''}
      </p>
      <p className="meta-score" data-score={getScoreClass(game.meta_score)}>
        메타 점수: {game.meta_score}
      </p>
      <p className="user-score">유저 점수: {game.user_score}</p>
    </div>
  );
}

export default GameCard;
```

### GameCard.css
```bash
.game-card {
  background-color: #2a2a2a;
  padding: 1rem;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  text-align: center;
  color: #f1f1f1;
}
.game-link { text-decoration: none; color: inherit; }
.game-image { width: 100%; height: auto; border-radius: 6px; }
.game-title {
  font-size: 1.1rem;
  margin: 0.7rem 0 0.5rem;
  color: #ffffff;
  font-weight: bold;
  border-bottom: 1px solid #555;
  padding-bottom: 0.3rem;
}
.description {
  font-size: 0.95rem;
  color: #f5f5f5;
  margin-bottom: 0.7rem;
}
.meta-score {
  background-color: #4caf50;
  color: white;
  display: inline-block;
  padding: 0.2rem 0.6rem;
  border-radius: 5px;
  font-weight: bold;
  font-size: 0.9rem;
}
.user-score {
  font-size: 0.9rem;
  margin-top: 0.4rem;
  color: #ffffff;
}
```

## ReviewForm Component
---
### ReviewForm.jsx

```bash
import React, { useState } from 'react';

function ReviewForm({ gameId }) {
  const [nickname, setNickname] = useState('');
  const [rating, setRating] = useState('');
  const [content, setContent] = useState('');

  const handleSubmit = e => {
    e.preventDefault();
    fetch('http://localhost/server/api/add_review.php', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ game_id: gameId, nickname, rating, content })
    })
      .then(response => response.text())
      .then(() => {
        setNickname('');
        setRating('');
        setContent('');
      });
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" placeholder="닉네임" value={nickname} onChange={e => setNickname(e.target.value)} required />
      <input type="number" placeholder="평점" value={rating} onChange={e => setRating(e.target.value)} required min="0" max="10" />
      <textarea placeholder="리뷰를 작성하세요" value={content} onChange={e => setContent(e.target.value)} required></textarea>
      <button type="submit">리뷰 등록</button>
    </form>
  );
}

export default ReviewForm;
```

## ReviewList Component
---
### ReviewList.jsx

```bash
import React, { useEffect, useState } from 'react';

function ReviewList({ gameId }) {
  const [reviews, setReviews] = useState([]);

  useEffect(() => {
    fetch(`http://localhost/server/api/get_reviews.php?game_id=${gameId}`)
      .then(response => response.json())
      .then(data => setReviews(data));
  }, [gameId]);

  return (
    <div>
      <h3>리뷰 목록</h3>
      {reviews.map(review => (
        <div key={review.id}>
          <p><strong>{review.nickname}</strong> - 평점: {review.rating}</p>
          <p>{review.content}</p>
        </div>
      ))}
    </div>
  );
}

export default ReviewList;
```
## 📄 Pages
---
### Home Page

### Home.jsx
```bash
import React, { useEffect, useState } from 'react';
import GameCard from '../../components/GameCard/GameCard';
import './Home.css';

function Home() {
  const [games, setGames] = useState([]);

  useEffect(() => {
    fetch('/server/api/get_games.php')
      .then(res => res.json())
      .then(data => setGames(data));
  }, []);

  return (
    <main className="home">
      <h2>최신 게임</h2>
      <div className="game-list">
        {games.map(game => (
          <GameCard key={game.id} game={game} />
        ))}
      </div>
    </main>
  );
}

export default Home;
```

### Home.css
```bash
.home {
  padding: 2rem;
}

.game-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 1.5rem;
}
```
## Game List Page
---
### GameList.jsx
```bash
import React, { useEffect, useState } from 'react';
import './GameList.css';

function GameList() {
  const [games, setGames] = useState([]);
  const [searchTerm, setSearchTerm] = useState('');

  useEffect(() => {
    fetch('/server/api/get_games.php')
      .then(res => res.json())
      .then(data => setGames(data));
  }, []);

  const filteredGames = games.filter(game =>
    game.title.toLowerCase().includes(searchTerm.toLowerCase())
  );

  return (
    <main className="game-list-wrapper">
      <h2 className="page-title">전체 게임 목록</h2>
      <input
        type="text"
        className="search-input"
        placeholder="게임 제목 검색..."
        value={searchTerm}
        onChange={(e) => setSearchTerm(e.target.value)}
      />
      <div className="game-horizontal-list">
        {filteredGames.map(game => (
          <div className="horizontal-game-card" key={game.id}>
            <img src={game.image_url} alt={game.title} className="horizontal-game-image" />
            <div className="horizontal-game-info">
              <h3 className="horizontal-game-title">{game.title}</h3>
              <p className="horizontal-description">{game.description?.slice(0, 120)}...</p>
              <p className="meta-score">메타 점수: {game.meta_score}</p>
              <p className="user-score">유저 점수: {game.user_score}</p>
            </div>
          </div>
        ))}
      </div>
    </main>
  );
}

export default GameList;
```
### GameList.css

```bash
body {
  margin: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #1c1c1c;
  color: #f0f0f0;
}

.site-title {
  font-size: 4rem;
  color: #ffffff;
  margin-bottom: 0.3rem;
  font-weight: 700;
}

.nav-links {
  font-size: 2rem;
  margin-bottom: 1rem;
}

.nav-links a {
  color: #f0f0f0;
  margin-right: 0.8rem;
  text-decoration: none;
  font-weight: 500;
}

.nav-links a:hover {
  color: #f5c518;
}

.game-list-wrapper {
  max-width: 1200px;
  margin: 2rem auto;
  padding: 2rem;
}

.page-title {
  font-size: 1.8rem;
  color: #f5c518;
  border-bottom: 1px solid #444;
  padding-bottom: 0.5rem;
  margin-bottom: 1rem;
}

.search-input {
  width: 100%;
  padding: 0.5rem 1rem;
  font-size: 1rem;
  border-radius: 6px;
  border: none;
  margin-bottom: 1.5rem;
  background-color: #2e2e2e;
  color: #fff;
}

.search-input::placeholder {
  color: #aaa;
}

.game-horizontal-list {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.horizontal-game-card {
  display: flex;
  gap: 1.2rem;
  padding: 1rem;
  border-radius: 10px;
  background-color: #2b2b2b;
  box-shadow: 0 0 6px rgba(0, 0, 0, 0.4);
  align-items: center;
}

.horizontal-game-image {
  width: 320px;
  height: 180px;
  object-fit: cover;
  border-radius: 8px;
}

.horizontal-game-info {
  flex: 1;
}

.horizontal-game-title {
  font-size: 1.6rem;
  color: #ffffff;
  font-weight: 800;
  margin-bottom: 0.5rem;
}

.horizontal-description {
  font-size: 1.05rem;
  color: #f2f2f2;
  margin-bottom: 0.6rem;
  line-height: 1.6;
}

.meta-score {
  font-size: 1rem;
  font-weight: 600;
  background-color: #66bb6a;
  display: inline-block;
  padding: 4px 8px;
  border-radius: 4px;
  color: #000;
  margin-right: 0.5rem;
}

.user-score {
  font-size: 1rem;
  color: #dddddd;
}
```
## Game Detail Page
---
### GameDetail.jsx

```bash
import React, { useEffect, useState } from 'react';
import { useParams } from 'react-router-dom';
import ReviewList from '../../components/ReviewList/ReviewList';
import ReviewForm from '../../components/ReviewForm/ReviewForm';
import './GameDetail.css';

function GameDetail() {
  const { id } = useParams();
  const [game, setGame] = useState(null);

  useEffect(() => {
    fetch(`/server/api/get_game.php?id=${id}`)
      .then((res) => res.json())
      .then(setGame);
  }, [id]);

  if (!game) return <p>로딩 중...</p>;

  return (
    <div className="game-detail">
      <h2>{game.title}</h2>
      <img src={game.image_url} alt={game.title} className="game-detail-image" />
      <p className="description">{game.description}</p>
      <p className="meta-score">메타 점수: {game.meta_score}</p>
      <p className="user-score">유저 점수: {game.user_score}</p>

      <h3>리뷰</h3>
      <ReviewList gameId={id} />
      <ReviewForm gameId={id} />
    </div>
  );
}

export default GameDetail;
```

### GameDetail.css

```bash
.game-detail {
  max-width: 800px;
  margin: 2rem auto;
  padding: 2rem;
  background-color: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  font-family: 'Helvetica Neue', sans-serif;
}

.game-detail h2 {
  font-size: 2rem;
  margin-bottom: 1rem;
}

.game-detail-image {
  width: 100%;
  max-height: 400px;
  object-fit: cover;
  border-radius: 10px;
  margin-bottom: 1rem;
}

.description {
  font-size: 1rem;
  color: #333;
  margin-bottom: 1rem;
  line-height: 1.6;
}

.meta-score,
.user-score {
  font-weight: bold;
  margin-bottom: 0.5rem;
  color: #444;
}

h3 {
  margin-top: 2rem;
  font-size: 1.5rem;
  border-bottom: 1px solid #ccc;
  padding-bottom: 0.5rem;
}
```
## Login Page
---
### Login.jsx

```bash
import React, { useState } from 'react';

function Login() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');

  const handleLogin = () => {
    fetch('/server/api/login.php', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ email, password }),
    })
      .then(res => res.json())
      .then(data => {
        if (data.success) {
          alert('로그인 성공');
          localStorage.setItem('user', JSON.stringify(data.user));
          window.location.href = '/';
        } else {
          alert(data.message);
        }
      });
  };

  return (
    <div className="login-container">
      <h2>로그인</h2>
      <input
        type="email"
        placeholder="이메일"
        value={email}
        onChange={e => setEmail(e.target.value)}
      />
      <input
        type="password"
        placeholder="비밀번호"
        value={password}
        onChange={e => setPassword(e.target.value)}
      />
      <button onClick={handleLogin}>로그인</button>
    </div>
  );
}

export default Login;
```

## Signup Page
---
### Signup.jsx

```bash
import React, { useState } from 'react';

function Signup() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [mode, setMode] = useState('manual');

  const handleManualSignup = () => {
    fetch('/server/api/signup_manual.php', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ email, password }),
    })
      .then(res => res.json())
      .then(data => {
        if (data.success) {
          alert('가입 완료');
        } else {
          alert(data.message);
        }
      });
  };

  const handleEmailSignup = () => {
    fetch('/reactproject/api/signup_email.php', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ email }),
    })
      .then(res => res.json())
      .then(data => {
        if (data.success) {
          alert('이메일 인증 완료');
        } else {
          alert(data.message);
        }
      });
  };

  return (
    <div className="signup-container">
      <h2>회원가입</h2>
      <div>
        <button onClick={() => setMode('manual')}>ID/비밀번호로 가입</button>
        <button onClick={() => setMode('email')}>이메일로 가입</button>
      </div>

      {mode === 'manual' && (
        <div>
          <input
            type="email"
            placeholder="이메일"
            value={email}
            onChange={e => setEmail(e.target.value)}
          />
          <input
            type="password"
            placeholder="비밀번호"
            value={password}
            onChange={e => setPassword(e.target.value)}
          />
          <button onClick={handleManualSignup}>가입하기</button>
        </div>
      )}

      {mode === 'email' && (
        <div>
          <input
            type="email"
            placeholder="이메일"
            value={email}
            onChange={e => setEmail(e.target.value)}
          />
          <button onClick={handleEmailSignup}>인증 메일 보내기</button>
        </div>
      )}
    </div>
  );
}

export default Signup;
```

---
## 백엔드 코드 구조
---
### 데이터베이스 스키마 (db/schema.sql)


## games 테이블
```bash
CREATE TABLE games (
  id INT AUTO_INCREMENT PRIMARY KEY,
  title VARCHAR(255) NOT NULL,
  description TEXT,
  meta_score INT,
  user_score FLOAT,
  release_date DATE,
  image_url TEXT
);
```
## game_reviews 테이블
```bash
CREATE TABLE game_reviews (
  id INT AUTO_INCREMENT PRIMARY KEY,
  game_id INT NOT NULL,
  nickname VARCHAR(100),
  rating FLOAT,
  content TEXT,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (game_id) REFERENCES games(id) ON DELETE CASCADE
);
```

## posts 테이블
```bash
CREATE TABLE posts (
  id INT AUTO_INCREMENT PRIMARY KEY,
  title VARCHAR(255) NOT NULL,
  content TEXT,
  author VARCHAR(100),
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```


## post_comments 테이블
```bash
CREATE TABLE post_comments (
  id INT AUTO_INCREMENT PRIMARY KEY,
  post_id INT NOT NULL,
  nickname VARCHAR(100),
  comment TEXT,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (post_id) REFERENCES posts(id) ON DELETE CASCADE
);
```

## users 테이블 (회원가입용)
```bash
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  email VARCHAR(255) NOT NULL UNIQUE,
  password VARCHAR(255),
  signup_method VARCHAR(50) NOT NULL DEFAULT 'manual',
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

## 설정 파일 (config/db_connect.php
```bash
<?php
$host = 'localhost';
$db   = 'metacritic';
$user = 'root';
$pass = '';
$charset = 'utf8mb4';

$dsn = "mysql:host=$host;dbname=$db;charset=$charset";
$options = [
    PDO::ATTR_ERRMODE            => PDO::ERRMODE_EXCEPTION,
    PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
];

try {
     $pdo = new PDO($dsn, $user, $pass, $options);
} catch (\PDOException $e) {
     throw new \PDOException($e->getMessage(), (int)$e->getCode());
}
?>
```
## API 엔드포인트 (api 폴더)
### api/get_games.php

```bash
<?php
require_once __DIR__ . '/../config/db_connect.php';
header('Content-Type: application/json; charset=utf-8');

$sql = "SELECT * FROM games";
$stmt = $pdo->query($sql);
$games = $stmt->fetchAll();

echo json_encode($games);
?>
```

### api/get_game.php
```bash
<?php
require_once __DIR__ . '/../config/db_connect.php';
header('Content-Type: application/json; charset=utf-8');

$id = isset($_GET['id']) ? intval($_GET['id']) : 0;
if ($id <= 0) {
    http_response_code(400);
    echo json_encode(['error' => '잘못된 요청']);
    exit;
}

$stmt = $pdo->prepare("SELECT * FROM games WHERE id = ?");
$stmt->execute([$id]);
$game = $stmt->fetch();

if ($game) {
    echo json_encode($game);
} else {
    http_response_code(404);
    echo json_encode(['error' => '게임을 찾을 수 없습니다']);
}
?>
```

### api/add_review.php
```bash
<?php
require_once __DIR__ . '/../config/db_connect.php';
header('Content-Type: application/json; charset=utf-8');

$data = json_decode(file_get_contents("php://input"), true);

$game_id = intval($data['game_id'] ?? 0);
$nickname = trim($data['nickname'] ?? '');
$rating = floatval($data['rating'] ?? 0);
$content = trim($data['content'] ?? '');

if ($game_id <= 0 || $nickname === '' || $content === '') {
    http_response_code(400);
    echo json_encode(['error' => '입력값이 유효하지 않습니다']);
    exit;
}

$stmt = $pdo->prepare("INSERT INTO game_reviews (game_id, nickname, rating, content, created_at) VALUES (?, ?, ?, ?, NOW())");
$success = $stmt->execute([$game_id, $nickname, $rating, $content]);

echo json_encode(['success' => $success]);
?>
```

### api/get_reviews.php
```bash
<?php
require_once __DIR__ . '/../config/db_connect.php';
header('Content-Type: application/json; charset=utf-8');

$game_id = isset($_GET['game_id']) ? intval($_GET['game_id']) : 0;
if ($game_id <= 0) {
    http_response_code(400);
    echo json_encode(['error' => '잘못된 요청']);
    exit;
}

$stmt = $pdo->prepare("SELECT * FROM game_reviews WHERE game_id = ? ORDER BY created_at DESC");
$stmt->execute([$game_id]);
$reviews = $stmt->fetchAll();

echo json_encode($reviews);
?>
```

### api/signup_manual.php
```bash
<?php
require_once __DIR__ . '/../config/db_connect.php';
header('Content-Type: application/json; charset=utf-8');

$data = json_decode(file_get_contents("php://input"), true);

$email = trim($data['email'] ?? '');
$password = trim($data['password'] ?? '');

if (!filter_var($email, FILTER_VALIDATE_EMAIL) || strlen($password) < 4) {
    http_response_code(400);
    echo json_encode(['success' => false, 'message' => '유효한 이메일/비밀번호 필요']);
    exit;
}

$stmt = $pdo->prepare("SELECT id FROM users WHERE email = ?");
$stmt->execute([$email]);
if ($stmt->fetch()) {
    echo json_encode(['success' => false, 'message' => '이미 존재하는 이메일']);
    exit;
}

$hashed = password_hash($password, PASSWORD_DEFAULT);
$stmt = $pdo->prepare("INSERT INTO users (email, password, signup_method) VALUES (?, ?, 'manual')");
$success = $stmt->execute([$email, $hashed]);

echo json_encode(['success' => $success]);
?>
```

### api/signup_email.php
```bash
<?php
require_once __DIR__ . '/../config/db_connect.php';
header('Content-Type: application/json; charset=utf-8');

$data = json_decode(file_get_contents("php://input"), true);

$email = trim($data['email'] ?? '');

if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
    http_response_code(400);
    echo json_encode(['success' => false, 'message' => '이메일 형식이 올바르지 않음']);
    exit;
}

$stmt = $pdo->prepare("SELECT id FROM users WHERE email = ?");
$stmt->execute([$email]);
if ($stmt->fetch()) {
    echo json_encode(['success' => false, 'message' => '이미 가입된 이메일']);
    exit;
}

 // 실제 인증 메일 발송 대신, 지금은 바로 저장
$stmt = $pdo->prepare("INSERT INTO users (email, signup_method) VALUES (?, 'email_auth')");
$success = $stmt->execute([$email]);

echo json_encode(['success' => $success]);
?>
```

### api/update_games.php
```bash
<?php
ini_set('display_errors', 1);
ini_set('display_startup_errors', 1);
error_reporting(E_ALL);

require_once __DIR__ . '/../config/db_connect.php';

$apiKey = '4182ef1bcc1b4031a914a1077401eb6e'; // RAWG API 키
$totalPages = 3; // 최대 120개 게임 가져오기
$pageSize = 40;

// cURL 함수 정의
function curl_get($url) {
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
    $response = curl_exec($ch);

    if (curl_errno($ch)) {
        echo '❌ cURL 오류: ' . curl_error($ch);
        curl_close($ch);
        exit;
    }

    curl_close($ch);
    return $response;
}

for ($page = 1; $page <= $totalPages; $page++) {
    $apiUrl = "https://api.rawg.io/api/games?key={$apiKey}&page={$page}&page_size={$pageSize}";
    $response = curl_get($apiUrl);
    $data = json_decode($response, true);

    if (!isset($data['results'])) {
        echo "❌ page $page: 응답에 results 없음<br>";
        echo "<pre>"; print_r($data); echo "</pre>";
        continue;
    }

    echo "✅ page $page: " . count($data['results']) . "개 수신<br>";

    foreach ($data['results'] as $game) {
        $title = $game['name'];
        $meta_score = $game['metacritic'] ?? null;
        $user_score = $game['rating'] ?? null;
        $image_url = $game['background_image'] ?? 'https://via.placeholder.com/300x160?text=No+Image';

        // 상세 정보 가져오기 (description)
        $detailUrl = "https://api.rawg.io/api/games/{$game['id']}?key={$apiKey}";
        $detailData = json_decode(curl_get($detailUrl), true);
        $description = $detailData['description_raw'] ?? '';

        // INSERT 또는 UPDATE
        $stmt = $pdo->prepare("INSERT INTO games (title, description, meta_score, user_score, image_url)
                               VALUES (?, ?, ?, ?, ?)
                               ON DUPLICATE KEY UPDATE
                               description = VALUES(description),
                               meta_score = VALUES(meta_score),
                               user_score = VALUES(user_score),
                               image_url = VALUES(image_url)");

        if ($stmt->execute([$title, $description, $meta_score, $user_score, $image_url])) {
            echo "✅ 저장됨: $title<br>";
        } else {
            echo "❌ 저장 실패: $title<br>";
        }
    }

    echo "<hr>";
}

echo "<br>🎉 전체 완료!";
?>
```

## 서버 설정 (.htaccess)
```bash
Options -MultiViews
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^ index.html [QSA,L]
```

## (tasks.json)
```bash
{
    "version": "2.0.0",
    "tasks" : [
        {
            "label": "Run PHP",
            "type": "shell",
            "command": "경로",
            "args": [
                "${file}"
            ],
            "group": {
                "kind": "build",
                "inDefault": true
            },
            "problemMatcher": []
        }
    ]
}
```
