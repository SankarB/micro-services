## upgrade control plane(master) 1.22-1.23.1
1) drain master node
 ```kubectl drain <master-node-name> --ignore-daemonsets --force```
2) apt-mark unhold kubeadm
3) apt-get install -y kubeadm=1.23.1-00
4) kubeadm upgrade plan--(which will give you major fix version on that release)
5) kubeadm upgrade plan v.1.23.1 (specific version what we need)
6) kubeadm upgrade plan apply v.1.23.1
7) apt-get upgrade
8) upgrade kubelet and kubectl(v.1.23.1)
apt-get install -y kubelet=1.23.1-00 kubectl=1.23.1-00
9) apt-mark hold kubelet kubectl kubeadm
10) restart kubelet: sudo systemctl daemon-reload & sudo systemctl restart kubelet

upgrade worker nodes
-------------------------------
1) drain worker node(execute from master) all objects will be scheduled to other worker nodes which are available
  ```kubectl drain <worker-node-name> --ignore-daemonsets --force```
# login to worker node and execute below steps
2) apt-mark unhold kubeadm
3) apt-get install -y kubeadm=1.23.1-00
4) apt-mark hold kubeadm
5) sudo kubeadm upgrade node
6) apt-mark unhold kubelet kubectl
7) apt-get update && apt-get install -y kubelet=1.23.1-00 kubectl=1.23.1-00
8) sudo systemctl daemon-reload && sudo systemctl restart kubelet

Repeat worker node steps for all the nodes available
