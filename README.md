# jdk8u332 codeql 数据库

> 直接下载解压了就能用，毕竟下载比编译省事

## 使用

```shell
git clone https://github.com/1nhann/jdk8u332_codeql_db.git
unzip jdk8u332_codeql_db.zip
```



## 创建 openjdk 的 codeql 数据库的过程

apt-get 安装一些软件：

```shell
apt-get install -y build-essential gdb cmake cpio file unzip zip wget ccache libfontconfig1-dev libfreetype6-dev  libcups2-dev libx11-dev  libxext-dev  libxrender-dev  libxrandr-dev  libxtst-dev  libxt-dev libasound2-dev  libffi-dev  autoconf
```

下载 codeql binary ：

```shell
url='https://github.com/github/codeql-cli-binaries/releases/latest/download/codeql-linux64.zip' && wget "$url" -O 1.zip && unzip 1.zip && ln -s `pwd`/codeql/codeql /usr/bin/codeql && rm 1.zip
```

下载 jdk8 源码，版本切换到 jdk8u332，创建 codeql 数据库：

```shell
git clone https://github.com/openjdk/jdk8u.git jdk8u332 && cd jdk8u332 && git checkout jdk8u332-b00 && chmod +x ./configure && ./configure --with-target-bits=64 --with-boot-jdk=/usr/lib/jvm/java-8-openjdk-amd64 --with-debug-level=slowdebug --enable-debug-symbols ZIP_DEBUGINFO_FILES=0 && codeql database create ./8u332_db --language="java" --command="make -j all DISABLE_HOTSPOT_OS_VERSION_CHECK=OK ZIP_DEBUGINFO_FILES=0"
```













