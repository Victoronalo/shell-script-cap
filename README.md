# shell-script-cap

Project-Linux Administration and Shell Script Scripting-2
Objective:



-I began with script enhancement of CentOS support.


#!/bin/bash

if [ -f /etc/redhat-release ]; the

    major_version=$(grep -oP '\d' /etc/redhat-release | head -1)

    if [ "$major_version" -eq 7 ]; then
        echo "This is CentOS/RHEL 7"

    elif [ "$major_version" -eq 8 ]; then
        echo "This is CentOS/RHEL 8"

    else
        echo "Unsupported CentOS/RHEL version: $major_version"
        exit 1
    fi
else
    echo "This script is intended for CentOS/RHEL."
    exit 1
fi



-To enhance support for CentOS in a shell script, you'll typically want to ensure compatibility with CentOS-specific commands, package managers, and system configurations. Here are some general tips and considerations to make your shell script CentOS-friendly.



-To proceed on, CentOS uses yum as its package manager (before CentOS 8) and dnf (starting from CentOS 8.


-to check for version of the centOS I used the below code.
if [ -f /etc/redhat-release ]; then
    if grep -q "release 8" /etc/redhat-release; then
        package_manager="dnf"
    else
        package_manager="yum"
    fi
else
    echo "Not running CentOS"
    exit 1
fi

# Example command using the selected package manager
sudo $package_manager install <package_name>

-To handle some configuration files on CentOS may be located differently compared to other distributions like Ubuntu. Ensure your script checks for these differences to avoid errors I used the below codes
# Example of checking existence of a config file
if [ -f /etc/httpd/conf/httpd.conf ]; then
    echo "Apache config found"
fi



-For best practice, I used POSIX-compliant bash scripting practices to ensure compatibility across different versions of bash and different Linux distributions.



-For enhancement, I used the script that checks for CentOS and installs a package using the appropriate package manager
#!/bin/bash

# Check if running on CentOS and select package manager
if [ -f /etc/redhat-release ]; then
    if grep -q "release 8" /etc/redhat-release; then
        package_manager="dnf"
    else
        package_manager="yum"
    fi
else
    echo "Not running CentOS"
    exit 1
fi

# Example: Install a package using the selected package manager
sudo $package_manager install <package_name>

exit 0



-I tested the script on centOS to make sure it functions well.




-Script modularity in scripting for CentOS involves structuring your scripts in a way that promotes reusability, maintainability, and compatibility across different CentOS versions and environments.


-I ensured encapsulate reusable tasks within functions. Functions help organize your code logically and make it easier to reuse the same functionality in different parts of your script or in other scripts using the below script.
#!/bin/bash

# Function to install a package based on CentOS version
install_package() {
    local package_manager
    if [ -f /etc/redhat-release ]; then
        if grep -q "release 8" /etc/redhat-release; then
            package_manager="dnf"
        else
            package_manager="yum"
        fi
        sudo $package_manager install "$1"
    else
        echo "Not running CentOS"
        exit 1
    fi
}

# Example usage of the function
install_package "httpd"


-I implement error handling to gracefully handle failures and provide meaningful messages to users when something goes wrong using the script
if ! sudo $package_manager install "$1"; then
    echo "Failed to install $1"
    exit 1
fi


-I also use variables for configuration settings that may vary between environments or versions of CentOS. This makes your script more adaptable without needing extensive modifications.


-I separated different functionalities into different scripts or script modules. This approach promotes clarity and makes it easier to maintain and update specific parts of your script without affecting others.
 Using the below script.
project/shell scripting
├── main_script.sh
├── functions/
│   ├── install_functions.sh
│   └── utility_functions.sh
└── configs/
    └── config.sh


-I went further to create an EC2 named new instance on Ubuntu AMI


-I also created a new keypair named new-keys


-I proceeded to create a security group namely new security group



-I  ssh -i "new-keys.pem" ubuntu@ec2-54-91-40-230.compute-1.amazonaws.com


-The instance connected via ssh



-Also the security group was configured by allowing ssh from anywhere.


-The keypairs too were securely stored to allow access.


-For remote execution of the EC2 instance, I ssh the instance.


-I ran sudo apt update on the Ubuntu machine.


-In the script upload I used git.


-I started by ssh using  ssh -i "new-keys.pem" ubuntu@ec2-54-91-40-230.compute-1.amazonaws.com


-I then ran sudo apt-get install git



-I then ran a clone on the repository.


-For secured handling of the script, I used keys instead of password.


-I also used secured file permission “chmod”


-I limited ssh acces specific address using security group


-For proper remote execution of script, I made sure I have all necessary permissions, files, and resources.



-I ran my script on .sh since it is a shell script.


-For error handling, I output stream for debugging.



-For apache deployment, I ran the below commands:
   * sudo apt update
   * sudo apt install apache2
   * sudo systemctl status apache2
   * sudo ufw allow 'Apache'
   * sudo systemctl restart apache2



-For the verification of apache web status I used the below command
  *systemctl status apache2



-For checking apache process I used
    *ps aux | grep apache2


-To verify apache is serving web page correctly, I used the below
     *curl -I http://localhost


Project: AWS IAM Shell Script


-I created a shell script file aws-iam-users.sh



-To create IAM for Datawise Solutions new five Staffmembers, I started by running the below command to define the variables.
    *IAM_USERNAME="John"



-I used the below command to create user.
    *aws iam create-user --user-name "$IAM_USERNAME"


-I then attached policies with the below command.
      *aws iam attach-user-policy --user-name "$IAM_USERNAME" –dev-team "arn:aws:iam::aws:policy/policy-arn-1"
aws iam attach-user-policy --user-name "$IAM_USERNAME" –dev-team "arn:aws:iam::aws:policy/policy-arn-2"



-I set additional permissions or configurations, such as enabling MFA (Multi-Factor Authentication) or setting up access keys.

-The shell script for IAM users
       *#!/bin/bash

IAM_USERNAME="John"
aws iam create-user --John "$IAM_USERNAME"

aws iam attach-user-policy --user-name "$IAM_USERNAME" –dev-team"arn:aws:iam::aws:policy/AmazonS3FullAccess"

echo "IAM user $IAM_USERNAME created successfully."



-For security, I ensure my AWS credentials are stored securely and never hardcode sensitive information in my scripts.


-For error handling, I implemented error handling and logging as per your requirements to handle any issues during execution.


-I tested my script in a controlled environment before using it in production.


-These projects have given me a lot of insight into shell scripting and I have learnt so much.


-I encountered a lot of challenges in the process of running this project but with the help of colleagues and the internet, I was able to overcome.





