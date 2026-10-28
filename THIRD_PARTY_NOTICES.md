# 第三方组件与用户权利

TaskFlow 使用 Qt 6.12.0 的动态库，选择 LGPL-3.0-only 许可；业务源码保持私有。Qt 库及插件由 Qt Company 和各贡献者拥有版权。许可证全文在 licenses/LGPL-3.0.txt 和 licenses/GPL-3.0.txt。

| 随包或嵌入组件 | 适用许可与材料 |
|---|---|
| Qt Core / Gui / Widgets / Sql / Svg、Windows/SQLite/图像/样式插件 | LGPLv3；实际文件及上游许可标注在 licenses/distributed-qt-components.json |
| 嵌入 EXE 的 Qt 中文标准控件翻译 | BSD-3-Clause；licenses/qttranslations/ |
| libgcc_s_seh-1.dll、libstdc++-6.dll，GCC 13.1.0 | GPLv3 + GCC Runtime Library Exception 3.1；licenses/gcc/COPYING3 与 COPYING.RUNTIME |
| MinGW-w64 运行时及 libwinpthread-1.dll | 对应 BSD/MIT/ZPL/公有领域声明；licenses/mingw-w64/ 与 licenses/winpthreads/ |
| Qt 内嵌的 FreeType、HarfBuzz、PCRE2、zlib、libpng、libjpeg-turbo、SQLite、double-conversion、md4c、Unicode 等 | 原始版本、版权与许可在 licenses/qt-upstream-attributions.json 和 licenses/qt-third-party-originals/ |

Portions of this software are copyright © 2026 The FreeType Project (www.freetype.org). All rights reserved. FreeType 选择 FreeType Project License（FTL），而非其 GPL 替代项。

Qt 归属材料收集自官方模块 src 范围，包含部分本构建未启用的代码。存在某许可文件不表示相应模块或开发工具随包分发。Qt 库选择 LGPLv3，Qt 翻译选择 BSD；GCC 运行库适用其运行库例外。GPL-only 开发工具没有作为应用运行件分发。

## 修改和替换 Qt 库

可使用兼容的修改版共享库替换包内 DLL 和插件，并运行组合后的程序；允许为调试这些修改进行必要的逆向工程。关闭 TaskFlow、备份数据和程序目录后操作。对应源码与替换步骤见 SOURCE_CODE.md。无需开发者签名或授权码解除库替换；哈希校验只报告与官方发行包是否一致，不阻止程序启动。

本包不包含可选的 Mesa opengl32sw.dll、Microsoft D3Dcompiler_47.dll、非 SQLite 数据库驱动或 QtNetwork；应用采用普通 Qt Widgets 界面。

参考：https://www.qt.io/development/open-source-lgpl-obligations 、 https://doc.qt.io/qt-6/licensing.html 、 https://www.gnu.org/licenses/lgpl-3.0.html 、 https://www.gnu.org/licenses/gcc-exception-3.1.html 。
