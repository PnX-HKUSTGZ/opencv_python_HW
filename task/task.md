编写一个Python脚本，该脚本能够：
1.  **输入**: 读取一个指定的视频文件（例如 `input.mp4`）。
2.  **处理**: 在视频的每一帧中，实时识别出所有规则的物体，并且标注其中心以及对应的颜色
3.  **输出**: 将处理后的视频保存为 `output.mp4`。

注：

- 规则的物体可以是圆形、矩形，三角形等。相同颜色重叠的时候可以不用管，不同颜色重叠的时候只用管上面那个
- `cv2.circle` 可以画出圆圈
- `image = cv2.putText(img, text, org, fontFace, fontScale, color[, thickness[, lineType[, bottomLeftOrigin]]])` 可以绘制文本

```python
import cv2
import numpy as np

# --- 1. 创建一个黑色的画布 ---
# 创建一个 600x800，3通道的黑色图像
canvas = np.zeros((600, 800, 3), dtype=np.uint8)

# --- 2. 定义字体和文本 ---
text_to_draw = "Hello, RobotMaster!"

# --- 3. 绘制不同样式的文本 ---

# 样式1: 基础的SIMPLEX字体
font_simplex = cv2.FONT_HERSHEY_SIMPLEX
org_1 = (50, 100) # 左下角坐标
font_scale_1 = 1.5
color_1 = (0, 255, 0) # 绿色
thickness_1 = 2
cv2.putText(canvas, text_to_draw, org_1, font_simplex, font_scale_1, color_1, thickness_1)


# 样式2: 更大的、带抗锯齿的COMPLEX字体
font_complex = cv2.FONT_HERSHEY_COMPLEX
org_2 = (50, 200)
font_scale_2 = 2.0
color_2 = (255, 255, 0) # 青色
thickness_2 = 3
# 使用 cv2.LINE_AA 来获得平滑的字体
cv2.putText(canvas, text_to_draw, org_2, font_complex, font_scale_2, color_2, thickness_2, cv2.LINE_AA)


# 样式3: 结合变量动态生成文本
area = 12345.67
score = 98
dynamic_text = f"Area: {area:.2f}, Score: {score}" # 使用f-string格式化文本
org_3 = (50, 300)
font_plain = cv2.FONT_HERSHEY_PLAIN
font_scale_3 = 2.0
color_3 = (0, 0, 255) # 红色
cv2.putText(canvas, dynamic_text, org_3, font_plain, font_scale_3, color_3, 1, cv2.LINE_AA)


# --- 4. 解释 org 参数的位置 ---
# 我们在 (50, 400) 处画一个点
point_org = (50, 400)
cv2.circle(canvas, point_org, 5, (255, 255, 255), -1)
# 然后以这个点为 org 绘制文本，观察文本是如何从这个点的右上方展开的
cv2.putText(canvas, "'org' is at the bottom-left of the text baseline", point_org, cv2.FONT_HERSHEY_SIMPLEX, 0.7, (255, 255, 255), 1, cv2.LINE_AA)

# --- 5. 显示结果 ---
cv2.imshow('Text Drawing Demo', canvas)
cv2.waitKey(0)
cv2.destroyAllWindows()

```

提交方式：

在GitHub上fork这个仓库

克隆被fork的仓库，在`homework`目录下创建一个自己名字的文件夹，完成作业，并将处理后的结果放在里面，名字为 `res.mp4` 

然后向战队的仓库提交pr即可。