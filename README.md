# Node.js Web App with AWS RDS and Docker

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

<img width="1389" alt="Screenshot 2025-04-03 at 11 36 16" src="https://github.com/user-attachments/assets/4e584d59-e2fc-4ec0-aa3e-78a3f63f4ce8" />
<img width="1409" alt="Screenshot 2025-04-03 at 11 27 36" src="https://github.com/user-attachments/assets/f42ad36d-722d-450d-8f57-4d52e7d6b82a" />
<img width="727" alt="Screenshot 2025-04-03 at 11 24 39" src="https://github.com/user-attachments/assets/511ee08e-f385-44d5-bd5f-7db2313f3db5" />
<img width="1440" alt="Screenshot 2025-04-03 at 11 24 23" src="https://github.com/user-attachments/assets/e8c87079-4261-486a-afab-1f0889bea9f0" />
<img width="1438" alt="Screenshot 2025-04-03 at 11 23 35" src="https://github.com/user-attachments/assets/b73bc41e-7fe8-41e4-a969-722ddd4505f7" />
<img width="1028" alt="Screenshot 2025-04-03 at 11 22 59" src="https://github.com/user-attachments/assets/41820318-6ff7-4c2f-95a2-56c2bb3b1b2a" />
<img width="1439" alt="Screenshot 2025-04-03 at 11 22 35" src="https://github.com/user-attachments/assets/36fdf513-0c0f-4e50-9b20-5d0095020976" />
<img width="779" alt="Screenshot 2025-04-03 at 11 22 18" src="https://github.com/user-attachments/assets/5cda7535-0fb5-40d5-bf3b-c72216a95b8b" />
<img width="1428" alt="Screenshot 2025-04-03 at 11 22 02" src="https://github.com/user-attachments/assets/5639d987-c192-4096-a7b4-8c37944d32ae" />
<img width="642" alt="Screenshot 2025-04-03 at 11 21 33" src="https://github.com/user-attachments/assets/b3785e51-6ac9-4de5-9c20-f96a8c94afe3" />
<img width="884" alt="Screenshot 2025-04-03 at 11 21 16" src="https://github.com/user-attachments/assets/cedb52e5-0e6b-460b-91ee-00e3cdc8531d" />
