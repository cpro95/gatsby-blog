---
title: 리눅스, 맥에서 oh my zsh 사용하기
date: 2020-02-02 21:03:91
category: oh-my-zsh
draft: false
---

![oh-my-zsh](./ohmyzsh.png)

예전에는 코딩을 할땐 IDE를 사용했었는데, 점점 리눅스(맥)의 터미널을 자주 사용 하게 되더군요. 그래서 해킨도 깔고, 남는 컴퓨터에 리눅스도 깔고 코딩을 하게 되었습니다. 최근 Visual Studio Code가 대세가 되면서 혹은 Web Programming을 하게 될땐 더더욱 터미널을 이용하게 됩니다.

## zsh / oh-my-zsh

기본적으로 터미널의 shell은 bash가 기본으로 깔려 있는데 우연히 웹써핑중에 zsh를 사용하는 미디엄 기사를 보고 한번 설치해 봤습니다.
보통 oh-my-zsh를 많이 쓰는데 이건 zsh의 확장 프로그램이라고 보면 됩니다.
굉장히 편한 기능이 많거든요.

## 설치하기

```
sudo apt install zsh
```

```bash
sudo pacman -S zsh
```

```bash
brew install zsh
```

각각 우분투, 아치, 맥에서 설치하는 방법입니다. 다들 아실건데요.
그러나 사실, oh-my-zsh 설치가 중요하죠.

```bash
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

```bash
sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

위에 두개 중에 한개로 설치하시면 됩니다.

그리고 중요한 플러그인이 있는데 추천드리고 싶은 거는 zsh-syntax-highlighting, zsh-autosuggestions 입니다.

설치방법은 간단합니다.

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

위 두가지를 설치하면 기본적으로 oh-my-zsh 폴더에 인스톨 됩니다.

이제 ~/.zshrc 파일에 넣어야 겠죠?
vim으로 ~/.zshrc 파일을 엽니다.
쭉 보시면 아래에 같은 부분이 있는데 이 부분을 다음과 같이 수정하시면 됩니다. 끝에 콤마는 쓰지 마세요.

```bash
plugins=(
   git
)
```

변경 후

```bash
plugins=(
   git
   zsh-autosuggestions
   zsh-syntax-highlighting
)
```

마지막으로 기존 bash 가 기본쉘로 설정되어 있는 걸 zsh로 기본쉘 변경을 해야 합니다.

```bash
chsh -s $(which zsh)
```

로그아웃하고 다시 접속하면 oh-my-zsh 가 잘 작동되는 걸 볼수 있을 겁니다.

그럼 이만.
