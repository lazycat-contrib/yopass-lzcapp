# Yopass 懒猫微服包

安全分享密文：一次性链接，读过即焚。

- 上游：<https://github.com/jhaals/yopass>
- 镜像：`jhaals/yopass`
- 许可：Apache-2.0（全文见 content/licenses/LICENSE，无子目录覆盖条款）

## 组成

| 服务 | 镜像 | 作用 |
| --- | --- | --- |
| `yopass` | `jhaals/yopass` | 应用本体，监听 1337 |
| `memcached` | `memcached:1.6-alpine` | 存放未读取的密文（短期） |

## 关键配置说明

- 存储后端通过启动参数指定：`--memcached=memcached:11211`
  （上游也支持 Redis，本包选 memcached 更轻）。
- **未读密文属短期数据**：memcached 不做持久化，重启即清空；
  已读密文本来就会被销毁，因此不需要持久卷。
- **没有账号体系**：安全性来自不可猜的链接 + 读过即焚；
  不加 `public_path`，访问由懒猫入口鉴权。

## 未验证部分

未在真机上实测：创建密文、读取与销毁、文件分享、过期清理。
