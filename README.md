# front_5th_chapter4-1

# 프론트엔드 배포 파이프라인

## 개요

![Image](https://github.com/user-attachments/assets/471e09f6-fbd4-4437-9174-c2cafa64e829)

1️⃣ GitHub Actions

워크플로우 구성: main 브랜치에 push 이벤트가 발생하면 배포가 자동으로 진행됩니다.
주요 작업:
Checkout: 저장소 코드를 내려받습니다.
npm ci: 프로젝트 의존성 설치
npm run build: Next.js 빌드 산출물 생성
AWS 자격 증명 설정 및 S3에 업로드
CloudFront 캐시 무효화로 최신 파일을 배포

2️⃣ Amazon S3
Next.js 빌드된 정적 파일을 저장하는 버킷 역할을 합니다.
정적 자산(HTML, JS, CSS)을 S3에서 호스팅합니다.

3️⃣ Amazon CloudFront
S3에서 가져온 파일을 전 세계 엣지 서버로 배포합니다.
사용자에게 더 빠르고 안정적으로 콘텐츠를 전달합니다.
새로 배포된 파일로 캐시 무효화가 진행됩니다.

4️⃣ IAM과 보안
GitHub Actions가 S3와 CloudFront에 접근할 수 있도록 IAM 역할(정책)을 구성했습니다.
AWS Secrets Manager나 GitHub Repository Secrets를 활용해 자격 증명을 안전하게 관리합니다.

## 주요 링크

- S3 버킷 웹사이트 엔드포인트: http://hanghae-yubin-bucket.s3-website-us-east-1.amazonaws.com
- CloudFrount 배포 도메인 이름: https://d116nkzjkpdj0x.cloudfront.net

## 주요 개념

- ### GitHub Actions과 CI/CD 도구

  GitHub Actions는 GitHub에서 제공하는 자동화 워크플로 도구입니다.
  CI(지속적 통합), CD(지속적 배포)를 자동화해주는 역할을 합니다.
  예를 들어, 코드 push 시 자동으로 테스트, 빌드, 배포 과정을 실행합니다.
  이를 통해 배포 오류를 줄이고, 일관된 개발 파이프라인을 유지할 수 있습니다.

- ### S3와 스토리지

  S3는 Amazon Web Services의 객체 스토리지 서비스입니다.
  정적 웹사이트 파일(html, css, js)이나 이미지, 동영상 같은 파일을 저장·서빙합니다.
  높은 내구성(99.999999999%)과 가용성을 제공해, 안전하게 정적 파일을 저장할 수 있습니다.

- ### CloudFront와 CDN

  CloudFront는 AWS의 CDN(콘텐츠 전송 네트워크) 서비스입니다.
  S3 같은 저장소에서 정적 파일을 가져와 전 세계 엣지 로케이션으로 배포해, 사용자에게 더 빠르게 콘텐츠를 전달합니다.
  CDN은 글로벌 사용자에게 콘텐츠를 빠르게 제공하고, 서버 부하를 줄여줍니다.

- ### 캐시 무효화(Cache Invalidation)

  캐시 무효화는 CDN이나 브라우저에 저장된 캐시를 지우는 작업입니다.
  사이트를 업데이트하면, 사용자에게 이전 버전 캐시가 남아있을 수 있습니다.
  이때 캐시 무효화를 통해 최신 콘텐츠로 빠르게 갱신할 수 있습니다.
  예) CloudFront의 Invalidation API를 사용해서 특정 경로 캐시를 제거.

- ### Repository secret과 환경변수
  Repository secret은 GitHub Actions 등에서 민감 정보를 안전하게 관리하는 방식입니다.
  예를 들어, 배포용 API 키, 데이터베이스 비밀번호 등을 저장하고, 워크플로에서 환경 변수로 불러와 사용합니다.
  이를 통해 보안을 유지하면서도 자동화 파이프라인을 안전하게 실행할 수 있습니다.

## CDN과 성능최적화

- (CDN 도입 전과 도입 후의 성능 개선 보고서 작성)
