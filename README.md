# Setup

* Create a project to contain resources used in this demo

### LMS setup
* Open GCP Cloud Shell with SDK pointed at demo project
* In Cloud Shell, run the deployment, providing preferred passwords for SQL and Supervisor
```
cd ~
git clone https://github.com/jwdavis/ce-demo-lms.git
cd ~/ce-demo-lms/deploy
. ./start_deployment.sh <sql_pass> <supervisor_pass>
```
* Wait 60-90 seconds for load balancer to come online
* Open browser pointed at load balancer IP and validate app is running

# Demo instructions

### Stage 1 - Show app
* show home page
* show modules
* show module
* show create module - don't actually create module

### Stage 2 - Show architecture
![Architecture diagram](./arch.png)
* walk them through diagram
* point out pub/sub is there if you want

### Stage 3 - Show load balancer
* global ip
* backend service page

### Stage 4 - Show managed instance groups
* show the three web and one transcode
* show autoscaling setup

### Stage 5 - show traffic distribution
* start up test machines (if they have been stopped)
* ssh into test machines in na,eu,asia
* generate load from three regions
```ab -n 1500 -c 1 http://<your ip>/gcs/mantas.mp4```
* backend takes 30-60 seconds to refresh; stall
* show traffic from origins going to correct backends

### Stage 6 - show autoscaling web app
* generate high rps load from each test machine
```ab -n 150000 -c 16 http://<your ip>/```
* show instance groups changing size
* show backend page update

### Stage 7 - show autoscaling transcoding servers
* show raw media bucket
* show transcoded media bucket
* create module with video
* backend takes 30-60 seconds to kickoff
* show new server spinning up
* show cpu utilization in instance group

### optional Stage 8 - build the whole thing from scratch
