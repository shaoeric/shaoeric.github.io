# Matplotlib中文设置

```python
import numpy as np
import matplotlib.pyplot as plt
import os
import seaborn as sns

from matplotlib.ticker import FuncFormatter
from matplotlib.font_manager import FontProperties

# 全局设置
font_size = 20
config = {
    "font.family":'serif',
    "font.size": font_size,
    "mathtext.fontset":'stix'
}
plt.rcParams.update(config)
plt.rcParams['axes.unicode_minus'] = False  # 用来正常显示负号


# 字体设置
zh_font = FontProperties(fname='字体路径.ttf', size=font_size)
font_dict = {
    'fontproperties': zh_font,
    'size': font_size
}

f, ax = plt.subplots(1, 1, figsize=(8, 6), dpi=200)
x = np.linspace(0, 10, 100)
y = np.exp(2*x)

plt.plot(x, y, label='测试$y=e^{2x}$')

plt.legend(loc='best', prop=zh_font)

# plt.subplots_adjust(left=0.102, bottom=0.115, right=0.990, top=0.990, hspace=0.2,wspace=0.2)
plt.xlabel(u'横轴', **font_dict)
plt.ylabel(r'纵轴$\times 10^{6}$', **font_dict)  # 反斜杠有特殊含义 所以用raw string,或者用\\times


def formatnum(x, pos):
    return '$%d$' % (x // 1e6)
formatter = FuncFormatter(formatnum)
ax.yaxis.set_major_formatter(formatter)  # y轴用1e6表示


plt.yticks(**font_dict)  # 自定义字体
plt.xticks(fontproperties='Times New Roman', size=font_size)  # 系统自带字体
plt.show()

# plt.savefig("xxx.tif", bbox_inches='tight', pad_inches=0)
```

<div align=center>
<img src="../img/codepocket/matplotlib.png"/>
</div>
