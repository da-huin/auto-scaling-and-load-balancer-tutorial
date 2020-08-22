## Set up Load Balancer

**What is Load Balancer?**

* The Load Balacner distributes of incoming requests.
* You can check details at https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html

### **Tutorial**

1. **Open EC2 Console at https://console.aws.amazon.com/ec2**

1. **Create TWO EC2 Instance with properties below**
    
    * Open 80(HTTP) for load balancer, 22(SSH) port

    ![](./static/20200822_161552.png)

1. **Each one connects to SSH and execute the following command to open the HTTP server.**

    ```bash
    python3 -m http.server 80
    ```

    * result: 
    
        ```bash
        Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
        ```

1. **Create Target Groups**

    1. Click `Create` Button.

        ![](./static/20200822_161908.png)

    2. Fill `Target Group Name` and click `Next` button.

        ![](./static/20200822_161956.png)

    3. Add instances and click `Create` button

        ![](./static/20200822_162039.png)

1. **Create Load Balancer**

    ![](./static/1.png)

1. **Configure Load Balancer. In this page, you can also specify the AZ(Availability Zones).**

    * (Caution!) If your load balancer Availability Zone is not includes your EC2 instance's AZ, it will not work correctly.

    ![](./static/20200822_154351.png)

1. **Configure Security Groups. Open `80` port for users.**

1. **Configure Routing. You can specify Target Group. Fill the `Name` form and Click `Next` Button.**

    ![](./static/3.png)

1. **Register Targets**

    ![](./static/20200822_162327.png)

1. **Click `Create Button`.**

1. **Successfully created load balancer.**

    ![](./static/20200822_154758.png)

1. **Wait until your load balancer's state be `active`.**

1. **Click your `target` name at `Target Groups`.**

    ![](./static/20200822_155238.png)
    
1. **Check your `Instance State`.**

    ![](./static/20200822_155421.png)

1. **Check your server that opened 80 port in ssh.**

    ```bash
    ...

    172.31.45.3 - - [22/Aug/2020 06:52:23] "GET / HTTP/1.1" 200 -
    172.31.3.112 - - [22/Aug/2020 06:52:29] "GET / HTTP/1.1" 200 -
    172.31.45.3 - - [22/Aug/2020 06:52:53] "GET / HTTP/1.1" 200 -
    172.31.3.112 - - [22/Aug/2020 06:52:59] "GET / HTTP/1.1" 200 -
    172.31.45.3 - - [22/Aug/2020 06:53:23] "GET / HTTP/1.1" 200 -
    172.31.3.112 - - [22/Aug/2020 06:53:29] "GET / HTTP/1.1" 200 -
    172.31.45.3 - - [22/Aug/2020 06:53:53] "GET / HTTP/1.1" 200 -
    172.31.3.112 - - [22/Aug/2020 06:53:59] "GET / HTTP/1.1" 200 -
    172.31.45.3 - - [22/Aug/2020 06:54:23] "GET / HTTP/1.1" 200 -
    172.31.3.112 - - [22/Aug/2020 06:54:29] "GET / HTTP/1.1" 200 -

    ...
    ```

    ![](./static/20200822_155756.png)

1. **Load Balancer is set up successfully!**

## Set up Auto Scaling.

1. Connect your fisrt instance with SSH and enter the command below for AMI.

    ```
    vim /home/ubuntu/run_http.sh

    #! /bin/bash
    /usr/bin/python3.6m -m http.server 80&
    ```

1. Create an AMI with your fisrt instance for `Auto Scaling Instance`.

    ![](./static/20200822_162943.png)
    ![](./static/20200822_163009.png)

1. check created AMI.

    ![](./static/20200822_163236.png)

1. Create Launch Configuration.

    1. Click `Create Launch Configuration` button.

        ![](./static/20200822_163513.png)

    1. Fill the forms.

        ![](./static/20200822_163753.png)
        ![](./static/20200822_163954.png)


1. Create an Auto Scaling group.

    ![](./static/20200822_162705.png)

1. Choose launch configuration.

    ![](./static/20200822_164124.png)

1. Configure settings.

    ![](./static/20200822_164227.png)

1. Configure advanced options.

    ![](./static/20200822_164327.png)

1. Configure groups size and scaling policies.

    ![](./static/20200822_164517.png)

1. Add notifications

1. Add Tags

1. Review and Create Auto Scaling group.

    ![](./static/20200822_164647.png)

1. Go to your Target group page.

    ![](./static/20200822_175917.png)

1. Check your instances state.

    ![](./static/20200822_175808.png)

1. Check your auto created instances.

    ![](./static/20200822_180214.png)


1. **Auto Scaling is set up successfully!**
