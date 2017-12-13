## Yarn

安装yarn( Yarn是Facebook提供的替代npm的工具，可以加速node模块的下载)与react-native-cli（React Native的命令行工具用于执行创建、初始化、更新项目、运行打包服务（packager）等任务）。快速(缓存它下载的每个包，所以不需要重复下载)、可靠(每个安装包的代码执行前使用校验码验证包的完整性)、安全的依赖管理(用一个格式详尽但简洁的 lockfile 和一个精确的算法来安装)

[中文文档](https://yarnpkg.com/zh-Hans/)

### 安装

```sh
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

sudo apt-get update && sudo apt-get install yarn

npm install -g yarn
brew install yarn
```

### 镜像源配置

```
yarn config set registry https://registry.npm.taobao.org --global
yarn config set disturl https://npm.taobao.org/dist --global
```

### 使用

* 开始新项目:yarn init 打开一个交互式表单天剑项目信息,生成package.json信息文件
* 添加依赖包: yarn add [package] yarn add [package]@[version] 1.2.3 ^1.0.0 yarn add [package]@[tag]
* 分别添加到 devDependencies、peerDependencies 和 optionalDependencies： yarn add [package] --dev yarn add [package] --peer yarn add [package] --optional
* 升级依赖包: yarn upgrade [package] yarn upgrade [package]@[version] yarn upgrade [package]@[tag]
* 移除依赖包: yarn remove [package]
* 安装项目的全部依赖:yarn || yarn install --flat 安装一个包的单一版本 --force 强制重新下载所有包 --production 只安装生产环境依赖