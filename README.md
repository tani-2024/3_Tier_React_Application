Here's a **reframed and professionally polished version** of your `README.md` file for the 3-Tier Application project:

# 🚀 3-Tier Web Application Deployment on Azure

This project demonstrates the deployment of a **3-Tier Web Application** using:

* **Frontend**: React.js (Hosted on Azure VM)
* **Backend**: FastAPI (Python on Azure VM)
* **Database**: Azure SQL Server (PaaS)

---

## 🛠️ Technologies Used

* Cloud Computing (Azure)
* Virtualization
* RESTful APIs
* Git & Version Control
* Networking Concepts

---

## 📦 Project Structure

```
📁 frontend/       --> React.js App
📁 backend/        --> FastAPI App with MS SQL Server
```

---

## 🌐 Frontend Setup (React.js)

### ⚙️ Prerequisites

* Ubuntu-based system
* Node.js v16.x and npm

### 🔧 Installation

```bash
curl -s https://deb.nodesource.com/setup_16.x | sudo bash
sudo apt install nodejs -y
```

### 🛠 Configuration

* Navigate to: `src/TodoApp.js`
* Update the backend URL with your API endpoint
  (e.g., `http://<VM_Private_IP>:8000/api/tasks`)

### 🚀 Run the Application

```bash
npm install        # Install project dependencies
npm start          # Run the app locally
```

---

## 🧠 Backend Setup (Python FastAPI + MS SQL Server)

### ⚙️ Prerequisites

* Ubuntu 20.04 LTS (Azure VM)
* Python & pip installed
* MS SQL Server ODBC Driver (v17)

> Sample Azure VM Image:

```hcl
source_image_reference = {
  publisher = "Canonical"
  offer     = "0001-com-ubuntu-server-focal"
  sku       = "20_04-lts"
  version   = "latest"
}
```

### 🧾 Step-by-Step Instructions

#### 1. Clone the Repository

```bash
git clone <repository_url>
cd <repository_directory>
```

#### 2. Update DB Connection String

* Edit `app.py`
* Replace the `connection_string` with your Azure SQL Server details (ensure ODBC version is 17)

#### 3. Install ODBC Driver & Dependencies

```bash
sudo su
apt-get update && apt-get install -y unixodbc unixodbc-dev
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/debian/10/prod.list > /etc/apt/sources.list.d/mssql-release.list
apt-get update
ACCEPT_EULA=Y apt-get install -y msodbcsql17
```

#### 4. Install Python Dependencies

```bash
pip install -r requirements.txt
```

#### 5. Run the FastAPI App

```bash
uvicorn app:app --host 0.0.0.0 --port 8000
```

---

## 📡 Accessing the Application

Once running, access the backend API:

```
http://<VM_Public_IP>:8000
```

Or test via Swagger UI:

```
http://<VM_Public_IP>:8000/docs
```

---

## 🔁 API Endpoints

| Method | Endpoint               | Description         |
| ------ | ---------------------- | ------------------- |
| GET    | `/api/tasks`           | List all tasks      |
| GET    | `/api/tasks/{task_id}` | Get task by ID      |
| POST   | `/api/tasks`           | Create a new task   |
| PUT    | `/api/tasks/{task_id}` | Update a task by ID |
| DELETE | `/api/tasks/{task_id}` | Delete a task by ID |

---

## 📌 Notes

* Use **private IP** of the backend VM in the frontend app when both tiers are in the same VNet/subnet.
* Configure Azure NSG rules to allow traffic between frontend and backend as well as external access on ports (e.g., 80/443/8000).

---

Let me know if you'd like to include deployment architecture diagrams or Azure resource provisioning steps using Terraform or ARM templates.
