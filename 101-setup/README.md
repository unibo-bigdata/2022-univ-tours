# 101 Setup

The goal of this package is to enable access to the Virtual Lab on AWS Academy and load some datasets on S3 (that will be used in future packages).

## 101-1 Access the Virtual Lab on AWS Academy

Follow these steps to accees the Virtual Lab on AWS Academy with a 100$ credit.

- Click on the invite to AWS Academy received via email
  - Registration to AWS Academy is necessary
  - No credit card is necessary
- Go to "Modules" > "Learner Lab - Foundational Services"
  - Agree to the terms and conditions
- Click on "Student access"
  - **Bookmark this page**: it will be your entry point for the next times
- Click the "Start Lab" button (top-right corner)
  - The first time, it will take about 5 minutes to startup
  - Next times, it will take only a few seconds
- A **credit counter** will appear, indicating the amount of credit left
- Click on "AWS" (top-left corner) when you have a green light
  - You will now be in your own virtual lab
  - This is the ***Console home*** of the Lab
- **Click the "End Lab"** button (top-right corner) at the end of class
  - If you don't, it should automatically shutdown in 4 hours, but 1) it will consume credit (only EC2 instances are automatically shut down), and 2) better safe than sorry.

>*What happens when I end the lab?*  
>It depends on the service: for instance, data in S3 will persist (and consume very little credit even when the Lab is down), whereas EMR clusters (and all data within them) will be completely destroyed.
>
>*What happens when I finish my credits?*  
>You will not be able to use the Lab anymore, not even the data in S3. However, you can request an additional Lab environment to be instantiated on a different account (with a different email), just ask the teacher.



## 101-2 Configure S3 and upload some datasets

Follow these steps to activate the S3 service and start loading some datasets.

- From the *console home*, click on "Services" (top-left corner) > "S3"
- Create a bucket (it is a namespace for folders and files)
  - Its name must be unique within S3
  - Suggestion: "univ-tours-bd2223-[username]" where [username] is the first letter of your first name, followed by your last name (e.g., "univ-tours-bd2223-egallinucci")
- Enter the newly created bucket and create a folder called "datasets"
- Enter the newly created folder and upload the following datasets:
  - The "riddle.txt" file in this repo
  - Download the fiction ZIP [here](https://big.csr.unibo.it/downloads/bigdata/fiction.zip), unzip on your machine and upload all files in a new folder called "fiction"
  - Download the MovieLens ZIP [here](https://big.csr.unibo.it/downloads/bigdata/ml-dataset.zip), unzip on your machine and upload all files in a new folder called "movielens"

All these files will continue to be available even after the Lab is ended.



## 101-3 Enable SSH access to the Lab's machines (key pair)

In the following packages you will be required to instantiate machines through the Lab and access them via SSH (e.g., Putty). In order to do it, you will need a Private Key file (.ppk).

From the *Console home*, select the EC2 service, then go to "Network and security" > "Key pairs", then click on "Create a key pair":
  - Put some name (e.g., "bigdata")
  - Choose .ppk as the format
  - Create the key pair > the .ppk file will be automatically downloaded
    - **Do not lose it**, or you will need to create a new key pair!

The downloaded .ppk file will be your **Key pair**.