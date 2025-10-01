# 📌 Git Branch 전략 (5인 팀 프로젝트)

## 1. 브랜치 구조
- **main**
  - 최종 배포 브랜치
  - 항상 안정적인 상태만 유지 (관리자만 merge 가능)

- **develop**
  - 공용 통합 브랜치
  - Pull Request(PR)로만 merge
  - 직접 push 금지

- **dev_xxx**
  - 팀원 개인 개발 브랜치
  - 자유롭게 commit & push 가능
  - 예시: `dev_kth`, `dev_jh`, `dev_mj`

---

## 2. 작업 흐름

### 🧑‍💻 개인 작업
1. 브랜치 이동
   ```bash
   git checkout dev_xxx
   ```
2. 개발 후 commit
   ```bash
   git add .
   git commit -m "feat: 로그인 기능 구현"
   ```
3. 병합 전 최신 develop 반영
   ```bash
   git pull origin develop
   ```
   - 충돌 발생 시 로컬에서 해결 후 다시 push

---

### 🔀 병합 (Merge)
1. GitHub에서 Pull Request(PR) 생성
   - base: `develop`
   - compare: `dev_xxx`
2. 팀원 코드 리뷰 & 승인
3. Merge → `develop`
4. 모든 팀원은 develop 최신화
   ```bash
   git checkout develop
   git pull origin develop
   git checkout dev_xxx
   git merge develop
   ```

---

### 🚀 배포
1. `develop`에서 기능 안정화 확인
2. PR 생성 (base = `main`, compare = `develop`)
3. Merge → `main`
4. 배포 진행

---

## 3. 규칙
- `main`, `develop` 직접 push ❌ (항상 PR로만 merge)
- 충돌은 **본인 브랜치에서 해결** (GitHub conflict editor 최소화)
- 커밋 메시지 컨벤션 통일
  - `feat: 기능 추가`
  - `fix: 버그 수정`
  - `refactor: 코드 리팩토링`
- 작업 시작 전 항상 최신 develop 반영
  ```bash
  git pull origin develop
  ```

---

## 4. 브랜치 워크플로우 다이어그램

```
main  ---------------------------●───────── 배포
                                  ↑
develop  --------------------●----●----●---- 통합
                              ↑    ↑    ↑
dev_kth   --------●---●---PR--┘         
dev_jh    --------●-----PR-----┘
dev_mj    ----●-----●--PR------┘
...
```

---

✅ 이 전략을 따르면  
- 코드 사라짐 방지  
- 충돌 최소화  
- 리뷰 & 테스트 후 안정적으로 통합 가능
