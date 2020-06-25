# RunShadowsocks
a shell to build&amp;run shadowsocks on service
## edit the shell then run it as the follow comand
```bash
wget  -N --no-check-certificate https://github.com/droidzf/RunShadowsocks/releases/download/v1.0/runss && chmod +x runss && bash runss
```
>注意：如果pip安装过程出现

`Traceback (most recent call last):
  File "/usr/bin/pip", line 11, in <module>
    sys.exit(main())
  File "/usr/lib/python2.7/dist-packages/pip/__init__.py", line 215, in main
    locale.setlocale(locale.LC_ALL, '')
  File "/usr/lib/python2.7/locale.py", line 581, in setlocale
    return _setlocale(category, locale)`
执行export LC_ALL=C


>AttributeError: /usr/lib/x86_64-linux-gnu/libcrypto.so.1.1: undefined symbol: EVP_CIPHER_CTX_cleanup

vim /usr/local/lib/python2.7/dist-packages/shadowsocks/crypto/openssl.py
52行libcrypto.EVP_CIPHER_CTX_cleanup.argtypes = (c_void_p,) 改为libcrypto.EVP_CIPHER_CTX_reset.argtypes = (c_void_p,)
111行将libcrypto.EVP_CIPHER_CTX_cleanup(self._ctx) 改为libcrypto.EVP_CIPHER_CTX_reset(self._ctx)

BBR 加速

Linux kernel 4.9 及以上已支持 tcp_bbr

1.查看系统内核版本：

uname -r

2.开启BBR：

echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf

echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf

3.保存生效：

sysctl -p

4.检查BBR是否启用：

sysctl net.ipv4.tcp_available_congestion_control

返回值一般为：net.ipv4.tcp_available_congestion_control = reno cubic bbr

sysctl net.ipv4.tcp_congestion_control

返回值一般为：net.ipv4.tcp_congestion_control = bbr

sysctl net.core.default_qdisc

返回值一般为：net.core.default_qdisc = fq

lsmod | grep bbr

返回值有 tcp_bbr 模块则BBR已启动：

tcp_bbr 20480 10
