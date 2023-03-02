# 源码安装 vim

仅仅阐述在 ubuntu18.04.2 下如何编译安装.

## 删除之前装过的 vim, vi 等

``` shell
bash
sudo apt-get remove -y vim vim-runtime gvim vim-tiny vim-common vim-gui-common vim-nox
sudo rm -rf /usr/bin/vim*
sudo rm -rf /usr/local/bin/vim*
sudo rm -rf /usr/share/vim/vim*
sudo rm -rf /usr/local/share/vim/vim*
exit
```

## 安装依赖

``` shell
sudo apt install libncurses5-dev libgnome2-dev libgnomeui-dev \
libgtk2.0-dev libatk1.0-dev libbonoboui2-dev \
libcairo2-dev libx11-dev libxpm-dev libxt-dev python-dev \
python3-dev ruby-dev lua5.1 liblua5.1-dev libperl-dev git
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
            --enable-pythoninterp=yes \
            --enable-python3interp=yes \
            --enable-perlinterp=yes \
            --enable-luainterp=yes \
            --enable-gui=gtk2 \
            --enable-cscope \
            --prefix=/usr
```

one-line

```shell
./configure --with-features=huge --enable-multibyte --enable-rubyinterp=yes --enable-pythoninterp=yes --enable-python3interp=yes --enable-perlinterp=yes --enable-luainterp=yes --enable-gui=gtk2 --enable-cscope --prefix=/usr
```

__NOTICE1:__  `--prefix=/usr` 是安装位置, 请自行斟酌.  
__NOTICE2:__  可以使用 `./configure --help` 查看更多 configure 信息.  
__NOTICE3:__ 网上很多教程有 `--with-python-config-dir=xxx` 和 `--with-python3-config-dir=xxx`, 但是已经 deprecated 了.

### 特殊情况

在一些情况下面, 如果系统装有 python3.6, 同时又装
有 anaconda3(也即有另一个 python3.7),
那么在编译时最好指定使用哪个 python, 不然可能会出现
__找不到libpython.3.7m.a__ 这样的错误.
这样的情况是因为不能正确加载 libpython3.7m.a 文件, 导致使用 python3/dyn
特性的一些插件(诸 YouCompleteMe) 不能使用.


``` shell
./configure --with-features=huge \
            --enable-multibyte \
            --enable-rubyinterp=yes \
            --enable-pythoninterp=yes \
            --enable-python3interp=yes \
            --with-python3-command=/usr/bin/python3.8 \
            --enable-perlinterp=yes \
            --enable-luainterp=yes \
            --enable-gui=gtk2 \
            --enable-cscope \
            --prefix=/usr
```

__NOTICE:__ 我在编译时指定了 python3.6, 但是在配置 ycm 时指定了 anaconda3 的
python3.7, 这说明在一定版本差距上, lib库是可以通用的.

## make

``` shell
make && sudo make install
```
因为我的安装位置是 `/usr`, 所以需要 root 权限.

## vim --version

使用 `vim --version` 看看编译时间等.

## 使 vim 是默认编辑器

``` shell
sudo update-alternatives --install /usr/bin/editor editor /usr/bin/vim 100
```

查看编辑器

``` shell
update-alternatives --config editor
```
