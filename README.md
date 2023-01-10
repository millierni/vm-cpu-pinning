# Virtual Machine - CPU Pinning
## VIRTUAL MACHINE - CPU PINNING
- Find the topology for your CPU
  ```
  lscpu -e
  ```
  ```
  lstopo
  ```
- Edit your virtual machine config
  - Replace `win10` by your vm name
  ```
  sudo EDITOR=nano virsh edit win10
  ```
  - Add this below `<vcpu>...</vcpu>`  
    This is to isolate (8-core, 16-thread) of a (16-core, 32-thread) CPU using topology isolation
    ```
    <iothreads>1</iothreads>
    <cputune>
      <vcpupin vcpu='0' cpuset='0'/>
      <vcpupin vcpu='1' cpuset='16'/>
      <vcpupin vcpu='2' cpuset='1'/>
      <vcpupin vcpu='3' cpuset='17'/>
      <vcpupin vcpu='4' cpuset='2'/>
      <vcpupin vcpu='5' cpuset='18'/>
      <vcpupin vcpu='6' cpuset='3'/>
      <vcpupin vcpu='7' cpuset='19'/>
      <vcpupin vcpu='8' cpuset='4'/>
      <vcpupin vcpu='9' cpuset='20'/>
      <vcpupin vcpu='10' cpuset='5'/>
      <vcpupin vcpu='11' cpuset='21'/>
      <vcpupin vcpu='12' cpuset='6'/>
      <vcpupin vcpu='13' cpuset='22'/>
      <vcpupin vcpu='14' cpuset='7'/>
      <vcpupin vcpu='15' cpuset='23'/>
      <emulatorpin cpuset='0,16,1,17,2,18,3,19,4,20,5,21,6,22,7,23'/>
      <iothreadpin iothread='1' cpuset='0,16,1,17,2,18,3,19,4,20,5,21,6,22,7,23'/>
    </cputune>
    ```
  - Modify `<cpu mode='host-passthrough'>` to looks like this
    ```
    <cpu mode='host-passthrough'>
      <topology sockets='1' cores='8' threads='2'/>
    </cpu>
    ```
