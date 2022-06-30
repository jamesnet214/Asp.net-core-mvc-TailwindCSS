# Asp.net Core MVC + TailwindCSS
Asp.net Core MVC 프로젝트에 TailwindCSS 적용하기
<br />

## TailwindCSS란


## TailwindCSS 설치
- TailwindCSS를 설치하고자 하는 Asp.net Core 프로젝트에서 PowerShell 열기
- npm 명령어를 이용해 TailwindCSS를 설치하기<br />
`npm install -D tailwindcss@latest postcss@latest autoprefixer@latest`
- 설치가 완료되면 프로젝트에 project.json, tailwind.config.js, postcss.config.js 파일이 추가됨

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

- TailwindCSS가 설치가 끝났으면 프로젝트를 빌드할때마다 TailwindCSS가 자동으로 빌드될 수 있게 설정을<br />
해줘야 하는데 project.json 파일과 프로젝트명.csproj 파일을 아래와 같이 수정해준다.

project.json
```json
"scripts": {
  "style:build": "npx tailwind build -i ./wwwroot/css/site.css -o ./wwwroot/css/output.css"
},
```

프로젝트명.csproj
```csproj
<Target Name="프로젝트명" BeforeTargets="Build">
    <Exec Command="npm run style:build"/>
</Target>
```
이렇게 설정을 하면 프로젝트 빌드시마다 위 코드에 의해 wwwroot/css/output.css 파일이 생성된다.

빌드된 css파일을 사용해야 하므로 _Layout.cshtml 파일에 css를 링크한다.
```html
<head>
  <link rel="stylesheet" href="~/css/output.css" />
</head>
```

## TailwindCSS HotReload 
TailwindCSS 특성상 프로젝트 빌드시에만 css를 빌드하게 되면 편하게 작업할 수 없으므로<br />
파일 수정시에도 바로바로 빌드될 수 있게 해줘야 한다.<br />
PowerShell을 열고 프로젝트 경로로 이동후 아래 명령어를 입력하면 된다.
물론 작업할때마다 아래 명령어를 실행시켜줘야 하는 번거로움은 있다.
이 부분도 추후에 자동으로 할 수 있는지 알아봐야겠다.
```npm
npx tailwind build -i ./wwwroot/css/site.css -o ./wwwroot/css/output.css --watch
```


## TailwindCSS Intellicense
















