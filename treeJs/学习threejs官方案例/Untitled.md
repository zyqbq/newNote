## 多边形偏移polygon offset

- polygonOffset 是否开启多边形偏移
- polygonOffsetFactor 多边形偏移因子
- polygonOffsetUnits 多边形偏移单位

当两个面深度相同时，设置了polygonOffset 的会发生会向前或向后偏移一段距离，就能区分前后了

当`polygonOffsetFactor`和 `polygonOffsetUnits`的都是正值时，向远离相机的方向偏移

当两者都是负值时，向靠近相机的地方偏移

- 当面和近平面（near）、远平面（far）几乎平行的时候，一个很小的偏移就足够，你可以设置`polygonOffsetFactor=0`, `polygonOffsetUnits=1.0`
- 当面和近平面（near）、远平面（far）有一个明显的角度时，这时候就需要一个较大的偏移和一个较小但非零的偏移因子。这是因为要分开两个交叉的面要比分开两个重合的面要更大的偏移。你可以设置如`polygonOffsetFactor=0.75`, `polygonOffsetUnits=4.0`

参考：https://www.cnblogs.com/lst619247/p/9098845.html