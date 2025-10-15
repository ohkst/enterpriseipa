# 아이콘 이미지 생성 가이드

## 필요한 아이콘

1. **icon-57.png** - 57x57 픽셀
2. **icon-512.png** - 512x512 픽셀

## 빠른 생성 방법

### 방법 1: Xcode 프로젝트에서 추출

```bash
# AppIcon에서 이미지 추출
cd "/Users/a115221/Documents/Goldman Sachs/Goldman Sachs/Assets.xcassets/AppIcon.appiconset"

# 기존 이미지를 복사하여 리사이즈
# (온라인 도구 사용: https://imageresizer.com/)
```

### 방법 2: 명령줄로 간단한 아이콘 생성 (ImageMagick 필요)

```bash
# ImageMagick 설치 (Homebrew)
brew install imagemagick

# 512x512 아이콘 생성
convert -size 512x512 xc:'#0066cc' \
        -fill white -font Arial-Bold -pointsize 200 \
        -gravity center -annotate +0+0 'GS' \
        -bordercolor '#004999' -border 0 \
        icon-512.png

# 57x57 아이콘 생성
convert icon-512.png -resize 57x57 icon-57.png
```

### 방법 3: 온라인 도구 사용

1. **Canva** (https://www.canva.com/)
   - 512x512 캔버스 생성
   - 배경색: #0066cc
   - "GS" 텍스트 추가 (흰색, 굵게)
   - PNG로 다운로드

2. **Image Resizer** (https://imageresizer.com/)
   - 512x512 이미지를 57x57로 리사이즈

### 방법 4: 기본 이미지로 임시 사용

현재 배포 파일에 포함된 `Goldman Sachs.ipa`는 빈 파일입니다.
실제 아이콘이 없어도 앱 설치는 가능하지만, 아이콘이 표시되지 않을 수 있습니다.

## 아이콘 추가 후 푸시

```bash
cd "/Users/a115221/Documents/Goldman Sachs/Goldman Sachs/distribution"

# 아이콘 파일 추가
git add icon-57.png icon-512.png

# 커밋
git commit -m "Add app icons"

# 푸시
git push
```

## 아이콘 디자인 가이드라인

### 권장 사양
- **포맷**: PNG (투명 배경 가능)
- **색상**: Goldman Sachs 브랜드 색상
  - Primary: #0066cc
  - Secondary: #004999
- **텍스트**: "GS" 또는 Goldman Sachs 로고
- **스타일**: 미니멀, 프로페셔널

### iOS 앱 아이콘 가이드라인
- 모서리는 iOS가 자동으로 둥글게 처리
- 투명 배경 사용 가능
- 고해상도 (레티나 디스플레이 대응)

