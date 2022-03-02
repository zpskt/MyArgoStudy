# MyArgoStudy
进行Argo的学习
## 相关链接
[官网:  https://argoproj.github.io](https://argoproj.github.io/)   
[github官网:  https://github.com/argoproj/argo-workflows](https://github.com/argoproj/argo-workflows)
## Argo is ？
go语言写的。  
Argo官方被写为：The workflow engine for Kubernetes
为Kubernetes提供了云原生工作流，将工作流中的每个步骤实现为容器。Argo使用户能够使用类似于传统YAML的自定义DSL启动多步管道。  
该框架提供了复杂的循环，条件，与DAG的依赖关系管理等，这有助于提高部署应用程序堆栈时的灵活性以及配置和依赖关系的灵活性。  
目前被多方信任，redhat，谷歌，特斯拉等牛b厂子。

**我可以用Argo干什么？**

使用Argo，用户可以定义依赖项，以编程方式构造复杂的工作流程，用于将任何步骤的输出链接为后续步骤的输入的工件管理，并在易于阅读的UI中监视计划的作业。

Argo V2被实现为Kubernetes CRD（自定义资源）。因此，可以使用kubectl管理Argo工作流程，并与其他Kubernetes服务。    
Argo中的工作流程自动化由YAML模板（易于采用，因为Kubernetes主要使用相同的DSL）驱动，使用ADSL（Argo域特定语言）设计的。使用ADSL提供的每条指令都被视为一段代码，并与应用程序代码一起托管在SCM（源代码管理）中。  
Argo提供/支持6种不同的YAML构造：
>容器模板：根据需要创建单个容器和参数  
工作流程模板：定义作业，即short-running-app，工作流中的一个步骤可以是容器  
策略模板：用于触发/调用作业或通知的规则  
部署模板：创建长期运行的应用程序  
装置模板：在Argo之外粘贴第三方资源  
项目模板：工作流定义可在Argo目录中访问
>
Argo支持几种不同的方式来定义Kubernetes清单：kubectl应用程序，Helm图表和YAML / json清单的简单目录。

### 怎么看Argo
我的理解就是Argo就是一个框架，安装完毕后，会在K8s生成四个pod，然后这四个就是argo了。  
在argo-server中生成的多级容器，或者工作流，都不会在最外层的K8s中显示出来，只有在argoworkflow-ui中可以看到。
argo可以有条件的开启容器，比如循环，when，等类似的语句使用不同pod
### 安装流程
我的github：[https://github.com/zpskt/MyArgoStudy](https://github.com/zpskt/MyArgoStudy)
git clone git@github.com:zpskt/MyArgoStudy.git
配置文件就用我install里面的quick-start-postgres.yaml
到当前git库的根目录  
cd MyArgoStudy  
cd install  
安装argocli(v3.2.8)

    gunzip argo-linux-amd64.gz
    chmod +x argo-linux-amd64
    sudo mv ./argo-linux-amd64 /usr/local/bin/argo
    argo version
安装argoworkflow

    kubectl create ns argo
    kubectl create -n argo -f quick-start-postgres.yaml
等待pod全部启动后再下一步
端口转发到本机端口

    kubectl -n argo port-forward svc/argo-server 2746:2746

此时打开浏览器：http://127.0.0.1:2746  
用install创建的argoworkflow只有两个pod，argo-server和workflow-controller。  
