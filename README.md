# react 설치

```bash
npm create vite@latest todo-js -- --template react

cd todo-js
npm i
```

## 프로젝트 루트 기준 절대경로 설정하기

**jsconfig.json**

```jsx
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  }
}
```

```bash
npm i vite-jsconfig-path -D
```

**vite.config.js**

```jsx
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import jsconfigPaths from "vite-jsconfig-paths";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react(), jsconfigPaths()],
});
```

## tailwindcss 설치하기

```bash
npm i tailwindcss postcss autoprefixer -D
```

**postcss.config.js**

```jsx
postcss.config.js;
```

```bash
npx tailwindcss init
```

**tailwind.config.js**
content 필드에는 변화를 감시할 파일을 적어주는 걸 잊지 마세요.

```jsx
/** @type {import('tailwindcss').Config} */
export default {
  content: ["./index.html", "./src/**/*.jsx"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

**src/index.css**

```jsx
@import 'tailwindcss/base';
@import 'tailwindcss/components';
@import 'tailwindcss/utilities';
```

## test 해보기

**src/App.tsx**

```jsx
<h1 className="text-3xl font-bold underline">Hello world!</h1>
```

### html 을 jsx 로 변환시켜주는 플러그인

body 안쪽 영역을 붙여넣고 바꾸고 싶은 범위를 선택한 다음에 마우스 오른쪽 버튼을 누르세요.

이어서 표시된 컨텍스트 메뉴에서 `Convert HTML to JSX` 를 선택하세요.

https://marketplace.visualstudio.com/items?itemName=riazxrazor.html-to-jsx

## 작동을 확인한 다음 git에 커밋하고 푸시하기

```bash
npx mrm gitignore
```

## github pages 에 배포하기

```bash
mkdir pages-test
cd pages-test
touch index.html
code .
```

```bash
npm run build
```

build 후 생성된 dist 를 깃헙에 올리면 배포 끝

```bash
// gh-pages 안에 dist 를 -d 복사해서 넣겠다
npx gh-pages -d dist
```

gh-pages 브런치가 자동생성되고 setting - pages root 브런치가 gh-pages 로 자동설정되게된다.

setting - action 에서 배포 진행 상황을 확인할수있다.

**그런데 하얀 화면만 표시가 된다.**
리소스 주소가 서브 디렉토리 기준이라 그렇다.
**vite.config.js**

```jsx
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import jsconfigPaths from "vite-jsconfig-paths";

// https://vitejs.dev/config/
export default defineConfig({
  // 여기서 내 깃헙 레포 이름을 똑같이 적어준다
  base: "/TodoList_react/",
  plugins: [react(), jsconfigPaths()],
});
```
