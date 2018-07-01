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


chzar:~/C/SageMaker/sagemaker-lhr-summit-demo (master) $ ./predict_img_endpoint.py -e sagemaker-chazarey-sagemaker-e2e-try2
Traceback (most recent call last):
  File "./predict_img_endpoint.py", line 9, in <module>
    import boto3
ImportError: No module named boto3

chzar:~/C/SageMaker/sagemaker-lhr-summit-demo (master) $ ls
build_train_custom_model.ipynb  call_endpoint.ipynb  configs  container  data  dogscats.zip  LICENSE  local_test  predict_img_endpoint.py  README.md
chzar:~/C/SageMaker/sagemaker-lhr-summit-demo (master) $ sudo su - 
Last login: Sun Jul  1 18:11:44 UTC 2018 on pts/1
[root@ip-10-0-0-99 ~]# pip install boto3
Collecting boto3
  Downloading https://files.pythonhosted.org/packages/17/18/7d71d17ad31dc7faa5e25cada1d9876a3f85abdbfa9a599f76bc074b60d7/boto3-1.7.48-py2.py3-none-any.whl (128kB)
    100% |████████████████████████████████| 133kB 5.1MB/s 
Collecting s3transfer<0.2.0,>=0.1.10 (from boto3)
  Downloading https://files.pythonhosted.org/packages/d7/14/2a0004d487464d120c9fb85313a75cd3d71a7506955be458eebfe19a6b1d/s3transfer-0.1.13-py2.py3-none-any.whl (59kB)
    100% |████████████████████████████████| 61kB 8.2MB/s 
Collecting botocore<1.11.0,>=1.10.48 (from boto3)
  Downloading https://files.pythonhosted.org/packages/0b/56/44067a8f0cae5f33007e7cbdbaac67cbd9fa598c733ad25eb8f252288fe9/botocore-1.10.48-py2.py3-none-any.whl (4.4MB)
    100% |████████████████████████████████| 4.4MB 277kB/s 
Requirement already satisfied: jmespath<1.0.0,>=0.7.1 in /usr/lib/python2.7/dist-packages (from boto3)
Requirement already satisfied: futures<4.0.0,>=2.2.0; python_version == "2.6" or python_version == "2.7" in /usr/lib/python2.7/dist-packages (from s3transfer<0.2.0,>=0.1.10->boto3)
Requirement already satisfied: python-dateutil<3.0.0,>=2.1; python_version >= "2.7" in /usr/lib/python2.7/dist-packages (from botocore<1.11.0,>=1.10.48->boto3)
Requirement already satisfied: docutils>=0.10 in /usr/lib/python2.7/dist-packages (from botocore<1.11.0,>=1.10.48->boto3)
Requirement already satisfied: six in /usr/local/lib/python2.7/site-packages (from python-dateutil<3.0.0,>=2.1; python_version >= "2.7"->botocore<1.11.0,>=1.10.48->boto3)
Installing collected packages: botocore, s3transfer, boto3
  Found existing installation: botocore 1.8.13
    Uninstalling botocore-1.8.13:
      Successfully uninstalled botocore-1.8.13
Successfully installed boto3-1.7.48 botocore-1.10.48 s3transfer-0.1.13
You are using pip version 9.0.3, however version 10.0.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
[root@ip-10-0-0-99 ~]# 

chzar:~/C/SageMaker/sagemaker-lhr-summit-demo (master) $ ipypython -c "import math"^C
chzar:~/C/SageMaker/sagemaker-lhr-summit-demo (master) $ python -c "import boto3"
chzar:~/C/SageMaker/sagemaker-lhr-summit-demo (master) $ python -c "import boto"
chzar:~/C/SageMaker/sagemaker-lhr-summit-demo (master) $ python -c "import boto6"
Traceback (most recent call last):
  File "<string>", line 1, in <module>
ImportError: No module named boto6
chzar:~/C/SageMaker/sagemaker-lhr-summit-demo (master) $ 

chzar:~ $ tree -d
.
├── C
│   └── SageMaker
│       ├── SageMaker-E2E-Workshop
│       │   └── configs
│       └── sagemaker-lhr-summit-demo
│           ├── configs
│           ├── container
│           │   └── conv_net
│           ├── data
│           │   └── dogscats
│           │       ├── models
│           │       ├── sample
│           │       │   ├── train
│           │       │   │   ├── cats
│           │       │   │   └── dogs
│           │       │   └── valid
│           │       │       ├── cats
│           │       │       └── dogs
│           │       ├── test1
│           │       ├── train
│           │       │   ├── cats
│           │       │   └── dogs
│           │       └── valid
│           │           ├── cats
│           │           └── dogs
│           └── local_test
│               └── test_dir
│                   ├── input
│                   │   └── config
│                   ├── model
│                   └── output
└── environment
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
    └── sagemaker-lhr-summit-demo
        ├── container
        │   └── conv_net
        └── local_test
            └── test_dir
                ├── input
                │   └── config
                ├── model
                └── output

58 directories



Create mobile app quick for uploading pics and getting answer 

Try to implement a generic framework for workship 

Try to implement a new website 

watch -n1 ./predict_img_endpoint.py -e sagemaker-chazarey-sagemaker-e2e-try2

see graphs 

