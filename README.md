# 关于这个项目
> 创建这个项目的原因是自己菜,经常记不住很多不常有的API,以及不常使用的方法,但是有时确非常的有用  
> 因此欢迎大家也在里面添加内容,一个人的力量是有限的,但是众人的力量确实不可估量的
# 开始进入正题
## 一.TV适配 
### 1. 判断是否是TV
- 1.通过UIModeManager
```
UIModeManager.getCurrentModeType() == Configuration.UI_MODE_TYPE_TELEVISION
```
