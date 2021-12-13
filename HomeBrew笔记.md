# HomeBrew系列操作

## 解决brew安装速度慢的问题(替换homebrew镜像源)

1.替换brew.git:

```bash
cd "$(brew --repo)”
# 阿里源
git remote set-url origin https://mirrors.aliyun.com/homebrew/brew.git
# 清华源
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
```

2.替换homebrew-core.git:

```bash
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
# 阿里源
git remote set-url origin https://mirrors.aliyun.com/homebrew/homebrew-core.git
# 清华源
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
```

3.终端输入命令：

> echo $SHELL 看输出结果是/bin/zsh还是/bin/bash

- /bin/zsh替换homebrew-bottles:

```bash
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.aliyun.com/homebrew/homebrew-bottles' >> ~/.zshrc
source ~/.zshrc
```

- /bin/bash替换homebrew-bottles:

```bash
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
source ~/.bash_profile
```

4.恢复homebrew国内镜像源配置

- 重置brew.git

```bash
cd "$(brew --repo)"
git remote set-url origin https://github.com/Homebrew/brew.git
```

- 重置homebrew-core.git

```bash
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://github.com/Homebrew/homebrew-core.git
```

- 重置homebrew-bottles

```bash
将刚添加到~/.bash_profile文件的语句注释掉即可
```