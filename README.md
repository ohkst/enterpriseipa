# Goldman Sachs GS Note - Enterprise 앱 배포

## 📱 개요

Goldman Sachs GS Note는 Goldman Sachs의 리서치 노트를 제공하는 Enterprise iOS 앱입니다.

## 🚀 GitHub Pages 배포 방법

### 1. GitHub Repository 설정

1. GitHub에서 새 리포지토리 생성 (예: `gs-note-app`)
2. Settings → Pages → Source를 `main` 브랜치로 설정
3. GitHub Pages가 활성화되면 URL 확인 (예: `https://username.github.io/gs-note-app/`)

### 2. 파일 업로드

다음 파일들을 리포지토리에 업로드:

```
/
├── index.html           # 다운로드 페이지
├── manifest.plist       # 앱 배포 매니페스트
├── GoldmanSachs.ipa     # 빌드된 IPA 파일
├── icon-57.png          # 작은 아이콘 (57x57) (선택적)
└── icon-512.png         # 큰 아이콘 (512x512) (선택적)
```

### 3. manifest.plist 수정

`manifest.plist` 파일에서 다음 항목들을 수정:

```xml
<!-- IPA 파일 URL -->
<string>https://YOUR_GITHUB_USERNAME.github.io/YOUR_REPO_NAME/GoldmanSachs.ipa</string>

<!-- 아이콘 URL -->
<string>https://YOUR_GITHUB_USERNAME.github.io/YOUR_REPO_NAME/icon-57.png</string>
<string>https://YOUR_GITHUB_USERNAME.github.io/YOUR_REPO_NAME/icon-512.png</string>

<!-- Bundle Identifier -->
<string>com.goldmansachs.app</string>

<!-- 버전 -->
<string>1.0.0</string>
```

### 4. index.html 수정

`index.html` 파일에서 다음 URL을 수정:

```html
<a href="itms-services://?action=download-manifest&url=https://YOUR_GITHUB_USERNAME.github.io/YOUR_REPO_NAME/manifest.plist">
```

## 📦 IPA 파일 생성 방법

### Xcode에서 Archive 생성

1. Xcode에서 프로젝트 열기
2. Product → Scheme → Edit Scheme
3. Run → Build Configuration을 **Release**로 설정
4. Product → Archive
5. Organizer에서 Archive 선택
6. Distribute App → Enterprise → Export
7. 서명 인증서 선택 (Enterprise Distribution Certificate)
8. Export하여 IPA 파일 생성

### 명령줄에서 빌드 (선택적)

```bash
# Archive 생성
xcodebuild -workspace "Goldman Sachs.xcworkspace" \
           -scheme "Goldman Sachs" \
           -configuration Release \
           -archivePath ./build/GoldmanSachs.xcarchive \
           archive

# IPA 내보내기
xcodebuild -exportArchive \
           -archivePath ./build/GoldmanSachs.xcarchive \
           -exportPath ./build \
           -exportOptionsPlist ExportOptions.plist
```

## 🔐 인증서 요구사항

### 필수 인증서

- **Apple Enterprise Distribution Certificate**: Enterprise 앱 서명용
- **Provisioning Profile**: Enterprise Distribution용 프로비저닝 프로파일

### 인증서 설정

1. Apple Developer Enterprise Program 계정 필요
2. Certificates, Identifiers & Profiles → Certificates
3. Enterprise Distribution 인증서 생성
4. Provisioning Profile 생성 (Distribution → In House)
5. Xcode에서 인증서 및 프로파일 다운로드

## 📋 사전 요구사항

### 앱 설치 조건

- **iOS 버전**: iOS 15.6 이상
- **MDM 설치**: mGuard MDM이 설치되어 있어야 함
- **인터넷 연결**: 앱 다운로드 및 실행 시 필요
- **기기 신뢰**: Enterprise 개발자 인증서 신뢰 필요

### 사용자 안내사항

설치 후 다음 과정이 필요합니다:

1. **설정 → 일반 → VPN 및 기기 관리**로 이동
2. **엔터프라이즈 앱** 섹션에서 Goldman Sachs 선택
3. **"Goldman Sachs 신뢰"** 버튼 클릭
4. 확인 팝업에서 **"신뢰"** 선택

## 🔗 배포 URL 예시

```
다운로드 페이지:
https://username.github.io/gs-note-app/

설치 링크:
itms-services://?action=download-manifest&url=https://username.github.io/gs-note-app/manifest.plist
```

## 📱 QR 코드 생성 (선택적)

사용자의 편의를 위해 QR 코드를 생성할 수 있습니다:

1. https://www.qr-code-generator.com/ 방문
2. URL 입력: 배포 페이지 URL
3. QR 코드 생성 및 다운로드
4. `index.html`에 QR 코드 이미지 추가

## 🛠️ 문제 해결

### "Unable to Download App" 오류

**원인:**
- HTTPS를 사용하지 않는 경우
- manifest.plist 또는 IPA 파일 경로 오류
- 잘못된 Bundle Identifier

**해결 방법:**
- GitHub Pages는 자동으로 HTTPS 제공
- manifest.plist의 모든 URL이 정확한지 확인
- Bundle Identifier가 프로젝트와 일치하는지 확인

### "Untrusted Enterprise Developer" 오류

**해결 방법:**
1. 설정 → 일반 → VPN 및 기기 관리
2. 엔터프라이즈 앱에서 개발자 선택
3. "개발자 신뢰" 클릭

### MDM 관련 오류

**증상:**
- 앱 실행 시 "MDM이 설치되지 않았습니다" 메시지

**해결 방법:**
1. mGuard MDM 앱 설치 확인
2. 키체인에 `KC_MGUARD_SHARED_DATA` 존재 확인
3. MDM 프로필이 정상 설치되었는지 확인

## 📞 지원

문의사항이나 문제가 발생하면 IT 지원팀에 연락하시기 바랍니다.

---

**마지막 업데이트:** 2025-10-15  
**버전:** 1.0.0  
**플랫폼:** iOS 15.6+

