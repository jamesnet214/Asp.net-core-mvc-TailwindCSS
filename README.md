# Asp.net Core MVC + TailwindCSS                 
Asp.net Core MVC 프로젝트에 TailwindCSS 적용하기 
<br />

<img width="459" alt="image" src="https://user-images.githubusercontent.com/52397976/176645754-327f0c36-3fa5-4dd5-9064-3100e42b6099.png">


## TailwindCSS란
- Bootstrap과 마찬가지로 정의된 클래스명을 사용하면서도 정의된 클래스명 + 임의값 설정이 가능하다.<br />
```html
// 정의된 클래스 사용 예시
<div class="border-1 border-red-100">
</div>

// 정의된 클래스 + 임의값 사용 예시
<div class="border-[1px] border-[#333333]">
</div>
```
- 정의된 클래스 + 임의값만으로도 거의 대부분의 스타일을 쓸 수 있으므로 클래스명을 지어야하는 번거로움이 없고<br />
Html내에서 거의 모든 작업이 이루어지므로 가독성 또한 엄청나게 좋아진다.
- 사용한 스타일만 빌드해서 css파일로 만들어 주기 때문에 css파일 용량을 최적화 할 수 있다.

## TailwindCSS 설치
- TailwindCSS를 설치하고자 하는 Asp.net Core 프로젝트에서 PowerShell을 연다.
- npm 명령어를 이용해 TailwindCSS를 설치한다.<br />
`npm init -y`<br />
`npm install -D tailwindcss@latest postcss@latest autoprefixer@latest`<br />
`npx tailwind init -p`<br />
- 설치가 완료되면 프로젝트에 project.json, tailwind.config.js, postcss.config.js 파일이 추가된다.

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
해줘야 하는데 project.json / 프로젝트명.csproj / tailwind.config.js / wwwroot/css/site.css 파일을 아래와 같이 수정해준다.

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

tailwind.config.js
```js
content: ['./Views/**/*.cshtml'],
```

wwwroot/css/site.css
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
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
파일 수정시에도 바로바로 css파일이 빌드될 수 있게 해줘야 한다.<br />
PowerShell을 열고 프로젝트 경로로 이동후 아래 명령어를 입력하면 된다.<br />
물론 작업할때마다 아래 명령어를 실행시켜줘야 하는 번거로움은 있다.<br />
이 부분도 추후에 자동으로 할 수 있는지 알아볼 계획이다.
```npm
npx tailwind build -i ./wwwroot/css/site.css -o ./wwwroot/css/output.css --watch
```


## TailwindCSS Intellisense
아쉽게도 아직 VisualStudio에서는 지원하는 플러그인이 없다...<br />
임시방편으로 cshtml 작업을 vscode로 하면 확장을 통해서 Intellisense를 사용할 수 있다.
추후에 VisualStudio용 Intellisense를 만들수 있는지 알아볼 예정이다.


## TailwindCSS 자주 쓰는 스타일 메모
- container: 속성: width: 100% / 고정된 화면 크기 세트를 디자인하려는 경우에 유용<br />
- mx-auto: 속성: margin-left: auto, margin-right-auto / 컨테이너 가로 중앙배치<br />
- basis-1/2 : flex-basis: 50%; / flex사용시 차지할 비율 설정
- basis-[{값}%] : flex-basis: {값}%; 
```html
<div class="flex">
  <div class="basis-1/4"></div> // 1/4 영역 차지
  <div class="basis-2/4"></div> // 2/4 영역 차지 
  <div class="basis-1/4"></div> // 1/4 영역 차지
</div>

<div class="flex">
  <div class="basis-[23%]"></div>
  <div class="basis-[47%]"></div>
  <div class="basis-[30%]"></div>
</div>
```


- m-1: margin: 0.25rem; /* 4px */
- m-[{값}px] : margin: {값}px;
- p-[{값}px] : padding: {값}px;
- bg-[{색상}] : background: {색상};
- border-[{값}px] : border: {값}px;
- border-[{색상}] : border-color: {색상};
- gap-[{값}px] : gap: {값}px;

