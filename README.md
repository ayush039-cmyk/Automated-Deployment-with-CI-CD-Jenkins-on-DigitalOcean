# Automated-Deployment-with-CI-CD-Jenkins-on-DigitalOcean
Designed and implemented a CI/CD pipeline using Jenkins to automate application deployment on DigitalOcean. Integrated GitHub for source control, Jenkins for continuous integration and delivery, and cloud infrastructure for production deployment.

## Steps to follow

1.Deploy a Droplet(Server) on Digital Ocean

2.SSH into it

3.Install python3 , pip , python3-venv

4.Create a .service file in order to run the webpage:

 vi /etc/systemd/system/flask.service
 
   [Unit]
   
   Discription=flask app
   
   After=network.target

  [Service]
  
  User=root
  
  WorkingDirectory=/root/GMS
  
  Environment="PATH=/root/GMS/venv/bin"
  
  ExecStart=/root/GMS/venv/bin/python3 /root/app/app.py

  [Install]
  
  WantedBy=multi-user.target
  
  ::: Copy paste exactly

5.Open Jenkins and create a new pipeline job

6.Webhook into github repo 

All Set!!!
