# 7day-devops-setup-webapp
<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Set Up a Web App in the Cloud

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-vscode)

**Author:** Andrei Morosan  
**Email:** andrei.morosan2994@gmail.com

---

## Set Up a Web App Using AWS and VS Code

![Image](http://learn.nextwork.org/heartfelt_olive_loyal_melon/uploads/aws-devops-vscode_7a1de541)

---

## Introducing Today's Project!

The purpose of today's topic is to set up a Web App in the Cloud. We would need to do this as the Web App will be the 'culprit' we will experiment on and build the DevOps project around.

The objectives for today are the following:
💻 Launch an EC2 instance.
🔌 Use VS Code to set up a remote SSH connection to your EC2 instance.
☕️ Install Maven and Java and generate a basic web app.
💎 Edit code without VS Code - you'll see why IDEs are so well loved after this!

### Key tools and concepts

Services I used were:
+ Amazon EC2
+ Amazon IAM
+ Java/Maven
+ VSCode
+ Terminal Commands
+ Nano Editor

Key concepts I learned through this project include:
+ How to setup an EC2 securely with RSA key pair
+ Using SSH to connect to the EC2 instance securely with a private key
+ Linking VSCode to the EC2 instance to be able to edit project files directly

### Project reflection

Not that I wouldn't expect it in the project, but a mistake I did while trying to finish it was to hung up the SSH connection by attempting to run it in a couple of parallel terminals. Not recommended!

A couple of hours, it could have been shorter, but I wanted to take advantage to refresh my memory and dig deeper into being able to explain the theoretical concepts behind it.

This project is part one of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project in the following days, while I love taking my time with the challenges, being constrainted by a full time job and life I still want to develop my portfolio faster and of course, deepen my understanding of Cloud Services!

---

## Launching an EC2 instance

I started this project by launching an EC2 instance because it is very important to lay out the means of storing the web app files in a structured way. Let's call this the foundation of our project on which we will build upon.

### I also enabled SSH

SSH (Secure Shell Protocol) is a protocol that makes sure that only authorized users are allowed to access a remote server on the internet. I enabled SSH to make sure the EC2 instance can be accessed only from my IP. 

SSH acts also as a type of network traffic and once an SSH connection is created between us and the server, all the traffic we send there will be encrypted for the safety, and security of our data!

### Key pairs

A key pair is a way to access in the most secure way any resource that should be secured. We can imagine the key pair for an EC2 Instance like the key you would use to your house or your car. 

The key pair in this case is made up of two parts or as I like to imagine them:
+ The Lock -> The public key which is stored in cloud.
+ The Key that opens the lock -> The private key which is stored on my computer.

In this way we know that everything is secured just for us. The private key will be the only KEY that will open the LOCK which is the public key.

Once I set up my key pair, AWS automatically downloaded a .pem a format which comes from Privacy Enhanced Mails. This was initially a way to secure emails and has become the go-to format for cryptographic keys because it works with many different types of servers and in our case today, EC2 instances!

---

## Set up VS Code

VS Code is an IDE (Integrated Development Environment) as I was trying to hint at above as well. 

In a nutshell it's a software application that provides a comprehensive environment for software development, combining various tools like code editors, compilers, debuggers, and more, into a single, user-friendly interface.

P.S. I might not be having the regular VS Code first welcome page probably here, as I used VS Code extensively in the past for other projects as well, and it will 'always' be one of the first applications I install on any local machines I own. :)

In this project I will use VS Code to connect to my instance, so I can create and edit my web app's code.

![Image](http://learn.nextwork.org/heartfelt_olive_loyal_melon/uploads/aws-devops-vscode_53d05e68)

---

## My first terminal commands

A terminal is a place where you send instructions to the computer using text instead of the GUI (Graphic User Interface). Every computer would have a terminal no matter which Operating System is used.

For example in Windows the terminal is called the Command Prompt or Powershell, while in Linux and macOS distributions it is simply called a Terminal.

By using the chmod ("change mode") command I was able to update my private key's permission to read-only. This is a neat way to make the private key more secure, by changing its permissions to readable only by the Admin user, and of course inaccessible by other users.

![Image](http://learn.nextwork.org/heartfelt_olive_loyal_melon/uploads/aws-devops-vscode_9328ada1)

---

## SSH connection to EC2 instance

To connect to the EC2 instance I ran the command 

ssh -i /path/to/snowlynx-keypair.pem ec2-user@[EC2-Instance-IPv4]

The command essentially intiates the SSH protocol between the local machine and the EC2 instance, it passes two parameters:
1. The location to our private key to authenticate and ensure the encrypted flow of data in between the local machine and the EC2 server.
2. the user@[ec2-ipv4] -> The person and the address of the 'location' we are trying to access.

### This command required an IPv4 address

A server's IPv4 DNS (Internet Protocol v4 Domain Name System) is a public address for the EC2 server that the internet uses to find and connect to it. 

The local computer I am using to do this project will find and connect to the EC2 instance created earlier through this IPv4 DNS.

![Image](http://learn.nextwork.org/heartfelt_olive_loyal_melon/uploads/aws-devops-vscode_e3069dca)

---

## Maven & Java

Think of Apache Maven as a smart assistant for building Java projects. It automates the process of compiling your code and, more importantly, manages the project's dependencies, automatically downloading any external libraries your code needs to work.

We're using it because it's fantastic for getting a new project off the ground quickly. Maven uses "archetypes," which are essentially project templates, to instantly create the basic structure for different applications, like web apps, so you can start coding right away.

Later on, we'll let Maven do the heavy lifting by automatically setting up our web app's file structure. This way, we can skip the tedious setup and get right to the fun part of actually building the application.

Java is a popular programming language that is used to build different types of applications, from mobile devices to large enterprise ones. What is a neat feature of Java is that the language is cross-platform in the sense that it works on all types of operating systems, and the apps released in Java will run on pretty much any machine that has Java installed. 

Java is required in this project because Maven as a framework needs it to run. If we wouldn't install Java on the EC2 we wouldn't be able to run Maven to simply deploy our project.

---

## Create the Application

I generated the Java web app using the following command:
mvn archetype:generate \
   -DgroupId=com.snowlynx.app \ 
   -DartifactId=snowlynx-web-project \
   -DarchetypeArtifactId=maven-archetype-webapp \
   -DinteractiveMode=false

I installed Remote - SSH, which is an extension made by Microsoft for VSCode. The extension needs to be installed, as I hinted at earlier in the project, to be able to visualize the project that we will be working on in a better manner in our file explorer inside VSCode. It is a way to make our life and job easier in this case!

Configuration details required to set up a remote connection include:
- Host - which is the EC2 server
- Hostname - which is the name of the EC2 server
- IdentityFile - which is the location to our private key on the local machine
- User - which is the user we will use to connect remotely to the instance

![Image](http://learn.nextwork.org/heartfelt_olive_loyal_melon/uploads/aws-devops-vscode_2939cf01)

---

## Create the Application

Using VS Code's file explorer, we are able to see now the locations on the EC2 instance. That is of course possible because now, while using the Remote - SSH extension we connected to the EC2 instance and we've already linked the interface of VSCode to it. 

Two of the project folders created by Maven are:
1. src - (source) folder holds all the source code files that define how your web app looks and works.
2. webapp - located inside the src folder which are the web app's files e.g. HTML, CSS, JavaScript, and JSP files, and resources.

![Image](http://learn.nextwork.org/heartfelt_olive_loyal_melon/uploads/aws-devops-vscode_45f91fd7)

---

## Using Remote - SSH

index.jsp  is a file used in Java web apps. It's similar to an HTML file because it contains markup to display web pages.

However, index.jsp can also include Java code, which lets it generate dynamic content.

I edited index.jsp by accessing the file in the explorer, and changing as it can be observed the text and adding HTML specific tags for formatting it.

![Image](http://learn.nextwork.org/heartfelt_olive_loyal_melon/uploads/aws-devops-vscode_7a1de541)

---

## Using nano

An alternative to using IDEs is to edit files in terminal with built-in text editors like VIM or Nano. In this screenshot you can see how used nano to edit index.jsp. 

After I found the index.jsp file with the usage of the terminal on the EC2 instance I ran the commmand

nano index.jsp 

This command opens the index.jsp file in the nano editor which you can use to further change the contents of index.jsp

Comparing the IDE and the Terminal for editing index.jsp is definitely a bit different. The IDE is definitely tailored for better visualization and control over the project, while the terminal is what I would describe a quicker, dirty way to do it. 

The biggest takeaway however, is the fact that I believe both have their respective use cases. While the IDE is definitely a lot more powerful and useful in working on a project, the Terminal can be used for a quick fix. Like if you know there is a specific line of code that needs to be changed, the terminal would definitely surpass working with the whole IDE in speed to achieve that quick fix goal.

![Image](http://learn.nextwork.org/heartfelt_olive_loyal_melon/uploads/aws-devops-vscode_a3324ad41)

---

---
