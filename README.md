# QtPDF

# 编译条件

 - Qt

请自己更改Qt的目录，这里应该加上自定义路径，请自己改下cmakelist


# 注意

## 从官方拷贝不能修改的目录
- pdf  为Qt官方拷贝过来   C:\Qt\5.15.2\Src\qtwebengine\src 下
- pdfwidget 为Qt官方拷贝过来
- 3rdparty  为pdfium二进制官方，不可修改
- QtPdf是从官方文档include路径拷贝过来的    C:\Qt\5.15.2\Src\qtwebengine\include 下
## Others
- [ ] third_party改成自动拷贝生成

- [ ]  QtPdf模块改成自动拷贝生成
- [ ]  third_party改为自动拷贝生成
- [ ]  QT_BUILD_PDF_LIB 改成cmake自定义命名为1
- [ ]  Qt路径改成自定义的命名

