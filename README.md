# RunShadowsocks
a shell to build&amp;run shadowsocks on service
## edit the shell then run it as the follow comand
```bash
wget  -N --no-check-certificate https://github.com/droidzf/RunShadowsocks/releases/download/v1.0/runss && chmod +x runss && bash runss
```
注意：如果pip安装过程出现
`Traceback (most recent call last):
  File "/usr/bin/pip", line 11, in <module>
    sys.exit(main())
  File "/usr/lib/python2.7/dist-packages/pip/__init__.py", line 215, in main
    locale.setlocale(locale.LC_ALL, '')
  File "/usr/lib/python2.7/locale.py", line 581, in setlocale
    return _setlocale(category, locale)`
执行export LC_ALL=C
