# Route Configuration

This repository is a lab for NCTU course "Introduction to Computer Networks 2018".

---
## Abstract

In this lab, we are going to write a Python program with Ryu SDN framework to build a simple software-defined network and compare the different between two forwarding rules.

---
## Objectives

1. Learn how to build a simple software-defined networking with Ryu SDN framework
2. Learn how to add forwarding rule into each OpenFlow switch

---
## Execution

> TODO:
> * How to run your program?
> * What is the meaning of the executing command (both Mininet and Ryu controller)?
> * Show the screenshot of using iPerf command in Mininet (both `SimpleController.py` and `controller.py`)  

1. How to run my program?  
   1) Run topology with SimpleController.py  
      * 先在一個terminal中跑topo.py  
         `sudo mn --custom topo.py --topo topo --link tc --controller remote`
      * 開啟另一個termina跑SimpleController.py  
         `sudo ryu-manager SimpleController.py –-observe-links`
   2) Measure the bandwidth
      * 在 Mininet CLI 中用iperf指令測量bandwidth  
         `h1 iperf -s -u -i 1 –p 5566 > ./out/result1 &`  
         `h2 iperf -c 10.0.0.1 -u –i 1 –p 5566`  
   3) Run topology with controller.py  
      * 先在一個terminal中跑topo.py  
         `sudo mn --custom topo.py --topo topo --link tc --controller remote`
      * 開啟另一個termina跑controller.py  
         `sudo ryu-manager controller.py –-observe-links`
   4) Measure the bandwidth  
       * 在 Mininet CLI 中用iperf指令測量bandwidth  
         `h1 iperf -s -u -i 1 –p 5566 > ./out/result2 &`  
         `h2 iperf -c 10.0.0.1 -u –i 1 –p 5566` 
2. The meaning of the executing command
3. The screenshot
   * result1 (SimpleController)  
      ![SimpleController](https://github.com/nctucn/lab3-kuanchiehwu/blob/master/SimpleController%20result.png)
   * result2 (controller)  
      ![controller](https://github.com/nctucn/lab3-kuanchiehwu/blob/master/controller%20result.png)
   
---
## Description

### Tasks

> TODO:
> * Describe how you finish this work in detail

1. Environment Setup
   1) 加入GitHub Classroom，拿到Lab2的資料
   2) 用SSH指令進入container中(For MacOS)  
      `ssh -p 16206 root@140.13.195.69`  
      password:cn2018
   3) Clone your GitHub repository to “Route_Configuration”  
      `git clone https://github.com/nctucn/lab3-0616206.git Route_Configuration`  
   4) 確認root中有資料夾Route_Configuration  
      `ls /root/`
   5) 測試Mininet  
      * 如果出現error `You may wish to try "service openvswitch-switch start".`  
        用指令 `sudo service openvswitch-switch start` 來排除錯誤  
        再測試一次Mininet `sudo mn`
   6) 確認成功後就可以進行第二步   

2. Example of Ryu SDN
   1) 確認在src資料夾中
   2) 在第一個編譯器用 Mininet 跑 SimpleTopo.py  
      `sudo mn --custom SimpleTopo.py --topo topo --link tc --controller remote`  
      * 如果有錯誤可以試試看 `sudo mn -c`
      * 離開 Mininet CLI `exit`
      * 離開後要清除連線 `mn -c`
   3) 開一個新的terminal，進到/root/Route_Configuration/src/  
      用 Ryu manager 跑 SimpleController.py  
      `sudo ryu-manager SimpleController.py --observe-links`  
      * 離開 Mininet CLI 用 Ctrl+z
      * 離開後要清除 “RTNETLINK” `mn -c`

3. Mininet Topology
   1) 透過 Mininet 建 topology
      * 確認在src資料夾中
      * 複製範例程式 SimpleTopo.py 並命名為 topo.py  
         `cp SimpleTopo.py topo.py`
      * 在 topo.py 中照著 topo.png 中的敘述，在link之間加入bandwidth, delay 和 loss rate
         ![topo.png](https://github.com/nctucn/lab3-kuanchiehwu/blob/master/new_topo.jpg)
   2) Run Mininet topology and controller
      * 在第一個terminal中跑 topo.py  
         `sudo mn --custom topo.py --topo topo --link tc --controller remote`
      * 開啟另一個terminal跑 SimpleController.py  
         `sudo ryu-manager SimpleController.py --observe-links`  
      * 可以在Mininet’s CLI mode中ping每個link  
         `h1 ping h2` 可以測試h1和h2間的連接

4. Ryu Controller
   1) 在範例程式 SimpleController.py 中找到 `switch_features_handler(self, ev)`  
      修改裡面的程式
   2) 寫另一個 Ryu controller，修改路徑，從原本的s1->s3換走s1->s2->s3(來回都一樣路徑)  
      * 確認在src資料夾中
      * 複製範例程式 SimpleController.py 並命名為 controller.py  
         `cp SimpleController.py controller.py`
      * 修改 controller.py 中 switch 的傳送規則

5. Measurement
   1) Run topology with SimpleController.py
      * 先跑 topo.py  
         `sudo mn --custom topo.py --topo topo --link tc --controller remote`
      * 開另一個terminal跑 SimpleController,py  
         `sudo ryu-manager SimpleController.py --observe-links` 
   2) Measure the bandwidth  
      * 用下面的iPerf指令在 Mininet CLI 中來測量bandwidth  
         `h1 iperf -s -u -i 1 –p 5566 > ./out/result1 &`  
         `h2 iperf -c 10.0.0.1 -u –i 1 –p 5566`  
      * 確認結果後截圖，先退出 topo.py 再退出 SimpleController.py  
      * 確認“RTNETLINK”被清除  
         `mn -c`
   3) Run topology with controller.py
      * 先跑 topo.py  
         `sudo mn --custom topo.py --topo topo --link tc --controller remote`
      * 開另一個terminal跑 controller.py  
         `sudo ryu-manager controller.py --observe-links` 
   4) Measure the bandwidth
      * 用下面的iPerf指令在 Mininet CLI 中來測量bandwidth  
         `h1 iperf -s -u -i 1 –p 5566 > ./out/result2 &`  
         `h2 iperf -c 10.0.0.1 -u –i 1 –p 5566`
      * 確認結果後截圖，先退出 topo.py 再退出 controller.py 
      * 確認“RTNETLINK”被清除  
         `mn -c`

### Discussion

> TODO:
> * Answer the following questions

1. Describe the difference between packet-in and packet-out in detail.
   
2. What is “table-miss” in SDN?
   
3. Why is "`(app_manager.RyuApp)`" adding after the declaration of class in `controller.py`?
   
4. Explain the following code in `controller.py`.
    ```python
    @set_ev_cls(ofp_event.EventOFPPacketIn, CONFIG_DISPATCHER)
    ```

5. What is the meaning of “datapath” in `controller.py`?
   
6. Why need to set "`ip_proto=17`" in the flow entry?
   
7. Compare the differences between the iPerf results of `SimpleController.py` and `controller.py` in detail.
   
8. Which forwarding rule is better? Why?

---
## References

> TODO: 
> * Please add your references in the following

* **Reference**
    * [OpenFlow 通訊協定 - Ryubook 1.0 說明文件](https://osrg.github.io/ryu-book/zh_tw/html/openflow_protocol.html)
* **Ryu SDN**
    * [Ryubook Documentation](https://osrg.github.io/ryu-book/en/html/)
    * [Ryubook [PDF]](https://osrg.github.io/ryu-book/en/Ryubook.pdf)
    * [Ryu 4.30 Documentation](https://github.com/mininet/mininet/wiki/Introduction-to-Mininet)
    * [Ryu Controller Tutorial](http://sdnhub.org/tutorials/ryu/)
    * [OpenFlow 1.3 Switch Specification](https://www.opennetworking.org/wp-content/uploads/2014/10/openflow-spec-v1.3.0.pdf)
    * [Ryubook 說明文件](https://osrg.github.io/ryu-book/zh_tw/html/)
    * [GitHub - Ryu Controller 教學專案](https://github.com/OSE-Lab/Learning-SDN/blob/master/Controller/Ryu/README.md)
    * [Ryu SDN 指南 – Pengfei Ni](https://feisky.gitbooks.io/sdn/sdn/ryu.html)
    * [OpenFlow 通訊協定](https://osrg.github.io/ryu-book/zh_tw/html/openflow_protocol.html)
* **Python**
    * [Python 2.7.15 Standard Library](https://docs.python.org/2/library/index.html)
    * [Python Tutorial - Tutorialspoint](https://www.tutorialspoint.com/python/)
* **Others**
    * [Cheat Sheet of Markdown Syntax](https://www.markdownguide.org/cheat-sheet)
    * [Vim Tutorial – Tutorialspoint](https://www.tutorialspoint.com/vim/index.htm)
    * [鳥哥的 Linux 私房菜 – 第九章、vim 程式編輯器](http://linux.vbird.org/linux_basic/0310vi.php)

---
## Contributors

> TODO:
> * Please replace "`YOUR_NAME`" and "`YOUR_GITHUB_LINK`" into yours

* [吳冠潔](https://github.com/kuanchiehwu)
* [David Lu](https://github.com/yungshenglu)

---
## License

GNU GENERAL PUBLIC LICENSE Version 3
