# 自動画像圧縮の設定
## 画像圧縮ツールのインストール
1. 下記画像圧縮ツールをインストールする
- jpegoptim
- pngquant

```
brew install jpegoptim pngquant
```

## huskyの設定

1. 下記パッケージをインストールする
- lint-staged
- husky
- svgo

```
npm i -D lint-staged husky svgo
```

2. ```.package.json```ファイルのdevDependenciesの項目の下に下記コードを記述する。
```
  "devDependencies": {
    "xxx": "xxx",
  },
  // この下からコピー
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "./**/*.{jpg,jpeg,JPG,JPEG}": [
      "jpegoptim --strip-all --max=80 -t"
    ],
    "./**/*.{png,PNG}": [
      "pngquant --ext .png --speed 1 --force",
      "git add"
    ],
    "./**/*.svg": [
      "svgo --config=.svgo.yml --enable='removeComments,mergePaths'"
    ]
  }
```