# Webpack
> [Webpack의 등장배경과 사용하는이유](https://velog.io/@radin/webpack-1)   
> [Webpack 설정 및 실행하기](https://velog.io/@radin/webpack-2)

<br/>

## Webpack이란?
- Webpack은 여러 개의 파일을 하나의 파일로 합쳐주는 **모듈 번들러(Module bundler)** 이다.

<br/>

## 모듈 번들러(Module Bundler)란?
![image (7)](https://github.com/heereal/Frontend_Dev_Articles/assets/117061017/4cdc6e98-f5d6-4ef5-8aa4-65f362b42307)

- 모듈 번들러는 여러 모듈을 모아 번들링 함으로써 **하나의 파일로 병합 및 압축** 해주는 도구이다.

<br/>

## 모듈화를 위한 3가지 요건
1. **스코프** - 각각의 모듈은 독립적인 스코프를 가져야 한다.
2. **정의** - 모듈을 정의할 수 있어야 한다. (만들 수 있어야 한다.)
3. **사용** - 정의된 모듈을 가져다 사용할 수 있어야 한다.

<br/>

## Webpack으로 해결하려는 문제
1. **자바스크립트 변수 유효 범위**: 웹팩은 변수 유효 범위의 문제점을 ES6의 Modules 문법과 웹팩의 모듈 번들링으로 해결한다.
2. **브라우저별 HTTP 요청 숫자의 제약**: 웹팩을 이용해 여러 개의 파일을 하나로 합치면 브라우저별 HTTP 요청 숫자 제약을 피할 수 있다.
3. **Dynamic Loading & Lazy Loading 미지원**: 웹팩의 Code Splitting 기능을 이용하여 원하는 모듈을 원하는 타이밍에 로딩할 수 있다.

<br/>

## Webpack config 파일 설정
```javascript
// webpack.config.js
module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js', // 최종 번들링된 자바스크립트
    path: path.resolve(__dirname, 'dist') // dist를 배포용 폴더로 사용
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /(node_modules|pages)/,
        use: {
          loader: 'babel-loader',
        },
      },
      {
        test: /\.css$/,
        use: [
          { loader: MiniCssExtractPlugin.loader },
          {
            loader: 'css-loader',
            options: { import: true },
          },
        ],
      },
      {
        test: /\.png$/,
        type: 'asset/resource',
      },
    ],
  },
  plugins: [new HtmlWebpackPlugin({ template: './src/index.html' }), new MiniCssExtractPlugin()],
}
```
- 웹팩 설정에서 중요한 Core Concepts는 entry, output, loader, plugins 4가지가 있다.
### entry
- webpack은 번들링 과정에서 특정 시작 지점부터 애플리케이션에 필요한 모든 모듈을 포함하는 `dependency graph`를 재귀적으로 완성해 나간다. 
- 그래프를 모두 그리고 나면 이 모든 모듈을 소수의 번들로 묶어서 (보통 하나의 번들로 묶는다) 브라우저에 로드될 준비를 마친다.
- `entry` 속성을 설정해서 웹팩이 **어떤 모듈로부터 시작해서 `dependency graph`를 그려나갈지 명시**해줄 수 있다.
### output
- `output`은 웹팩이 **번들 후 결과물을 어디로 내보낼지 지정**하는 속성이다.
- 파일 이름(filename), 경로(path)를 별도로 지정할 수 있고, `clean`을 `true`로 설정하면 지정한 결과물이 내보내지는 디렉토리에 사용하지 않는 파일을 알아서 정리해 준다.
### loader
- Webpack은 기본적으로 JavaScript와 JSON 파일만 이해할 수 있기 때문에, 사용하려는 포맷에 대응하는 `loader`를 설정해 주어야 **다른 포맷의 리소스도 `dependency graph`에 추가**할 수 있다.
- `loader`를 설정하려면 `test`와 `use` 두 가지 필수 속성을 적어주어야 한다. `test`는 어떤 파일을 변환할지 지정하는 속성으로, 보통 정규표현식으로 작성한다. `use`는 파일을 변환할 때 어떤 로더를 사용해야하는지 명시하는 속성이다.
### plugins
- `html-webpack-plugin`을 사용하면 dist의 main.js를 스크립트 파일로 포함하는 HTML 문서를 dist 디렉토리 내에 자동으로 생성해 준다.
- `mini-css-extract-plugin`을 사용하면 빌드 결과 JS 파일에서 스타일시트를 분리해서 CSS 파일을 따로 만들어 준다. 
