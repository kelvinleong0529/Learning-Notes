# **NSIS**
- `Nullsoft Scriptable Install System (NSIS)` is a open source system to create Windows installer, it is designed to be as small and flexible as possible and is therefore very suitable for internet distribution
- `NSIS` is script-based and allows you to create the logic to handle even the most complex installation tasks
- many plug-ins and scripts are already available, we can create web installers, communicate with Windows and other software components, install or update shared components or more

```nsis
# helloworld.nsi
Name "Hello World~
OutFile "helloworld.exe"
Section "Hello World"
MessageBox MB_OK "Hello World!"
SectionEnd
```
- Compile with the following command:
```
<Path to NSIS> \makensis.exe <Path to script> \helloworld.nsi
```