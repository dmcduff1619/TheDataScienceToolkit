# TheDataScienceToolkit


SSH KEYS
- Go to Bash
- Type "ssh-keygen"
- Save in default location
- Don't add passphrase; hit enter again.
- Type "ls ~/.ssh" to view contents of ssh folder
- Type "cat ~/.ssh/id_rsa.pub" to view id_rsa.pub key, not the id_rsa one.
- Copy the key.
- Go to AWS and click on the "Key Pairs" link.
- Click on "Import Key Pair" button.
- Add a name in the "Key pair name" field
- Paste the key in the "Public key contents" field.
- Click on "Import" 


AMAZON EC2
- Login into AWS.
- Click on "Services" header link 
- Click on the "EC2" link to get the EC2 Dashboard.
- Make sure the region selected (located on the right side of the header) is the closest one to your geographic location.


SECURITY GROUPS
- Navigate to AWS and log in.
- Click the "EC2 Dashboard" link.
- Click "Instances" (or "Running Instances")
- Click on "Launch Instance" 
- Click on "Security Groups" 
- Click on "Create Security Group" 
- Fill out the :Security Group Name" and "Description" fields 
- Click on "Add Rule" button and add the following rules: SSH - 22, HTTP - 443, HTTPS - 80, PostgreSQL - 5432, and Custom TCP - 27016 
- Set all of the "Source" dropdowns to "Anywhere"
- Click "Create" button 

AWS OPERATING SYSTEM
- Navigate to AWS and log in.
- Click the "EC2 Dashboard" link.
- Click on "Instances" (or "Running Instances")
- Click on "Launch Instance" 
- There should be a list of numbered steps at the top of the screen.
- For step "1. Choose AMI": Select "Ubuntu Server 16.04 LTS (HVM), SSD Volume Type" 
- For step "2. Choose Instance Type": Select "t2.micro" 
- Skip "3. Configure Instance" 
- In "4. Add Storage": Change Size field to "20" 
- Skip "5. Add Tags" 
- For step "6. Configure Security Group": Create a new security group or select an existing security group 
- Click "Review and Launch" button 
- Click "Launch"

DOCKER INSTALLATION
- Grab the public IP address 
- Go to Bash
- Type "ssh ubuntu@<public IP address>" (or ssh ubuntu@<public IP address> -i ~/Downloads/newkey.pem)
- Type "yes" to continue connecting
- Type "curl -sSL https://get.docker.com | sh"
- Copy and run "sudo usermod -aG docker ubuntu"
- Type "exit"
- Log back in using "ssh ubuntu@<public IP address>"
- Type "docker -v" to view and verify the version of Docker you just installed

OBTAINING THE CORRECT DOCKER IMAGE
- Log back in using "ssh ubuntu@<public IP address>"
- Type "docker -v" to view and verify the version of Docker you just installed  
- Run "docker pull jupyter/datascience-notebook"
- Verify pull by typing "docker images"
- Tag image with "docker tag <image ID> dsnb"
- Verify name change with "docker images" (Notice images are the same size and have the same image ID, but different names.)
- Run the following: docker run -v /home/ubuntu:/home/jovyan -p 80:8888 -d dsnb
- Verify with "docker ps"
- Open new browser
- Type in the public IP address and the Jupyter notebook should appear


RUNNING THE CORRECT DOCKER IMAGE AS A CONTAINER
- Go back to Bash and run the following command to get a token: docker exec <container ID> jupyter notebook list
- If that doesn't work, then run "docker logs <container ID> to get token
- Copy and paste token into Jupyter notebook on other browser
- Log in and don't save any passwords


JUPYTER NOTEBOOK SECURITY CONCERNS
- Running the "curl -sSL https://get.docker.com | sh" or any other shell is a security concern.  Not recommended, but Docker is a trusted site.
- Because Jupyter notebooks can run a variety of code/languages, they run the risk of malicious attackers running arbitrary harmful code within a notebook.
- Similarly, hackers can execute local systems commands within a notebook, taking advantage of the Jupyter's ability to run multiple languages.
 
ANYTHING ELSE I MAY HAVE FORGOTTEN...
- id_rsa = "the key" = private key
- id_rsa.pub = "the lock" = public key
- ssh ubuntu@<ip address> -i ~/.ssh/id_rsa.aws
- Docker container is a virtual process.


CREATE AT LEAST ONE DIAGRAM OF YOUR OVERALL SYSTEM.

- https://i.imgur.com/z5TzNHz.jpg


A DETAILED BUDGET of the costs of running a Jupyter Data Science Notebook Server for three months using at least three different kinds of EC 2 instances.
- t2.micro = $0.0138/hr = $9.936/mo = $29.808/every 3 mo.
- t2.medium = $0.0552/hr = $119.232/every 90 days
- m5.large = $0.112/hr = $241.92/every 90 days
- d2.8xlarge = $6.25/hr = $13,500/every 90 days

