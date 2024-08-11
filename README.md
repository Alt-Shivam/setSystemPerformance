# Get Started with paramaters affecting your system performace for different workloads

## RAN workloads
- Set CPU latency to minimum
```
echo 0 | sudo tee /dev/cpu_dma_latency
```
- To disable all CPU sleep states
```
sudo cpupower idle-set -D0
```
To revert back to original state of sleep state
```
sudo cpupower idle-set -E
```
Sometimes, dependencies might not be installed, in which case you should
install what cpupower asks you to install. Note that this is not persistent.
- Increase the ringbuffers to a maximum. Read on interface `<fronthaul-interface-name>`
using option -g, then set it with -G:
```
ethtool -g <fronthaul-interface-name>
ethtool -G <fronthaul-interface-name> rx <maximum-rx-value> tx <maixmum-tx-value>
```
-  increase the kernel's default and maximum read and write socket
buffer sizes to a high values, e.g., 134217728:
```
sudo sysctl -n -e -q -w net.core.rmem_default=134217728
sudo sysctl -n -e -q -w net.core.rmem_max=134217728
sudo sysctl -n -e -q -w net.core.wmem_default=134217728
sudo sysctl -n -e -q -w net.core.wmem_max=134217728
```
- Set MTU to max of your interfaces as per ORU device.
```
ip link set ens2f0 mtu 9000
```
- Activate real time profile
```
tuned-adm profile realtime
```
