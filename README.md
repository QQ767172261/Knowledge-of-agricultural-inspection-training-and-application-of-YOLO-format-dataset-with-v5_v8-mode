蘑菇数据集(有v5/v8模型)/YOLO蘑菇检测」
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/f007b4f87c6d4704ad31e09d239a6f7f.png)


【说明】
图片数量9266张，已标注txt格式
训练集验证集按7234:2032划分，可直接用于目标检测训练
有yolov5-v7.0训练好的模型结果(如图4、训练100轮、预训练模型yolov5s.pt、map0.950)
有yolov8训练好的模型结果(如图5、训练100轮、预训练模型yolov8n.pt、map0.951)


【类别】
①Amanita citrina(黄毒蝇鹅膏菌)
②Gyromitra infula(鞍形鹿花菌)
③Hygrophoropsis aurantiaca(橙黄蜡伞)
④Imleria badia(褐绒盖牛肝菌)
⑤Lactarius turpis(劣味乳菇)
⑥Boletus reticulatus(网纹牛肝菌)
⑦Suillus grevillei(厚环乳牛肝菌)
⑧Suillus luteus(乳牛肝菌)
⑨Amanita pantherina(豹斑毒鹅膏菌)
⑩Coltricia perennis(多年生集毛菌)
①①Amanita hemibapha(半红鹅膏菌)
①②Amanita javanica(爪哇鹅膏菌)
①③Amanita princeps(王子鹅膏菌)
①④Russula emetica(呕吐红菇)


# 蘑菇种类识别YOLO目标检测数据集（9266张+14分类+双版本训练代码）

## 一、数据集信息表格
| 项目 | 详情 |
|------|------|
| 数据集名称 | 蘑菇种类识别检测数据集 |
| 总图片数量 | 9266 张 |
| 标注格式 | YOLO 标准 TXT 格式 |
| 数据划分 | 训练集：7234 张<br>验证集：2032 张 |
| 类别数量 | 14 类（蘑菇细分类） |
| 支持模型 | YOLOv5、YOLOv8 |
| YOLOv5 效果 | yolov5s.pt / 100 轮 / mAP=0.950 |
| YOLOv8 效果 | yolov8n.pt / 100 轮 / mAP=0.951 |
| 适用任务 | 野生蘑菇识别、毒蘑菇预警、物种分类检测 |

---

## 二、14 类蘑菇类别清单
| 序号 | 类别名称 | 中文名称 |
|------|----------|----------|
| 0 | Amanita citrina | 黄毒蝇鹅膏菌 |
| 1 | Gyromitra infula | 鞍形鹿花菌 |
| 2 | Hygrophoropsis aurantiaca | 橙黄蜡伞 |
| 3 | Imleria badia | 褐绒盖牛肝菌 |
| 4 | Lactarius turpis | 劣味乳菇 |
| 5 | Boletus reticulatus | 网纹牛肝菌 |
| 6 | Suillus grevillei | 厚环乳牛肝菌 |
| 7 | Suillus luteus | 乳牛肝菌 |
| 8 | Amanita pantherina | 豹斑毒鹅膏菌 |
| 9 | Coltricia perennis | 多年生集毛菌 |
| 10 | Amanita hemibapha | 半红鹅膏菌 |
| 11 | Amanita javanica | 爪哇鹅膏菌 |
| 12 | Amanita princeps | 王子鹅膏菌 |
| 13 | Russula emetica | 呕吐红菇 |

---

## 三、数据集配置文件 `mushroom.yaml`
```yaml
train: ./images/train
val: ./images/val

nc: 14
names:
  0: Amanita citrina
  1: Gyromitra infula
  2: Hygrophoropsis aurantiaca
  3: Imleria badia
  4: Lactarius turpis
  5: Boletus reticulatus
  6: Suillus grevillei
  7: Suillus luteus
  8: Amanita pantherina
  9: Coltricia perennis
  10: Amanita hemibapha
  11: Amanita javanica
  12: Amanita princeps
  13: Russula emetica
```

---

## 四、YOLOv8 训练代码（直接运行）
```python
from ultralytics import YOLO

# 加载YOLOv8n模型
model = YOLO("yolov8n.pt")

# 开始训练
model.train(
    data="mushroom.yaml",
    epochs=100,
    imgsz=640,
    batch=16,
    device=0,
    patience=20,
    project="mushroom_detect",
    name="yolov8n_mushroom",
    save=True
)

# 验证模型
model.val()
```

---

## 五、YOLOv5 训练命令（一键训练）
```bash
python train.py --data mushroom.yaml --cfg yolov5s.yaml --weights yolov5s.pt --epochs 100 --batch 16 --img 640
```

---

## 六、环境安装
```bash
# YOLOv8 环境
pip install ultralytics

# YOLOv5 环境
git clone https://github.com/ultralytics/yolov5
cd yolov5
pip install -r requirements.txt
```

---


