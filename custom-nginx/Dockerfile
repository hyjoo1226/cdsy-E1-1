# 1. 베이스 이미지 선택 (경량화된 alpine 버전 사용)
FROM nginx:alpine

# 2. 커스텀 포인트: 관리용 메타데이터 추가
LABEL maintainer="hyjoo1226"
LABEL description="My Custom Web Server for Mission"

# 3. 커스텀 포인트: 환경 변수 설정
ENV APP_ENV=Development

# 4. 커스텀 포인트: 호스트의 html 파일을 컨테이너 내부의 NGINX 기본 경로로 복사
COPY html/ /usr/share/nginx/html/

# 5. 포트 노출 (문서화 용도)
EXPOSE 80
