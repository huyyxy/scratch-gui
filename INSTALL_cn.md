# 安装手册
## 安装步骤

```
git clone https://github.com/huyyxy/scratch-vm.git
cd scratch-vm
npm install
npm link

# 新开一个shell
git clone https://github.com/huyyxy/scratch-gui.git
cd scratch-gui
npm link scratch-vm
npm run prepublish
npm install
npm start
```

## 参考信息
http://adapter.codelab.club/dev_guide/first-Scratch3-Extension/
