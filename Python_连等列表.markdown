现象: 读取两个目录不同大小的图片, A目录下全部是8*8*3, B全是16*24*3, 但是最后得到的图像矩阵却是一个一维的狗币矩阵,原因在于使用连等的列表,那么连等的列表是浅拷贝, 改变一个另外一个也同时被改变. 卧槽,无情!
将
`a = b = []`
改为
```python
a = []
b = []
```
还以为是自己在`tqdm`库和`zip`连用出错了呢.

让我倍感诡异的是, 明明全部元素的shape都是(8,8,3),但最后使用`np.array(dataA)`得到的矩阵却是(15824,).
```Python
def load_data(self):
  dataA = []
  dataB = []
  for A, B in tqdm(zip(glob.glob(os.path.join(self.path1, '*')), glob.glob(os.path.join(self.path2, '*')))):
    imgA = cv2.imread(A, cv2.IMREAD_COLOR).astype('float32')
    imgB = cv2.imread(B, cv2.IMREAD_COLOR).astype('float32')
    assert imgA.shape==(8,8,3)
    imgA = imgA / 255.    # 预处理方式不同: 对于生成器的输入数据, 归一化到[0,1]
    imgB = imgB / 127.5 - 1  # 对于判别器的输入数据, 标准化到[-1,1]
    dataA.append(imgA)
    dataB.append(imgB)
```








