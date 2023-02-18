```
git clone git@github.com:jhbaang/.dotfiles --depth=1 ~/.dotfiles

ln -s ~/.dotfiles/.vimrc ~/.vimrc
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
vim +PlugInstall

bash -c "$(curl --fail --show-error --silent --location https://raw.githubusercontent.com/zdharma-continuum/zinit/HEAD/scripts/install.sh)"
# 뭐 물어보면 no
ln -sf ~/.dotfiles/.zshrc ~
# zsh 설치
exec zsh
p10k configure

ln -sf ~/.dotfiles/.gitconfig ~
ln -sf ~/.dotfiles/.gitexclude ~
cp ~/.dotfiles/.gitconfig.local ~
```




terminal
- Ctrl-R : turn on fzf
- Ctrl-T : fzf file find
- bat : Beautiful cat
- fd  : Beautiful find
- rg  : RipGrep, much better grep

vim
hyphen : 파일 브라우저로 나가기
alt + - or \ : 화면 가르기
; 눌러도 : 나감
