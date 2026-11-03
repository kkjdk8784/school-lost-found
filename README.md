# 학교 분실물 찾기 · GitHub Pages 업로드용

Supabase 프로젝트와 공개 키가 연결된 버전입니다. 비밀키·관리자 비밀번호는 포함되지 않습니다.
기존 사이트를 수정하거나 기존 게시글을 자동 삭제하지 않습니다.

## 지금 할 일
1. 이 ZIP을 압축 해제합니다.
2. GitHub `kkjdk8784/school-lost-found` 저장소에서 Add file → Upload files를 선택합니다.
3. 압축을 푼 폴더 **안의 파일과 assets 폴더**를 모두 올립니다. ZIP 자체나 바깥 폴더를 올리지 않습니다.
4. Commit changes를 누릅니다. 저장소 첫 화면에 index.html과 assets가 바로 보여야 합니다.
5. Settings → Pages → Source: Deploy from a branch → main → /(root) → Save.
6. 배포가 완료되면 아래 주소에서 관리자 로그인을 먼저 시험합니다.

- 학생: https://kkjdk8784.github.io/school-lost-found/
- 학생회: https://kkjdk8784.github.io/school-lost-found/?view=council
- 관리자: https://kkjdk8784.github.io/school-lost-found/?view=admin

관리자 이메일: wjswnsgk09@naver.com. Supabase에서 직접 만든 비밀번호를 사용합니다.
학생용 › 또는 학생회 계정 ›를 눌러 로그인할 수 있습니다. 관리자만 계정 관리가 보입니다.
승인 권한은 Supabase SQL 정책에서 검사합니다. 주소 변경만으로 권한이 생기지 않습니다.
신청자는 계정 만들기 → 이메일 인증 → 로그인 → 학생용 › → 학생회 계정으로 변경 신청.
관리자는 계정 관리에서 승인·거절·권한 해제를 합니다.

## 학교 공유 전에 반드시 확인할 사항
- Supabase SQL 설정이 정상 실행되어 있어야 합니다.
- Authentication → URL Configuration의 Site URL과 Redirect URL에
  https://kkjdk8784.github.io/school-lost-found/ 를 등록합니다.
- Authentication → Sign In / Providers에서 Email과 Confirm Email을 유지합니다.
- Supabase 기본 메일 발송은 프로젝트 팀원 외 이메일 전송을 제한하므로,
  일반 학생의 가입 인증·비밀번호 찾기를 운영하려면 Custom SMTP를 설정해야 합니다.
  학생들에게 Supabase 프로젝트 팀원 권한을 줄 필요는 없습니다.
- 관리자는 직접 생성하고 이메일 확인한 계정으로 비밀번호 로그인할 수 있습니다.
- Apple 로그인 버튼은 이 버전에 포함되지 않습니다. 기존 Apple 비밀번호를 입력하지 않습니다.
- 새 Supabase의 분실물 목록은 이전 작업 전에는 비어 있습니다. 기존 사이트를 먼저 닫지 마세요.

## 기존 게시글 보존·이전 (원본에 쓰기 작업 없음)
1. Python 3가 설치된 컴퓨터에서 tools/backup_old_site.py를 실행합니다.
   예: python tools/backup_old_site.py
2. 생성되는 lost-found-backup-날짜.json에는 기존 사이트의 게시글과 사진 데이터가 함께 담깁니다.
   오류가 발생하면 완료로 취급하지 않습니다. 원본 사이트 주소가 바뀌면 SOURCE만 수정합니다.
3. 새 사이트에 관리자 로그인 → 계정 관리 → 기존 게시글 백업 가져오기에서 JSON을 선택합니다.
4. 게시글 ID를 보존하고, 같은 ID가 이미 있으면 덮어쓰지 않고 건너뜁니다.
5. 이전 중 일부가 실패해도 동일한 백업을 다시 가져올 수 있습니다.
6. 원본과 새 사이트의 개수, 내용, 사진을 대조한 뒤 공유 주소를 바꿉니다.
7. 옮기는 동안 원본에서 새로 등록한 글이 있다면 다시 백업·가져오기합니다.

기존 사이트에서 이미지 자체가 저장되지 않았던 글은 사진을 복구할 수 없습니다.
해당 글의 나머지 내용은 보존됩니다. 기존 계정·비밀번호는 이전되지 않으며,
학생회 구성원은 새 사이트에 가입하고 관리자의 재승인을 받습니다.

## 개발용 소스
src/: React 및 Supabase 연결 코드. public/sage.png: 기존 로고.
package.json, package-lock.json, vite.config.ts: 빌드 설정.
수정 후 npm ci && npm run build 로 dist를 생성합니다.
dist의 내용이 업로드할 파일입니다. 이 ZIP 최상위에는 이미 빌드된 파일이 있습니다.
공개 키는 브라우저용이며 데이터 접근은 Supabase RLS에서 제어합니다.
service_role, sb_secret 키, 관리자 비밀번호는 GitHub에 올리지 마세요.

현재 산출물은 로컬 빌드 검증본입니다. 실제 관리자 비밀번호 로그인, 일반 사용자 메일,
게시글 이전 완료는 사용자의 배포 환경에서 별도로 확인해야 합니다.
