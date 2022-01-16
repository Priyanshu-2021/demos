# Starting Wordpress Blog along with MySQL instance
# Creating Docker Compose Yml 
# Objective : To configure and launch container infrastructure using docker-compose.

 The docker-compose yaml consists of 2 images  “wordpress:latest” and “mysql:8.0.27” to start  the Wordpress Blog with an attached mysql instance.
 
 ⦁	Installed docker and docker-compose version:
 ![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/docker-compose/docker_version.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEHkaCmFwLXNvdXRoLTEiSDBGAiEAqpGfd6Dika3qX14%2FhQO2eiK9YnWe1QYu35wRC4XJw3gCIQDs5UkzMqlgYDfGTMlyMRKW9rpGFwe8j5dyuGRcYCnBWSrtAgiS%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDY3NTkxNDgzOTM2OSIMnoBjT4L6LOOoEzkxKsEC4zQxOYsENKLL7zqXvttPvuHtXm6Brroi5HqKum0CXSKIxfleZXoTHcnfj9kAPOhdLukkaNm8YxLmoIBcJsqWSaZ8lVOEY7ltEru%2BCP7ZUe1s2b1jMY%2BdZrajSh5n3Udc%2BQH%2FvaS21sr2SB9oUKfRXndPt12gsdURi%2FUC0769v6c32ff68%2B581ge9RfrbQ0WTbD6rPioMcCFfyaL9UBejKXioM4mqvQwLMRYlpiFClax5YxjO5RRv24GyL%2B8RBTFazUXyOgM8YB6Uadn7QaLMnJJM1e%2Fx0airvzTjbN%2FKDEmPMFMC9sWvMM8dHXr%2B59UFGuP0qpEoqeksyrif%2FsSN4x38sG%2FzU4vD1LN9kld3WiRHMDG5WAm9Rxb2h1F1zZWdgzyeCgnY52iz298n9sDZLOmLIZZwpVz1JHGEPPvqU8JLMLXAio8GOrIC0D9GvviHtkHMtnBBgg9cObf%2BGGuoahJzlnttigqBrD1zMY4fBPSvp%2BUvpYLL6hbezVBDVWAkACPTixEj7QhvqyNh05cm3oKgztbxac0lcJOZjGiOIpTziDVHtTw0Qb%2BQjswVloaKhesuIxr%2F3%2BblfZtwhF4C%2BtiQX18tDxlB6AOlD3%2BXXt1547H02tU4MXF2xqzT1Op6T%2FXy5MyWnTQj7p%2BCzDUOzy76ahkL6YZmJinUhReiXrAjvc%2FR2jXMOdpzOA9GGovmMtkr2C84rMG8WB%2B0f6TjEr0j3QHkSHf1Lg0YbKGW9%2BkXbModO%2Fd57ly7D4MMnAV%2FbuveGi6NkpAaee7fYLnlKmg72IyG9MiTdDwrvnkmR56Z7BluUg5HW8Ok391Tm30X5ocUVy5OHdsWVApG&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220115T175047Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAZ2X5J6VE45QRPMGH%2F20220115%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=cc026ece1bcff78957fdad71f0e31622ce9ba9904606c0b70857b87c799c845c)
             
              Docker version : 20.10.12
              Docker-composer version : 1.29.2
              
    
    
⦁	docker-compose.yaml :
    
    
                          version: "3.0"
                          services:
                            db:   
                              image: mysql:8.0.27   
                              volumes:
                                - data_mysql:/var/lib/mysql   
                              restart: always   
                              environment:
                                - MYSQL_ROOT_PASSWORD=rootpassword
                                - MYSQL_DATABASE=wordpress
                                - MYSQL_USER=priyanshu
                                - MYSQL_PASSWORD=wordpressmysql    
                              expose:
                                - 3306
                                - 33060
                            wordpress:
                              image: wordpress:latest  
                              volumes:
                                - data_wordpress:/var/www/html
                              ports:
                                - 80:80
                              restart: always
                              environment:
                                - WORDPRESS_DB_HOST=db
                                - WORDPRESS_DB_USER=priyanshu
                                - WORDPRESS_DB_PASSWORD=wordpressmysql
                                - WORDPRESS_DB_NAME=wordpress
                          volumes:
                            data_mysql:
                            data_wordpress:


⦁	Running docker-compose in detached mode

              docker-compose up -d 
 ![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/docker-compose/docker-compose_up.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEHkaCmFwLXNvdXRoLTEiSDBGAiEAqpGfd6Dika3qX14%2FhQO2eiK9YnWe1QYu35wRC4XJw3gCIQDs5UkzMqlgYDfGTMlyMRKW9rpGFwe8j5dyuGRcYCnBWSrtAgiS%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDY3NTkxNDgzOTM2OSIMnoBjT4L6LOOoEzkxKsEC4zQxOYsENKLL7zqXvttPvuHtXm6Brroi5HqKum0CXSKIxfleZXoTHcnfj9kAPOhdLukkaNm8YxLmoIBcJsqWSaZ8lVOEY7ltEru%2BCP7ZUe1s2b1jMY%2BdZrajSh5n3Udc%2BQH%2FvaS21sr2SB9oUKfRXndPt12gsdURi%2FUC0769v6c32ff68%2B581ge9RfrbQ0WTbD6rPioMcCFfyaL9UBejKXioM4mqvQwLMRYlpiFClax5YxjO5RRv24GyL%2B8RBTFazUXyOgM8YB6Uadn7QaLMnJJM1e%2Fx0airvzTjbN%2FKDEmPMFMC9sWvMM8dHXr%2B59UFGuP0qpEoqeksyrif%2FsSN4x38sG%2FzU4vD1LN9kld3WiRHMDG5WAm9Rxb2h1F1zZWdgzyeCgnY52iz298n9sDZLOmLIZZwpVz1JHGEPPvqU8JLMLXAio8GOrIC0D9GvviHtkHMtnBBgg9cObf%2BGGuoahJzlnttigqBrD1zMY4fBPSvp%2BUvpYLL6hbezVBDVWAkACPTixEj7QhvqyNh05cm3oKgztbxac0lcJOZjGiOIpTziDVHtTw0Qb%2BQjswVloaKhesuIxr%2F3%2BblfZtwhF4C%2BtiQX18tDxlB6AOlD3%2BXXt1547H02tU4MXF2xqzT1Op6T%2FXy5MyWnTQj7p%2BCzDUOzy76ahkL6YZmJinUhReiXrAjvc%2FR2jXMOdpzOA9GGovmMtkr2C84rMG8WB%2B0f6TjEr0j3QHkSHf1Lg0YbKGW9%2BkXbModO%2Fd57ly7D4MMnAV%2FbuveGi6NkpAaee7fYLnlKmg72IyG9MiTdDwrvnkmR56Z7BluUg5HW8Ok391Tm30X5ocUVy5OHdsWVApG&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220115T182936Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAZ2X5J6VE45QRPMGH%2F20220115%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=a30a974c552d9a3cf20224048f1f9c3b459c53345db6ba19e871b4592b7ebd26)
               
 
⦁	The containers are now running successfully: 2 containers are namely  docker-compose_wordpress_1 and docker-compose_db_1.
 
 ![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/docker-compose/containers_running.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEHkaCmFwLXNvdXRoLTEiSDBGAiEAqpGfd6Dika3qX14%2FhQO2eiK9YnWe1QYu35wRC4XJw3gCIQDs5UkzMqlgYDfGTMlyMRKW9rpGFwe8j5dyuGRcYCnBWSrtAgiS%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDY3NTkxNDgzOTM2OSIMnoBjT4L6LOOoEzkxKsEC4zQxOYsENKLL7zqXvttPvuHtXm6Brroi5HqKum0CXSKIxfleZXoTHcnfj9kAPOhdLukkaNm8YxLmoIBcJsqWSaZ8lVOEY7ltEru%2BCP7ZUe1s2b1jMY%2BdZrajSh5n3Udc%2BQH%2FvaS21sr2SB9oUKfRXndPt12gsdURi%2FUC0769v6c32ff68%2B581ge9RfrbQ0WTbD6rPioMcCFfyaL9UBejKXioM4mqvQwLMRYlpiFClax5YxjO5RRv24GyL%2B8RBTFazUXyOgM8YB6Uadn7QaLMnJJM1e%2Fx0airvzTjbN%2FKDEmPMFMC9sWvMM8dHXr%2B59UFGuP0qpEoqeksyrif%2FsSN4x38sG%2FzU4vD1LN9kld3WiRHMDG5WAm9Rxb2h1F1zZWdgzyeCgnY52iz298n9sDZLOmLIZZwpVz1JHGEPPvqU8JLMLXAio8GOrIC0D9GvviHtkHMtnBBgg9cObf%2BGGuoahJzlnttigqBrD1zMY4fBPSvp%2BUvpYLL6hbezVBDVWAkACPTixEj7QhvqyNh05cm3oKgztbxac0lcJOZjGiOIpTziDVHtTw0Qb%2BQjswVloaKhesuIxr%2F3%2BblfZtwhF4C%2BtiQX18tDxlB6AOlD3%2BXXt1547H02tU4MXF2xqzT1Op6T%2FXy5MyWnTQj7p%2BCzDUOzy76ahkL6YZmJinUhReiXrAjvc%2FR2jXMOdpzOA9GGovmMtkr2C84rMG8WB%2B0f6TjEr0j3QHkSHf1Lg0YbKGW9%2BkXbModO%2Fd57ly7D4MMnAV%2FbuveGi6NkpAaee7fYLnlKmg72IyG9MiTdDwrvnkmR56Z7BluUg5HW8Ok391Tm30X5ocUVy5OHdsWVApG&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220115T183034Z&X-Amz-SignedHeaders=host&X-Amz-Expires=299&X-Amz-Credential=ASIAZ2X5J6VE45QRPMGH%2F20220115%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=bf3e32530e1238d3b38d6ad01920daf4b2451e666d8c3546b8f20243a76e7be8)
 
⦁	The Wordpress is now running and accessible on port 80 of host( port 80 of ec2 instance in our case)

![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/docker-compose/ec2_ip.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEHkaCmFwLXNvdXRoLTEiSDBGAiEAqpGfd6Dika3qX14%2FhQO2eiK9YnWe1QYu35wRC4XJw3gCIQDs5UkzMqlgYDfGTMlyMRKW9rpGFwe8j5dyuGRcYCnBWSrtAgiS%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDY3NTkxNDgzOTM2OSIMnoBjT4L6LOOoEzkxKsEC4zQxOYsENKLL7zqXvttPvuHtXm6Brroi5HqKum0CXSKIxfleZXoTHcnfj9kAPOhdLukkaNm8YxLmoIBcJsqWSaZ8lVOEY7ltEru%2BCP7ZUe1s2b1jMY%2BdZrajSh5n3Udc%2BQH%2FvaS21sr2SB9oUKfRXndPt12gsdURi%2FUC0769v6c32ff68%2B581ge9RfrbQ0WTbD6rPioMcCFfyaL9UBejKXioM4mqvQwLMRYlpiFClax5YxjO5RRv24GyL%2B8RBTFazUXyOgM8YB6Uadn7QaLMnJJM1e%2Fx0airvzTjbN%2FKDEmPMFMC9sWvMM8dHXr%2B59UFGuP0qpEoqeksyrif%2FsSN4x38sG%2FzU4vD1LN9kld3WiRHMDG5WAm9Rxb2h1F1zZWdgzyeCgnY52iz298n9sDZLOmLIZZwpVz1JHGEPPvqU8JLMLXAio8GOrIC0D9GvviHtkHMtnBBgg9cObf%2BGGuoahJzlnttigqBrD1zMY4fBPSvp%2BUvpYLL6hbezVBDVWAkACPTixEj7QhvqyNh05cm3oKgztbxac0lcJOZjGiOIpTziDVHtTw0Qb%2BQjswVloaKhesuIxr%2F3%2BblfZtwhF4C%2BtiQX18tDxlB6AOlD3%2BXXt1547H02tU4MXF2xqzT1Op6T%2FXy5MyWnTQj7p%2BCzDUOzy76ahkL6YZmJinUhReiXrAjvc%2FR2jXMOdpzOA9GGovmMtkr2C84rMG8WB%2B0f6TjEr0j3QHkSHf1Lg0YbKGW9%2BkXbModO%2Fd57ly7D4MMnAV%2FbuveGi6NkpAaee7fYLnlKmg72IyG9MiTdDwrvnkmR56Z7BluUg5HW8Ok391Tm30X5ocUVy5OHdsWVApG&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220115T183520Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAZ2X5J6VE45QRPMGH%2F20220115%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=4a5c01ceb51681d4df4a9de121cbe394bc03c3d6ebaa41648b9e6ebe76917f4b)

![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/docker-compose/wordpress.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEHkaCmFwLXNvdXRoLTEiSDBGAiEAqpGfd6Dika3qX14%2FhQO2eiK9YnWe1QYu35wRC4XJw3gCIQDs5UkzMqlgYDfGTMlyMRKW9rpGFwe8j5dyuGRcYCnBWSrtAgiS%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDY3NTkxNDgzOTM2OSIMnoBjT4L6LOOoEzkxKsEC4zQxOYsENKLL7zqXvttPvuHtXm6Brroi5HqKum0CXSKIxfleZXoTHcnfj9kAPOhdLukkaNm8YxLmoIBcJsqWSaZ8lVOEY7ltEru%2BCP7ZUe1s2b1jMY%2BdZrajSh5n3Udc%2BQH%2FvaS21sr2SB9oUKfRXndPt12gsdURi%2FUC0769v6c32ff68%2B581ge9RfrbQ0WTbD6rPioMcCFfyaL9UBejKXioM4mqvQwLMRYlpiFClax5YxjO5RRv24GyL%2B8RBTFazUXyOgM8YB6Uadn7QaLMnJJM1e%2Fx0airvzTjbN%2FKDEmPMFMC9sWvMM8dHXr%2B59UFGuP0qpEoqeksyrif%2FsSN4x38sG%2FzU4vD1LN9kld3WiRHMDG5WAm9Rxb2h1F1zZWdgzyeCgnY52iz298n9sDZLOmLIZZwpVz1JHGEPPvqU8JLMLXAio8GOrIC0D9GvviHtkHMtnBBgg9cObf%2BGGuoahJzlnttigqBrD1zMY4fBPSvp%2BUvpYLL6hbezVBDVWAkACPTixEj7QhvqyNh05cm3oKgztbxac0lcJOZjGiOIpTziDVHtTw0Qb%2BQjswVloaKhesuIxr%2F3%2BblfZtwhF4C%2BtiQX18tDxlB6AOlD3%2BXXt1547H02tU4MXF2xqzT1Op6T%2FXy5MyWnTQj7p%2BCzDUOzy76ahkL6YZmJinUhReiXrAjvc%2FR2jXMOdpzOA9GGovmMtkr2C84rMG8WB%2B0f6TjEr0j3QHkSHf1Lg0YbKGW9%2BkXbModO%2Fd57ly7D4MMnAV%2FbuveGi6NkpAaee7fYLnlKmg72IyG9MiTdDwrvnkmR56Z7BluUg5HW8Ok391Tm30X5ocUVy5OHdsWVApG&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220115T183611Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAZ2X5J6VE45QRPMGH%2F20220115%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=3657ba367dd20c91929ba3638aa8ca7cc5dfea07a33b190756644a32c97d2016)

The Wordpress Blog is now acessibel as shown in above snip.

⦁	Also you can now log into mysql in container docker-compose_db_1 to show database “wordpress” as shown below

![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/docker-compose/mysql_login.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEHkaCmFwLXNvdXRoLTEiSDBGAiEAqpGfd6Dika3qX14%2FhQO2eiK9YnWe1QYu35wRC4XJw3gCIQDs5UkzMqlgYDfGTMlyMRKW9rpGFwe8j5dyuGRcYCnBWSrtAgiS%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDY3NTkxNDgzOTM2OSIMnoBjT4L6LOOoEzkxKsEC4zQxOYsENKLL7zqXvttPvuHtXm6Brroi5HqKum0CXSKIxfleZXoTHcnfj9kAPOhdLukkaNm8YxLmoIBcJsqWSaZ8lVOEY7ltEru%2BCP7ZUe1s2b1jMY%2BdZrajSh5n3Udc%2BQH%2FvaS21sr2SB9oUKfRXndPt12gsdURi%2FUC0769v6c32ff68%2B581ge9RfrbQ0WTbD6rPioMcCFfyaL9UBejKXioM4mqvQwLMRYlpiFClax5YxjO5RRv24GyL%2B8RBTFazUXyOgM8YB6Uadn7QaLMnJJM1e%2Fx0airvzTjbN%2FKDEmPMFMC9sWvMM8dHXr%2B59UFGuP0qpEoqeksyrif%2FsSN4x38sG%2FzU4vD1LN9kld3WiRHMDG5WAm9Rxb2h1F1zZWdgzyeCgnY52iz298n9sDZLOmLIZZwpVz1JHGEPPvqU8JLMLXAio8GOrIC0D9GvviHtkHMtnBBgg9cObf%2BGGuoahJzlnttigqBrD1zMY4fBPSvp%2BUvpYLL6hbezVBDVWAkACPTixEj7QhvqyNh05cm3oKgztbxac0lcJOZjGiOIpTziDVHtTw0Qb%2BQjswVloaKhesuIxr%2F3%2BblfZtwhF4C%2BtiQX18tDxlB6AOlD3%2BXXt1547H02tU4MXF2xqzT1Op6T%2FXy5MyWnTQj7p%2BCzDUOzy76ahkL6YZmJinUhReiXrAjvc%2FR2jXMOdpzOA9GGovmMtkr2C84rMG8WB%2B0f6TjEr0j3QHkSHf1Lg0YbKGW9%2BkXbModO%2Fd57ly7D4MMnAV%2FbuveGi6NkpAaee7fYLnlKmg72IyG9MiTdDwrvnkmR56Z7BluUg5HW8Ok391Tm30X5ocUVy5OHdsWVApG&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220115T185558Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAZ2X5J6VE45QRPMGH%2F20220115%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=09ce73c0a21b1b392bccde43a77fb203fc0a1ff4c2f292b9f50db8f875fea6b8)


⦁	Show database “wordpress” and tables within the database, retells the fact that our database "wordpress" is also succesfully ceated

![alt text](https://bucketforowork.s3.us-east-2.amazonaws.com/docker-compose/db-tables.PNG?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEHkaCmFwLXNvdXRoLTEiSDBGAiEAqpGfd6Dika3qX14%2FhQO2eiK9YnWe1QYu35wRC4XJw3gCIQDs5UkzMqlgYDfGTMlyMRKW9rpGFwe8j5dyuGRcYCnBWSrtAgiS%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDY3NTkxNDgzOTM2OSIMnoBjT4L6LOOoEzkxKsEC4zQxOYsENKLL7zqXvttPvuHtXm6Brroi5HqKum0CXSKIxfleZXoTHcnfj9kAPOhdLukkaNm8YxLmoIBcJsqWSaZ8lVOEY7ltEru%2BCP7ZUe1s2b1jMY%2BdZrajSh5n3Udc%2BQH%2FvaS21sr2SB9oUKfRXndPt12gsdURi%2FUC0769v6c32ff68%2B581ge9RfrbQ0WTbD6rPioMcCFfyaL9UBejKXioM4mqvQwLMRYlpiFClax5YxjO5RRv24GyL%2B8RBTFazUXyOgM8YB6Uadn7QaLMnJJM1e%2Fx0airvzTjbN%2FKDEmPMFMC9sWvMM8dHXr%2B59UFGuP0qpEoqeksyrif%2FsSN4x38sG%2FzU4vD1LN9kld3WiRHMDG5WAm9Rxb2h1F1zZWdgzyeCgnY52iz298n9sDZLOmLIZZwpVz1JHGEPPvqU8JLMLXAio8GOrIC0D9GvviHtkHMtnBBgg9cObf%2BGGuoahJzlnttigqBrD1zMY4fBPSvp%2BUvpYLL6hbezVBDVWAkACPTixEj7QhvqyNh05cm3oKgztbxac0lcJOZjGiOIpTziDVHtTw0Qb%2BQjswVloaKhesuIxr%2F3%2BblfZtwhF4C%2BtiQX18tDxlB6AOlD3%2BXXt1547H02tU4MXF2xqzT1Op6T%2FXy5MyWnTQj7p%2BCzDUOzy76ahkL6YZmJinUhReiXrAjvc%2FR2jXMOdpzOA9GGovmMtkr2C84rMG8WB%2B0f6TjEr0j3QHkSHf1Lg0YbKGW9%2BkXbModO%2Fd57ly7D4MMnAV%2FbuveGi6NkpAaee7fYLnlKmg72IyG9MiTdDwrvnkmR56Z7BluUg5HW8Ok391Tm30X5ocUVy5OHdsWVApG&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20220115T185738Z&X-Amz-SignedHeaders=host&X-Amz-Expires=299&X-Amz-Credential=ASIAZ2X5J6VE45QRPMGH%2F20220115%2Fus-east-2%2Fs3%2Faws4_request&X-Amz-Signature=8a99e2dd3f00ebc6058fd07bd473b258be1832c3b9551f2300e4142c3df24976)

!!End


          
  
