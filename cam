#! /bin/sh
# Author:   Maple
# website:  http://blog.esazx.com
# Description: 给摄像头推流添加开关
NAME=USB Camera Stream
APP=ffmpeg
# 输出格式
OUTPUT=flv
# rtmp-nginx 设置的推流 application 名称
APPLICATION=app
# 自定义摄像头的推流后缀
NAMESPACE=cam

case "$1" in
    start)
        echo -n "Starting $NAME... "

        nohup nice -n 0 $APP -re -an -f v4l2 -input_format h264 -i /dev/video0 -c:v copy -strict experimental -avoid_negative_ts make_zero -f $OUTPUT rtmp://127.0.0.1:1935/$APPLICATION/$NAMESPACE

        if [ "$?" != 0 ] ; then
            echo " failed"
            exit 1
        else
            echo " done"
        fi
        ;;

    stop)
        echo -n "Stoping $NAME... "

        killall $APP

        if [ "$?" != 0 ] ; then
            echo " failed."
            exit 1
        else
            echo " done"
        fi
        ;;
    restart)
    $0 stop
    sleep 1
    $0 start
    ;;
    *)
        echo "Usage: $0 {start|stop|restart|}"
        exit 1
        ;;

esac


