# 源码安装 vim

阐述在 macOS Big Sur 11.4 下如何编译安装.

## 安装依赖

TODO
``` shell
```

## clone 源码

``` shell
rm -rf '~/vim' && git clone https://github.com/vim/vim.git --depth 1 ~/vim
```

## configure

``` shell
./configure --with-features=huge \
            --enable-multibyte \
            --enable-rubyinterp=yes \
            --enable-python3interp=yes \
            --with-python3-command=python3 \
            --enable-perlinterp=yes \
            --enable-luainterp=yes \
            --enable-gui=gtk2 \
            --enable-cscope \
            --prefix=/usr/local
```

one-line

```shell
./configure --with-features=huge --enable-multibyte --enable-rubyinterp=yes --enable-python3interp=yes --with-python3-command=python3 --enable-perlinterp=yes --enable-luainterp=yes --enable-gui=gtk2 --enable-cscope --prefix=/usr/local
```

__NOTICE1:__ `--prefix=/usr/local` 是安装位置, 请自行斟酌.  
__NOTICE2:__ 因为系统自带的 vim 没有删除, 所以需要在 bashrc 或 zshrc 中 `alias vim=/usr/local/bin/vim`.
__NOTICE3:__ 网上很多教程有 `--with-python-config-dir=xxx` 和 `--with-python3-config-dir=xxx`, 但是已经 deprecated 了.

## make

``` shell
make && sudo make install
```

## vim --version

使用 `vim --version` 看看编译时间等.

