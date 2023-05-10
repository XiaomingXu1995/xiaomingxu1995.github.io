# shadowsocks 配置

```bash
# install shadowsocks
pip3 install shadowsocks

# create the config file
cd /etc/ && mkdir shadowsocks && cd shadowsocks && touch config.json

# copy the config.json content

# start the shadowsocks
sslocal -d start -c /etc/shadowsocks/config.json

# it may be errors: reset
# to modify the source code: /usr/local/lib/python3.6/site-packages/shadowsocks/crypto/openssl.py
# it depends on the different version of python (python3.6 or python3.8, etc.)

#change the next two lines (change the cleanup into reset)
#libcrypto.EVP_CIPHER_CTX_cleanup.argtypes = (c_void_p,)
libcrypto.EVP_CIPHER_CTX_reset.argtypes = (c_void_p,)
#libcrypto.EVP_CIPHER_CTX_cleanup(self._ctx)
libcrypto.EVP_CIPHER_CTX_reset(self._ctx)

# in your users set the http configures.
git config --global http.proxy socks5://127.0.0.1:1080
```
