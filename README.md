# SageMaker-E2E-Workshop


SageMaker End 2 End Workshop

Issue in setting up fastai kernel - in Jupyter notebook

Once you start and stop - this is gone

sh-4.2$ ls -al /home/ec2-user/SageMaker/fastai/courses/dl1/data
ls: cannot access /home/ec2-user/SageMaker/fastai/courses/dl1/data: No such file or directory
sh-4.2$


Terminal sudo su - 

[root@ip-172-16-44-133 ~]# watch -n1 nvidia-smi

nvidia-smi --query-gpu=timestamp,name,pci.bus_id,driver_version,pstate,pcie.link.gen.max,pcie.link.gen.current,temperature.gpu,utilization.gpu,utilization.memory,memory.total,memory.free,memory.used --format=csv -l 5

http://developer.download.nvidia.com/compute/DCGM/docs/nvidia-smi-367.38.pdf

 nvidia-smi -i 0 -q -d MEMORY,UTILIZATION,ECC,TEMPERATURE,POWER,CLOCK,COMPUTE,PIDS,PERFORMANCE,SUPPORTED_CLOCKS,PAGE_RETIREMENT,ACCOUNTING 

 nvidia-smi -i 0 -q -d MEMORY,UTILIZATION,ECC,TEMPERATURE,POWER,CLOCK,COMPUTE,PIDS,PERFORMANCE,PAGE_RETIREMENT,ACCOUNTING

sagemaker-chazarey-sagemaker-e2e-try2 - endpoint_name = 'sagemaker-chazarey-sagemaker-e2e-try2'

container - is the container containing the inference code for your model that you have as a model.tar.gz

The most reliable way is to check /proc/1/cgroup. It will tell you the control groups of the init process, and when you are not in a container, that will be / for all hierarchies. When you are inside a container, you will see the name of the anchor point; which, with LXC/Docker containers, will be something like /lxc/<containerid> or /docker/<containerid> respectively.

[root@ip-172-16-44-133 ~]# cat /proc/1/cgroup
9:perf_event:/
8:memory:/
7:hugetlb:/
6:freezer:/
5:devices:/
4:cpuset:/
3:cpuacct:/
2:cpu:/
1:blkio:/
[root@ip-172-16-44-133 ~]# cat /proc/1/env
cat: /proc/1/env: No such file or directory
[root@ip-172-16-44-133 ~]# cat /proc/1/environ
HOME=/TERM=linuxPATH=/sbin:/bin:/usr/sbin:/usr/bin[root@ip-172-16-44-133 ~]#


Anybucket role - reate just for confirmation and fun and make sure its work

http://files.fast.ai/data/


chzar:~/C/SageMaker/sagemaker-lhr-summit-demo (master) $ tree -d
.
├── configs
├── container
│   └── conv_net
├── data
│   └── dogscats
│       ├── models
│       ├── sample
│       │   ├── train
│       │   │   ├── cats
│       │   │   └── dogs
│       │   └── valid
│       │       ├── cats
│       │       └── dogs
│       ├── test1
│       ├── train
│       │   ├── cats
│       │   └── dogs
│       └── valid
│           ├── cats
│           └── dogs
└── local_test
    └── test_dir
        ├── input
        │   └── config
        ├── model
        └── output


