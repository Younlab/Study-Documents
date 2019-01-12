# Vuepress

## Local install vuepress

본인의 Project 내부에서 아래의 commend 를 실행

```sh
# install as a local dependency
yarn add -D vuepress # OR npm install -D vuepress

# create a docs directory
mkdir docs
# create a markdown file
echo '# Hello VuePress' > docs/README.md
```

## Run Commend Add

`package.json` 에 아래의 내용을 추가한다.

```sh
{
  "scripts": {
    "docs:dev": "vuepress dev docs",
    "docs:build": "vuepress build docs"
  }
}
```

서버 실행
```sh
yarn docs:dev
```

정적파일 렌더링/생성
```sh
yarn docs:build
```

## Directory Structure

Vuepress 에서 권장되는 디렉토리 구조

```sh
.
├── docs
│   ├── .vuepress (Optional)
│   │   ├── components (Optional)
│   │   ├── theme (Optional)
│   │   │   └── Layout.vue
│   │   ├── public (Optional)
│   │   ├── styles (Optional)
│   │   │   ├── index.styl
│   │   │   └── palette.styl
│   │   ├── templates (Optional, Danger Zone)
│   │   │   ├── dev.html
│   │   │   └── ssr.html
│   │   ├── config.js (Optional)
│   │   └── enhanceApp.js (Optional)
│   │ 
│   ├── README.md
│   ├── guide
│   │   └── README.md
│   └── config.md
│ 
└── package.json
```