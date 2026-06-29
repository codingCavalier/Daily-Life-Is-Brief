#### 编译pdfium
- 起因是需要同时使用VLC和pdfium，而这俩项目都带了libc++_shared.so，且版本不同，要么将其中一个使用静态链接库方式重新编，将libc++_shared.so直接编进产物的so，要么将俩库的libc++_shared.so搞成相同版本的，也是需要重新编
- 用的这个开源项目: https://github.com/paulocoutinhox/pdfium-lib
