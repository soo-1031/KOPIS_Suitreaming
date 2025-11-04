# 🎯 로컬 데모 실행 가이드

이 문서는 GitHub에 업로드하지 않고 로컬에서만 데모를 실행하는 방법을 안내합니다.

## ✅ 사전 준비 완료

- ✅ Python 3.13.2 설치 완료
- ✅ Node.js v22.19.0 설치 완료
- ✅ Backend 의존성 설치 완료
- ✅ Frontend 의존성 설치 완료
- ✅ PAMS.csv 파일 확인 완료

## 🚀 서버 실행 방법

### 방법 1: 두 개의 터미널 사용 (권장)

#### 터미널 1: Backend 서버 실행
```bash
cd /Users/hyunsoolee/Desktop/KOPIS_2025/KOPIS_원본코드s/backend
python -m uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

**성공 메시지:**
```
INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
INFO:     Started reloader process
INFO:     Started server process
INFO:     Waiting for application startup.
Loading PAMS.csv into database...
Data loaded successfully!
Initializing Chroma vector store...
```

#### 터미널 2: Frontend 서버 실행
```bash
cd /Users/hyunsoolee/Desktop/KOPIS_2025/KOPIS_원본코드s/frontend
npm start
```

**성공 메시지:**
```
Compiled successfully!

You can now view frontend in the browser.

  Local:            http://localhost:3001
  On Your Network:  http://192.168.x.x:3001
```

### 방법 2: 자동 스크립트 사용

**macOS/Linux:**
```bash
cd /Users/hyunsoolee/Desktop/KOPIS_2025/KOPIS_원본코드s
./start.sh
```

**Windows:**
```bash
cd C:\Users\...\KOPIS_원본코드s
start.bat
```

## 🌐 접속 주소

서버가 실행되면 다음 주소로 접속할 수 있습니다:

### 1. **프론트엔드 (메인 웹사이트)**
```
http://localhost:3001
```
브라우저에서 이 주소를 열면 데모 웹사이트를 볼 수 있습니다.

### 2. **백엔드 API**
```
http://localhost:8000
```

### 3. **API 문서 (Swagger UI)**
```
http://localhost:8000/docs
```
모든 API 엔드포인트를 테스트할 수 있는 인터랙티브 문서입니다.

### 4. **API 문서 (ReDoc)**
```
http://localhost:8000/redoc
```

## 📱 데모 기능 체크리스트

서버가 실행되면 다음 기능들을 테스트해보세요:

- [ ] **홈페이지**: http://localhost:3001 에서 메인 페이지 확인
- [ ] **쇼케이스 목록**: 공연 목록 조회
- [ ] **쇼케이스 상세**: 개별 공연 정보 확인
- [ ] **유사도 검색**: BGE-M3 벡터 검색 테스트
- [ ] **북커 매칭**: 프로필 기반 추천 기능
- [ ] **ROI 계산기**: 수익성 분석 도구
- [ ] **KOPIS 데이터**: KOPIS API 연동 확인 (인터넷 필요)

## 🛑 서버 중지 방법

### 방법 1: 터미널에서
각 터미널에서 `Ctrl + C`를 누르면 서버가 중지됩니다.

### 방법 2: 프로세스 종료
```bash
# Backend 프로세스 종료
lsof -ti:8000 | xargs kill

# Frontend 프로세스 종료
lsof -ti:3001 | xargs kill
```

## ⚠️ 문제 해결

### 포트가 이미 사용 중인 경우

**Backend 포트 변경:**
```bash
# 터미널에서
python -m uvicorn main:app --reload --host 0.0.0.0 --port 8001
```

**Frontend 포트 변경:**
```bash
# frontend/.env 파일 생성
echo "PORT=3002" > frontend/.env
```

그리고 `main.py`의 CORS 설정도 업데이트:
```python
allow_origins=["http://localhost:3000", "http://localhost:3001", "http://localhost:3002"],
```

### ChromaDB 초기화 오류

```bash
cd backend
rm -rf chroma_db/
# 서버 재시작 시 자동으로 재생성됩니다
```

### PAMS.csv 파일 없음

```bash
# 파일 위치 확인
ls -la backend/PAMS.csv

# 없으면 수동으로 복사
cp /path/to/PAMS.csv backend/
```

## 📊 데모 시연 시나리오

1. **홈페이지 접속**
   - http://localhost:3001 접속
   - 메인 화면 확인

2. **쇼케이스 탐색**
   - "Showcases" 메뉴 클릭
   - 공연 목록 확인
   - 개별 공연 클릭하여 상세 정보 확인

3. **AI 추천 기능**
   - "Booker Matching" 또는 "Recommendations" 메뉴
   - 프로필 입력 후 추천 결과 확인

4. **API 테스트**
   - http://localhost:8000/docs 접속
   - "Try it out" 버튼으로 API 직접 테스트

## 🎉 데모 준비 완료!

이제 로컬 서버에서 완전히 작동하는 데모를 실행할 수 있습니다.
다른 사람에게 보여주려면 같은 네트워크에 연결된 상태에서:

```
http://YOUR_IP_ADDRESS:3001
```

를 사용할 수 있습니다 (방화벽 설정 필요할 수 있음).

