# 第三方对应源码、构建与库替换

本文件对应 TaskFlow 0.1 的 Windows x64 便携发布。提供的是第三方对应源码，不公开 TaskFlow 自有业务源码。

## 免费获取完整对应源码

QtBase 与 GCC 采用 GPLv3 第 6(d) 节的网络源码方式：在程序包、下载仓库及 Release 页面旁明确给出可免费、无需登录下载的对应源码地址，源码可由上游或第三方服务器提供。具体 URL、大小及已核验 SHA-256 同时写在 SOURCE_DOWNLOADS.json。发布者仍负责在适用分发义务期间保持源码可获取；链接失效时请通过本仓库 Issues 报告，需恢复源码可获取性后再继续相应分发。

### QtBase 6.12.0 完整源码

包含 Core/Gui/Widgets/Sql、Windows/SQLite 等插件、内嵌第三方代码和构建脚本。源码提交 `025bdad181de241e81bf853c8a2d7bf3d19261a9`。

- [Qt 官方下载](https://download.qt.io/official_releases/qt/6.12/6.12.0/submodules/qtbase-everywhere-src-6.12.0.tar.xz)
- [Qt 官方镜像网络中的 JAIST 下载](https://ftp.jaist.ac.jp/pub/qtproject/archive/qt/6.12/6.12.0/submodules/qtbase-everywhere-src-6.12.0.tar.xz)
- 文件名 `qtbase-everywhere-src-6.12.0.tar.xz`，51,220,268 字节。
- SHA-256：`a951bd163c7b80fc6b8c88d7668fb56abf91c152373e13c10666763238131307`。

### GCC 13.1.0 完整源码

包含 libgcc、libstdc++ 及原始构建文件；另须使用同一 Release 附带的 MinGW-Builds 配方及 10 个 GCC 补丁。

- [GNU 官方下载](https://ftp.gnu.org/gnu/gcc/gcc-13.1.0/gcc-13.1.0.tar.xz)
- [清华 GNU 镜像下载](https://mirrors.tuna.tsinghua.edu.cn/gnu/gcc/gcc-13.1.0/gcc-13.1.0.tar.xz)
- 文件名 `gcc-13.1.0.tar.xz`，87,451,196 字节。
- SHA-256：`61d684f0aa5e76ac6585ad8898a2427aade8979ed5e7f85492286c4dfc13ee86`。

上述两份完整源码已实际下载并通过上游摘要核对；GitHub 大附件上传超时，因此没有将未完成附件作为完整源码发布。

## 同一 Release 内的其余源码及构建附件

在 https://github.com/hqf2335/TaskFlow-Releases/releases/tag/v0.1.0 免费下载：

- qtsvg-everywhere-src-6.12.0.tar.xz：Svg 和 SVG 插件；提交 883a58532078d003cefef0a549bfe9f885ce41f5。
- qttranslations-everywhere-src-6.12.0.tar.xz：翻译源；提交 2811457ceff8f0c24a1c4d14f947a283a17239d0。
- mingw-w64-v11.0.0.tar.gz：MinGW-w64 和 winpthreads 源码。
- mingw-builds-gcc13-recipes.tar.gz：构建配方与补丁，固定提交 7ff96692a8032d893781523b311ac9b6cbbda0a1，对应工具链构建时期。
- third-party-build-info.zip：Qt 官方配置、工具链原始构建记录、10 个已使用 GCC 补丁和说明。

这些文件依各自许可证分发。Release 的 SHA256SUMS.txt 核对实际附件，SOURCE_DOWNLOADS.json 核对外部两份大源码。GitHub 自动生成的 Source code.zip/tar.gz 只是公开下载仓库说明文件快照，不是应用业务源码或完整第三方源码，请按上述地址下载具名文件。

## 来源核对

Qt 源码包的 .tag 与安装包模块提交相同。随包 Qt DLL/插件与本机官方安装文件逐字节一致，其 Qt Company Authenticode 签名验证有效；安装 SBOM 中的文件摘要与这些已签名二进制不同，未将 SBOM 摘要核对记为通过。组件许可标注使用官方 SBOM，源码身份使用模块提交标记，并保留独立文件摘要。Qt 库源码未由 TaskFlow 修改。

官方 Qt 与 TaskFlow 应用所用编译器版本不能混同：TaskFlow 应用使用 MinGW 13.1.0；Qt 原始编译器和配置以 third-party-build-info.zip 内 config_qtbase.summary 为准。不承诺位级复现。

## 构建与替换

按源码内 README/INSTALL、configure 脚本及 https://doc.qt.io/qt-6/windows-building.html 准备 Windows x64 Qt 构建环境。使用共享库配置 BUILD_SHARED_LIBS=ON，先构建安装 qtbase，再用该安装的 qt-configure-module/CMake 构建 qtsvg。保留与原库兼容的 Qt 6 ABI、体系结构、运行时和插件接口。官方配置记录随 third-party-build-info.zip 提供，不直接照搬上游机器绝对路径。

MinGW 运行库按 build-info.txt 的 GCC 配置、MinGW-Builds 脚本与列出的 10 个 GCC 补丁构建，使用 x86_64、POSIX threads、SEH、MSVCRT、MinGW-w64 v11；源码附件包含上游构建说明。构建配方与未修改上游源分别提供，补丁应用次序以原构建记录为准。

替换前退出程序并备份数据/目录，把兼容修改版 Qt6Core/Gui/Widgets/Sql/Svg DLL 放在 TaskFlow.exe 旁，对应插件放入 platforms、sqldrivers、imageformats、iconengines、styles。qt.conf 指向当前目录。正常启动没有官方哈希或签名白名单锁定；替换后 Verify-Package.ps1 报哈希变化属预期，不阻止运行修改后的组合。

本包是可复制 Windows 程序目录，无产品密钥、签名白名单或安装锁，不需要发布者解锁材料。涉及数据库兼容性的修改，请用隔离测试账号和数据库副本验证。
