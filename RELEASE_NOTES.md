# TaskFlow 0.1.0 Windows x64

首次公开二进制发布；应用内部版本为 0.1，本次分发编号为 0.1.0。

## 下载

普通用户下载 **TaskFlow-0.1.0-windows-x64.zip**，完整解压后运行 `TaskFlow/TaskFlow.exe`，无需安装 Qt。请保留整个文件夹，不要只复制 EXE。

其他源码附件用于履行第三方许可并方便修改/重建库，正常使用无需下载。GitHub 自动生成的 Source code (zip/tar.gz) 仅包含公开下载仓库的说明资料，不是可运行软件。

## 功能

项目分类、任务搜索筛选排序、今日/逾期/未来 7 天、任务统计、回收站、分钟级截止与运行期间提醒、托盘、数据备份恢复，以及白色/深石墨/跟随系统、字体字号和中英文设置。

## 数据与许可

程序包不含个人数据库。数据通常保存在当前 Windows 用户的 AppData/TaskFlow/TaskFlow；复制程序目录不隔离数据，升级/恢复前请备份。自有程序按包内 LICENSE.txt 免费使用，业务源码保持私有；第三方组件保留各自许可及修改/替换权利。

QtSvg、QtTranslations、MinGW-w64 v11 源码、MinGW-Builds 配方及原始构建记录作为本 Release 附件提供。QtBase 和 GCC 采用 GPLv3 第 6(d) 节网络源码方式，通过以下对应上游源码下载，完整地址、大小、摘要见 SOURCE_DOWNLOADS.json 和 [源码说明](https://github.com/hqf2335/TaskFlow-Releases/blob/main/SOURCE_CODE.md)：

- [QtBase 6.12.0 完整源码](https://download.qt.io/official_releases/qt/6.12/6.12.0/submodules/qtbase-everywhere-src-6.12.0.tar.xz)
- [GCC 13.1.0 完整源码](https://ftp.gnu.org/gnu/gcc/gcc-13.1.0/gcc-13.1.0.tar.xz)

两份大源码均已实际下载并核对上游摘要，包内提供备用镜像地址。Qt 动态库采用 LGPLv3；库替换、调试修改所需逆向工程不受应用许可限制。

## 本次检查与限制

- 文件清单、SHA256、DLL 导入依赖、SQLite 文件头和个人设置排查通过。
- 包内完整性校验通过；篡改文件、混入数据库、缺少许可的反例均被拒绝。
- 从无开发 Qt PATH 的隔离检查副本运行临时 SQLite/INI Windows UI 烟测，退出码 0，生成 11 张控件截图；检查程序不随运行包分发。
- 复用既有 Release 应用二进制，没有重编译业务逻辑；历史 Release CTest 30/30 不记成本次重新执行。
- 独立无 Qt Windows、真实物理 DPI/多屏、托盘休眠/锁屏及读屏仍待全面人工验收；应用未作代码签名。本发布面向早期使用与反馈。

总 SHA256SUMS.txt 用于核对下载附件；ZIP 内 Verify-Package.ps1 用于核对解压目录。哈希校验不等于身份签名认证。
