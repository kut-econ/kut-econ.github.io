# 第10回　Pandas入門

## matplotlibの日本語化

matplotlibのグラフで日本語を使うには、フォントを変更する必要があります。

```python
# MS ゴシックに変更
import matplotlib
matplotlib.rcParams['font.family'] = 'MS gothic'
```

```python
import matplotlib
# MS 明朝に変更
matplotlib.rcParams['font.family'] = 'MS mincho'
```
