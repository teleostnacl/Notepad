``` shell
# 获取顶层Activity
dumpsys activity | grep "mResumedActivity"

# 获取顶层Window
dumpsys window | grep 'mCurrentFocus' 
```