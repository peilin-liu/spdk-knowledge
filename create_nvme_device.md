# 如何创建一个spdk 的nvme device

想要使用spdk 的各种工具，并使用spdk Polling 来读写数据，需要spdk 设备支持

## 编译
可以根据 https://github.com/spdk/spdk#documentation 来编译，

## 挂载驱动
使用 ./scripts/setup.sh 可以挂载 uio 驱动到 nvme 设备上。

## 生成device 配置文件
./scripts/gen_nvme.sh --json-with-subsystems > ./build/bin/nvme_bdev.json
这样可以生成一个配置文件，提供给其他需要操作 nvme 设备的 spdk 工具使用

## spdk_dd 工具(使用本工具举例)
./bin/spdk_dd --config ./bin/nvme_bdev.json --ob Nvme0n1 --if /dev/zero --bs 1024 --count 1024
这里关键需要将配置文件带入，不然初始化的时候是找不到设备的。
