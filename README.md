<img width="1440" alt="Screenshot 2025-04-03 at 11 24 23" src="https://github.com/user-attachments/assets/574cac95-cbbe-4648-9f43-054d7067d766" /># Node.js Web App with AWS RDS and Docker

This project sets up a Node.js web application running in a Docker container on an AWS EC2 instance. The application connects to an AWS RDS MySQL database for data storage.

## Architecture Overview
![ScreenRecording2025-04-04at11 10 13-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/b6bb2a9b-8712-408e-b55b-ada48b22805c)


### 1. RDS MySQL Database Setup

- Create an **AWS RDS instance**.
- Select **MySQL** as the database engine.
- Set a **database name, username, and password**.
- Enable **public access** if needed.
- Configure **security groups** to allow connections on **port 3306**.

### 2. EC2 Instance Setup

- Launch an **AWS EC2 instance** (Amazon Linux/Ubuntu recommended).
- Configure security groups to allow **SSH (port 22) and HTTP (port 80)**.
- Connect to the instance via SSH.

### 3. Install Docker on EC2

```bash
sudo yum update -y  # For Amazon Linux
sudo yum install docker -y  # For Amazon Linux
sudo apt update && sudo apt install docker.io -y  # For Ubuntu
sudo systemctl start docker
sudo systemctl enable docker
```

### 4. Pull and Run the Docker Container

```bash
sudo docker pull philippaul/node-mysql-app:02
sudo docker run -d -p 80:3000 \
   -e DB_HOST=<RDS_ENDPOINT> \
   -e DB_USER=<USERNAME> \
   -e DB_PASS=<PASSWORD> \
   --name node-app philippaul/node-mysql-app:02
```

Replace `<RDS_ENDPOINT>`, `<USERNAME>`, and `<PASSWORD>` with your RDS credentials.

### 5. Verify Database Connection

- SSH into the EC2 instance and connect to MySQL:
  ```bash
  mysql -u <USERNAME> -p -h <RDS_ENDPOINT>
  ```
- Run SQL queries to check data:
  ```sql
  USE your_database;
  SELECT * FROM your_table;
  ```

### 6. Access the Application

- Open the EC2 **public IP** in your browser.
- The Node.js app should be running and interacting with the RDS database.

### 7. Logs and Troubleshooting

- Check container logs:
  ```bash
  docker logs node-app
  ```
- Restart the container:
  ```bash
  docker restart node-app
  ```
- Check if the app is running:
  ```bash
  docker ps
  ```

## Notes

- Ensure your **RDS security group allows connections from EC2**.
- Use **environment variables** to securely pass database credentials.
- **Docker Compose** can be used for managing multiple containers.
- Regularly **update your dependencies** to ensure security and stability.

<img width="1438" alt="Screenshot 2025-04-03 at 11 23 35" src="https://github.com/user-attachments/assets/9e3df65a-6e95-4930-b694-58692f53118f" />
<img width="1028" alt="Screenshot 2025-04-03 at 11 22 59" src="https://github.com/user-attachments/assets/1b4c82fb-4926-4a5f-bb79-f52dc16adb82" />
<img width="1439" alt="Screenshot 2025-04-03 at 11 22 35" src="https://github.com/user-attachments/assets/5fd9ff10-2750-47dc-bad0-c1ec80dee68b" />
<img width="779" alt="Screenshot 2025-04-03 at 11 22 18" src="https://github.com/user-attachments/assets/6a8f3fb2-599d-4e22-b3c5-84f806f7fe07" />
<img width="1428" alt="Screenshot 2025-04-03 at 11 22 02" src="https://github.com/user-attachments/assets/44434b9c-4157-4078-81ee-92cf7496f23e" />
<img width="642" alt="Screenshot 2025-04-03 at 11 21 33" src="https://github.com/user-attachments/assets/4048cbff-2d56-4e79-a99c-4097b75a77de" />
<img width="884" alt="Screenshot 2025-04-03 at 11 21 16" src="https://github.com/user-attachments/assets/aeb92116-1015-4ae8-8a19-4bfb7a4c0b8c" />
<img width="727" alt="Screenshot 2025-04-03 at 11 24 39" src="https://github.com/user-attachments/assets/d12ee768-0aee-449a-a04d-d2b48521cff6" />
<img width="1440" alt="Screenshot 2025-04-03 at 11 24 23" src="https://github.com/user-attachments/assets/20294bd2-5500-4ae7-9251-3d30bf494e9f" />
<img width="1389" alt="Screenshot 2025-04-03 at 11 36 16" src="https://github.com/user-attachments/assets/0fd6f858-5aba-4a10-a1db-43e3c9ac4041" />
<img width="1409" alt="Screenshot 2025-04-03 at 11 27 36" src="https://github.com/user-attachments/assets/6d62dad1-bb84-442a-91f9-66072fea0c92" />


