# Deploying Wordpress Application on Amazon EC2 instance  with database over Amazon RDS	

**Some of below steps (installing mysql, nginx, downloading and extracting Wordpress tarball, starting nginx) can de done automatically by using script.sh

Following are the Steps to follow:

Step 1: Create a RDS instance on AWS 

            1.MySQL Engine and version Selected	
            2.DB instance identifier provided , give master username and password
            3.DB instance class (db.t2.micro : 1 vCPU 1 GB RAM ) selected.
            4.Storage Volume (gp2 SSD of 20GB storage ) selected
            5.Storage autoscaling disabled (currently not envisaged)
            6.Multi AZ deployment of RDS instance not enabled.
            7.VPC selected for the RDS , Wordpress EC2 instance will also be deployed in same VPC.
            
![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/WordpresswithRDS/VPC.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEIn%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCmFwLXNvdXRoLTEiRzBFAiEAxRh7aFMtMnaILMY4mrbz%2FqacBd5kRIbbsiW543h3ARICIB5X8nV538aiiHEWmCbcnqHOaJGG8L6tO1hkLM5q85jVKu0CCKL%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjc1OTE0ODM5MzY5IgyozldS36kH0oSaDyEqwQIIYPb7Yo9BrcmkCo5qhfhXLHx3SYIAcSBNaXFiy6IlqPRt0iiCGR57KElNCEqu7Ybpg61%2F2oB2TaBCNn3wEgr0ZuItZ%2FxFwjzsQImMJSS6P9eWO0ZlkG%2F4DwtjJCTg1H9GxPns3Mi2YSjr4Aamm0mrRyYRifKmuToE7efMl0INiweMboZjqHbix6m8T9QKLVE8ZaK1Z77cUTUktwd8FrJohpylqxW6%2F0SpZ9mV7%2B3YxgzX2dS4TneEz6xXGaml0JRRY3chRSTJo3%2FQgiL2L6B6lV81%2BBpDi3gcbbmDv%2BeZpwWPYOE3UNieffir0bcTfDyzV3PsA9OLGzqCuVmALl1b4LB%2BB2GxP4Kj1mlkZ39QWP5gM5Ok4u%2FvCT8VPtYKk9uqvWcLOcd%2F9lDl6%2FxN79e1%2FAQCsmdP2am3vxQop%2FvZvjcwsNaOjwY6swJh70h%2F6uScz%2Bv4K60P0KNK7wefEDM9CwfENFF1O8mOtPbRwnrVOcqC514FXxDhLQw8P6iM%2BwtrVzGzEbql3EJClNb0ZXWFmL2Pfh1kquxm%2BB6%2BGAQ1SYnDVzV2KKBv0BXwPIhtnzEiUwm0%2BUWXBkWZDArfDmh3MPtmSg0DLLWFanG4D4quxL7c45CJ%2Ba%2F2GK9aJQ3kSfM0KGIgY4i%2BinkM22JHHinFbZwMVw%2FRg1nAmsLLa%2FZWI9VI6RnjiGzF6zS%2F3%2BtKTRm1MaNRFe2BeDWz744iz3Xhct%2B71rFvhL%2BLwwKo2BdHLEpT8R2G9DCeNoAFBhaNqs9QFCCKdrt%2FQxmp3%2F7rhJ%2F1j%2BR6F9PaBOXn0%2BVy17fcj9opPCyVGR1%2BBXk9aTTzMOPvT4Q6xdB4KnqMozsH&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220116T145149Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAZ2X5J6VEZRCMMHWJ%2F20220116%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=34391c6278713637c7c360109e1aa7417dfaa9a7765e7cef44c0076dad85f751)
            
            The RDS instance and EC2 instance have to be launched in same VPC, to enable EC2 instance to connect with RDS using  its Private IP.
            Also, it is a security practice that Database instance is not accessed publicly and is only made accessible within VPC. 
            VPC Group of RDS instance: vpc-0dd84b36be3237583

            8.Public access to RDS disabled , RDS instance will accessed only by its private IP within VPC (shown in above snip)

            9.Additional configuration like initial Database name given: Initial database is “wordpress”.
            10.Finally create the MySQL RDS instance.


Step 2: Create an EC2 instance

            1.Choosing Amazon Linux 2 AMI 
            2.Choosing instance type ( t2.micro , 1 vCPU , 1 GB RAM)
            3.Configuring Instance details, the EC2 instance will be launched in the same VPC as of RDS instance.

            VPC Group of EC2 instance: vpc-0dd84b36be3237583,same as of RDS instance
            3.Root Volume is EBS Storage (gp2) , 8 GB capacity
            4.Security Group for the EC2 instance configured 
              a) SSH traffic(port 22) enabled from personal machine IP
              b) HTTP traffic ( port 80 ) enabled from all IP's , so that users can visit the website.  

            5.Setting the Security group for RDS instance, allowing MYSQL /Aurora protocol on port 3306 by EC2 instance security group , this will enable any EC2 instance part of that particular security group to connect with RDS instance on port 3306)

![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/WordpresswithRDS/RDS_inbound%20rule.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEIn%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCmFwLXNvdXRoLTEiRzBFAiEAxRh7aFMtMnaILMY4mrbz%2FqacBd5kRIbbsiW543h3ARICIB5X8nV538aiiHEWmCbcnqHOaJGG8L6tO1hkLM5q85jVKu0CCKL%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjc1OTE0ODM5MzY5IgyozldS36kH0oSaDyEqwQIIYPb7Yo9BrcmkCo5qhfhXLHx3SYIAcSBNaXFiy6IlqPRt0iiCGR57KElNCEqu7Ybpg61%2F2oB2TaBCNn3wEgr0ZuItZ%2FxFwjzsQImMJSS6P9eWO0ZlkG%2F4DwtjJCTg1H9GxPns3Mi2YSjr4Aamm0mrRyYRifKmuToE7efMl0INiweMboZjqHbix6m8T9QKLVE8ZaK1Z77cUTUktwd8FrJohpylqxW6%2F0SpZ9mV7%2B3YxgzX2dS4TneEz6xXGaml0JRRY3chRSTJo3%2FQgiL2L6B6lV81%2BBpDi3gcbbmDv%2BeZpwWPYOE3UNieffir0bcTfDyzV3PsA9OLGzqCuVmALl1b4LB%2BB2GxP4Kj1mlkZ39QWP5gM5Ok4u%2FvCT8VPtYKk9uqvWcLOcd%2F9lDl6%2FxN79e1%2FAQCsmdP2am3vxQop%2FvZvjcwsNaOjwY6swJh70h%2F6uScz%2Bv4K60P0KNK7wefEDM9CwfENFF1O8mOtPbRwnrVOcqC514FXxDhLQw8P6iM%2BwtrVzGzEbql3EJClNb0ZXWFmL2Pfh1kquxm%2BB6%2BGAQ1SYnDVzV2KKBv0BXwPIhtnzEiUwm0%2BUWXBkWZDArfDmh3MPtmSg0DLLWFanG4D4quxL7c45CJ%2Ba%2F2GK9aJQ3kSfM0KGIgY4i%2BinkM22JHHinFbZwMVw%2FRg1nAmsLLa%2FZWI9VI6RnjiGzF6zS%2F3%2BtKTRm1MaNRFe2BeDWz744iz3Xhct%2B71rFvhL%2BLwwKo2BdHLEpT8R2G9DCeNoAFBhaNqs9QFCCKdrt%2FQxmp3%2F7rhJ%2F1j%2BR6F9PaBOXn0%2BVy17fcj9opPCyVGR1%2BBXk9aTTzMOPvT4Q6xdB4KnqMozsH&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220116T145606Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAZ2X5J6VEZRCMMHWJ%2F20220116%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=fef0bf1c20238d52b91cbfa69650f01c76f728bd077d51741718147c62ad1cf0)

Step 3: Installing MYSQL Client on your EC2 instance and creating a configuring a database user for your wordpress site ans view wordpress databses finally

                       sudo yum install -y mysql
	                     export MYSQL_HOST=<your-endpoint> with your RDS instance endpoint to set environment variable for your host
                       export MYSQL_HOST=wordpress.cjs5jt8ei7j4.us-east-2.rds.amazonaws.com
                       mysql -u admin -p  
                       CREATE USER 'wordpressuser' IDENTIFIED BY '****';
                       GRANT ALL PRIVILEGES ON wordpress.* TO wordpressuser;
                       FLUSH PRIVILEGES;
                       Exit 

                       
![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/WordpresswithRDS/mysql-install.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEIn%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCmFwLXNvdXRoLTEiRzBFAiEAxRh7aFMtMnaILMY4mrbz%2FqacBd5kRIbbsiW543h3ARICIB5X8nV538aiiHEWmCbcnqHOaJGG8L6tO1hkLM5q85jVKu0CCKL%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjc1OTE0ODM5MzY5IgyozldS36kH0oSaDyEqwQIIYPb7Yo9BrcmkCo5qhfhXLHx3SYIAcSBNaXFiy6IlqPRt0iiCGR57KElNCEqu7Ybpg61%2F2oB2TaBCNn3wEgr0ZuItZ%2FxFwjzsQImMJSS6P9eWO0ZlkG%2F4DwtjJCTg1H9GxPns3Mi2YSjr4Aamm0mrRyYRifKmuToE7efMl0INiweMboZjqHbix6m8T9QKLVE8ZaK1Z77cUTUktwd8FrJohpylqxW6%2F0SpZ9mV7%2B3YxgzX2dS4TneEz6xXGaml0JRRY3chRSTJo3%2FQgiL2L6B6lV81%2BBpDi3gcbbmDv%2BeZpwWPYOE3UNieffir0bcTfDyzV3PsA9OLGzqCuVmALl1b4LB%2BB2GxP4Kj1mlkZ39QWP5gM5Ok4u%2FvCT8VPtYKk9uqvWcLOcd%2F9lDl6%2FxN79e1%2FAQCsmdP2am3vxQop%2FvZvjcwsNaOjwY6swJh70h%2F6uScz%2Bv4K60P0KNK7wefEDM9CwfENFF1O8mOtPbRwnrVOcqC514FXxDhLQw8P6iM%2BwtrVzGzEbql3EJClNb0ZXWFmL2Pfh1kquxm%2BB6%2BGAQ1SYnDVzV2KKBv0BXwPIhtnzEiUwm0%2BUWXBkWZDArfDmh3MPtmSg0DLLWFanG4D4quxL7c45CJ%2Ba%2F2GK9aJQ3kSfM0KGIgY4i%2BinkM22JHHinFbZwMVw%2FRg1nAmsLLa%2FZWI9VI6RnjiGzF6zS%2F3%2BtKTRm1MaNRFe2BeDWz744iz3Xhct%2B71rFvhL%2BLwwKo2BdHLEpT8R2G9DCeNoAFBhaNqs9QFCCKdrt%2FQxmp3%2F7rhJ%2F1j%2BR6F9PaBOXn0%2BVy17fcj9opPCyVGR1%2BBXk9aTTzMOPvT4Q6xdB4KnqMozsH&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220116T150445Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAZ2X5J6VEZRCMMHWJ%2F20220116%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=752813b0b7857d850ba45ad14e5d58c306ea58e0107689273985954acdaaf2cf)
![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/WordpresswithRDS/mysql_login.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEIn%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCmFwLXNvdXRoLTEiRzBFAiEAxRh7aFMtMnaILMY4mrbz%2FqacBd5kRIbbsiW543h3ARICIB5X8nV538aiiHEWmCbcnqHOaJGG8L6tO1hkLM5q85jVKu0CCKL%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjc1OTE0ODM5MzY5IgyozldS36kH0oSaDyEqwQIIYPb7Yo9BrcmkCo5qhfhXLHx3SYIAcSBNaXFiy6IlqPRt0iiCGR57KElNCEqu7Ybpg61%2F2oB2TaBCNn3wEgr0ZuItZ%2FxFwjzsQImMJSS6P9eWO0ZlkG%2F4DwtjJCTg1H9GxPns3Mi2YSjr4Aamm0mrRyYRifKmuToE7efMl0INiweMboZjqHbix6m8T9QKLVE8ZaK1Z77cUTUktwd8FrJohpylqxW6%2F0SpZ9mV7%2B3YxgzX2dS4TneEz6xXGaml0JRRY3chRSTJo3%2FQgiL2L6B6lV81%2BBpDi3gcbbmDv%2BeZpwWPYOE3UNieffir0bcTfDyzV3PsA9OLGzqCuVmALl1b4LB%2BB2GxP4Kj1mlkZ39QWP5gM5Ok4u%2FvCT8VPtYKk9uqvWcLOcd%2F9lDl6%2FxN79e1%2FAQCsmdP2am3vxQop%2FvZvjcwsNaOjwY6swJh70h%2F6uScz%2Bv4K60P0KNK7wefEDM9CwfENFF1O8mOtPbRwnrVOcqC514FXxDhLQw8P6iM%2BwtrVzGzEbql3EJClNb0ZXWFmL2Pfh1kquxm%2BB6%2BGAQ1SYnDVzV2KKBv0BXwPIhtnzEiUwm0%2BUWXBkWZDArfDmh3MPtmSg0DLLWFanG4D4quxL7c45CJ%2Ba%2F2GK9aJQ3kSfM0KGIgY4i%2BinkM22JHHinFbZwMVw%2FRg1nAmsLLa%2FZWI9VI6RnjiGzF6zS%2F3%2BtKTRm1MaNRFe2BeDWz744iz3Xhct%2B71rFvhL%2BLwwKo2BdHLEpT8R2G9DCeNoAFBhaNqs9QFCCKdrt%2FQxmp3%2F7rhJ%2F1j%2BR6F9PaBOXn0%2BVy17fcj9opPCyVGR1%2BBXk9aTTzMOPvT4Q6xdB4KnqMozsH&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220116T150520Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAZ2X5J6VEZRCMMHWJ%2F20220116%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=5cf06a8e2d299debe79d6d651abd693adc1ae55b08522f59cf06451796a37766)
![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/WordpresswithRDS/showdatabases.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEIn%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCmFwLXNvdXRoLTEiRzBFAiEAxRh7aFMtMnaILMY4mrbz%2FqacBd5kRIbbsiW543h3ARICIB5X8nV538aiiHEWmCbcnqHOaJGG8L6tO1hkLM5q85jVKu0CCKL%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjc1OTE0ODM5MzY5IgyozldS36kH0oSaDyEqwQIIYPb7Yo9BrcmkCo5qhfhXLHx3SYIAcSBNaXFiy6IlqPRt0iiCGR57KElNCEqu7Ybpg61%2F2oB2TaBCNn3wEgr0ZuItZ%2FxFwjzsQImMJSS6P9eWO0ZlkG%2F4DwtjJCTg1H9GxPns3Mi2YSjr4Aamm0mrRyYRifKmuToE7efMl0INiweMboZjqHbix6m8T9QKLVE8ZaK1Z77cUTUktwd8FrJohpylqxW6%2F0SpZ9mV7%2B3YxgzX2dS4TneEz6xXGaml0JRRY3chRSTJo3%2FQgiL2L6B6lV81%2BBpDi3gcbbmDv%2BeZpwWPYOE3UNieffir0bcTfDyzV3PsA9OLGzqCuVmALl1b4LB%2BB2GxP4Kj1mlkZ39QWP5gM5Ok4u%2FvCT8VPtYKk9uqvWcLOcd%2F9lDl6%2FxN79e1%2FAQCsmdP2am3vxQop%2FvZvjcwsNaOjwY6swJh70h%2F6uScz%2Bv4K60P0KNK7wefEDM9CwfENFF1O8mOtPbRwnrVOcqC514FXxDhLQw8P6iM%2BwtrVzGzEbql3EJClNb0ZXWFmL2Pfh1kquxm%2BB6%2BGAQ1SYnDVzV2KKBv0BXwPIhtnzEiUwm0%2BUWXBkWZDArfDmh3MPtmSg0DLLWFanG4D4quxL7c45CJ%2Ba%2F2GK9aJQ3kSfM0KGIgY4i%2BinkM22JHHinFbZwMVw%2FRg1nAmsLLa%2FZWI9VI6RnjiGzF6zS%2F3%2BtKTRm1MaNRFe2BeDWz744iz3Xhct%2B71rFvhL%2BLwwKo2BdHLEpT8R2G9DCeNoAFBhaNqs9QFCCKdrt%2FQxmp3%2F7rhJ%2F1j%2BR6F9PaBOXn0%2BVy17fcj9opPCyVGR1%2BBXk9aTTzMOPvT4Q6xdB4KnqMozsH&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220116T150607Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAZ2X5J6VEZRCMMHWJ%2F20220116%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=bb40e8afb0889e108a7968f7a775be363a635b3c1842df706e5b3b5becda8be1)
![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/WordpresswithRDS/user-privileges.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEIn%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCmFwLXNvdXRoLTEiRzBFAiEAxRh7aFMtMnaILMY4mrbz%2FqacBd5kRIbbsiW543h3ARICIB5X8nV538aiiHEWmCbcnqHOaJGG8L6tO1hkLM5q85jVKu0CCKL%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjc1OTE0ODM5MzY5IgyozldS36kH0oSaDyEqwQIIYPb7Yo9BrcmkCo5qhfhXLHx3SYIAcSBNaXFiy6IlqPRt0iiCGR57KElNCEqu7Ybpg61%2F2oB2TaBCNn3wEgr0ZuItZ%2FxFwjzsQImMJSS6P9eWO0ZlkG%2F4DwtjJCTg1H9GxPns3Mi2YSjr4Aamm0mrRyYRifKmuToE7efMl0INiweMboZjqHbix6m8T9QKLVE8ZaK1Z77cUTUktwd8FrJohpylqxW6%2F0SpZ9mV7%2B3YxgzX2dS4TneEz6xXGaml0JRRY3chRSTJo3%2FQgiL2L6B6lV81%2BBpDi3gcbbmDv%2BeZpwWPYOE3UNieffir0bcTfDyzV3PsA9OLGzqCuVmALl1b4LB%2BB2GxP4Kj1mlkZ39QWP5gM5Ok4u%2FvCT8VPtYKk9uqvWcLOcd%2F9lDl6%2FxN79e1%2FAQCsmdP2am3vxQop%2FvZvjcwsNaOjwY6swJh70h%2F6uScz%2Bv4K60P0KNK7wefEDM9CwfENFF1O8mOtPbRwnrVOcqC514FXxDhLQw8P6iM%2BwtrVzGzEbql3EJClNb0ZXWFmL2Pfh1kquxm%2BB6%2BGAQ1SYnDVzV2KKBv0BXwPIhtnzEiUwm0%2BUWXBkWZDArfDmh3MPtmSg0DLLWFanG4D4quxL7c45CJ%2Ba%2F2GK9aJQ3kSfM0KGIgY4i%2BinkM22JHHinFbZwMVw%2FRg1nAmsLLa%2FZWI9VI6RnjiGzF6zS%2F3%2BtKTRm1MaNRFe2BeDWz744iz3Xhct%2B71rFvhL%2BLwwKo2BdHLEpT8R2G9DCeNoAFBhaNqs9QFCCKdrt%2FQxmp3%2F7rhJ%2F1j%2BR6F9PaBOXn0%2BVy17fcj9opPCyVGR1%2BBXk9aTTzMOPvT4Q6xdB4KnqMozsH&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220116T150917Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAZ2X5J6VEZRCMMHWJ%2F20220116%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=5f408a417f625eacd597c80887279acd02e6a0d6c75c80646166cadad027a845)


Step 4 : installing and starting apache httpd / nginx (choose any one) on amazon-linux  

            1.sudo yum install -y http / sudo amazon-linux-extras install -y nginx1
            2.sudo service httpd start / sudo service nginx start 

Step 5 : Download and Configure Wordpress : 

            1. wget https://wordpress.org/latest.tar.gz   (downloading wordpress tar ball)
            2. tar -xzf latest.tar.gz (unzipping tar file) { a wordpress folder will be made after unzipping the tar file}
            3. cd wordpress (moving to wordpress directory)
            4. cp wp-config-sample.php wp-config.php (making a copy of sample config file)
            5. nano wp-config.php (opening the wp-config.php file) and provide credentials as defined earlier and also provide Authentication Unique Keys and Salts(click here)
            6.sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2  (Installing dependencies for Wordpress)
            
            With Step 5 now your Wordpress is configured with RDS DB instance credentials.
            
           
Step 6 : Deploying the Wordpress Application in /usr/share/nginx/html to enable it to be accessible via internet.

  		        1. cd /home/ec2-user 
              2. sudo cp -r wordpress/*  /var/www/html (OR /usr/share/nginx/html )
              3. to reflect changes restart the server
                 sudo service httpd restart / sudo service nginx restart 
                 
                 
WORDPRESS welcome page is now available at http://<ec2instance_Public IPv4 DNS>
Below snip of Five-minute Wordpress installation, after selecting language

![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/WordpresswithRDS/wordpress.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEIn%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCmFwLXNvdXRoLTEiRzBFAiEAxRh7aFMtMnaILMY4mrbz%2FqacBd5kRIbbsiW543h3ARICIB5X8nV538aiiHEWmCbcnqHOaJGG8L6tO1hkLM5q85jVKu0CCKL%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjc1OTE0ODM5MzY5IgyozldS36kH0oSaDyEqwQIIYPb7Yo9BrcmkCo5qhfhXLHx3SYIAcSBNaXFiy6IlqPRt0iiCGR57KElNCEqu7Ybpg61%2F2oB2TaBCNn3wEgr0ZuItZ%2FxFwjzsQImMJSS6P9eWO0ZlkG%2F4DwtjJCTg1H9GxPns3Mi2YSjr4Aamm0mrRyYRifKmuToE7efMl0INiweMboZjqHbix6m8T9QKLVE8ZaK1Z77cUTUktwd8FrJohpylqxW6%2F0SpZ9mV7%2B3YxgzX2dS4TneEz6xXGaml0JRRY3chRSTJo3%2FQgiL2L6B6lV81%2BBpDi3gcbbmDv%2BeZpwWPYOE3UNieffir0bcTfDyzV3PsA9OLGzqCuVmALl1b4LB%2BB2GxP4Kj1mlkZ39QWP5gM5Ok4u%2FvCT8VPtYKk9uqvWcLOcd%2F9lDl6%2FxN79e1%2FAQCsmdP2am3vxQop%2FvZvjcwsNaOjwY6swJh70h%2F6uScz%2Bv4K60P0KNK7wefEDM9CwfENFF1O8mOtPbRwnrVOcqC514FXxDhLQw8P6iM%2BwtrVzGzEbql3EJClNb0ZXWFmL2Pfh1kquxm%2BB6%2BGAQ1SYnDVzV2KKBv0BXwPIhtnzEiUwm0%2BUWXBkWZDArfDmh3MPtmSg0DLLWFanG4D4quxL7c45CJ%2Ba%2F2GK9aJQ3kSfM0KGIgY4i%2BinkM22JHHinFbZwMVw%2FRg1nAmsLLa%2FZWI9VI6RnjiGzF6zS%2F3%2BtKTRm1MaNRFe2BeDWz744iz3Xhct%2B71rFvhL%2BLwwKo2BdHLEpT8R2G9DCeNoAFBhaNqs9QFCCKdrt%2FQxmp3%2F7rhJ%2F1j%2BR6F9PaBOXn0%2BVy17fcj9opPCyVGR1%2BBXk9aTTzMOPvT4Q6xdB4KnqMozsH&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220116T151800Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAZ2X5J6VEZRCMMHWJ%2F20220116%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=0710005b1f84c27c46b786a0fe1b75315d2422226e0f5ffb136fe598f2c04f51)



                       

