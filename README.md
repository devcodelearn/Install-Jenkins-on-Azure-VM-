💻 Steps Covered in This Video:

Step 1: Create an Azure VM

# Log in to Azure
az login

# Create a resource group
az group create --name CICDResourceGroup --location eastus

# Create a virtual machine
az vm create --resource-group CICDResourceGroup --name CICDVM --image Ubuntu2204 --admin-username cicduser --admin-password CICDPassword123!

Step 2: Open Ports for SSH and Jenkins
# Open port 22 for SSH
az vm open-port --port 22 --resource-group CICDResourceGroup --name CICDVM --priority 900

# Open port 8080 for Jenkins
az vm open-port --port 8080 --resource-group CICDResourceGroup --name CICDVM --priority 901

Step 3: Connect to the VM
# SSH into the VM
ssh <your_user_name>@<public_ip_address>

ssh cicduser@<public_ip_address>

Step 4: Install Jenkins
# Update package lists
sudo apt update

# Install necessary packages
sudo apt install vim wget git -y

# Install Java Development Kit (JDK)
sudo apt install fontconfig openjdk-17-jre -y

# Download and install Jenkins
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian/jenkins.io.key

echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install jenkins

Step 5: Start Jenkins
# Enable and start Jenkins
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins

Step 6: Access Jenkins via Browser
# Copy the admin password:
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
🌐 Go to http://<public-ip-address>:8080 in your browser, paste the admin password, and you're good to go!
