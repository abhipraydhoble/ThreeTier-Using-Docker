# Three-Tier Architecture using Docker 

## **Overview**
This project demonstrates a three-tier architecture using Docker containers for a **frontend, backend, and database** setup. The setup involves:
- **Database**: MySQL
- **Backend**: Java (Spring Boot or Servlet-based)
- **Frontend**: HTML, CSS, JavaScript

---

## **Prerequisites**
Ensure you have the following installed:
- [Docker](https://docs.docker.com/get-docker/)
- Git

---

## **Project Setup Steps**

### **Step 1: Clone the Repository**
```bash
sudo yum install git -y
git clone https://github.com/abhipraydhoble/ThreeTier-Using-Docker.git
cd ThreeTier-Using-Docker
```

---

### **Step 2: Set Up the Database**
Navigate to the `database` directory:
```bash
cd database
```
##### The SQL script creates a studentapp database and a students table with student details.

- The Dockerfile:
- Uses the MariaDB base image.
- Sets the root password (1234).
- Copies student-rds.sql into the container for automatic database initialization.
- Starts the MariaDB service (mariadbd).

#### **2.1 Build the MySQL Docker Image**
```bash
docker build -t my-mysql-db .
```

#### **2.2 Run the MySQL Container**
```bash
docker run -d --name my-mysql-container -p 3306:3306 my-mysql-db
```

#### **2.3 Get the MySQL Container IP**
```bash
docker inspect my-mysql-container
```
Copy this IP address for the next step.

---

### **Step 3: Configure and Run the Backend**
Navigate to the `backend` directory:
```bash
cd ../backend
```

#### **3.1 Update the `context.xml` File**
Edit `context.xml` and replace `<MYSQL_CONTAINER_IP>` with the actual MySQL container IP from Step 2.3:
```xml
<Context>
    <Resource name="jdbc/StudentDB" auth="Container"
        type="javax.sql.DataSource" driverClassName="com.mysql.cj.jdbc.Driver"
        url="jdbc:mysql://<MYSQL_CONTAINER_IP>:3306/studentdb"
        username="root" password="root" maxTotal="10" maxIdle="5"/>
</Context>
```

#### **3.2 Build the Backend Image**
```bash
docker build -t my-backend-app .
```

#### **3.3 Run the Backend Container**
```bash
docker run -d --name my-backend-container -p 8080:8080 my-backend-app
```

#### **3.4 Verify Backend**
Check if the backend is working:
```bash
curl http://<INSTANCE_PUBLIC_IP>:8080/student
```
Replace `<INSTANCE_PUBLIC_IP>` with your server's public IP.

---

### **Step 4: Configure and Run the Frontend**
Navigate to the `frontend` directory:
```bash
cd ../frontend
```

#### **4.1 Update the `index.html` File in Frontend Directory**
Edit `index.html` and replace the backend URL:
```html
<a href="http://54.169.189.50:8080/student/">Register Here</a>
```
Replace `<INSTANCE_PUBLIC_IP>` with your actual server's public IP.

#### **4.2 Build the Frontend Image**
```bash
docker build -t my-frontend-app .
```

#### **4.3 Run the Frontend Container**
```bash
docker run -d --name my-frontend-container -p 80:80 my-frontend-app
```

---

## **Step 5: Access the Final Application**
Now, open your browser and go to:
```
http://<INSTANCE_PUBLIC_IP>
```
You should see the final application running!

---

## **Troubleshooting**
- **Check running containers**: `docker ps`
- **View logs**: `docker logs my-backend-container`
- **Stop all containers**: `docker stop my-mysql-container my-backend-container my-frontend-container`
- **Remove all containers**: `docker rm my-mysql-container my-backend-container my-frontend-container`

---

