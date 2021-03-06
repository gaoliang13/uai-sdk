# CIFAR-10 Example
CIFAR-10 is a common benchmark in machine learning for image recognition.                                                                                      
                                                                                                                                                               
http://www.cs.toronto.edu/~kriz/cifar.html                                                                                                                     

## Original Example
Code here is an example of how to run tensorflow cifar example on UAI Train platform                                                                           
                                                                                                                                                               
The original code can see here: https://github.com/tensorflow/models/tree/master/tutorials/image/cifar10_estimator                                             

## UAI Example                                                                                                                                                 
We do following modifications to the cifar10_main.py:  
                                                                                                        
1. Add UAI SDK related arguments: --data\_dir, --output\_dir, --work\_dir, --log\_dir, --num\_gpus, these arguments are auto generated by UAI Train Platform, see: https://github.com/ucloud/uai-sdk/blob/master/uaitrain/arch/tensorflow/uflag.py for more details                                                                
2. Modify code to use UAI arguments: use data_dir as input dir and use output_dir as model output dir  

## How to run
We assume you fully understand how UAI Train docker image works and has already reads the DOCS here: https://docs.ucloud.cn/ai/uai-train/guide/tensorflow

1. Follow https://github.com/tensorflow/models/tree/master/tutorials/image/cifar10\_estimator to generate tfrecords of cifar10
2. Pack the cifar10 example code into docker using tf\_tools.py provided in https://github.com/ucloud/uai-sdk/blob/master/uaitrain\_tool/tf/
3. Run the docker locally or push it into UAI Train platform to run.
   
#### The simplest CMD applied to run is 
    /data/cifar10_main.py --train-batch-size=16

#### An pack cmd example is:

    sudo python tf_tool.py pack --public_key=<UCLOUD_PUB_KEY> \ 
    --private_key=<UCLOUD_PRIV_KEY> \
    --code_path=code/ \
    --mainfile_path=cifar10_main.py \
    --uhub_username=<UCLOUD_ACCOUNT> \
    --uhub_password=<UCLOUD_ACCOUNT_PASSWD> \
    --uhub_registry=<UHUB_DOCKER_REGISTRY> \
    --uhub_imagename=resnet-cifar-tf \
    --ai_arch_v=tensorflow-1.4.0 \
    --test_data_path=<LOCAL_PATH_TO_CIFAR10_DATA_FOR_TEST> \
    --test_output_path=<LOCAL_PATH_TO_OUTOUT_FOR_TEST> \
    --train_params="--batch_size=128"
   
Note: 
The tfrecords should stored in LOCAL\_PATH\_TO\_CIFAR10\_DATA\_FOR\_TEST in this example.
