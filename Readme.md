加密算法
===
### base64

算法核心：

* 将字符串拆成每三个字符一组
* 计算每一个字符对应的 ASCII 码二进制
* 将 8 位的二进制码，按照每 6 位一组重新分组，不足 6 位的在后面补 0 
* 计算对应的十进制编码
* 按照 base64 表，查看对应的字符

实现方式：
```python
import base64

s = 'hello kitty'
# 加密
jm = base64.b64encode(s.encode())
print(jm)

# 解密
jm1 = base64.b64decode(jm)
print(jm1.decode())
```
注：
```python
# 重写 b64encode 方法
@staticmethod
def b64encode(content):
	return base64.urlsafe_b64encode(content).replace(b'=', b'')

# 重写 b64decode 方法
@staticmethod
def b64decode(b):
	'''
	把丢失的 = 号加回来
	'''
	sem = len(b) % 4
	if sem > 0:
		b += b'=' * (4 - sem)
	return base64.urlsafe_b64decode(b)
```

### hash( hashlib )

* 摘要算法又称哈希算法、散列算法。它通过一个函数，把任意长度的数据转换为一个长度固定的数据串
	
* 三大特点：1) 定长输出  2) 不可逆  3) 雪崩
	
	+ #### md5
		```python
		import hashlib
			
		str = 'hello kitty'  # 创建加密对象
		h5 = hashlib.md5()  # 创建md5对象
		h5.update(str.encode())  # 将对象属性转化为字节码
		print(h5.hexdigest())  # 加密后
		```
		
	+ #### sha256
		```python
		import hashlib
		
		str = 'hello kitty'  # 创建加密对象
		h6 = hashlib.sha256()  # 创建md5对象
		h6.update(str.encode())  # 将对象属性转化为字节码
		print(h6.hexdigest())  # 加密后
		```