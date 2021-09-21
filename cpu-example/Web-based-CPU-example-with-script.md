# Web based Execution with Script

1. Launch instances on [EC2 console](https://us-west-2.console.aws.amazon.com/ec2/v2/home):   
<p align="center"><img src="../docs/launchvms.png"/></p><br/>

2. Choose an Amazon Machine Image (AMI)  
An AMI is a template that contains the software configuration (operating system, application server, and applications) required to launch your instance.
For CPU applications, we use Ubuntu Server 16.04 LTS (HVM), SSD Volume Type; for GPU case, we use Deep Learning Base AMI (Ubuntu 16.04) Version 40.0.  
<p align="center"><img src="../docs/ami.png"/></p><br/>

3. Choose an Instance Type  
Based on your purpose, AWS provides various instance types on [https://aws.amazon.com/ec2/instance-types/](https://aws.amazon.com/ec2/instance-types/). For CPU application, we recommand to use c5.2xlarge instance; For GPU application, we recommand to use p3.2xlarge instance.
<p align="center"><img src="../docs/vmtype.png"/></p><br/>

4. Configure Number of instances  
We use 1 instance for single machine computation, and 2 instances for distributed computation.
<p align="center"><img src="../docs/instancenumber.png"/></p><br/>

5. Configure Security Group
<p align="center"><img src="../docs/sg.png"/></p><br/>

6. Review, Create your SSH key pair, and Launch
<p align="center"><img src="../docs/keypair.png"/></p><br/>

7. View your Instance and wait for Initialing
<p align="center"><img src="../docs/status.png"/></p><br/>

8. SSH into your instance
<p align="center"><img src="../docs/ssh.png"/></p><br/>

9. Copy [bootstrap.sh](bootstrap.sh) to your instance, and run the script
```bash
sudo bash bootstrap.sh
```

10. Run ML CPU application:
    - Run application:
    ```bash
    cd ML_based_Cloud_Retrieval_Use_Case/Code && /usr/bin/python3.6 ml_based_cloud_retrieval_with_data_preprocessing.py
    ```
    - (Optional) Run application with DASK:
      - Run dask cluster on VM in background:
        ```bash
        dask-scheduler & 
        dask-worker <your-dask-scheduler-address> &
        ```
      - Run application:
        ```bash
        cd ML_based_Cloud_Retrieval_Use_Case/Code && /usr/bin/python3.6 dask_ml_based_cloud_retrieval_with_data_preprocessing.py <your-dask-scheduler-address>
        ```
      - See dask dashboard in your web browser at: [http://<vm_public_ip>:8787]()

16. Terminate all VMs on EC2 when finishing experiments.
<p align="center"><img src="../docs/terminate.png"/></p>
