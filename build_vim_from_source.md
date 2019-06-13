# 源码安装 vim

仅仅阐述在 ubuntu18.04.2 下如何编译安装.

1. 删除之前装过的 vim, vi 等

``` shell
sudo apt-get remove -y vim vim-runtime gvim
sudo apt-get remove -y vim-tiny vim-common vim-gui-common vim-nox
sudo rm -rf /usr/bin/vim*
sudo rm -rf /usr/local/bin/vim*
sudo rm -rf /usr/share/vim/vim*
sudo rm -rf /usr/local/share/vim/vim*
```

2. 安装依赖

``` shell
sudo apt install libncurses5-dev libgnome2-dev libgnomeui-dev \
libgtk2.0-dev libatk1.0-dev libbonoboui2-dev \
libcairo2-dev libx11-dev libxpm-dev libxt-dev python-dev \
python3-dev ruby-dev lua5.1 liblua5.1-dev libperl-dev git
```

3. clone 源码

``` shell
rm -rf '~/vim' && git clone https://github.com/vim/vim.git ~/vim
```

4. configure

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

**NOTICE1:**  `--prefix=/usr` 是安装位置, 请自行斟酌.  
**NOTICE2:**  可以使用 `./configure --help` 查看更多 configure 信息.  
**NOTICE3:** 网上很多教程有 `--with-python-config-dir=xxx` 和 `--with-python3-config-dir=xxx`, 但是已经 deprecated 了.

5. make 

``` shell
make && sudo make install
```
因为我的安装位置是 `/usr`, 所以需要 root 权限.

6. vim --version

使用 `vim --version` 看看编译时间等.
