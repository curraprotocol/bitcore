# How to install bitcoin node for local development

```zsh
xcode-select --install

brew install automake libtool boost pkg-config libevent

git clone https://github.com/bitcoin/bitcoin.git


brew install berkeley-db@4 # only for legacy wallet support
brew install qt@5 # only for GUI

cd bitcoin/

# We will use configuration without legacy wallet support
./autogen.sh
./configure --without-bdb --with-gui=yes

make
make install
```
