# ຕິດຕັ້ງ Loadbalancer ສຳລັບ master node
master node ແຕ່ລະໂຕຖືກອອກແບບໃຫ້ສາມາດເຮັດວຽກແຍກກັນໄດ້ຢ່າງອິດສະຫຼະ ຜູ້ໃຊ້ງານ Kubernetes Cluster ສາມາດເຊື່ອມຕໍ່ໄປໃຊ້ງານທີ່ master node ໂຕໃດກໍ່ໄດ້ ດັງນັ້ນເພື່ອໃຫ້ສະດວກກັບການເຊື່ອມຕໍ່ໄປຍັງ master node ຈຶ່ງນິຍົມໃຫ້ມີ loadbalancer ເຮັດໜ້າທີ່ຈັດການ loadbalancer ໄປຍັງ master node ແຕ່ລະໂຕ ເຊິ່ງຜູ້ຂຽນເລືອກໃຊ້ NGINX ມາເຮັດໜ້າທີ່ເປັນ loadbalancer

## ຂັ້ນຕອນການຕິດຕັ້ງ NGINX [loadbalancer node]
```
yum install -y nginx
echo " 
stream{
  upstream kubernetes {
      server 192.168.254.61:6443;
      server 192.168.254.62:6443;
      server 192.168.254.63:6443;
  }
  server {
      listen 6443;
      proxy_pass kubernetes;
  }
}
" >> /etc/nginx/nginx.conf
systemctl enable --now nginx
```
**Next>** [ຕິດຕັ້ງ Kubernetes Worker Nodes](10-install-worker-node.md)

**<Prev** [ຕິດຕັ້ງ Kubernetes Control Plane](08-install_kubernetes_control_plane.md)
