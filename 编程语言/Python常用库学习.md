### 重要的python库

## NumPy(Numerical Python)

提供多种数据结构、算法以及大部分涉及Python数值计算所需的接口



## pandas

提供高级数据结构和函数

## matplotlib



## qrcode、image、opencv使用

```python
#=======================安装qrcode和image库============================
# 安装qrcode和image库
pip install qrcode
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple image
pip install opencv-python    			# 修改突变，添加文字
#=============================使用======================================
"""
	
"""
import qrcode
url = "http://www.zhuolu2018.com/www/shopjoin/QcAction.jsp?QC_CD="
# img = qrcode.make(url)
qr = qrcode.QRCode(
    version=1,  # 生成二维码尺寸的大小 1-40 1:21*21（21+(n-1)*4）
    error_correction=qrcode.constants.ERROR_CORRECT_L,  # L:7% M:15% Q:25% H:30%
    box_size=10,  # 每个格子的像素大小
    border=3,  # 边框的格子宽度大小
)
qr.add_data(url + qcCd)
qr.make(fit=True)
# 生成图片
img = qr.make_image()
# 更改大小
out = img.resize((240, 240))
# 基于图片创建画布
draw = ImageDraw.Draw(out)
# 字体
fnt = ImageFont.truetype(r'C:\Windows\Fonts\simsun.ttc', 12)
#(16, 226)-位置, name-添加的文本,font-字体
draw.text((16, 226),
          name, font=fnt)
# 保存图片
out.save('D:\\workspace\\zhuolu\\datadash\\static\\image\\'+name + '.png')

```

