# Goldman Sachs GS Note - 배포 설정 가이드

## 🎯 빠른 시작

### 1단계: 파일 수정

#### manifest.plist 수정
```xml
<!-- 모든 YOUR_GITHUB_USERNAME을 실제 GitHub 사용자명으로 변경 -->
<!-- 모든 YOUR_REPO_NAME을 실제 리포지토리명으로 변경 -->

예시:
YOUR_GITHUB_USERNAME → koreainvestment
YOUR_REPO_NAME → gs-note-app

변경 전:
https://YOUR_GITHUB_USERNAME.github.io/YOUR_REPO_NAME/Goldman_Sachs.ipa

변경 후:
https://koreainvestment.github.io/gs-note-app/Goldman_Sachs.ipa
```

#### index.html 수정
```html
<!-- itms-services 링크의 URL 수정 -->

변경 전:
itms-services://?action=download-manifest&url=https://YOUR_GITHUB_USERNAME.github.io/YOUR_REPO_NAME/manifest.plist

변경 후:
itms-services://?action=download-manifest&url=https://koreainvestment.github.io/gs-note-app/manifest.plist
```

### 2단계: 아이콘 이미지 준비

#### 필요한 아이콘
1. **icon-57.png** - 57x57 픽셀 (작은 아이콘)
2. **icon-512.png** - 512x512 픽셀 (큰 아이콘)

#### 아이콘 생성 방법

**옵션 1: Xcode에서 추출**
1. `Assets.xcassets/AppIcon.appiconset` 폴더 열기
2. 기존 아이콘 이미지 사용 또는 새로 생성
3. 온라인 도구로 리사이즈: https://appicon.co/

**옵션 2: 온라인 도구 사용**
1. https://www.canva.com/ 또는 https://www.figma.com/ 방문
2. 512x512 캔버스 생성
3. "GS" 텍스트와 Goldman Sachs 색상 사용
4. PNG로 내보내기
5. https://imageresizer.com/에서 57x57로 리사이즈

**추천 색상:**
- 배경: #0066cc (Goldman Sachs Blue)
- 텍스트: #ffffff (White)

### 3단계: GitHub Pages 배포

#### 파일 구조
```
gs-note-app/               # 리포지토리 루트
├── index.html            # 배포 페이지
├── manifest.plist        # 앱 매니페스트
├── Goldman_Sachs.ipa     # IPA 파일 (빌드 후 추가)
├── icon-57.png           # 작은 아이콘
├── icon-512.png          # 큰 아이콘
└── README.md             # 설명서
```

#### GitHub Repository 생성 및 업로드

```bash
# 1. GitHub에서 새 리포지토리 생성 (예: gs-note-app)

# 2. 로컬에서 초기화
cd distribution
git init
git add .
git commit -m "Initial commit - Goldman Sachs GS Note distribution"

# 3. GitHub 리포지토리와 연결
git remote add origin https://github.com/YOUR_USERNAME/gs-note-app.git
git branch -M main
git push -u origin main

# 4. GitHub Pages 활성화
# GitHub 웹사이트에서:
# Settings → Pages → Source: main branch → Save
```

### 4단계: IPA 파일 업로드

#### IPA 파일 생성 후

```bash
# IPA 파일을 distribution 폴더로 복사
cp /path/to/Goldman_Sachs.ipa ./Goldman_Sachs.ipa

# Git에 추가 및 푸시
git add Goldman_Sachs.ipa
git commit -m "Add Goldman Sachs IPA file v1.0.0"
git push
```

**⚠️ 주의사항:**
- IPA 파일은 크기가 클 수 있습니다 (100MB 이하 권장)
- Git LFS 사용 권장: `git lfs install` 및 `git lfs track "*.ipa"`
- GitHub의 파일 크기 제한: 100MB (LFS 사용 시 더 큰 파일 가능)

### 5단계: 배포 확인

#### 확인 사항

1. **페이지 접근 확인**
   ```
   https://YOUR_USERNAME.github.io/gs-note-app/
   ```

2. **manifest.plist 접근 확인**
   ```
   https://YOUR_USERNAME.github.io/gs-note-app/manifest.plist
   ```

3. **IPA 파일 접근 확인**
   ```
   https://YOUR_USERNAME.github.io/gs-note-app/Goldman_Sachs.ipa
   ```

4. **아이콘 접근 확인**
   ```
   https://YOUR_USERNAME.github.io/gs-note-app/icon-57.png
   https://YOUR_USERNAME.github.io/gs-note-app/icon-512.png
   ```

## 🔧 고급 설정

### Git LFS 설정 (대용량 IPA 파일용)

```bash
# Git LFS 설치 (한 번만)
git lfs install

# IPA 파일을 LFS로 추적
git lfs track "*.ipa"

# .gitattributes 파일 커밋
git add .gitattributes
git commit -m "Track IPA files with Git LFS"

# IPA 파일 추가 및 푸시
git add Goldman_Sachs.ipa
git commit -m "Add IPA file via Git LFS"
git push
```

### Custom Domain 설정 (선택적)

1. GitHub Pages Settings에서 Custom domain 설정
2. DNS에서 CNAME 레코드 추가:
   ```
   gs-note.yourdomain.com → YOUR_USERNAME.github.io
   ```
3. HTTPS 활성화 (GitHub에서 자동 제공)

### 버전 관리

새 버전을 배포할 때:

```bash
# 1. 새 IPA 파일로 교체
cp /path/to/Goldman_Sachs_v1.1.0.ipa ./Goldman_Sachs.ipa

# 2. manifest.plist의 버전 업데이트
# <string>1.1.0</string>

# 3. index.html의 버전 표시 업데이트
# <div class="version">버전 1.1.0</div>

# 4. Git에 커밋 및 푸시
git add .
git commit -m "Update to version 1.1.0"
git push
```

## 📱 테스트

### 배포 전 체크리스트

- [ ] manifest.plist의 모든 URL이 정확한가?
- [ ] Bundle Identifier가 올바른가?
- [ ] IPA 파일이 정상적으로 업로드되었는가?
- [ ] 아이콘 이미지가 표시되는가?
- [ ] HTTPS로 접근 가능한가?
- [ ] iOS 기기에서 다운로드 링크가 작동하는가?

### 실제 기기에서 테스트

1. Safari에서 배포 페이지 열기
2. "앱 다운로드" 버튼 클릭
3. 설치 프로세스 확인
4. 신뢰 설정 후 앱 실행 테스트

## 🛡️ 보안 고려사항

### HTTPS 필수

- GitHub Pages는 자동으로 HTTPS 제공
- manifest.plist의 모든 URL은 HTTPS여야 함
- HTTP는 iOS에서 차단됨

### Enterprise 인증서

- Enterprise Distribution Certificate 유효 기간 확인
- 인증서 만료 전 갱신 필요
- Provisioning Profile 업데이트

### MDM 요구사항

이 앱은 다음 MDM 기능을 요구합니다:
- mGuard MDM 설치
- KC_MGUARD_SHARED_DATA 키체인 데이터
- MDM 프로필 설치

## 🔄 자동 배포 (GitHub Actions)

### .github/workflows/deploy.yml 생성

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]
  workflow_dispatch:

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./
          publish_branch: gh-pages
```

## 📊 Analytics

배포 페이지에서 다음 이벤트를 추적합니다:
- 페이지 로드
- 다운로드 버튼 클릭
- iOS 버전 확인
- 설치 오류

## 📞 문제 해결

### 자주 묻는 질문

**Q: "Unable to Download App" 오류가 발생합니다.**  
A: manifest.plist의 URL이 정확한지, HTTPS로 접근 가능한지 확인하세요.

**Q: 다운로드는 되는데 설치가 안됩니다.**  
A: Enterprise 인증서를 신뢰해야 합니다. 설정 → 일반 → VPN 및 기기 관리에서 신뢰 설정을 확인하세요.

**Q: 앱이 실행 후 바로 종료됩니다.**  
A: MDM이 설치되어 있는지 확인하세요. mGuard 앱이 설치되어 있어야 합니다.

**Q: GitHub Pages URL이 작동하지 않습니다.**  
A: Settings → Pages에서 GitHub Pages가 활성화되어 있는지, 올바른 브랜치가 선택되어 있는지 확인하세요.

## 📝 체크리스트

배포 완료 전 최종 확인:

```
□ manifest.plist URL 수정 완료
□ index.html URL 수정 완료
□ IPA 파일 업로드 완료
□ 아이콘 이미지 업로드 완료 (icon-57.png, icon-512.png)
□ GitHub Pages 활성화 완료
□ HTTPS 접근 확인 완료
□ 실제 iOS 기기에서 다운로드 테스트 완료
□ Enterprise 인증서 신뢰 설정 확인 완료
□ MDM 설치 확인 완료
□ 앱 실행 테스트 완료
```

---

**도움이 필요하신가요?**  
IT 지원팀에 문의하거나 이 문서의 문제 해결 섹션을 참조하세요.

