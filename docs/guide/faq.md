# FAQ
### IOS10.3系统安装mitmproxy证书后仍无法抓取https接口数据

>IOS10.3 升级了ssl证书验证机制。 如果只是安装了证书而没有在关于里添加信任，客户端会主动关闭连接。
（10.2安装了证书，在升级到10.3时，默认是信任的）

**解决办法：**

在安装了相关证书后，需要到设置 → 通过 → 关于本机 → 证书信任设置,选择对应的证书，启用完全信任。
 
### 执行setup.sh时，提示SSL证书验证失败

>在pip安装依赖库的时候提示“There was a problem confirming the ssl certificate: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed”

**解决办法1：**

当前https请求使用了未认证的ssl证书，请检查当前环境是不是在代理环境下，如果是，请关闭代理服务，中心执行setup即可。

**解决办法2：**

如果仍要在此环境下使用，需在setup.sh中做如下修改：
```bash
pip3 install -r ./requirements.txt --trusted-host pypi.python.org
```
 
### 执行setup时报错，没有执行虚拟环境中的pip3

>由于本地python3环境中没有pip，创建虚拟环境中不包含pip命令，从而导致虚拟环境变量没有覆盖系统的pip。

**解决办法：**

重新安装python3

* 如果使用brew安装的可以使用brew uninstall python3卸载
* 如果使用其他方式安装的可以直接删除python安装的目录。
* 然后再使用brew install python3安装python3

**注意：** 不要误删/System目录下的python2
 

### 使用brew时提示安装权限问题或安装其他依赖失败

>由于macos10.12后进行了安全机制更新，旧版本的brew即使在更新后仍无法正常工作。需要卸载后重新安装即可。

```bash
uninstall
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"
homebrew doc
```
 
### 执行setup报错，pip install PyYAML失败

>错误提示: 使用xcode build 失败。

**解决办法：**

需要切换xcode sdk

在xcode preferences中选择8.0以上的xcode command line tools，然后重新build。


### 提示无法找到lyrebird命令
>Python安装到系统Library目录下时，没有足够的权限。
可以尝试使用虚拟环境。

```bash
python3 -m venv venv
source venv/bin/activate
pip3 install lyrebird    
```