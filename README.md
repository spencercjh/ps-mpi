# ps-mpi

> code is based on [ps-lite](https://github.com/dmlc/ps-lite).

### Build

#### Update your own proxy config in the [dependency](make/deps.mk)

```makefile
ifndef WGET
# PLEASE use your own proxy config
WGET = wget -e use_proxy=yes -e http_proxy=127.0.0.1:8889 -e https_proxy=127.0.0.1:8889
endif
```

#### Clone and build

```bash
git clone https://github.com/DLFC/ps-mpi
cd ps-lite && make -j4
```

### Run example

```shell
cd tests
./local_mpi.sh
```

在 `./local_mpi.sh` 中修改，可运行三个示例。


### 修改细节

1. 修改 `Makefile` 修改编译器 `g++` 为 `mpic++` 。
2. 修改运行脚本和测试样例，使得其适合 `mpi` 启动。
3. 修改 `postoffice.cc` ，初始化时按 `mpi` 的 `rank` 分配 `role` 。
4. 增加 `message.h` 中结构 `Node` 的成员 `rank_mpi` 记录节点的 `mpi_rank` 。并修改 `meta.proto` 。
5. 修改 `zmq_van.h` 。将 `data` 传递的方式改为 `mpi` 。
