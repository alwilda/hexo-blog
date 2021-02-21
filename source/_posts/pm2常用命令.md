---
title: pm2常用命令
author: kinglyq
tags:
categories: []
date: 2019-09-11 23:32:04
---
# 一 PM2常用命令

假设你现在已经写好了一个app.js的文件，需要启动，你可以使用pm2进行管理

## (一) 启动
```shell
# pm2 start app.js
# pm2 start app.js --name my-api   # my-api为PM2进程名称
# pm2 start app.js -i 0            # 根据CPU核数启动进程个数
# pm2 start app.js --watch         # 实时监控app.js的方式启动，当app.js文件有变动时，pm2会自动 reload
```

<!--more-->

## (二) 查看进程
```shell
# pm2 list
# pm2 show 0 或者 # pm2 info 0  # 查看进程详细信息，0为PM2进程id
```

## (三) 监控
```shell
# pm2 monit
```

## (四) 停止
```shell
# pm2 stop all  # 停止PM2列表中所有的进程
# pm2 stop 0    # 停止PM2列表中进程为0的进程
```

## (五) 重载
```shell
# pm2 reload all    # 重载PM2列表中所有的进程
# pm2 reload 0      # 重载PM2列表中进程为0的进程
```

## (六) 重启
```shell
# pm2 restart all     # 重启PM2列表中所有的进程
# pm2 restart 0       # 重启PM2列表中进程为0的进程
```

## (七) 删除PM2进程
```shell
# pm2 delete 0     # 删除PM2列表中进程为0的进程
# pm2 delete all   # 删除PM2列表中所有的进程
```

## (八) 日志操作
```shell
# pm2 logs [--raw]       # Display all processes logs in streaming
# pm2 flush              # Empty all log file
# pm2 reloadLogs         # eload all logs
```

## (九) 升级PM2
```shell
# npm install pm2@lastest -g      # 安装最新的PM2版本
# pm2 updatePM2                   # 升级pm2
```

## (一) 更多命令参数请查看帮助
```shell
# pm2 --help
```

# 二 PM2目录结构

默认的目录是：当前用于的家目录下的.pm2目录（此目录可以自定义，请参考：五、自定义启动文件），详细信息如下：

$HOME/.pm2                   #will contain all PM2 related files
$HOME/.pm2/logs           #will contain all applications logs
$HOME/.pm2/pids           #will contain all applications pids
$HOME/.pm2/pm2.log    #PM2 logs
$HOME/.pm2/pm2.pid    #PM2 pid
$HOME/.pm2/rpc.sock    #Socket file for remote commands
$HOME/.pm2/pub.sock   #Socket file for publishable events
$HOME/.pm2/conf.js       #PM2 Configuration

# 三 自定义启动文件

1. 创建一个test.json的示例文件，格式如下：
```json
{
  "apps":
    {
      "name": "test",
      "cwd": "/data/wwwroot/nodejs",
      "script": "./test.sh",
      "exec_interpreter": "bash",
      "min_uptime": "60s",
      "max_restarts": 30,
      "exec_mode" : "cluster_mode",
      "error_file" : "./test-err.log",
      "out_file": "./test-out.log",
      "pid_file": "./test.pid"
      "watch": false
    }
}
```

- 说明：

1. apps：json结构，apps是一个数组，每一个数组成员就是对应一个pm2中运行的应用

2. name：应用程序的名称

3. cwd：应用程序所在的目录

4. script：应用程序的脚本路径

5. exec_interpreter：应用程序的脚本类型，这里使用的shell，默认是nodejs

6. min_uptime：最小运行时间，这里设置的是60s即如果应用程序在60s内退出，pm2会认为程序异常退出，此时触发重启max_restarts设置数量

7. max_restarts：设置应用程序异常退出重启的次数，默认15次（从0开始计数）

8. exec_mode：应用程序启动模式，这里设置的是cluster_mode（集群），默认是fork

9. error_file：自定义应用程序的错误日志文件

10. out_file：自定义应用程序日志文件

11. pid_file：自定义应用程序的pid文件

12. watch：是否启用监控模式，默认是false。如果设置成true，当应用程序变动时，pm2会自动重载。这里也可以设置你要监控的文件。

详细参数列表：见附件八

# 四 实例

已上面的test.json为例
```shell
# cat > /data/wwwroot/nodejs/test.sh << EOF
#!/bin/bash
while :
do
    echo "Test" >> 1.log
    sleep 5
done
EOF
```

```shell
# chmod +x test.sh      #添加执行权限
# pm2 start test.json    #启动，如下图：
```

1. \# pm2 list    #查看pm2进程，如下图：


# 五 备注

- 其他可参数见官网：http://pm2.keymetrics.io

# 六 附件

Field | Type | Example | Description  
-|-|-|-
name | string | "myAPI" | name your app will have in PM2 
script |	string |	"bin/app.js" |	path of your app
args | list |	["--enable-logs", "-n", "15"]	| arguments given to your app when it is launched
node_args |	list | ["--harmony", "--max-stack-size=1024"] |	arguments given to node when it is launched
cwd |	string |	"/var/www/app/prod" |	the directory from which your app will be launched
exec_mode |	string |	"cluster" |	"fork" mode is used by default, "cluster" mode can be configured with instances field
instances |	number | 4 | number of instances for your clustered app, 0 means as much instances as you have CPU cores. a negative value means CPU cores - value (e.g -1 on a 4 cores machine will spawn 3 instances)
exec_interpreter |	string |	"node" |	defaults to "node". can be "python", "ruby", "bash" or whatever interpreter you wish to use. "none" will execute your app as a binary executable
log_date_format |	string |	"YYYY-MM-DD HH:mm Z" |	format in which timestamps will be displayed in the logs
error_file |	string |	"/var/log/node-app/node-app.stderr.log" |	path to the specified error log file. PM2 generates one by default if not specified and you can find it by typing pm2 desc &lt;app id&gt; 
out_file |	string |	"/var/log/node-app/node-app.stdout.log" | path to the specified output log file. PM2 generates one by default if not specified and you can find it by typing pm2 desc &lt;app id&gt; 
pid_file |	string |	"pids/node-geo-api.pid" |	path to the specified pid file. PM2 generates one by default if not specified and you can find it by typing pm2 desc &lt;app id&gt; 
merge_logs | boolean |	false |	defaults to false. if true, it will merge logs from all instances of the same app into the same file
cron_restart |	string |	"1 0 * * *" |	a cron pattern to restart your app. only works in "cluster" mode for now. soon to be avaible in "fork" mode as well
watch |	boolean |	true |	enables the watch feature, defaults to "false". if true, it will restart your app everytime a file change is detected on the folder or subfolder of your app.
ignore_watch |	list |	["[\\/\\\\ &#93;\\./", "node_modules"] |	list of regex to ignore some file or folder names by the watch feature
min_uptime |	number |	1000 |	min uptime of the app to be considered started (i.e. if the app crashes in this time frame, the app will only be restarted the number set in max_restarts (default 15), after that it's errored)
max_restarts | number | 10 | number of consecutive unstable restarts (less than 1sec interval or custom time via min_uptime) before your app is considered errored and stop being
max_memory_restart | string	| "150M" | your app will be restarted by PM2 if it exceeds the amount of memory specified. human-friendly format : it can be "10M", "100K", "2G" and so on...
env |	object | {"NODE_ENV": "production", "ID": "42"} | env variables which will appear in your app
autorestart |	boolean |	false |	true by default. if false, PM2 will not restart your app if it crashes or ends peacefully
vizion |	boolean |	false	| true by default. if false, PM2 will start without vizion features (versioning control metadatas)
post_update |	list | ["npm install", "echo launching the app"] | a list of commands which will be executed after you perform a Pull/Upgrade operation from Keymetrics dashboard
force |	boolean |	true | defaults to false. if true, you can start the same script several times which is usually not allowed by PM2
next_gen_js |	boolean |	true | defaults to false. if true, PM2 will launch your app using embedded BabelJS features which means you can run ES6/ES7 javascript code
restart_delay |	number | 4000 | time to wait before restarting a crashed app (in milliseconds). defaults to 0.

