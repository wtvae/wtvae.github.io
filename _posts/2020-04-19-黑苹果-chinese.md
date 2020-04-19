title: 解决opencore引导黑苹果关闭sip后无法使用hidpi的问题
layout: post
categories: 黑苹果
tags: hidpi 黑苹果 10.15.4 Catalina
excerpt: 介绍解决opencore引导黑苹果关闭sip后无法使用hidpi的问题

在用opencore升级Catalina10.15.4后，在config里添加了E7030000，进入恢复模式后关闭sip，使用hipdi仍然提示需要关闭sip

针对这个问题，只需要将hidpi.sh下载到本地，然后去除对sip的相关判断的代码删除即可

hidpi源码在GitHub[链接](https://github.com/xzhih/one-key-hidpi)
下载hidpi.sh到本地[链接](https://www.lanzous.com/ib62z1a)
右击选择打开方式为文本编辑，找到如下代码

*****

```
fi
downloadHost="https://raw.githubusercontent.com/xzhih/one-key-hidpi/master"
# downloadHost="https://raw.githubusercontent.com/xzhih/one-key-hidpi/dev"
# downloadHost="http://127.0.0.1:8080"

if [[ "${sipInfo}" == *"Filesystem Protections: disabled"* ]] || [[ "$(awk '{print $5}' <<< "${sipInfo}")" == "disabled." ]]; then
    :
else
    echo "${disableSIP}";
    exit 0
fi

if [[ "${systemVersion}" -ge "15" ]]; then
    sudo mount -uw / && killall Finder
```

![](images/截屏2020-04-09下午10.14.26.png)
然后**删除保存**，将hidpi拖入终端即可

### **已修改好的文件**[链接](https://www.lanzous.com/ib62z2b)
