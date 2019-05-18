# 个性化 vim

在 ubuntu18.04.2 上个性化 vim.

## 插件管理 [vim-plug](https://github.com/junegunn/vim-plug)

``` shell
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

## color

软链接 colors 文件夹到  `~/.vim/colors`

``` shell
ln -s colors ~/.vim
```
## vimrc

软链接 .vimrc 文件夹到  `~/.vimrc`

``` shell
ln -s ./vimrc ~
```

## 感谢

.vimrc 文件大部分参考了 [vimplus](https://github.com/chxuan/vimplus)项目, 感谢 chxuan.

