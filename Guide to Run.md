# Guide to Run — Risk Heatmap Visualiser

This guide provides step-by-step instructions to set up and run the **Risk Heatmap Visualiser** project on a Windows machine. Whether you are a developer, trainer, or evaluator, following these steps will ensure the full project is running successfully from scratch.

---

## 1. Project Overview

The **Risk Heatmap Visualiser** is a full-stack application designed for risk management and visualisation.

- **Backend**: Spring Boot (Java 17)
- **Frontend**: React (Vite)
- **Database**: PostgreSQL
- **Caching**: Redis
- **Containerization**: Docker Compose
- **Security**: JWT Authentication
- **Documentation**: Swagger UI / OpenAPI 3

---

## 2. Prerequisites

Ensure the following software is installed on your Windows laptop:

- **Java 17**: Required for manual backend execution.
- **Maven**: For dependency management and building the backend.
- **Node.js (LTS)**: Required for manual frontend execution.
- **Docker Desktop**: **Crucial** for running the entire stack easily.
- **Git** (Optional): For cloning the repository (if not using ZIP).
- **VS Code** or **IntelliJ IDEA** (Optional): For code exploration.

---

## 3. ZIP Extraction Steps

1. Locate the `risk-heatmap-visualiser.zip` file.
2. Right-click and select **Extract All...** to a folder of your choice.
3. Open the extracted folder in your preferred IDE (VS Code or IntelliJ IDEA).

---

## 4. Docker Desktop Setup

1. [Download and Install Docker Desktop](https://www.docker.com/products/docker-desktop/) for Windows.
2. Launch Docker Desktop and ensure the **Docker Engine** is running (indicated by a green icon in the bottom corner).
3. Ensure you have enabled WSL 2 integration if prompted during installation.

---

## 5. Environment Variables

The project requires an `.env` file in the root directory to manage configurations. 

1. Create a file named `.env` in the root folder (or rename `.env.example` to `.env`).
2. Add the following configuration:

```env
# Database Configuration
DB_URL=jdbc:postgresql://postgres:5432/risk_heatmap_db
DB_USERNAME=postgres
DB_PASSWORD=postgres

# JWT Security
JWT_SECRET=RiskHeatmapVisualiserJwtSecretKey2026VerySecureForSpringBoot
JWT_EXPIRATION=86400000

# Redis Configuration
REDIS_HOST=redis
REDIS_PORT=6379

# Mail Configuration (Optional)
MAIL_USERNAME=your_email@gmail.com
MAIL_PASSWORD=your_app_password

# AI Service Configuration
AI_SERVICE_URL=http://localhost:5000
```

---

## 6. Steps to Run using Docker

This is the recommended method as it sets up all services automatically.

1. Open a terminal (PowerShell or CMD) in the project root folder.
2. Run the following command:

   ```bash
   docker compose up --build
   ```

**What happens next?**
- **PostgreSQL** starts and initializes the database.
- **Redis** starts for caching.
- **Backend** builds and starts on port **8080**.
- **Frontend** builds and starts on port **80**.

Wait until the logs show that the backend and frontend are ready.

---

## 7. Access URLs

Once the containers are running, you can access the application at:

- **Frontend (Web App)**: [http://localhost](http://localhost)
- **Swagger API Docs**: [http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html)
- **Health Check API**: [http://localhost:8080/api/health](http://localhost:8080/api/health)

---

## 8. Demo Login Credentials

The application is pre-seeded with demo accounts for different roles:

| Role | Email | Password |
| :--- | :--- | :--- |
| **ADMIN** | `admin@riskheatmap.com` | `admin123` |
| **MANAGER** | `manager@riskheatmap.com` | `manager123` |
| **VIEWER** | `viewer@riskheatmap.com` | `viewer123` |

---

## 9. How to Stop the Project

To stop all services and remove the containers, run:

```bash
docker compose down
```

---

## 10. Alternative Manual Run

If you prefer to run the components individually without Docker:

### Backend
1. Navigate to the backend folder: `cd backend`
2. Run the application: `mvn spring-boot:run`
3. *Note: You must have PostgreSQL and Redis running locally on your machine.*

### Frontend
1. Navigate to the frontend folder: `cd frontend`
2. Install dependencies: `npm install`
3. Run in development mode: `npm run dev`

---

## 11. Troubleshooting

- **Docker Engine not running**: Ensure Docker Desktop is open and the engine is started.
- **Port already in use**: If port 80 or 8080 is taken, stop the conflicting service or modify the `docker-compose.yml` file.
- **PostgreSQL Connection Failed**: Ensure the `DB_URL` in `.env` matches the service name in `docker-compose.yml` (usually `postgres`).
- **Redis Connection Failed**: Ensure the `REDIS_HOST` is set to `redis` when running in Docker.
- **Frontend not loading**: Clear browser cache or try accessing via `http://localhost:80`.
- **JWT Login Issues**: Ensure the `JWT_SECRET` is at least 32 characters long.

---

## 12. Final Notes

- **Flyway Migrations**: The backend uses Flyway to automatically create all necessary database tables on startup.
- **Data Seeding**: A seeder service automatically inserts the demo users and **30 sample risks** upon the first successful run.
- **No Manual DB Setup**: You do **not** need to manually create the database or run SQL scripts when using the Docker method.

---
*Happy Reviewing!*
