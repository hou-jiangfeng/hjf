## 第一周技术预研报告

### 任务目标

* 学习使用github。使用个人笔记本电脑，在github注册账户，创建仓库，提交代码，修改代码，冲突解决等操作。

* 搭建个人开发环境。在个人笔记本电脑搭建开发环境。如python java 前端框架等。

*  学习理解单点登录、前后端分离、微服务等概念，并结合自身选择的开发语言，熟悉相关实现模块。

* 学习理解bpmn概念，学习使用camunda相关软件，搭建相关测试环境，并实现各类流程。

*  理解docker和容器，并尝试使用容器封装各自编写的微服务框架。

### 关于GitHub

1. 个人帐号：  hou-jiangfeng

2. 基本操作
   代码clone到本地：git clone +地址

   代码上传到仓库：

   git init 初始化git

   git status 查看增加、更改了什么文件

   git add . /git add +文件名  

   git commit -m ‘提交信息’把本地仓库暂存区的文件提交到本地仓库

   git push -u origin master 把本地仓库中的文件同步到远程仓库中

3. 冲突解决
   **原因及场景**
    情景一：多个分支代码合并到一个分支时；

   情景二：多个分支向同一个远端分支推送代码时；

   实际上，push操作即是将本地代码merge到远端库分支上。

   关于push和pull其实就分别是用本地分支合并到远程分支 和 将远程分支合并到本地分支所以这两个过程中也可能存在冲突。git的合并中产生冲突的具体情况：

   　　<1>两个分支中修改了同一个文件（不管什么地方）

   　　<2>两个分支中修改了同一个文件的名称

   两个分支中分别修改了不同文件中的部分，不会产生冲突，可以直接将两部分合并。

   **解决方法**

   情景一：在当前分支上，直接修改冲突代码--->add--->commit。

   情景二：在本地当前分支上，修改冲突代码--->add--->commit--->push

### 个人开发环境搭建

Python、java环境配置及各种模块已完成
vscode、ideal2018.1、sublime等编译工具已安装

### 单点登录

####  单点登录的相关概念

 	**单点登录定义**：单点登录（Single Sign On），简称为 SSO，是比较流行的企业业务整合的解决方案之一。SSO的定义是在多个应用系统中，用户只需要登录一次就可以访问所有相互信任的应用系统。

 	**现实中的应用场景**：百度旗下有很多的产品，比如百度贴吧、百度知道、百度文库等，只要登录百度账号，在任何一个地方都是已登录状态，不需要重新登录。

 	**主要实现的功能：**

 		1. 所有应用系统共享一个身份认证系统。

 		统一的认证系统是SSO的前提之一。认证系统的主要功能是将用户的登录信息和用户信息库相比较，对用户进行登录认证；认证成功后，认证系统应该生成统一的认证标志（ticket），返还给用户。另外，认证系统还应该对ticket进行效验，判断其有效性。

 		2. 所有应用系统能够识别和提取ticket信息

 		要实现SSO的功能，让用户只登录一次，就必须让应用系统能够识别已经登录过的用户。应用系统应该能对ticket进行识别和提取，通过与认证系统的通讯，能自动判断当前用户是否登录过，从而完成单点登录的功能。

 	**优缺点：**

 		1）提高用户的效率

 		用户不再被多次登录困扰，也不需要记住多个 ID 和密码。另外，用户忘记密码并求助于支持人员的情况也会减少。 

 		2）提高开发人员的效率

 		3）简化管理

#### 单点登录技术实现机制

1. **以Cookie作为凭证媒介**
    	最简单的单点登录实现方式，是使用cookie作为媒介，存放用户凭证。
   用户登录父应用之后，应用返回一个加密的cookie，当用户访问子应用的时候，携带上这个cookie，授权应用解密cookie并进行校验，校验通过则登录当前用户。

   ![image-20200731093752111](C:\Users\hou\AppData\Roaming\Typora\typora-user-images\image-20200731093752111.png)

2. **通过jsonp实现**
         Jsonp(JSON with Padding) 是 json 的一种"使用模式"，可以让网页从别的域名（网站）那获取资料，即跨域读取数据。

   ​     用户在父应用中登录后，跟Session匹配的Cookie会存到客户端中，当用户需要登录子应用的时候，授权应用访问父应用提供的JSONP接口，并在请求中带上父应用域名下的Cookie，父应用接收到请求，验证用户的登录状态，返回加密的信息，子应用通过解析返回来的加密信息来验证用户，如果通过验证则登录用户

   ​            ![image-20200731094122566](C:\Users\hou\AppData\Roaming\Typora\typora-user-images\image-20200731094122566.png)

3. **使用独立登录系统**

     	一般说来，大型应用会把授权的逻辑与用户信息的相关逻辑独立成一个应用，称为用户中心。用户中心不处理业务逻辑，只是处理用户信息的管理以及授权给第三方应用。第三方应用需要登录的时候，则把用户的登录请求转发给用户中心进行处理，用户处理完毕返回凭证，第三方应用验证凭证，通过后就登录用户。

### 前后端分离

#### 前后端分离相关概念

 	**前端：**

 	概念：前端指的是用户可见的界面，网站前端页面也就是网页的页面开发，比如网页上的特效、布局、图片、视频，音频等内容。

 	工作内容：将美工设计的效果图的设计成浏览器可以运行的网页，并配合后端做网页的数据显示和交互等可视方面的工作内容。

 	使用技术：前端开发用到的技术包括但不限于html5、css3、javascript、jquery、Bootstrap、Node.js 、Webpack，AngularJs，ReactJs，VueJs等技术。

​	 **后端：**

 	概念：指用户看不见的东西，通常是与前端工程师进行数据交互及网站数据的保存和读取，相对来说后端涉及到的逻辑代码比前端要多的多，

 	工作内容：底层业务逻辑的实现，平台的稳定性与性能等。

 	使用技术：后端开发 以java为例 主要用到的 是包括但不限于Struts spring springmvc Hibernate Http协议 Servlet Tomcat服务器等技术

​	**前后端分离:** 

 	在前后端不分离的应用模式中，前端页面看到的效果都是由后端控制，由后端渲染页面或重定向，也就是后端需要控制前端的展示，前端与后端的耦合度很高。

 	这种应用模式比较适合纯网页应用，但是当后端对接App时，App可能并不需要后端返回一个HTML网页，而仅仅是数据本身，所以后端原本返回网页的接口不再适用于前端App应用，为了对接App后端还需再开发一套接口。

![image-20200731094747001](C:\Users\hou\AppData\Roaming\Typora\typora-user-images\image-20200731094747001.png)在前 	后端分离的应用模式中，后端仅返回前端所需的数据，不再渲染HTML页面，不再控制前端的效果。至于前端用户看到什么效果，从后端请求的数据如何加载到前端中，都由前端自己决定，网页有网页的处理方式，App有App的处理方式，但无论哪种前端，所需的数据基本相同，后端仅需开发一套逻辑对外提供数据即可。

 	在前后端分离的应用模式中，前端与后端的耦合度相对较低。

 	在前后端分离的应用模式中，我们通常将后端开发的每个视图都称为一个接口，或者API，前端通过访问接口来对数据进行增删改查。

 	对应的数据交互如下图 :

![image-20200731095025094](C:\Users\hou\AppData\Roaming\Typora\typora-user-images\image-20200731095025094.png)

#### 前后端分离实现过程

 	 前后端分离过程中两者的主要工作：
  	前端的工作：实现整一个前端页面以及交互逻辑，有自己的独立服务器

 	 后端的工作：提供API接口，利用redis来管理session,与数据库交互

 	开发过程中并行开发二者互相看不见对方的代码可以更专注于自己的模块设计，其设计模式如下图所示

![image-20200731095133543](C:\Users\hou\AppData\Roaming\Typora\typora-user-images\image-20200731095133543.png)

### 微服务

#### 微服务相关概念

**微服务概念**

 	常而言，微服务架构是一种架构模式或者说是一种架构风格。它提倡将单一应用程序划分成一组小的服务，每个服务运行独立的自己的进程中，服务之间互相协调、互相配合，为用户提供最终价值。服务之间采用轻量级的通信机制互相沟通（通常是基于 HTTP 的 RESTful API) 。每个服务都围绕着具体业务进行构建，并且能够被独立地部署到生产环境、类生产环境等。

**微服务优点**

 	通俗地讲，“单体应用（monolith application）”就是将应用程序的所有功能都打包成一个独立的单元，可以是JAR、EXE、BIN或其它归档格式。

![image-20200731095354894](C:\Users\hou\AppData\Roaming\Typora\typora-user-images\image-20200731095354894.png)

 	这种模式的缺点在于

 	1.开发效率低：所有的开发在一个项目改代码，递交代码相互等待，代码冲突不断

 	2.代码维护难：代码功能耦合在一起，新人不知道何从下手

 	3.部署不灵活：构建时间长，任何小修改必须重新构建整个项目，这个过程往往很长

 	4.稳定性不高：一个微不足道的小问题，可以导致整个应用挂掉

 	5.扩展性不够：无法满足高并发情况下的业务需要

 	如果应用程序较小，此模型运行良好，并且易于单个团队维护。

 	随着业务需求的快速发展变化，敏捷性、灵活性和可扩展性需求不断增长，迫切需要一种更加快速高效的软件交付方式。微服务就是一种可以满足这种需求的软件架构风格。单体应用被分解成多个更小的服务，每个服务有自己的归档文件，单独部署，然后共同组成一个应用程序。这里的“微”不是针对代码行数而言，而是说服务的范围限定到单个功能

![image-20200731095457679](C:\Users\hou\AppData\Roaming\Typora\typora-user-images\image-20200731095457679.png)

 	微服务有如下优点：

 	1.微服务是松藕合的，无论是在开发阶段或部署阶段都是独立的。

 	2.能够快速响应, 局部修改容易, 一个服务出现问题不会影响整个应用。

 	3.易于和第三方应用系统集成, 支持使用不同的语言开发, 允许你利用融合最新技术。

 	4.每个微服务都很小，足够内聚，足够小，代码容易理解。团队能够更关注自己的工作成果, 聚焦指定的业务功能或业务需求。

 	5.开发简单、开发效率提高，一个服务可能就是专一的只干一件事, 能够被小团队单独开发，这个小团队可以是 2 到 5 人的开发人员组成。

#### 微服务的实现

 	微服务会将代码组织到几个单独的组件中，这些组件在不同的进程中运行。每个组件使用HTTP协议进行通信，并通过RESTful Web服务提供接口。没有集中式数据库，因为每个微服务在内部处理自己的数据结构，而进出的数据使用JSON等语言无关的格式。它可以使用XML或YAML，只要它可以由任何语言生成和使用，并通过HTTP请求和响应传播。微服务是专注于特定任务，是轻量级的应用程序，它提供了缩小的功能列表，具有明确定义的合同。它是单一责任的组件，可以独立开发和部署。

### BPMN&Camunda

#### BPMN

 **相关概念**

 	由BPMI(The Business Process Management Initiative)开发的一套标准叫业务流程建模符号(BPMN - Business Process Modeling Notation)。

 	BPMN定义了一个业务流程图（Business Process Diagram），该业务流程图基于一个流程图（flowcharting），该流程图被设计用于创建业务流程操作的图形化模型。而一个业务流程模型（Business Process Model），指一个由图形对象（graphical objects）组成的网状图，图形对象包括活动（activities)和用于定义这些活动执行顺序的流程控制器（flow controls）。

 	BPMN的目的是为用户提供一套容易理解的标准符号。这些符号，作为BPMN的基础元素，将业务流程建模简单化、图形化，将复杂的建模过程视觉化，让业务建模者、业务实施人员、管理监督人员对BPMN描述的业务流程都有一个更加清晰明了的了解。

**BPMN元素**

   	1. 流对象（Flow Objects）：
       流对象是用于定义业务流程行为的主要图形元素。它们是活动（或称任务、节点），事件和网关三种。

2.  连接对象（Connecting Objects）：
   连接对象将流对象连接在一起或连接到其他信息（如数据），它们控制着活动的顺序和过程的整体流程。连接对象的类型是“顺序流”，“消息流”和“关联”。
3. 泳道（Swimlanes）：
   泳道用于对主要建模元素进行分组。包括池和道两种类型
4. 人工信息（Artifacts）：包括数据对象、组、注释

**BPMN优点**

 	1. BPMN为业务相关者提供易于理解的标准标记法（符号），其中业务相关者包括创造与梳理流程的业务分析师、负责实施流程的技术开发者、以及业务管理者和监督人。用标准符号对业务流程进行建模描述的BPMN，扮演着促进这些人员在业务流程设计和实施之间沟通交流的角色；

 	2. BPMN是从许多已经存在的建模标记中吸收再生的，形成的一套标准的标记语言。它的出现，规范了建模标记的标准，改善了因为存在不同的业务建模工具和标记而导致的交流理解的混乱情况；

 	3. BPMN通过解决在业务流程管理上存在的问题，提高业务实施与管理的效率，最终达到促进企业的管理发展的目的。

#### Camunda

Camunda是一个流程引擎，用于流程管理、流程解决方案

支持语言:java , nodejs

工作流引擎指“业务过程的部分或整体在计算机应用环境下的自动化”。是对工作流程及其各操作步骤之间业务规则的抽象、概括描述。在计算机中，工作流属于计算机支持的协同工作（CSCW）的一部分。

工作流主要解决的主要问题是：为了实现某个业务目标，利用计算机在多个参与者之间按某种预定规则自动传递文档、信息或者任务，流程系统的核心价值就是提升人和组织的生产力。

工作流概念起源于生产组织和办公自动化领域，是针对日常工作中具有固定程序活动而提出的一个概念，目的是通过将工作分解成定义良好的任务或角色，按照一定的规则和过程来执行这些任务并对其进行监控，达到提高工作效率、更好的控制过程、增强对客户的服务、有效管理业务流程等目的。

Camunda应用：流程设计、监控、测试

使用Camunda的开发流程：

1.使用modeler画图，可视化编辑（BPMN）

添加逻辑变量、设置类型、添加表单参数、代码逻辑等

2.编写后端代码，通过Camunda提供的方法配置用户、权限等，部署流程，提供接口

3.编写前端画面处理逻辑

4.部署项目调度Camunda 

### Docker&容器 

#### 容器 

**概念**：容器就是将软件打包成标准化单元，以用于开发、交付和部署。

**特点**：

1. 容器镜像是轻量的、可执行的独立软件包 ，包含软件运行所需的所有内容：代码、运行时环境、系统工具、系统库和设置

2.  容器化软件适用于基于Linux和Windows的应用，在任何环境中都能够始终如一地运行。

3. 容器赋予了软件独立性，使其免受外在环境差异（例如，开发和预演环境的差异）的影响，从而有助于减少团队间在相同基础设施上运行不同软件时的冲突。

**容器理解**

 	通俗的描述容器的话，容器就是一个存放东西的地方，就像书包可以装各种文具、衣柜可以放各种衣服、鞋架可以放各种鞋子一样。我们现在所说的容器存放的东西可能更偏向于应用比如网站、程序甚至是系统环境。

![image-20200731100703495](C:\Users\hou\AppData\Roaming\Typora\typora-user-images\image-20200731100703495.png)

#### Docker

**概念：**

Docker是世界领先的软件容器平台。

Docker使用Google公司推出的Go语言进行开发实现，基于Linux内核，对进程进行封装隔离，属于操作系统层面的虚拟化技术，由于隔离的进程独立于宿主和其它的隔离的进程，因此也称其为容器。。

Docker能够自动执行重复性任务，例如搭建和配置开发环境，从而解放了开发人员以便他们专注在真正重要的事情上：构建杰出的软件。

用户可以方便地创建和使用容器，把自己的应用放入容器。容器还可以进行版本管理、复制、分享、修改，就像管理普通的代码一样。

**特点：**

1. 轻量，在一台机器上运行的多个Docker容器可以共享这台机器的操作系统内核；它们能够迅速启动，只需占用很少的计算和内存资源。镜像是通过文件系统层进行构造的，并共享一些公共文件。这样就能尽量降低磁盘用量，并能更快地下载镜像。

2. 标准，Docker容器基于开放式标准，能够在所有主流Linux版本、Microsoft Windows以及包括VM、裸机服务器和云在内的任何基础设施上运行。

3. 安全，Docker赋予应用的隔离性不仅限于彼此隔离，还独立于底层的基础设施。Docker默认提供最强的隔离，因此应用出现问题，也只是单个容器的问题，而不会波及到整台机器。

**Docker解决的开发过程中的问题：**

1. Docker的镜像提供了除内核外完整的运行时环境，确保了应用运行环境一致性，从而不会再出现“这段代码在我机器上没问题啊”这类问题；——一致的运行环境

2. 可以做到秒级、甚至毫秒级的启动时间。大大的节约了开发、测试、部署的时间。——更快速的启动时间

3. 避免公用的服务器，资源会容易受到其他用户的影响。——隔离性

4. 善于处理集中爆发的服务器使用压力；——弹性伸缩，快速扩展

5. 可以很轻易的将在一个平台上运行的应用，迁移到另一个平台上，而不用担心运行环境的变化导致应用无法正常运行的情况。——迁移方便

6. 使用Docker可以通过定制应用镜像来实现持续集成、持续交付、部署。——持续交付和部署

**Docker和虚拟机：**

 	容器和虚拟机具有相似的资源隔离和分配优势，但功能有所不同，因为容器虚拟化的是操作系统，而不是硬件，因此容器更容易移植，效率也更高。

 	传统虚拟机技术是虚拟出一套硬件后，在其上运行一个完整操作系统，在该系统上再运行所需应用进程；而容器内的应用进程直接运行于宿主的内核，容器内没有自己的内核，而且也没有进行硬件虚拟。因此容器要比传统虚拟机更为轻便。

![image-20200731100851759](C:\Users\hou\AppData\Roaming\Typora\typora-user-images\image-20200731100851759.png)

**Docker组成**

Docker包括三个基本概念：

镜像（Image）

容器（Container）

仓库（Repository）

1. 镜像（Image）——一个特殊的文件系统

​    操作系统分为内核和用户空间。对于Linux而言，内核启动后，会挂载root文件系统为其提供用户空间支持。而Docker镜像（Image），就相当于是一个root文件系统。

​    Docker镜像是一个特殊的文件系统，除了提供容器运行时所需的程序、库、资源、配置等文件外，还包含了一些为运行时准备的一些配置参数（如匿名卷、环境变量、用户等）。 镜像不包含任何动态数据，其内容在构建之后也不会被改变。

​    Docker设计时，就充分利用Union FS的技术，将其设计为分层存储的架构。 镜像实际是由多层文件系统联合组成。

​    镜像构建时，会一层层构建，前一层是后一层的基础。每一层构建完就不会再发生改变，后一层上的任何改变只发生在自己这一层。比如，删除前一层文件的操作，实际不是真的删除前一层的文件，而是仅在当前层标记为该文件已删除。在最终容器运行的时候，虽然不会看到这个文件，但是实际上该文件会一直跟随镜像。因此，在构建镜像的时候，需要额外小心，每一层尽量只包含该层需要添加的东西，任何额外的东西应该在该层构建结束前清理掉。

​    分层存储的特征还使得镜像的复用、定制变的更为容易。甚至可以用之前构建好的镜像作为基础层，然后进一步添加新的层，以定制自己所需的内容，构建新的镜像。

2. 容器（Container）——镜像运行时的实体

​    镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等 。

​    容器的实质是进程，但与直接在宿主执行的进程不同，容器进程运行于属于自己的独立的命名空间。前面讲过镜像使用的是分层存储，容器也是如此。

​    容器存储层的生存周期和容器一样，容器消亡时，容器存储层也随之消亡。因此，任何保存于容器存储层的信息都会随容器删除而丢失。

​    按照Docker最佳实践的要求，容器不应该向其存储层内写入任何数据 ，容器存储层要保持无状态化。所有的文件写入操作，都应该使用数据卷（Volume）、或者绑定宿主目录，在这些位置的读写会跳过容器存储层，直接对宿主（或网络存储）发生读写，其性能和稳定性更高。数据卷的生存周期独立于容器，容器消亡，数据卷不会消亡。因此， 使用数据卷后，容器可以随意删除、重新run，数据却不会丢失。

3. 仓库（Repository）——集中存放镜像文件的地方

​    镜像构建完成后，可以很容易的在当前宿主上运行，但是， 如果需要在其它服务器上使用这个镜像，我们就需要一个集中的存储、分发镜像的服务，Docker Registry就是这样的服务。

​    一个Docker Registry中可以包含多个仓库（Repository）；每个仓库可以包含多个标签（Tag）；每个标签对应一个镜像。所以说：镜像仓库是Docker用来集中存放镜像文件的地方类似于我们之前常用的代码仓库。

​    通常，一个仓库会包含同一个软件不同版本的镜像，而标签就常用于对应该软件的各个版本 。我们可以通过<仓库名>:<标签>的格式来指定具体是这个软件哪个版本的镜像。如果不给出标签，将以latest作为默认标签。