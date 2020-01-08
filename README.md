# React with Tailwind

> create-react-app에서 tailwind 설치

dev 사이트의 hagnerd님의 글을 인용하였습니다. [링크](https://dev.to/hagnerd/setting-up-tailwind-with-create-react-app-4jd)

## 설치

create-react-app을 설치합니다.

```
npx create-react-app react_tailwind && cd react_tailwind
```

생성한 프로젝트에서 tailwind와 dependancy들을 설치합니다.

```
yarn add -D tailwindcss autoprefixer postcss-cli
```

## 설정

root 폴더에서 `postcss.config.js` 파일을 생성하고 아래와 같이 입력합니다.

```
// postcss.config.js

module.exports = {
  plugins: [
    require('tailwindcss'),
    require('autoprefixer'),
  ]
}
```

> 현재 디렉토리
> |-📂react_tailwind (root)
> | |-📂node_modules
> | |-📂public
> | |-📂src
> | |-package.json
> | |-postcss.config.json

그다음 tailwind를 초기화 합니다.

```
npx tailwind init
```

`src` 폴더로 들어가 `styles` 폴더를 생성 후 들어가 `tailwind.css`를 생성합니다.
그리고 아래와 같이 입력합니다.

```
// src/styles/tailwind.css

@tailwind base;
@tailwind components;
@tailwind utilities;
```

##### package.json에서 다음과 같이 수정합니다.

```
// package.json
{
    //...
    "scripts": {
        "start": "react-scripts start",
        "build": "react-scripts build",
        "test": "react-scripts test",
        "eject": "react-scripts eject",

        // 추가
        "build:styles": "postcss src/styles/tailwind.css -o src/styles/styles.css",
        "prebuild": "yarn build:styles",
        "prestart": "yarn build:styles"
    }
}
```

만약 `yarn`이 깔려있지 않다면 `npm run`으로 바꿔도 상관 없습니다.

```
// package.json
{
    //...
    "scripts": {
        "start": "react-scripts start",
        "build": "react-scripts build",
        "test": "react-scripts test",
        "eject": "react-scripts eject",

        // 추가
        "build:styles": "postcss src/styles/tailwind.css -o src/styles/styles.css",
        "prebuild": "npm run build:styles",
        "prestart": "npm run build:styles"
    }
}
```

`src` 폴더로 들어가 필요없는 파일을 삭제합니다. (`App.js`와 `index.js`만 남김)

> 현재 디렉토리
> |-📂react_tailwind (root)
> | |-📂node_modules
> | |-📂public
> | |-📂src
> | | |-App.js
> | | |-index.js
> | |-package.json
> | |-postcss.config.json
> | |-tailwind.config.json

## 빌드 & 테스트

`index.js`로 들어가 아래와 같이 수정합니다.

```
// src/index.js

import React from "react";
import ReactDOM from "react-dom";
import App from "./App";
import "./styles/styles.css";

ReactDOM.render(<App />, document.getElementById("root"));
```

`App.js`도 수정합니다.

```
// src/App.js

import React from "react";
import Button from "Components/Button";

class App extends React.Component {
  render() {
    return (
      <div className="flex flex-col w-3/4 mx-auto my-12 items-center">
        <h1>Super cool page</h1>
        <Button onClick={() => alert("I was clicked")}>
          I am a button
        </Button>
      </div>
    );
  }
}

export default App;
```

`src` 폴더에 `Components` 폴더를 추가하여 `Button.js` 파일을 추가합니다.

```
// src/Components/Button.js

import React from "react";

export default function Button({ children, ...buttonProps }) {
  return (
    <button
      className="px-2 py-1 rounded-lg bg-green-400 text-green-800 text-xl font-light uppercase shadow-md hover:shadow-lg"
      {...buttonProps}
    >
      {children}
    </button>
  );
}
```

`yarn start` 혹은 `npm start` 를 실행 후 확인해 보세요.

## 🤝 Connect

잘못된 정보가 있으면 알려주세요!

```
github : https://github.com/halfmoonpdh
email  : enqn0903@naver.com
```
