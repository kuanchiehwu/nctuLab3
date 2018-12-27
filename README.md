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

---
## Description

### Tasks

> TODO:
> * Describe how you finish this work in detail

1. Environment Setup
   1) 加入GitHub Classroom，拿到Lab2的資料
   2) 用SSH指令進入資料夾(For MacOS)  
      `ssh -p 16206 root@140.13.195.69`  
      password:cn2018
   3) 用clone指令進到GitHub裡Lab3的資料庫Route_Configuration  
      登入GitHub  
   4) 確認root中有資料夾Route_Configuration
   5) 測試Mininet  
      * 如果有error `You may wish to try "service openvswitch-switch start".`  
      就用 `sudo service openvswitch-switch start` 指令來排除錯誤  
      在測試一次Mininet `sudo mn`
   6) 確認成功後就可以進行第二步   

2. Example of Ryu SDN
   1) 確認在src資料夾中
   2) 在第一個編譯器用 Mininet 跑 SimpleTopo.py  
      `sudo mn --custom SimpleTopo.py --topo topo --link tc --controller remote`  
      * 如果有錯誤可以試試看 `sudo mn -c`
      * 離開 Mininet CLI `exit`
      * 離開後要記得清除連線 `mn -c`
   3) 開一個新的terminal，進到/root/Route_Configuration/src/  
      用 Ryu manager 跑 SimpleController.py  
      `sudo ryu-manager SimpleController.py --observe-links`  
      * 離開 Mininet CLI 用 Ctrl+z
      * 離開後要記得清除連線 `mn -c`

3. Mininet Topology

4. Ryu Controller

5. Measurement

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
