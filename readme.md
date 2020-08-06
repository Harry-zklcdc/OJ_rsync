OJ rsync

~~~yaml
  oj-rsync-master:
    image: registry.cn-hangzhou.aliyuncs.com/wenjian_oj/oj-rsync
    container_name: oj-rsync-master
    volumes:
      - $PWD/data/backend/test_case:/test_case:ro
      - $PWD/rsync_master:/log
    environment:
      - RSYNC_MODE=master
      - RSYNC_USER=ojrsync
      - RSYNC_PASSWORD=CHANGE_THIS_PASSWORD
    ports:
      - "0.0.0.0:873:873"

  oj-rsync-slave:
    image: registry.cn-hangzhou.aliyuncs.com/wenjian_oj/oj-rsync
    container_name: oj-rsync-slave
    volumes:
      - $PWD/data/backend/test_case:/test_case
      - $PWD/rsync_slave:/log
    environment:
      - RSYNC_MODE=slave
      - RSYNC_USER=ojrsync
      - RSYNC_PASSWORD=CHANGE_THIS_PASSWORD
      - RSYNC_MASTER_ADDR=192.168.1.124
      - RSYNC_MASTER_PORT=873
~~~

`RSYNC_MASTER_PORT` 代表 master 服务暴露的端口