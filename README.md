# 🐍 Flask App with MySQL Docker Setup 🐳

This is a simple Flask app that interacts with a MySQL database. The app allows users to submit messages which are stored in the database and displayed.

🌟 **Key Features**:
- Flask frontend
- MySQL backend
- Docker containerization
- Easy setup

## 🧰 Prerequisites

Before you begin, ensure you have:

- Docker 🐳
- Git (optional) 🔄

## 🚀 Setup Steps

1. Clone repository:

```
git clone https://github.com/Yashraj-Garnayak/two-tier-flask-app.git
```

2. Navigate to project:

```
cd your-repo-name
```

3. Create environment file:

```
touch .env
```

4. Configure MySQL:

```
MYSQL_HOST=mysql
MYSQL_USER=your_username
MYSQL_PASSWORD=your_password
MYSQL_DB=your_database
```

## 🏃‍♂️ Running the App

### 🐳 Using Docker Compose

Start containers:

```
docker-compose up --build
```

Access:
- 🌐 Frontend: http://localhost
- ⚙️ Backend: http://localhost:5000

Initialize database:

```
CREATE TABLE messages (
    id INT AUTO_INCREMENT PRIMARY KEY,
    message TEXT
);
```

### ⚙️ Manual Docker Setup

1. Build image:

```
docker build -t flaskapp .
```

2. Create network:

```
docker network create twotier
```

3. Run MySQL:

```
docker run -d \
    --name mysql \
    -v mysql-data:/var/lib/mysql \
    --network=twotier \
    -e MYSQL_DATABASE=mydb \
    -e MYSQL_ROOT_PASSWORD=admin \
    -p 3306:3306 \
    mysql:5.7
```

4. Run Flask:

```
docker run -d \
    --name flaskapp \
    --network=twotier \
    -e MYSQL_HOST=mysql \
    -e MYSQL_USER=root \
    -e MYSQL_PASSWORD=admin \
    -e MYSQL_DB=mydb \
    -p 5000:5000 \
    flaskapp:latest
```

## 🧹 Cleanup

Stop containers:

```
docker-compose down
```

## ⚠️ Important Notes

🔐 **Security Tips**:
- Always change default credentials
- Use proper secrets management
- Sanitize user inputs

🐞 **Troubleshooting**:
- Check logs: `docker logs <container>`
- Verify network: `docker network inspect twotier`
