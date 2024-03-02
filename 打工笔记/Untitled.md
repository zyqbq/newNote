![image-20230813103120534](../../assests/image-20230813103120534.png)

### 如何实现移动

cub相机跟随点击的位置，根据点击的位置更替cub1到cub2

场景本身是一个粗糙的模型，cub相机在场景中不断的移动，更新cub的全景贴图，贴图有三种画质，由底到高依次加载

main函数

![image-20230829185939651](C:\Users\16665\AppData\Roaming\Typora\typora-user-images\image-20230829185939651.png)