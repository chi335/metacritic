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
└── backend/ # PHP 백엔드 코드
├── api/ # API 엔드포인트
├── config/ # 설정 파일
└── db/ # 데이터베이스 관련
```

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

##📋 Table of Contents
```bashCore Files```

```bashComponents```

```bash Pages```

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

##index.js
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

##App.css
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

##🎨 Components
---
##Header Component
###Header.jsx

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

###Header.css

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

##GameCard Component
---
###GameCard.jsx

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

###GameCard.css
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

##ReviewForm Component
---
###ReviewForm.jsx

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

##ReviewList Component
---
###ReviewList.jsx

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
##📄 Pages
---
###Home Page

###Home.jsx
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

