# front_5th_chapter4-1

# 프론트엔드 배포 파이프라인

## 개요

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/83c75a39-3aba-4ba4-a792-7aefe4b07895/6912169d-ce70-41bf-b624-946d4ee984eb/Untitled.png)

GitHub Actions에 워크플로우를 작성해 다음과 같이 배포가 진행되도록 합니다.

(사전작업: Ubuntu 최신 버전 설치)

1. Checkout 액션을 사용해 코드 내려받기
2. `npm ci` 명령어로 프로젝트 의존성 설치
3. `npm run build` 명령어로 Next.js 프로젝트 빌드
4. AWS 자격 증명 구성
5. 빌드된 파일을 S3 버킷에 동기화
6. CloudFront 캐시 무효화

## 주요 링크

- S3 버킷 웹사이트 엔드포인트: http://hanghae-yubin-bucket.s3-website-us-east-1.amazonaws.com
- CloudFrount 배포 도메인 이름: https://d116nkzjkpdj0x.cloudfront.net

## 주요 개념

- GitHub Actions과 CI/CD 도구: \***\*\_\*\***
- S3와 스토리지: \***\*\_\*\***
- CloudFront와 CDN: \***\*\_\*\***
- 캐시 무효화(Cache Invalidation): \***\*\_\*\***
- Repository secret과 환경변수: \***\*\_\*\***

## CDN과 성능최적화

- (CDN 도입 전과 도입 후의 성능 개선 보고서 작성)
