# 201 Spark basics

The goal of this package is to get familiar with Spark programming.

## 201-1 Cluster startup

EMR is AWS's service to provision clusters of machines pre-configured with applications in the Hadoop stack.

From your *Console home*, click on "Services" > "EMR", then "Create cluster".Click on "Advanced options" (top of the page) to be able to set all important configuration parameters.

- Software
    - Choose the latest EMR version
    - **Services: Hadoop, Hive, JupiterEnterpriseGateway, Spark, Livy**
    - After last step completes: Clusters enters waiting state
- Hardware
    - 1 Master node, On demand, m5.xlarge (default)
    - 2 Core nodes, On demand, m5.xlarge (default)
    - Disable automatic termination
- General
    - Name: whichever you prefer; the same name can be re-used several times
    - Enable log registration
- Security
    - Choose the *Key pair* created in 101-3

The cluster will be created in 5 to 10 minutes.

### Troubleshooting

*The cluster couldn't be created due to the following error: "The requested instance type m5.xlarge is not supported in the requested availability zone."* In the Hardware configuration, try a different EC2 subnet.

## 201-2 Connect via SSH to the master node

Once the cluster is up-and-running, you need to allow SSH access to the master node of the newly created EMR cluster.

- From the *EMR service console*, open the list of created clusters, then open the cluster currently running
  - Located the "Master's Public DNS" in the Summary - it will be used later
  - Under "Security and Access", click on the security group of the master node (ElasticMapReduce-master)
    - In the newly opened page, select again the ID of the security group of the master node (ElasticMapReduce-master)
    - Click on "Edit inbound rules"
    - Add an SSH rule that allows connections to port 22 from any IPv4

Now open **Putty** and enter the following configuration.

- Host Name: hadoop@ec2-xxx-xxx-xxx-xxx.compute-1.amazonaws.com
  - Replace "xxx-xxx-xxx-xxx" with the IP address of the "Master's Public DNS"
- Under "Connection" > Expand "SSH" > "Auth", click "Browse" and select your *Key pair*
- *Save the configuration*
- Open the connection

**Notice**: new clusters are created on different IPs, thus the configuration will need to be updated each time. 


## 201-3 Connect to services' GUIs through SSH tunnels

Many services (HDFS, YARN, Spark, etc.) expose GUIs with useful information, especially to monitor the execution of jobs and get interesting insights. To access them, SSH tunnels must be enable for each port.

Setup tunnels for ports 8088 (YARN), 19888, and 20888 (Spark).

- Reopen the configuration from 201-2
- Go to "Connection" > Expand "SSH" > "Tunnels"
- For each port XYZ, do the following:
  - Source port: XYZ
  - Destination: ec2-xxx-xxx-xxx-xxx.compute-1.amazonaws.com:XYZ
  - Click "Add"
- *Save the configuration*
- Open the connection

The GUIs are now available under [localhost:8088](), [localhost:19888](), and [localhost:20888]().

## 201-4 Launch the notebook
    
Click on "Notebook" on the left panel, then "Create notebook".
- In the configuration parameters, make sure that you associate the notebook to the created cluster.
- As "AWS Service Role" use "**LabRole**"

Once the notebook is running, click on the JupiterLab link.
- The notebook provides a shell-like interaction mode, but more powerful. You can create, save, run and re-run scripts whenever necessary, and you can alternate code snippets with markdown text.
- Upload the ```material/201.ipynb``` Spark notebook file and follow the instructions over there.