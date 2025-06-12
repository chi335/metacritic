## 🎮 게임 리뷰 웹사이트 프로젝트 - reactproject

게임 정보를 확인하고 사용자들이 리뷰를 작성할 수 있는 웹 애플리케이션입니다.
프론트엔드는 React, 백엔드는 PHP + MySQL로 구성되어 있으며, 간단한 로그인 기능과 리뷰 CRUD 기능을 제공합니다.

## 📁 프로젝트 구조

```php
reactproject/

├── frontend/       # React 기반 프론트엔드
│   ├── src/
│   │   ├── components/   # 재사용 가능한 UI 컴포넌트
│   │   ├── pages/        # 페이지별 라우팅 구성
│   │   └── App.jsx       # 메인 컴포넌트
│   ├── public/           # 정적 리소스
│   └── build/            # 빌드 결과물
├── backend/        # PHP 기반 백엔드
│   ├── api/        # API 엔드포인트 (게임/유저/리뷰 처리)
│   ├── db_connect.php    # DB 연결
│   └── static/     # 정적 CSS 리소스
```
## ✨ 주요 기능
---
- 🔍 게임 목록 조회

- 📋 게임 상세 정보 보기

- ✍ 리뷰 작성 및 조회

- 👤 사용자 회원가입 및 로그인

- 🔐 관리자 기능 (권한에 따른 리뷰 삭제 및 유저 관리)

## 🛠️ 기술 스택
### ✅ 프론트엔드
React (Hooks 기반)

React Router DOM

Fetch API

기본 CSS 스타일링

## ✅ 백엔드
PHP (절차지향 스타일)

MySQL (InnoDB)

RESTful API 설계

## ⚙️ 설치 방법
### 📥 리포지토리 클론
```php
git clone https://github.com/couque0319/reactproject.git
cd reactproject
```

## 🛠️ 프론트엔드 설정
'''bash
cd frontend
npm install
npm start
'''

### 🗄️ 백엔드 설정
- backend/db_connect.php 파일을 열어 본인의 DB 설정값을 입력하세요.

- MySQL에 backend/README.md에 포함된 테이블 스키마를 반영하세요.

### 🔄 라우팅 설정 (.htaccess)
- Apache 사용 시 SPA 라우팅 문제 방지를 위한 .htaccess 설정이 포함되어 있습니다.

### 📡 주요 API 엔드포인트 (백엔드)
메소드	경로	설명
| 메소드 | 경로                                 | 설명                 |
| ------ | ------------------------------------ | -------------------- |
| GET    | /api/get_games.php                   | 전체 게임 목록 조회  |
| GET    | /api/get_game.php?id=1               | 특정 게임 정보 조회  |
| POST   | /api/add_review.php                  | 리뷰 작성            |
| GET    | /api/get_reviews.php?game_id=1       | 게임별 리뷰 조회     |
| POST   | /api/register.php                    | 회원가입             |
| POST   | /api/login.php                       | 로그인               |
| GET    | /api/session_status.php              | 로그인 세션 확인     |

## 📄 라이선스
---
본 프로젝트는 학습 및 포트폴리오 용도로 자유롭게 활용 가능합니다.

api key (삭제 예정)

## 🔧 Backend - reactproject
---
React 기반 게임 리뷰 프로젝트의 **백엔드(PHP API)**입니다.

## 디렉토리구조

```php
backend/
├── .htaccess
├── db_connect.php
├── index.html
├── api/
│   ├── add_review.php
│   ├── ask_ai.php
│   ├── check_username.php
│   ├── db.php
│   ├── delete_game.php
│   ├── delete_review.php
│   ├── get_game.php
│   ├── get_games.php
│   ├── get_reviews.php
│   ├── get_reviews_by_user.php
│   ├── get_users.php
│   ├── login.php
│   ├── logout.php
│   ├── register.php
│   ├── session_status.php
│   ├── signup_manual.php
│   ├── update_games.php
│   ├── update_user_role.php
├── static/
│   └── css/
```

## 📌 주요 설명
---
- db_connect.php : DB 연결 설정
- api/ : 게임, 유저, 리뷰 관련 API 핸들러
- static/css/ : 정적 CSS 리소스

## 🧩 PHP API 코드

### api/add_review.php
---

```php
<?php
require_once '../db_connect.php';
header('Content-Type: application/json');
ini_set('display_errors', 1);
error_reporting(E_ALL);

$input = json_decode(file_get_contents("php://input"), true);

$game_id = $input['game_id'] ?? null;
$nickname = $input['nickname'] ?? null;
$rating = $input['rating'] ?? null;
$content = $input['content'] ?? null;

if (!$game_id || !$nickname || !$rating || !$content) {
  echo json_encode(['success' => false, 'message' => '모든 필드를 입력해주세요.']);
  exit;
}

$stmt = $pdo->prepare("INSERT INTO game_reviews (game_id, nickname, rating, content) VALUES (?, ?, ?, ?)");
$success = $stmt->execute([$game_id, $nickname, $rating, $content]);

echo json_encode(['success' => $success]);
?>
 ```

### api/ask_ai.php
---

```php
<?php
// 에러 출력 설정
ini_set('display_errors', 1);
error_reporting(E_ALL);

header('Content-Type: application/json');

// 사용자 입력 받기
$input = json_decode(file_get_contents("php://input"), true);
$question = trim($input['question'] ?? '');

if (!$question) {
  echo json_encode(['error' => '질문이 비어있습니다.']);
  exit;
}

// ✅ 여기 본인의 Gemini API 키 입력 (https://aistudio.google.com/app/apikey)
$apiKey = 'AIzaSyCOdZQkwRaVXqgVVwJ4lF_XH_PeNd7Nw_Q';  // ← 반드시 본인 키로 교체

$endpoint = "https://generativelanguage.googleapis.com/v1/models/gemini-1.5-pro-002:generateContent?key=$apiKey";

$data = [
  'contents' => [
    [
      'parts' => [
        ['text' => $question]
      ]
    ]
  ]
];

$ch = curl_init($endpoint);
curl_setopt_array($ch, [
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_POST => true,
  CURLOPT_HTTPHEADER => ['Content-Type: application/json'],
  CURLOPT_POSTFIELDS => json_encode($data)
]);

$response = curl_exec($ch);
$httpCode = curl_getinfo($ch, CURLINFO_HTTP_CODE);
curl_close($ch);

$result = json_decode($response, true);

// ✅ 성공 응답일 때
if ($httpCode === 200 && isset($result['candidates'][0]['content']['parts'][0]['text'])) {
  echo json_encode([
    'response' => $result['candidates'][0]['content']['parts'][0]['text']
  ]);
} else {
  echo json_encode([
    'error' => $result['error']['message'] ?? 'Gemini 응답 오류',
    'httpCode' => $httpCode,
    'raw' => $response // 필요 시 제거 가능
  ]);
}

```

### api/check_username.php
---

```php
<?php
require_once 'db_connect.php';
header('Content-Type: application/json');

$username = $_GET['username'] ?? '';

if (!$username) {
  echo json_encode(['exists' => false, 'message' => '입력 누락']);
  exit;
}

$stmt = $pdo->prepare("SELECT id FROM users WHERE username = ?");
$stmt->execute([$username]);

$exists = $stmt->fetch() !== false;
echo json_encode(['exists' => $exists]);
```

### api/db.php
---

```php
<?php
$host = 'localhost';
$user = 'root';
$password = '';
$dbname = 'metacritic';

$conn = new mysqli($host, $user, $password, $dbname);

if ($conn->connect_error) {
    die(json_encode(['success' => false, 'message' => 'DB 연결 실패: ' . $conn->connect_error]));
}
?>
```

### api/delete_game.php
---

```php
<?php
require_once 'db_connect.php';
header('Content-Type: application/json');

$data = json_decode(file_get_contents('php://input'), true);
$id = $data['id'] ?? 0;

if (!$id) {
  echo json_encode(['success' => false, 'message' => '게임 ID 누락']);
  exit;
}

$stmt = $pdo->prepare("DELETE FROM games WHERE id = ?");
$success = $stmt->execute([$id]);

echo json_encode(['success' => $success]);
```

### api/delete_review.php
---

```php
<?php
session_start();
require_once '../db_connect.php';
header('Content-Type: application/json');

$input = json_decode(file_get_contents("php://input"), true);
$review_id = $input['id'] ?? null;
$nickname = $_SESSION['nickname'] ?? null;

if (!$review_id || !$nickname) {
  echo json_encode(['success' => false, 'message' => '인증 실패']);
  exit;
}

$stmt = $pdo->prepare("DELETE FROM game_reviews WHERE id = ? AND nickname = ?");
$success = $stmt->execute([$review_id, $nickname]);

echo json_encode(['success' => $success]);
```

### api/get_game.php
---

```php
<?php
require_once(__DIR__ . '/../db_connect.php');
header('Content-Type: application/json');
ini_set('display_errors', 1);
error_reporting(E_ALL);

$id = $_GET['id'] ?? null;
if (!$id) {
  echo json_encode(["error" => "게임 ID 누락"]);
  exit;
}

$stmt = $pdo->prepare("SELECT * FROM games WHERE id = ?");
$stmt->execute([$id]);
$game = $stmt->fetch(PDO::FETCH_ASSOC);

if ($game) {
  echo json_encode($game);
} else {
  echo json_encode(["error" => "게임을 찾을 수 없습니다."]);
}
```

### api/get_games.php
---

```php
<?php
// 에러 표시 설정 (개발환경용)
ini_set('display_errors', 1);
error_reporting(E_ALL);

header('Content-Type: application/json');

// ✅ 정확한 상대경로로 DB 연결
require_once __DIR__ . '/../db_connect.php';

try {
    // 게임 데이터 가져오기
    $stmt = $pdo->prepare("SELECT id, title, description, image_url, meta_score, user_score FROM games");
    $stmt->execute();
    $games = $stmt->fetchAll(PDO::FETCH_ASSOC);

    // ⚠️ JSON 렌더링 불가능한 필드 제거 (선택적)
    /*
    foreach ($games as &$game) {
        foreach ($game as $key => $value) {
            if (is_object($value) || is_array($value)) {
                unset($game[$key]);
            }
        }
    }
    */

    echo json_encode($games);
} catch (Exception $e) {
    // ⛔ JSON 오류 응답
    http_response_code(500);
    echo json_encode([
        'error' => 'DB 오류: ' . $e->getMessage()
    ]);
}
```

### api/get_reviews.php
---

```php
<?php
require_once '../db_connect.php';
header('Content-Type: application/json');

$game_id = $_GET['game_id'] ?? null;

if (!$game_id) {
  echo json_encode(['error' => 'game_id 필요']);
  exit;
}

$stmt = $pdo->prepare("SELECT * FROM game_reviews WHERE game_id = ? ORDER BY created_at DESC");
$stmt->execute([$game_id]);

echo json_encode($stmt->fetchAll(PDO::FETCH_ASSOC));
```

### api/get_reviews_by_user.php
---

```php
<?php
require_once '../db_connect.php';
header('Content-Type: application/json');

$nickname = $_GET['nickname'] ?? '';

if (!$nickname) {
  echo json_encode(['error' => '닉네임이 필요합니다.']);
  exit;
}

$stmt = $pdo->prepare("
  SELECT r.id, r.rating, r.content, r.created_at, g.title AS game_title
  FROM game_reviews r
  JOIN games g ON r.game_id = g.id
  WHERE r.nickname = ?
  ORDER BY r.created_at DESC
");
$stmt->execute([$nickname]);

echo json_encode($stmt->fetchAll(PDO::FETCH_ASSOC));
```


### api/get_users.php
---

```php
<?php
require_once '../db_connect.php';
header('Content-Type: application/json');

$stmt = $pdo->prepare("SELECT id, username, nickname, role FROM users");
$stmt->execute();

$users = $stmt->fetchAll(PDO::FETCH_ASSOC);
echo json_encode($users);
```

### api/login.php
---

```php
<?php
require_once '../db_connect.php';
header('Content-Type: application/json');
session_start();

$input = json_decode(file_get_contents('php://input'), true);
$username = $input['username'] ?? '';
$password = $input['password'] ?? '';

$stmt = $pdo->prepare("SELECT * FROM users WHERE username = ?");
$stmt->execute([$username]);
$user = $stmt->fetch(PDO::FETCH_ASSOC);

if ($user && password_verify($password, $user['password'])) {
  $_SESSION['username'] = $user['username'];
  $_SESSION['nickname'] = $user['nickname'];
  $_SESSION['role'] = $user['role'];

  echo json_encode([
    'success' => true,
    'user' => [
      'username' => $user['username'],
      'nickname' => $user['nickname'],
      'role' => $user['role']
    ]
  ]);
} else {
  echo json_encode(['success' => false, 'message' => '아이디 또는 비밀번호가 틀렸습니다.']);
}
```

### api/logout.php
---

```
<?php
session_start();
session_destroy();
echo json_encode(['success' => true]);
```

### api/register.php
---

```php
<?php
require_once '../db_connect.php';
header('Content-Type: application/json');
session_start();

$input = json_decode(file_get_contents('php://input'), true);
$username = $input['username'] ?? '';
$password = $input['password'] ?? '';
$nickname = $input['nickname'] ?? '';

if (!$username || !$password || !$nickname) {
  echo json_encode(['success' => false, 'message' => '모든 항목을 입력해주세요.']);
  exit;
}

// 중복 체크
$stmt = $pdo->prepare("SELECT * FROM users WHERE username = ?");
$stmt->execute([$username]);
if ($stmt->fetch()) {
  echo json_encode(['success' => false, 'message' => '이미 존재하는 아이디입니다.']);
  exit;
}

$hashed = password_hash($password, PASSWORD_DEFAULT);

$stmt = $pdo->prepare("INSERT INTO users (username, password, nickname, role) VALUES (?, ?, ?, 'user')");
$success = $stmt->execute([$username, $hashed, $nickname]);

echo json_encode(['success' => $success]);
```

### api/session_status.php
---

```php
<?php
session_start();
header('Content-Type: application/json');

if (isset($_SESSION['username'])) {
  echo json_encode([
    'loggedIn' => true,
    'username' => $_SESSION['username'],
    'nickname' => $_SESSION['nickname'],
    'role' => $_SESSION['role']
  ]);
} else {
  echo json_encode(['loggedIn' => false]);
}
```

### api/signup_manual.php
---

```php
<?php
require_once __DIR__ . '/../db_connect.php';
header('Content-Type: application/json; charset=utf-8');

$data = json_decode(file_get_contents("php://input"), true);

$email = trim($data['email'] ?? '');
$username = trim($data['username'] ?? '');
$password = trim($data['password'] ?? '');

// 유효성 검사
if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
    http_response_code(400);
    echo json_encode(['success' => false, 'message' => '유효한 이메일 형식이 아닙니다']);
    exit;
}

if (strlen($username) < 4 || strlen($username) > 20) {
    http_response_code(400);
    echo json_encode(['success' => false, 'message' => 'ID는 4~20자여야 합니다']);
    exit;
}

if (strlen($password) < 6) {
    http_response_code(400);
    echo json_encode(['success' => false, 'message' => '비밀번호는 최소 6자 이상이어야 합니다']);
    exit;
}

// 중복 체크
$stmt = $pdo->prepare("SELECT id FROM users WHERE email = ?");
$stmt->execute([$email]);
if ($stmt->fetch()) {
    http_response_code(409);
    echo json_encode(['success' => false, 'message' => '이미 등록된 이메일입니다']);
    exit;
}

$stmt = $pdo->prepare("SELECT id FROM users WHERE username = ?");
$stmt->execute([$username]);
if ($stmt->fetch()) {
    http_response_code(409);
    echo json_encode(['success' => false, 'message' => '이미 사용 중인 ID입니다']);
    exit;
}

// 비밀번호 해싱
$hashed = password_hash($password, PASSWORD_DEFAULT);

// 저장
$stmt = $pdo->prepare("INSERT INTO users (email, username, password, signup_method, role) VALUES (?, ?, ?, 'manual', 'user')");
$success = $stmt->execute([$email, $username, $hashed]);

echo json_encode(['success' => $success]);
?>
```

### api/update_games.php
---

```php
<?php
ini_set('display_errors', 1);
ini_set('display_startup_errors', 1);
error_reporting(E_ALL);

require_once __DIR__ . '/../db_connect.php';

$apiKey = '672726e2c0b245d99db2592da35bfdc1'; // 🔑 여기에 본인의 RAWG API 키를 입력하세요
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

### api/update_user_role.php
---

```php
<?php
require_once '../db_connect.php';
header('Content-Type: application/json');
ini_set('display_errors', 1);
error_reporting(E_ALL);

$input = json_decode(file_get_contents("php://input"), true);

$id = isset($input['id']) ? (int)$input['id'] : null;
$role = isset($input['role']) ? trim($input['role']) : null;

// 정확하게 유효성 체크
if ($id === null || $id <= 0 || !$role || !in_array($role, ['user', 'admin'])) {
  echo json_encode([
    'success' => false,
    'message' => "잘못된 요청입니다",
    'debug' => ['id' => $id, 'role' => $role]
  ]);
  exit;
}

try {
  $stmt = $pdo->prepare("UPDATE users SET role = ? WHERE id = ?");
  $success = $stmt->execute([$role, $id]);

  echo json_encode([
    'success' => $success,
    'message' => $success ? '권한 변경 성공' : '쿼리 실패',
    'debug' => ['id' => $id, 'role' => $role]
  ]);
} catch (PDOException $e) {
  echo json_encode([
    'success' => false,
    'message' => '쿼리 오류: ' . $e->getMessage()
  ]);
}
```

## 🗄️ 데이터베이스 스키마 (db/schema.sql)
---

### games 테이블
```php
CREATE TABLE `games` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `title` varchar(255) NOT NULL,
  `description` text,
  `meta_score` int(11) DEFAULT NULL,
  `user_score` float DEFAULT NULL,
  `release_date` date DEFAULT NULL,
  `image_url` text,
  PRIMARY KEY (`id`),
  KEY `title` (`title`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;
```

### game_reviews 테이블
---

```php
CREATE TABLE `game_reviews` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `game_id` int(11) NOT NULL,
  `nickname` varchar(100) DEFAULT NULL,
  `rating` float DEFAULT NULL,
  `content` text,
  `created_at` datetime DEFAULT current_timestamp(),
  PRIMARY KEY (`id`),
  KEY `game_id` (`game_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;
```

### users 테이블
---

```php
CREATE TABLE `users` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(100) NOT NULL,
  `password` varchar(255) DEFAULT NULL,
  `signup_method` varchar(50) NOT NULL DEFAULT 'manual',
  `created_at` datetime DEFAULT current_timestamp(),
  `role` enum('user','admin') NOT NULL DEFAULT 'user',
  `nickname` varchar(100) DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `username` (`username`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;
```

### tasks.json

```php
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
---

## 📦 Frontend - reactproject
---
### React 기반 게임 리뷰 프로젝트의 프론트엔드입니다.

## 📁 디렉토리 구조

```php
---
frontend/
├── copy-to-xampp.js
├── package.json
├── package-lock.json
├── .env
├── .gitignore
├── README.md
├── build/
│   ├── index.html
│   ├── favicon.ico
│   ├── manifest.json
│   ├── robots.txt
│   └── static/
│       ├── css/
│       └── js/
├── node_modules/
```


## 📌 주요 설명
- package.json : 프로젝트 의존성과 실행 스크립트 정의
- build/ : npm run build로 생성된 정적 리소스
- .env : 환경 변수 정의 파일
- copy-to-xampp.js : 빌드 결과물을 XAMPP로 복사하는 유틸

## 🧩 JSX 파일 코드
---
### src/components/AIBar/AIBar.jsx
---

```php
import React, { useState } from 'react';
import './AIBar.css';

function AIBar() {
  const [input, setInput] = useState('');
  const [response, setResponse] = useState('');
  const [loading, setLoading] = useState(false);

  const handleSubmit = async (e) => {
    e.preventDefault();
    if (!input.trim()) return;

    setLoading(true);
    setResponse('');

    try {
      const res = await fetch('http://localhost/reactproject/api/ask_ai.php', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ question: input })
      });

      const data = await res.json();
      console.log("Gemini 응답:", data);

      if (data.response) {
        setResponse(data.response);
      } else if (data.error) {
        setResponse('❗ Gemini 오류: ' + data.error);
      } else {
        setResponse('AI 응답 오류');
      }
    } catch (err) {
      setResponse('요청 실패: ' + err.message);
    }

    setLoading(false);
    setInput('');
  };

  return (
    <div className={`ai-container ${response ? 'expanded' : ''}`}>
      <form className="ai-bar" onSubmit={handleSubmit}>
        <input
          type="text"
          placeholder="AI에게 물어보세요..."
          value={input}
          onChange={(e) => setInput(e.target.value)}
        />
        <button type="submit" disabled={loading}>
          {loading ? '...' : '▶'}
        </button>
      </form>

      {response && (
        <div className="ai-response">
          <strong>AI 응답:</strong>
          <p>{response}</p>
        </div>
      )}
    </div>
  );
}

export default AIBar;
```

### src/components/Auth/AuthModal.jsx
---

```php
// src/components/Auth/AuthModal.jsx
import React, { useState } from 'react';
import LoginForm from './LoginForm';
import SignupForm from './SignupForm';
import './AuthModal.css';

function AuthModal({ onClose }) {
  const [mode, setMode] = useState('login');

  return (
    <div className="auth-modal-overlay">
      <div className="auth-modal">
        <button className="close-button" onClick={onClose}>×</button>
        {mode === 'login' ? (
          <>
            <h2>로그인</h2>
            <LoginForm onClose={onClose} />
            <p onClick={() => setMode('signup')}>계정이 없으신가요? <strong>회원가입</strong></p>
          </>
        ) : (
          <>
            <h2>회원가입</h2>
            <SignupForm onClose={onClose} />
            <p onClick={() => setMode('login')}>이미 계정이 있으신가요? <strong>로그인</strong></p>
          </>
        )}
      </div>
    </div>
  );
}

export default AuthModal;
```

### src/components/Auth/LoginForm.jsx
---

```php
import React, { useState } from 'react';

function LoginForm({ onClose }) {
  const [username, setUsername] = useState('');
  const [password, setPassword] = useState('');
  const [loading, setLoading] = useState(false);

  const handleLogin = async () => {
    if (!username || !password) {
      alert('아이디와 비밀번호를 입력해주세요.');
      return;
    }

    setLoading(true);
    try {
      const res = await fetch('/reactproject/api/login.php', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ username, password })
      });

      const data = await res.json();
      if (data.success) {
       alert('로그인 성공');
        onClose();
        setTimeout(() => {
        window.location.reload();
    }, 100); // 짧은 지연으로 모달 정상 닫힘

      } else {
        alert(data.message || '로그인 실패');
      }
    } catch (err) {
      alert('서버 오류가 발생했습니다.');
    } finally {
      setLoading(false);
    }
  };

  return (
    <div className="auth-form">
      <input
        type="text"
        placeholder="아이디"
        value={username}
        onChange={(e) => setUsername(e.target.value)}
        className="auth-input"
      />
      <input
        type="password"
        placeholder="비밀번호"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
        className="auth-input"
      />
      <button onClick={handleLogin} className="auth-button" disabled={loading}>
        {loading ? '처리 중...' : '로그인'}
      </button>
    </div>
  );
}

export default LoginForm;
```

### src/components/Auth/SignupForm.jsx

```php
// SignupForm.jsx
import React, { useState } from 'react';

function SignupForm({ onClose }) {
  const [username, setUsername] = useState('');
  const [password, setPassword] = useState('');
  const [nickname, setNickname] = useState('');
  const [loading, setLoading] = useState(false);

  const handleSignup = async () => {
    if (!username || !password || !nickname) {
      alert('모든 항목을 입력해주세요.');
      return;
    }

    setLoading(true);
    try {
      const res = await fetch('/reactproject/api/register.php', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ username, password, nickname })
      });

      const data = await res.json();
      if (data.success) {
        alert('✅ 회원가입 완료! 로그인해주세요.');
        onClose();
      } else {
        alert(data.message || '❌ 회원가입 실패');
      }
    } catch (error) {
      alert('서버 오류가 발생했습니다.');
    } finally {
      setLoading(false);
    }
  };

  return (
    <div className="auth-form">
      <input
        type="text"
        placeholder="아이디"
        value={username}
        onChange={(e) => setUsername(e.target.value)}
        className="auth-input"
      />
      <input
        type="text"
        placeholder="닉네임"
        value={nickname}
        onChange={(e) => setNickname(e.target.value)}
        className="auth-input"
      />
      <input
        type="password"
        placeholder="비밀번호"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
        className="auth-input"
      />
      <button onClick={handleSignup} className="auth-button" disabled={loading}>
        {loading ? '처리 중...' : '회원가입'}
      </button>
    </div>
  );
}

export default SignupForm;
```

### src/components/GameCard/GameCard.jsx
---

```php
// GameCard.jsx
import React from 'react';
import './GameCard.css';
import { Link } from 'react-router-dom';

function getScoreClass(score) {
  if (score >= 75) return 'high';
  if (score >= 50) return 'mid';
  return 'low';
}

function GameCard({ game }) {
  // 안전하게 데이터 fallback 설정
  const title = typeof game.title === 'string' ? game.title : '제목 없음';
  const description = typeof game.description === 'string' ? game.description.slice(0, 100) + '...' : '설명이 없습니다.';
  const metaScore = typeof game.meta_score === 'number' ? game.meta_score : 'N/A';
  const userScore = typeof game.user_score === 'number' ? game.user_score : 'N/A';

  return (
    <div className="game-card">
      <Link to={`/games/${game.id}`} className="game-link">
        {game.image_url ? (
          <img
            src={game.image_url}
            alt={title}
            className="game-image"
            onError={(e) => (e.target.style.display = 'none')}
          />
        ) : (
          <div style={{ height: '200px', background: '#444' }}>이미지 없음</div>
        )}
        <h3 className="game-title">{title}</h3>
      </Link>

      <p className="description">{description}</p>
      <p className="meta-score" data-score={getScoreClass(game.meta_score)}>
        메타 점수: {metaScore}
      </p>
      <p className="user-score">
        유저 점수: {userScore}
      </p>
    </div>
  );
}

export default GameCard;
```

### src/components/Header/Header.jsx
---

```php
import React, { useEffect, useState } from 'react';
import { Link } from 'react-router-dom';
import './Header.css';

function Header({ onLoginClick }) {
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetch('/reactproject/api/session_status.php', {
      credentials: 'include'
    })
      .then(res => res.json())
      .then(data => {
      console.log("session_status 응답:", data);
      if (data.loggedIn) {
       // user 관련 정보만 따로 저장
       setUser({ username: data.username, role: data.role });
     }
    });
  }, []);

  const handleLogout = () => {
    fetch('/reactproject/api/logout.php', {
      credentials: 'include'
    }).then(() => {
      setUser(null);
      window.location.reload();
    });
  };

  return (
    <header className="header">
      <div className="header-inner">
        <div className="logo">
          <Link to="/">
            <span role="img" aria-label="controller">🎮</span> <strong>GameReview Hub</strong>
          </Link>
        </div>

        <nav className="nav-menu">
          <Link to="/">Home</Link>
          <Link to="/games">Games</Link>
          {user?.role === 'admin' && <Link to="/admin">Admin</Link>}

          {user ? (
            <>
              <span className="username">👤 {user.nickname}</span>
              <Link to="/profile">
                <button className="header-button">Profile</button>
              </Link>
              <button className="header-button" onClick={handleLogout}>Logout</button>
            </>
          ) : (
            <button className="header-button" onClick={onLoginClick}>Register</button>
          )}
        </nav>
      </div>
    </header>
  );
}

export default Header;
```

### src/components/Review/ReviewForm.jsx
---

```php
// ReviewForm.jsx
import React, { useEffect, useState } from 'react';
import './ReviewForm.css';

function ReviewForm({ gameId, onReviewAdded }) {
  const [nickname, setNickname] = useState('');
  const [rating, setRating] = useState('');
  const [content, setContent] = useState('');
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  useEffect(() => {
    fetch('/reactproject/api/session_status.php', {
      credentials: 'include'
    })
      .then(res => res.json())
      .then(data => {
        setIsLoggedIn(data.loggedIn);
        if (data.loggedIn) {
          setNickname(data.nickname);  // ✅ 정확히 nickname 사용
        }
      });
  }, []);

  const handleSubmit = async (e) => {
    e.preventDefault();

    if (!isLoggedIn) {
      alert("로그인 후 이용이 가능합니다.");
      window.dispatchEvent(new Event('open-auth-modal'));
      return;
    }

    const res = await fetch('/reactproject/api/add_review.php', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      credentials: 'include',
      body: JSON.stringify({ game_id: gameId, nickname, rating, content })
    });

    const result = await res.json();
    if (result.success) {
      setRating('');
      setContent('');
      onReviewAdded();  // 리뷰 목록 갱신
    } else {
      alert('리뷰 등록에 실패했습니다.');
    }
  };

  return (
    <form onSubmit={handleSubmit} className="review-form">
      <input type="text" placeholder="닉네임" value={nickname} disabled />
      <input
        type="number"
        placeholder="평점 (0~10)"
        value={rating}
        onChange={(e) => setRating(e.target.value)}
        required
        min="0"
        max="10"
      />
      <textarea
        placeholder="리뷰를 작성하세요"
        value={content}
        onChange={(e) => setContent(e.target.value)}
        required
      />
      <button type="submit">리뷰 등록</button>
    </form>
  );
}

export default ReviewForm;
```

### src/components/Review/ReviewList.jsx
---

```php
// ReviewList.jsx
import React, { useEffect, useState } from 'react';
import './ReviewList.css';

function ReviewList({ gameId }) {
  const [reviews, setReviews] = useState([]);
  const [currentUser, setCurrentUser] = useState('');

  useEffect(() => {
    fetch(`/reactproject/api/get_reviews.php?game_id=${gameId}`)
      .then(res => res.json())
      .then(setReviews);

    fetch('/reactproject/api/session_status.php', {
      credentials: 'include'
    })
      .then(res => res.json())
      .then(data => {
        if (data.loggedIn) {
          setCurrentUser(data.nickname);
        }
      });
  }, [gameId]);

  const handleDelete = (id) => {
    if (!window.confirm('정말 삭제하시겠습니까?')) return;

    fetch('/reactproject/api/delete_review.php', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      credentials: 'include',
      body: JSON.stringify({ id })
    })
      .then(res => res.json())
      .then(result => {
        if (result.success) {
          setReviews(reviews.filter(r => r.id !== id));
        } else {
          alert('삭제에 실패했습니다.');
        }
      });
  };

  if (reviews.length === 0) {
    return <p className="no-review">작성된 리뷰가 없습니다.</p>;
  }

  return (
    <div className="review-list">
      {reviews.map(review => (
        <div key={review.id} className="review-card">
          <div className={`review-score score-${Math.floor(review.rating)}`}>
            {review.rating}
          </div>
          <div className="review-info">
            <div className="review-meta">
              <strong>{review.nickname}</strong>
              <small>{review.created_at}</small>
            </div>
            <p className="review-content">{review.content}</p>
            {currentUser === review.nickname && (
              <div className="review-actions">
                <button onClick={() => handleDelete(review.id)}>삭제</button>
              </div>
            )}
          </div>
        </div>
      ))}
    </div>
  );
}

export default ReviewList;
```

### src/pages/Admin/Admin.jsx
---

```php
// src/pages/Admin.jsx
import React, { useEffect, useState } from 'react';

function Admin() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch('http://localhost/reactproject/api/get_users.php')
      .then(res => res.json())
      .then(data => setUsers(data));
  }, []);

  const updateRole = (username, newRole) => {
    fetch('http://localhost/reactproject/api/update_user_role.php', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ username, role: newRole })
    })
    .then(res => res.json())
    .then(data => alert(data.message));
  };

  const deleteReview = (reviewId) => {
    fetch('http://localhost/reactproject/api/delete_review.php', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ reviewId })
    })
    .then(res => res.json())
    .then(data => alert(data.message));
  };

  return (
    <div>
      <h2>회원 관리</h2>
      <table>
        <thead>
          <tr>
            <th>아이디</th>
            <th>권한</th>
            <th>권한 변경</th>
          </tr>
        </thead>
        <tbody>
          {users.map(user => (
            <tr key={user.username}>
              <td>{user.username}</td>
              <td>{user.role}</td>
              <td>
                <button onClick={() => updateRole(user.username, 'admin')}>Admin</button>
                <button onClick={() => updateRole(user.username, 'user')}>User</button>
              </td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
}

export default Admin;
```

### src/pages/Admin/AdminPanel.jsx
---

```php
import React, { useEffect, useState } from 'react';
import './AdminPanel.css';

function AdminPanel() {
  const [users, setUsers] = useState([]);
  const [selectedNickname, setSelectedNickname] = useState(null);
  const [userReviews, setUserReviews] = useState([]);

  useEffect(() => {
    fetch('/reactproject/api/get_users.php')
      .then(res => res.json())
      .then(setUsers);
  }, []);

  const changeRole = (userId, newRole) => {
    fetch('/reactproject/api/update_user_role.php', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ id: userId, role: newRole })
    })
      .then(res => res.json())
      .then(data => {
        if (data.success) {
          alert('권한 변경 완료');
          // ✅ 상태에서 해당 유저의 role만 업데이트
          setUsers(prev =>
            prev.map(u => (u.id === userId ? { ...u, role: newRole } : u))
          );
        } else {
          alert('변경 실패');
          console.log(data.message);
        }
      });
  };

  const handleUserClick = (nickname) => {
    setSelectedNickname(nickname);
    fetch(`/reactproject/api/get_reviews_by_user.php?nickname=${nickname}`)
      .then(res => res.json())
      .then(setUserReviews);
  };

  const deleteReview = (reviewId) => {
    if (!window.confirm('정말로 이 리뷰를 삭제하시겠습니까?')) return;

    fetch('/reactproject/api/delete_review.php', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ id: reviewId })
    })
      .then(res => res.json())
      .then(data => {
        if (data.success) {
          alert('리뷰 삭제 완료');
          setUserReviews(prev => prev.filter(r => r.id !== reviewId));
        } else {
          alert('리뷰 삭제 실패');
        }
      });
  };

  return (
    <div className="admin-container">
      <h2>👑 관리자 패널</h2>

      <table className="user-table">
        <thead>
          <tr>
            <th>아이디</th>
            <th>닉네임</th>
            <th>권한</th>
            <th>권한 변경</th>
          </tr>
        </thead>
        <tbody>
          {users.map(user => (
            <tr key={user.id}>
              <td>{user.username}</td>
              <td>
                <button
                  className="nickname-button"
                  onClick={() => handleUserClick(user.nickname)}
                >
                  {user.nickname}
                </button>
              </td>
              <td>{user.role}</td> {/* ✅ 현재 권한 표시 */}
              <td>
                <button
                  className="role-user"
                  onClick={() => changeRole(user.id, 'user')}
                >
                  user
                </button>
                <button
                  className="role-admin"
                  onClick={() => changeRole(user.id, 'admin')}
                >
                  admin
                </button>
              </td>
            </tr>
          ))}
        </tbody>
      </table>

      {selectedNickname && (
        <>
          <h3>📝 <span style={{ color: '#0ff' }}>{selectedNickname}</span> 님의 리뷰 목록</h3>
          {userReviews.length === 0 ? (
            <p>작성한 리뷰가 없습니다.</p>
          ) : (
            <div className="review-list">
              {userReviews.map(review => (
                <div className="review-card" key={review.id}>
                  <div className="review-card-header">
                    <div>
                      <p><strong>게임:</strong> {review.game_title}</p>
                      <p><strong>평점:</strong> {review.rating}</p>
                    </div>
                    <button
                      className="review-delete-btn"
                      onClick={() => deleteReview(review.id)}
                    >
                      리뷰 삭제
                    </button>
                  </div>
                  <p className="review-card-content">{review.content}</p>
                </div>
              ))}
            </div>
          )}
        </>
      )}
    </div>
  );
}

export default AdminPanel;
```

### src/pages/GameDetail/GameDetail.jsx
---

```php
// src/pages/GameDetail/GameDetail.jsx
import React, { useEffect, useState } from 'react';
import { useParams } from 'react-router-dom';
import ReviewList from '../../components/Review/ReviewList';
import ReviewForm from '../../components/Review/ReviewForm';
import './GameDetail.css';

function GameDetail() {
  const { id } = useParams();
  const [game, setGame] = useState(null);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch(`/reactproject/api/get_game.php?id=${id}`)
      .then(res => {
        if (!res.ok) throw new Error(`HTTP error: ${res.status}`);
        return res.json();
      })
      .then(data => {
        if (data?.error) {
          setError(data.error);
        } else {
          setGame(data);
        }
      })
      .catch(err => {
        console.error('게임 상세 정보 불러오기 실패:', err);
        setError('서버 오류가 발생했습니다.');
      });
  }, [id]);

  if (error) return <p className="game-detail-wrapper">⚠️ {error}</p>;
  if (!game) return <p className="game-detail-wrapper">로딩 중...</p>;

  return (
    <div className="game-detail-wrapper">
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
    </div>
  );
}

export default GameDetail;
```

### src/pages/GameList/GameList.jsx
---

```php
import React, { useEffect, useState } from 'react';
import { Link } from 'react-router-dom';
import './GameList.css';

function GameList() {
  const [games, setGames] = useState([]);
  const [searchTerm, setSearchTerm] = useState('');

  useEffect(() => {
    fetch('/reactproject/api/get_games.php')
  .then(res => {
    if (!res.ok) throw new Error(`HTTP error: ${res.status}`);
    return res.json();
  })
  .then(data => setGames(data))
  .catch(err => console.error("게임 데이터를 불러오는 중 오류 발생:", err));

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
          <Link to={`/games/${game.id}`} key={game.id} className="horizontal-game-card-link">
            <div className="horizontal-game-card">
              <img src={game.image_url} alt={game.title} className="horizontal-game-image" />
              <div className="horizontal-game-info">
                <h3 className="horizontal-game-title">{game.title}</h3>
                <p className="horizontal-description">{game.description?.slice(0, 120)}...</p>
                <p className="meta-score">메타 점수: {game.meta_score}</p>
                <p className="user-score">유저 점수: {game.user_score}</p>
              </div>
            </div>
          </Link>
        ))}
      </div>
    </main>
  );
}

export default GameList;
```

### src/pages/Home/Home.jsx
---

```php
// src/pages/Home/Home.jsx
import React, { useEffect, useState } from 'react';
import GameCard from '../../components/GameCard/GameCard';
import './Home.css';

function Home() {
  const [games, setGames] = useState([]);

  useEffect(() => {
    fetch('/reactproject/api/get_games.php')
      .then(res => res.json())
      .then(data => {
        console.log("게임 데이터 개수:", data.length);
        console.log("샘플 게임 구조:", data[0]);
        setGames(data);
      })
      .catch(err => console.error("게임 데이터를 불러오는 중 오류:", err));
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

### src/pages/Profile/Profile.jsx
---

```php
// Profile.jsx
import React, { useEffect, useState } from 'react';
import './Profile.css';
import { Link } from 'react-router-dom';

function Profile() {
  const [user, setUser] = useState(null);
  const [reviews, setReviews] = useState([]);

  useEffect(() => {
    fetch('/reactproject/api/session_status.php', {
      credentials: 'include'
    })
      .then(res => res.json())
      .then(data => {
        if (data.loggedIn) {
          setUser(data);

          // 사용자 리뷰 불러오기
          fetch(`/reactproject/api/get_reviews_by_user.php?nickname=${data.nickname}`)
            .then(res => res.json())
            .then(setReviews);
        }
      });
  }, []);

  if (!user) return <p>로그인이 필요합니다.</p>;

  return (
    <div className="profile-wrapper">
      <aside className="profile-sidebar">
        <h2>My Profile</h2>
        <nav>
          <ul>
            <li className="active">MY RATINGS & REVIEWS</li>
            <li><Link to="#">MY ACCOUNT</Link></li>
            <li><Link to="#" onClick={() => {
              fetch('/reactproject/api/logout.php', {
                credentials: 'include'
              }).then(() => window.location.href = '/');
            }}>SIGN OUT</Link></li>
          </ul>
        </nav>
      </aside>

      <main className="profile-main">
        <h3>My Ratings & Reviews</h3>
        {reviews.length === 0 ? (
          <p className="no-review">You haven’t rated anything yet</p>
        ) : (
          <ul className="review-list">
            {reviews.map(r => (
              <li key={r.id}>
                <Link to={`/games/${r.game_id}`}>
                  <strong>{r.game_title}</strong> - ⭐ {r.rating}
                </Link>
                <p>{r.content}</p>
              </li>
            ))}
          </ul>
        )}
      </main>
    </div>
  );
}

export default Profile;
```
