# Asp.net Core MVC + TailwindCSS
Asp.net Core MVC 프로젝트에 TailwindCSS 적용하기
<br />

## TailwindCSS 설치
- TailwindCSS를 설치하고자 하는 프로젝트에서 PowerShell 열기
- npm 명령어를 이용해 TailwindCSS를 설치하기<br />
npm install -D tailwindcss@latest postcss@latest autoprefixer@latest
- 설치가 완료되면 프로젝트에 project.json, tailwind.config.js, postcss.config.js 추가됨

project.json
```json
{
  "name": "프로젝트명",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "autoprefixer": "^10.2.6",
    "postcss": "^8.3.5",
    "tailwindcss": "^2.2.4"
  }
}
``` 

