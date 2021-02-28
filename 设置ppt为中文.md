```bash
defaults write com.microsoft.Word AppleLanguages '("zh-cn")'
defaults write com.microsoft.Excel AppleLanguages '("zh-cn")'
defaults write com.microsoft.Powerpoint AppleLanguages '("zh-cn")'
```

### git拉取大文件时修改过：

```bash
sudo /usr/local/McAfee/AntiMalware/VSControl stopoas

git clone https://github.com/xianyuzhang0709/ituring_books.git
//失败
cd C_Notes/
git config http.postBuffer 524288000
git config http.sslVerify “false”
cd ..
git clone https://github.com/xianyuzhang0709/ituring_books.git
cd C_Notes/
git clone https://github.com/xianyuzhang0709/ituring_books.git
报错
git config --global http.sslBackend "openssl"
git clone https://github.com/xianyuzhang0709/ituring_books.git
git config --global http.sslCAInfo "C:\Program Files\Git\mingw64\ssl\cert.pem"
git clone https://github.com/xianyuzhang0709/ituring_books.git

git config --global http.postBuffer 1048576000
git clone https://github.com/xianyuzhang0709/ituring_books.git
git config --global http.sslverify "false"
git clone https://github.com/xianyuzhang0709/ituring_books.git
git clone https://github.com/xianyuzhang0709/reborn.git
没问题
cd C_Notes/
git push
fatal: bad numeric config value '“false”' for 'http.sslverify': invalid unit
git config --global http.sslverify false
git push 
成功push C_Notes
cd ..
cd Java_Notes/
git push
fatal: unable to access 'https://github.com/xianyuzhang0709/JavaNotes.git/': LibreSSL SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443 
git config --global --add remote.origin.proxy ""
没用
git config --global --unset-all remote.origin.proxy
git push 成功
```

