#  Mini Project: Configuring Auto Scaling with ALB Using a Launch Template


In this project, I learned how to set up **Auto Scaling** in **AWS (Amazon Web Services)** using a **Launch Template**, along with an **Application Load Balancer (ALB)**. The goal was to make sure my application could **automatically add or remove EC2 instances** based on how much demand there is — this helps save money and improve performance.

---

##  What I Did (Objectives)

Here’s what I achieved in this project:

1. **Created a Launch Template** – This is like a saved plan that includes the EC2 configuration I want to reuse.
2. **Set Up an Auto Scaling Group** – This group automatically adds or removes EC2 instances as needed.
3. **Configured Scaling Policies** – These rules tell AWS when to scale out (add more instances) or scale in (remove instances).
4. **Attached the Auto Scaling Group to an ALB** – This allows traffic to be spread evenly across the instances.
5. **Tested Auto Scaling** – I used a tool to simulate traffic and watched my setup respond by adjusting the number of instances.

---

##  Task Breakdown

###  Task 1: Create Launch Template

**What is a Launch Template?**
A Launch Template is a reusable plan that defines how EC2 instances should be launched (e.g., AMI, instance type, user data).

**Steps I followed:**

1. Logged in to the AWS Management Console.
2. Went to the **EC2** service.
3. Clicked **“Launch Templates”** in the sidebar.
4. Clicked **“Create launch template”**.
5. I filled in the details like:

   * AMI (Amazon Machine Image) → Amazon Linux 2
   * Instance type → `t2.micro`
   * Key pair → My existing key
   * User data → Script to install a basic web server

---

### Task 2: Set Up Auto Scaling Group

**What is an Auto Scaling Group?**
An Auto Scaling Group is a set of EC2 instances managed together. It can automatically increase or decrease the number of instances.

**Steps I followed:**

1. Still in the EC2 dashboard, I clicked **“Auto Scaling Groups”**.
2. Clicked **“Create Auto Scaling Group”**.
3. Selected **“Use Launch Template”** and chose the one I just made.
4. Named the group and picked:

   * Minimum capacity: 1
   * Desired capacity: 1
   * Maximum capacity: 4
5. Chose my VPC and subnets.
6. Skipped health checks for now (used default settings).

---

### Task 3: Configure Scaling Policies

**What are Scaling Policies?**
These are rules that decide when and how the group should add or remove instances.

**Steps I followed:**

1. In the Auto Scaling Group settings, I went to **“Automatic scaling”**.
2. Created two policies:

   * **Scale Out:** Add 1 instance when CPU > 70% for 2 minutes.
   * **Scale In:** Remove 1 instance when CPU < 30% for 2 minutes.

---

###  Task 4: Attach ALB to Auto Scaling Group

**What is an Application Load Balancer (ALB)?**
An ALB spreads incoming web traffic across multiple EC2 instances to keep things running smoothly.

**Steps I followed:**

1. Went to the **Load balancing** section of the Auto Scaling group.
2. Clicked **“Edit”**.
3. Chose an existing **Application Load Balancer**.
4. Linked it with the Auto Scaling group and selected the right **Target Group**.

---

### Task 5: Test Auto Scaling

**How I tested scaling:**

1. Connected to an EC2 instance using SSH.
2. Installed the **stress** tool:

   ```bash
   sudo amazon-linux-extras install epel -y
   sudo yum install stress -y
   ```
3. Simulated CPU load:

   ```bash
   stress -c 4
   ```
4. Monitored the Auto Scaling group and saw **new EC2 instances launching** when the load increased.
5. When the load reduced, extra instances were **automatically terminated**.

---

## 📷 Screenshots

Here are some screenshots showing what I did:

### Launch Template Created
<img width="1920" height="950" alt="launch template" src="https://github.com/user-attachments/assets/c9fb0d10-3a17-4121-acae-a0495e2c5372" />

![Launch Template Screenshot](./screenshots/launch-template.png)

### Auto Scaling Group Configured
<img width="1920" height="949" alt="AUTOSGdashboard" src="https://github.com/user-attachments/assets/626dc446-b16b-417f-8fab-9e854692259f" />

![Auto Scaling Group Screenshot](./screenshots/auto-scaling-group.png)

### Scaling Policies Set
<img width="1920" height="949" alt="AUTOSGscalingpolicy" src="https://github.com/user-attachments/assets/d6a52667-794e-450b-9b83-32e193c33279" />


![ALB Attachment Screenshot](./screenshots/alb-attachment.png)

### Instances Increased During Load Test
<img width="1920" height="947" alt="activity tab" src="https://github.com/user-attachments/assets/27fc94d9-3f94-4d19-8371-13bd042ebd86" />


![Scaling Test Screenshot](./screenshots/scaling-test.png)
<img width="1577" height="778" alt="stress test" src="https://github.com/user-attachments/assets/458dc78b-a4a0-4657-9e66-b12845ba45f0" />


---

## 💭 What I Learned

* **Launch Templates** make it easy to reuse EC2 settings.
* **Auto Scaling Groups** help maintain application performance by automatically adjusting resources.
* **Application Load Balancers** make sure traffic is balanced and no server gets overloaded.
* **Scaling Policies** are important for managing cost and performance.
* I also saw **real-time scaling** in action, which was very exciting!

---

##  Final Notes

* I now understand how **Auto Scaling** improves both performance and cost efficiency in cloud environments.
* This was a very useful hands-on project that taught me a key part of building scalable cloud applications.

