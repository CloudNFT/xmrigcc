# xmrigcc

sudo apt-get install git build-essential cmake libuv1-dev libmicrohttpd-dev libssl-dev zlib1g-dev g++-7 libhwloc-dev

git clone https://github.com/Bendr0id/xmrigCC.git
git clone https://github.com/xmrig/xmrig.git

mkdir xmrig/build

cd xmrig/build

cmake ..

cmake .. -DCMAKE_C_COMPILER=gcc-7 -DCMAKE_CXX_COMPILER=g++-7

make




# mkdir /etc/xmrigCC

# mkdir /var/log/xmrigCC

nano /var/log/xmrigCC/xmrigCC.log


nano /etc/xmrigCC/config.json
nano /etc/xmrigCC/config_cc.json

cp xmrig /usr/local/bin/xmrig

nano /etc/systemd/system/xmrigServer.service

[Unit]
Description=xmrig Server
After=network.target
[Service]
Type=forking
GuessMainPID=no
ExecStart=/usr/local/bin/xmrigServer -c /etc/xmrigCC/config_cc.json --syslog /var/log/xmrigCC/xmrigCC.log -B
Restart=always
User=root
[Install]
WantedBy=multi-user.target

nano /etc/systemd/system/xmrigDaemon.service

[Unit]
Description=Xmring Daemon
After=network.target
[Service]
Type=forking
GuessMainPID=no
ExecStart=/usr/local/bin/xmrigDaemon -c /etc/xmrigCC/config.json -l /var/log/xmrigCC/xmrigCC.log -B
Restart=always
User=root
[Install]
WantedBy=multi-user.target


systemctl daemon-reload
systemctl enable xmrigServer
systemctl enable xmrigDaemon
systemctl disable

service xmrigServer start
service xmrigDaemon start

service xmrigServer status
service xmrigDaemon status

