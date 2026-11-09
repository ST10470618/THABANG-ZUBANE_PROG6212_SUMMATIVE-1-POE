# 🏁 RaceDay Application

An enterprise-ready ASP.NET Core web application and RESTful API designed for managing athletic events, venues, participants, and media storage. The application is built using a decoupled architecture separating the client view layer from the backend data services, complete with cloud blob storage, containerization, and continuous integration capabilities.

---

## 🛠️ Technology Stack
* **Backend API:** ASP.NET Core Web API (.NET 8.0)
* **Frontend Client:** ASP.NET Core MVC (.NET 8.0)
* **Data Persistence:** SQL Server LocalDB with Entity Framework Core
* **Cloud Storage:** Azure Blob Storage (Azurite / Local Emulator compatible)
* **Containerization:** Docker (Multi-stage build)
* **CI/CD Pipeline:** GitHub Actions

---

## 🚀 Project Architecture

The solution follows a modern client-server architecture split across two main projects:

1. **`RaceDayApi` (Backend):**
   * Exposes RESTful endpoints running on `https://localhost:7280`.
   * Manages Entity Framework Core database context and data models.
   * Handles cloud image uploads through `BlobService.cs` using Azure Storage Blob SDK.
   * Contains robust exception handling middleware to return structured JSON responses.

2. **`RaceDayMvc` (Frontend):**
   * Serves user-facing views rendered via Razor syntax.
   * Consumes API endpoints using typed `HttpClient` services (`ApiService.cs`).
   * Implements fallback UI logic and fault tolerance against backend service interruptions.

---

## ⚙️ Getting Started & Local Setup

### Prerequisites
* [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
* [Visual Studio 2022](https://visualstudio.microsoft.com/) (with ASP.NET and web development workload)
* SQL Server LocalDB
* Azure Storage Emulator / Azurite (Optional, for local blob testing)

### Configuration
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/RaceDay.git
   cd RaceDay
   ```
2. Verify `appsettings.json` in `RaceDayApi` contains the valid connection strings:
   ```json
   {
     "ConnectionStrings": {
       "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=RaceDayDb;Trusted_Connection=True;MultipleActiveResultSets=true",
       "AzureBlobStorage": "UseDevelopmentStorage=true"
     }
   }
   ```

### Execution (Visual Studio)
1. Open `RaceDay.sln` in Visual Studio.
2. Right-click the Solution in Solution Explorer and select **Configure Startup Projects...**
3. Choose **Multiple startup projects**, then set both `RaceDayApi` and `RaceDayMvc` to **Start**.
4. Press **F5** to build and launch both projects simultaneously.

---

## 🐳 Docker Containerization

A multi-stage `Dockerfile` is provided in the root directory for building light runtime images:

```bash
# Build the Docker image
docker build -t raceday-api:latest .

# Run the container locally
docker run -d -p 8080:8080 --name raceday_container raceday-api:latest
```

---

## 🔄 CI/CD Automation

Automated build, restore, and test checks are managed via **GitHub Actions**. The pipeline is defined in `.github/workflows/dotnet.yml` and executes on every push or pull request to the main branch:

* **Workflow steps:**
  1. Checks out repository code.
  2. Sets up .NET 8 SDK environment.
  3. Restores dependencies (`dotnet restore`).
  4. Builds the solution in Release configuration (`dotnet build`).
  5. Executes unit/integration test suites (`dotnet test`).

---

## 📝 Authors & Project Context
* **Project:** RaceDay Event Management System (Part 3 POE)
* **Framework:** ASP.NET Core .NET 8.0