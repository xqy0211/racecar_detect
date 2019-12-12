# racecar_detect
本功能包为ROS下的功能包，主要节点为detect_lane，通过名为detect_lane.launch的launch文件启动节点
## 实现功能
主要用于单目车道线检测，是在获取透视变换图像后，由detect_lane.py实现对图像进行处理，以得到车道线方程和图像信息。
<br>程序中主要定义了cbFindLane()，maskRightLane()，maskLeftLane()，fit_from_lines()，sliding_windown()和make_lane()的主要函数
## 参数
subscribe:  透视变换后的车道图/camera/image_projected_compensated<br>
publish:  中心车道线/detect/lane、右车道线/detect/image_right_lane_marker和左车道线/detect/image_left_lane_marker
## 具体说明
当启动车道检测launch文件后，调用detect_lane.py对应节点，在节点订阅了/camera/image_projected_compensated话题后，调用cbFindLane()回调函数。回调函数中调用了提取车道线的两个函数maskRightLane()和maskLeftLane()，处理出左右车道线后返回给fit_from_lines()和sliding_windown()用于拟合车道线方程。最后，通过make_lane()函数将中心线画在原图上，从而完成车道检测部分，发布中心车道线/detect/lane、右车道线/detect/image_right_lane_marker和左车道线/detect/image_left_lane_marker等消息。
<br>车道检测结果如下，均为rqt订阅图像消息的效果
<br>以下为直道检测效果图
![cannot show](https://github.com/xqy0211/racecar_detect/blob/master/%E8%BD%A6%E9%81%93%E7%BA%BF%E6%A3%80%E6%B5%8B%E7%9B%B4%E9%81%93.png)
<br>以下为弯道检测效果图
![cannot show](https://github.com/xqy0211/racecar_detect/blob/master/%E8%BD%A6%E9%81%93%E7%BA%BF%E6%A3%80%E6%B5%8B%E5%BC%AF%E9%81%93.jpg)
