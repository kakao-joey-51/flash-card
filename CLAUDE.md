# CLAUDE.md

이 파일은 Claude Code (claude.ai/code)가 이 저장소에서 작업할 때 참고하는 안내 문서입니다.

## 프로젝트 개요

영유아용 한국어 낱말카드 웹 앱. 사물 이미지와 한글 단어를 보여주고 TTS로 발음을 들려준다. 모바일/태블릿에 최적화되어 있으며 전체화면 및 PWA를 지원한다.

## 명령어

- `npm run dev` — Vite 개발 서버 실행
- `npm run build` — TypeScript 검사 + Vite 프로덕션 빌드 (`tsc && vite build`)
- `npm run preview` — 프로덕션 빌드 로컬 미리보기
- 테스트 러너나 린터는 설정되어 있지 않음.

## 아키텍처

Vite 기반 React 18 + TypeScript 단일 페이지 앱. 라우터나 상태관리 라이브러리 없이 `src/App.tsx` 하나의 컴포넌트로 구성.

- **단어 데이터**: `src/App.tsx`의 `wordData` 배열에 하드코딩. 각 항목은 `{ name: string, file: string }` 형태로 한글 단어와 `public/images/` 내 이미지 파일명을 매핑.
- **인터랙션 흐름**: 2단계 클릭 — 첫 클릭 시 단어 표시 + Web Speech API TTS 발음, 두 번째 클릭 시 다음 카드로 이동.
- **스타일링**: CSS 파일 없이 모두 인라인 스타일. 카드마다 파스텔 배경색이 순환.
- **배포**: GitHub Actions를 통한 GitHub Pages 배포. base URL은 `/flash-card/` (`vite.config.ts`에서 설정).

## 카드 추가 방법

`public/images/`에 이미지 추가 (영문 파일명, 50KB 미만) 후 `src/App.tsx`의 `wordData` 배열에 항목 추가.
