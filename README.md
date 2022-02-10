# 对比条形图（交错正负轴）
## 1. 概览
### 1.1 基本介绍
交错正负轴条形图，与一般条形图相比，展现了负半轴信息，可以对正负数据有一个更清晰的直观认识。（效果图见代码后）
### 1.2 适用情况
 - 正负值同类比较，即在该系统中，变量的数据值有正有负，正负展现变量值的大小。例如温度、水位等。这种情况下对比条形图有利于展示负值信息，对比正负变化。
 - 正负值并列比较，即在该系统中，变量的正负代表了相反的意义，例如经营的盈亏、人员的增减等。这种情况下对比条形图展示数据具体含义，并且便于分析数据直接关系，例如盈亏数据可以得出净收入。
## 2. 软件实现
### 2.1 Matlab
#### Draw picture
```
x = (1:1:8);
y = [12 -8 5 2 -10 6 -3 9; 6 7 -2 -5 14 -9 -2 8];
b = barh(x, y, 1); set(b, 'edgecolor', 'none');
hold on
legend('Tip1', 'Tip2', 'Location','northoutside','Orientation','horizontal', 'Edgecolor', 'none')
b(1).FaceColor = '#EDB120';
b(2).FaceColor = '#4DBEEE';
xlim([-13 17]);
```
#### Add label
```
xlabel('X(m)'); ylabel('Y(m)');
xtips1 = b(1).YEndPoints;
for i = 1:8
    if xtips1(i) > 0 
        xtips1(i) =  xtips1(i) + 0.3;
    else 
        xtips1(i) = xtips1(i) - 2;
    end
end
ytips1 = b(1).XEndPoints;
labels1 = string(b(1).YData);
text(xtips1,ytips1,labels1,'VerticalAlignment','middle', 'FontSize', 9)
xtips2 = b(2).YEndPoints;
for i = 1:8
    if xtips2(i) > 0 
        xtips2(i) =  xtips2(i) + 0.3;
    else 
        xtips2(i) = xtips2(i) - 2;
    end
end
ytips2 = b(2).XEndPoints;
labels2 = string(b(2).YData);
text(xtips2,ytips2,labels2,'VerticalAlignment','middle', 'FontSize', 9)
```

<img src="https://github.com/Jzyz-Q/MCM-bar/blob/main/picture/bar1.png?raw=true" width="400px">   

### 2.2 Python
```
import matplotlib.pyplot as plt
import numpy as np

size = 5
x = np.arange(size)
a = np.random.random(size)
b = np.random.random(size)
c = np.random.random(size)

plt.subplot(1, 2, 1)
plt.barh(x, a)
plt.barh(x, -b)
plt.subplot(1, 2, 2)
ax = plt.gca()
ax.barh(x, a)
ax.barh(x, -b)
ax.spines['top'].set_color('none')
ax.spines['right'].set_color('none')
ax.spines['left'].set_position(('data', 0))
ax.spines['bottom'].set_position(('data', 0))
plt.show()
```
<img src="https://github.com/Jzyz-Q/MCM-bar/blob/main/picture/bar2.png?raw=true" width="400px">
    
