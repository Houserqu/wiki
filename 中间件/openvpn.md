sudo iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o eno1 -j MASQUERADE
sudo systemctl restart openvpn-server@openvpn-server.service

iptables -L -t nat

systemctl status  openvpn-server@server.service