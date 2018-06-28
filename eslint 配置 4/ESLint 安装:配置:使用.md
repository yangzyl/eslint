基于小范围讨论及实验, 初步定下前端项目 ESLint 规范配置, 使用方法如下:

### 安装 eslint & babel-eslint

```
$ npm install --save-dev eslint babel-eslint
```

### 安装 eslint-config-airbnb
> 由于有部分特定依赖关系, 所以需要使用以下命令 ( 这是 airbnb 推荐安装方法, 直接安装相关包可能会安装不上, [参考](https://www.npmjs.com/package/eslint-config-airbnb) )
```
(
  export PKG=eslint-config-airbnb;
  npm info "$PKG@latest" peerDependencies --json | command sed 's/[\{\},]//g ; s/: /@/g' | xargs npm install --save-dev "$PKG@latest"
)
```
### 在根目录下添加 `.eslintignore` 文件

```
# /node_modules/* and /bower_components/* ignored by default

# Ignore built files except build/index.js
build/*

# Ignore css files
*.css
```
### 在根目录下添加 `.eslintrc.json` 文件
此文件为主要配置设置, 见附件 `.eslintrc.json`
另外, 可在 webstorm 中设置使用此配置文件直接在编辑时进行检查, 并提示: 

- `Preferences -> Languages & Frameworks -> JavaScript -> Code Quality Tools -> ESLint` 
- 开启, 选择 ESLint package 为 项目 中的 `<project path>/node_modules/eslint`
- 选择配置文件为前面添加的 `<project path>/.eslintrc.json`

### 命令行使用
```
$ ./node_modules/.bin/eslint src/* -o report.html -f html --fix
```
个人推荐使用 `html` format, 所有检查结果会呈现为一个 html 文件, 打开后, 可一个一个文件查看问题
![ESLint 检查结果](https://box.worktile.com/view/f168b98110a4499e80fb1ee19b971e73?pid=92b4779c87ee43f3ad9f5722d53e4e21)
**PS**: 项目成员可约定好一个文件夹如 `eslint`, 存放检查结果, 并将其添加至 `.gitignore`