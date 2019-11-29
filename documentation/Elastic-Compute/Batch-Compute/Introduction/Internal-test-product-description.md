# 1 产品简介
## 1.1 产品概述
批量计算（BatchCompute）是一种适用于大规模并行批处理作业的分布式云服务。支持海量任务自动调度，资源管理和数据加载，并按实际使用量计费。
## 1.2 产品架构

 **产品入口：** 控制台、SDK、API。

**运行环境：** 云主机，用户可采用batch基础镜像或私有镜像方式创建运行环境，支持Windows\Linux系统，用户程序运行在私有网络中。

**持久化存储：** 输入输出数据的持久化存储采用对象存储OSS或云文件服务CFS（Linux系统使用CFS或OSS，Windows系统使用CFS）。

 ![产品架构](https://github.com/jdcloudcom/cn/blob/batch1125/image/Elastic-Compute/Batch-Compute/Architecture.png)
 


## 1.3 核心概念
**作业（Job）：** 用户提交batch工作的最小单位，作业由单个或多个由前后依赖关系的任务组成，通过DAG（有向无环图）为多个任务设置依赖关系，共同组成一个作业，依赖关系在作业提交时指定，不可修改。作业之间可指定优先级顺序。

**任务（Task）：** 任务（Task）是作业的基本组成单位，包含了实际在一台云主机上执行的应用程序的相关信息。

**实例：** 调度执行最小单元。一个任务包含一个或多个任务实例，一个任务实例运行在一台云主机上，同一任务的各个实例并行处理各自的输入数据。

**计算环境：** 由单台或多台云主机实例组成的计算集群。当任务配置指定了计算环境，任务实例会调度到指定计算环境的节点上执行；当没有指定计算环境时，Batch 会创建云主机实例用于执行任务实例，并默认在任务实例完成后销毁云主机实例。

**镜像：** 任务运行环境的模板。是一个基础的batch镜像或用户私有镜像（包括batch agent）。

**任务模板：** 将常用的任务制作成任务模板，基于任务模板定制不同的任务，实现作业的快速提交。

## 1.4 产品优势

| 优势     | 批量计算                                                     | 自建计算集群                                                 |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 海量并发 | 依托京东云云主机海量计算资源，保证业务快速稳定执行。         | 海量计算资源的创建及维护需要巨额成本。                       |
| 易用安全 | 除计算环境外，批量计算还提供丰富的执行方法、多任务计算编排、日志及状态监控等，帮助用户在100% 网络逻辑隔离的私有网络中创建海量并发计算任务，快速安全执行。 | 自行开发批处理系统或依赖第三方工具，并自行进行集群安全建设。 |
| 成本优化 | 按需调用云主机资源，只需为您使用的计算及存储资源付费。       | 自建海量计算的大规模集群，资源及人力成本高，周期长 。        |
| 弹性伸缩 | 根据作业需求动态分配计算资源，任务完成即可释放。             | 需要自行预测计算量及所需的计算资源自建集群，容易造成计算量不足或闲置浪费。 |
| 完全托管 | 资源调度和流程调度全托管，用户只需定义并提交作业，即可查看分析运行结果。 | 手动或自行开发软件处理资源调度和流程调度，面对海量计算，投入大量精力和资源。 |


## 1.5 产品功能

### 1.5.1 运行作业

**提交作业**

batch使用云文件服务CFS和对象存储OSS作为用户数据输入和输出的持久化存存储，您可以根据计算环境的运行系统自行选择，Linux系统请任意选择CFS或OSS作为数据的输入和输出，Windows系统请使用CFS作为数据的输入和输出。

batch使用对象存储OSS存储任务日志，包括标准日志和错误日志。

batch默认运行在云主机中，用户可将执行程序包置于对象存储OSS、云文件服务CFS或云硬盘中，此外，也可将执行程序安装在私有镜像中。

**管理作业**

用户可以通过控制台，查看已提交作业的运行情况，包括其中各任务的运行情况，任务中各实例的运行情况及日志，此外，还可对作业进行停止、重启或删除。



### 1.5.2 计算环境

若用户选用自动计算环境则启动任务运行作业时，每次均需要新启动云主机，会占用一定的时间（一般几分钟左右），如遇资源紧张时可能无法即可申请到资源，您提交作业后可能需要等待一段时间才能运行。自动计算环境的好处是，即用即启动，结束即刻销毁，节约成本，使用灵活。

若您想要提高运行效率，可以先创建好计算环境，指定需要的云主机数量和镜像ID，Batch会为您分配好机器并启动，这些机器会一直处于运行状态，一旦您提交作业上来，就可以直接运行，效率较高。


### 1.5.3 镜像
用户提交作业或者创建集群时，可以使用批量计算官方提供的镜像，也可以使用私有镜像。私有镜像的好处是，可以自己安装需要的软件。


## 1.6 限制说明

| 限制类型 | 限额钟类                     | 限额                                 |
| -------- | ---------------------------- | ------------------------------------ |
| 计算环境 | 单用户最大计算环境数         | 10                                   |
|          | 单计算环境最大实例数         | 5000                                 |
|          | 单用户单地域最大并发实例数   | 20（云主机配额，如需提升请提交工单） |
| 作业     | 单用户最大作业数             | 100                                  |
|          | 单用户单作业最大任务数       | 10                                   |
|          | 单用户单地域单任务最大实例数 | 100                                  |



## 1.7 应用场景

**基因检测：** 调动海量计算资源快速完成基因大数据的处理；

**视频渲染：** 海量资源管理，计算任务调度，TB级数据在大量节点之间共享和并发访问；

**深度学习：** 适用于部署基于TensorFlow、Caffe、MXNet等框架的深度学习算法的离线批处理训练任务；

**金融服务：** 交易后分析，自动分析每天的交易费用、执行报告和市场绩效；

**生命科学：** 生物制药的药物筛选，快速地在小分子库中搜索以发现新药。


# 2 产品定价

批量计算服务本身完全免费。

批量计算调度作业过程中会根据用户配置的计算（云主机按配置计费）、存储（对象存储OSS、云文件服务CFS按量计费）资源，在对应产品线收取相应费用。


# 3 入门指南

## 3.1 控制台快速开始

本文介绍如何使用批量计算控制台提交一个作业，具体操作步骤如下。

### Step 1 作业准备

1.上传数据文件到存储服务，若您的业务基于Linux系统，您可以选择对象存储OSS或云文件服务CFS作为数据文件持久化存储；若您的业务是基于Windows系统，请选择云文件服务CFS作为数据文件持久化存储。

2.上传任务程序到对象存储OSS，或考虑将任务程序安装至私有镜像。

3.（可选） 创建对象存储bucket，用于存储任务运行的标准日志和错误日志。

### Step 2 创建任务模板

1. 进入批量计算控制台，单击左侧导航栏“任务模板”，选择“新建任务模板”。

2. 配置基本信息：

区域（默认）：华北-北京

任务模板名称：batch-hello

计算环境类型： 选择自动计算环境（也可选择已创建的计算环境，详情请参考计算环境）
             
   * 可用区（默认）：可用区A
   
   * 计费类型（默认）：按需
   
   * 实例规格：g.n2.medium（1核4GB）
  
   * 镜像：官方镜像 -- Batch-CentOS-6.9
  
   * 磁盘存储：系统盘--容量型HDD--40GB
  
   * 私有网络：BATCH_VPC_TEST--子网 BATCH_SUBNET_TEST

资源数量（默认）：1

超时时间（默认）：0 秒

重试次数（默认）：0

![newtemplate1](https://github.com/jdcloudcom/cn/blob/batch1125/image/Elastic-Compute/Batch-Compute/newtasktemplate.PNG)       
           
3. 配置程序运行配置

执行方式：package（程序包存储于对象存储OSS中，将hello.py文件打包为.zip文件上传至对象存储OSS相应bucket中）

程序包地址：oss://batch-input-1/gx-test/hello.zip

Stdout日志（可选）：oss://batch-input-1/gx-test/batch-hello-stderr/

Stderr日志（可选）：oss://batch-input-1/gx-test/batch-hello-stdout/

程序运行命令：python hello.py

![newtemplate2](https://github.com/jdcloudcom/cn/blob/batch1125/image/Elastic-Compute/Batch-Compute/newtasktemplate2.PNG)     

3. 环境变量（可选）

不配置环境变量，下一步

![newtemplate3](https://github.com/jdcloudcom/cn/blob/batch1125/image/Elastic-Compute/Batch-Compute/newtasktemplate3.PNG)  

4. 预览任务JSON文件，确认无误后，单击“完成”

![newtemplate4](https://github.com/jdcloudcom/cn/blob/batch1125/image/Elastic-Compute/Batch-Compute/newtasktemplate4.PNG)  

5. 查看任务模板

![tasklist](https://github.com/jdcloudcom/cn/blob/batch1125/image/Elastic-Compute/Batch-Compute/tasklist.PNG) 

### step 3：提交作业

1. 单击左侧导航栏“作业”，选择“新建作业”。

2. 配置作业信息

作业名称：helloworld

优先级：0

![newjob1](https://github.com/jdcloudcom/cn/blob/batch1125/image/Elastic-Compute/Batch-Compute/newjob1.PNG) 

3. 在下方画布左侧选择配置好的任务模板--“batch-hello”，选中拖至画布中。

![newjob2](https://github.com/jdcloudcom/cn/blob/batch1125/image/Elastic-Compute/Batch-Compute/newjob2.jpg) 

4.  双击画布中的任务模板，可在右侧弹出框中修改任务属性，单击“确认”保存修改（此修改只针对当前作业中任务属性，不会修改对应任务模板）。

![newjob3](https://github.com/jdcloudcom/cn/blob/batch1125/image/Elastic-Compute/Batch-Compute/newjob3.PNG) 

5. 确认无误后，单击“完成”。


### step 4：查询结果

在作业列表页，您可以查询作业运行状态及结果。

![jodlist](https://github.com/jdcloudcom/cn/blob/batch1125/image/Elastic-Compute/Batch-Compute/joblist.PNG) 

单击作业名称，进入“作业详情”页，在“任务运行情况”tab页可查看任务运行状态。

![jodtask](https://github.com/jdcloudcom/cn/blob/batch1125/image/Elastic-Compute/Batch-Compute/jobtask.PNG) 

在列表或画布中单击任务名称，进入“任务详情”页，在下方可查询任务中每个实例的运行情况。

![taskinstance](https://github.com/jdcloudcom/cn/blob/batch1125/image/Elastic-Compute/Batch-Compute/taskinstance.PNG) 

单击实例列表右侧“查看日志”，可查看单个实例标准日志和错误日志。

![log](https://github.com/jdcloudcom/cn/blob/batch1125/image/Elastic-Compute/Batch-Compute/log.PNG) 

### step 5：完成

以上，完成简单batch的作业执行，在此基础上，您可以：


**挂载数据存储：** 您可以为云主机添加数据盘，直接从数据盘中读取写入数据，或挂载对象存储OSS、云文件服务CFS至VM，存储访问简化为本地文件系统操作。

**执行业务程序：** 除了将代码包存储于对象存储bucket中，您还可以将程序包打包在私有镜像中，通过使用私有镜像执行代码。

**创建计算环境：** 若您需要提高作业的执行效率，可预先创建计算环境，随时可被调用。



# 4 操作指南

## 4.1 准备阶段

### 4.1.1 镜像

batch使用用户定的镜像来启动云主机实例。为了方便计算环境管理和运行状态收集，批量计算提供了预置agent的官方基础镜像。您可以直接使用这些基础镜像，也可以通过在batch的基础镜像内安装业务所需的软件制作私有镜像。

**batch镜像使用要求：**

* 镜像为batch提供的官方基础镜像；

* 镜像为基于batch官方基础镜像制作并完成的私有镜像。

否则计算环境会创建失败。

内测期间，batch官方镜像还未在云市场上架，创建计算环境镜像请参考以下：

1. 使用batch官方镜像：您可以在batch控制台，直接选择官方镜像中batch镜像创建计算环境。

batch官方基础镜像包括以下镜像ID：

* img-ektu820ft6  （Batch-Windows-Server2012）
* img-oywmjbtsoo  （Batch-CentOS-7.6）
* img-1s4quv73zl  （Batch-CentOS-6.9）

2. 创建私有镜像：

step1：创建batch计算环境实例

请先在batch控制台--“计算环境”中使用batch官方镜像创建一个计算环境

* 期望实例数为1

* 实例规格建议至少4核8GB

* 系统盘根据用户业务软件大小选择

step2：安装业务软件

实例创建成功后，请至云主机控制台，重置密码并重启实例。待实例处于运行状态后，可远程登陆实例进行安装，包括用于渲染的3DMax、X-ray、Maya软件，或用于基因数据分析工具等。

step3：创建私有镜像

您的业务软件安装完毕后，在云主机控制台对运行实例进行停止操作，对“已停止”状态的实例制作私有镜像。

详情可参考 [制作私有镜像](https://docs.jdcloud.com/cn/virtual-machines/create-private-image)。

step4：镜像验证

私有镜像制作完成后，以该镜像创建一个云主机实例，实例成功启动后进行远程连接，登录后请自行证以下两项内容：

* 安装的业务软件是否能正常运行。

* 若您选择Linux系统运行，请在根目录下检查/batch/文件夹中batch-agent、start_agent.sh文件是否存在；若您选择Window系统运行，请在c:\batch\目录下检查batch-agent.exe、start_agent.cmd文件是否存在。

以上，完成batch私有镜像的创建，创建成功后即可在batch控制台创建计算环境--私有镜像中选择创建。



### 4.1.2 网络

batch计算环境只支持创建在用户VPC中，如您选择云文件服务CFS作为持久化存储，请在创建CFS时与计算环境云主机在同一VPC中。

### 4.1.3 挂载磁盘

批量计算的计算环境中系统盘和数据盘均使用云盘创建。

您在创建计算环境时，若有较大本地数据需求，建议挂载数据盘。挂载数据盘后，对挂载目录中的数据读写与本地读写完全相同。

盘挂载至实例后将作为实例的一个设备被系统识别，以设备名进行区分不同磁盘，随后经过分区、格式化、实例内挂载（Linux配置挂载点，Windows分配盘符）等操作来实现磁盘在系统内的正确配置和使用。

Linux系统和Windows系统对设备的命名方式虽然不同，但是具有相同的顺序索引规则（见下表），详情可参见 [制作私有镜像](https://docs.jdcloud.com/cn/virtual-machines/assign-device-name)。

|              | 控制台显示          | Linux系统显示       | Windows系统显示 |
| ------------ | ------------------- | ------------------- | --------------- |
| 数据盘设备名 | /dev/vdb - /dev/vdm | /dev/vdb - /dev/vdm | 磁盘1-磁盘12    |


### 4.1.4 挂载云文件服务CFS

用户数据可选择存储于云文件服务CFS，以下简称“CFS”。创建batch计算环境或任务模板前，请先在CFS控制台[创建文件存储](https://docs.jdcloud.com/cn/cloud-file-service/creating-file-system)。

**说明：

* 网络：CFS与计算环境实例必须创建在同一VPC中；

* 挂载CFS支持读写；

* 挂载格式：同时指定源地址和目的地址，以CFS输入数据挂载为例：
 
   源地址格式以cfs://为前缀，后面加上cfs共享地址，例如：cfs://10.0.0.30
   
   目的地址格式根据计算环境运行环境：
  
   Windows系统目的地址格式示例： /home/subpath/ 
  
   Linux系统目的地址格式示例： D：
  

3DMAX用户请注意：  

因京东云CFS中的所有锁定都是建议性锁定，因此使用3Dmax进行渲染的用户在使用CFS时，需要CFS在后端进行单独的适配才能够支持3Dmax的使用。同时，该适配会对CFS的读写性能造成一定影响。使用3Dmax的用户可[提交工单](https://ticket.jdcloud.com/applyorder/applyportal)，提供文件存储ID后，申请对CFS进行3Dmax使用适配。

### 4.1.5 挂载OSS



### 4.1.6 环境变量

## 4.2 计算环境管理

## 4.3 任务模板管理

## 4.4 作业管理

## 4.5 运维监控