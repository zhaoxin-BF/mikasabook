* [介绍](README.md)

# 脚本自动拉起服务

```
#!/usr/bin/env python2
# -*- coding:utf-8 -*-

import sys
import os
import time

def main(service_name):
    check_cmd = "ps aux|grep -w %s |grep -v grep|wc -l" % service_name
    if os.popen(check_cmd).readlines()[0] == "0\n":
	restart_cmd ="nohup %s >/dev/null 2>&1 &" % service_name
	if os.system(restart_cmd) == 0:
	    if os.popen(check_cmd).readlines()[0] == "0\n":
	        print "%s restart fail ......" % service_name
	    else:
		print "%s restart success ......"  % service_name
	else:
	    print "%s command runing error" % restart_cmd

if __name__ == "__main__":
    service_name = "./mikasa_ufs_api"
    while True:
        time.sleep(5)
	main(service_name)

```

