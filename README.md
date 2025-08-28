# Notes App - CI/CD Pipeline

A simple Node.js notes application with comprehensive CI/CD pipeline using GitHub Actions.

## Features

- RESTful API for notes management
- ESLint for code linting
- Jest for unit testing with coverage
- SonarQube integration for code quality
- k6 for performance testing
- Docker containerization
- GitHub Actions CI/CD pipeline

## Local Development

### Prerequisites

- Node.js 18+
- npm
- Docker (optional)
- k6 (for performance testing)

### Setup

```bash
npm install
npm start
```

### Available Scripts

- `npm start` - Start the application
- `npm run dev` - Start with nodemon for development
- `npm test` - Run tests with coverage
- `npm run lint` - Run ESLint
- `npm run k6` - Run k6 performance tests

### Running k6 Tests Locally

1. Install k6:
   ```bash
   # macOS
   brew install k6
   
   # Ubuntu/Debian
   sudo gpg -k
   sudo gpg --no-default-keyring --keyring /usr/share/keyrings/k6-archive-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C5AD17C747E3415A3642D57D77C6C491D6AC1D69
   echo "deb [signed-by=/usr/share/keyrings/k6-archive-keyring.gpg] https://dl.k6.io/deb stable main" | sudo tee /etc/apt/sources.list.d/k6.list
   sudo apt-get update
   sudo apt-get install k6
   ```

2. Start the application:
   ```bash
   npm start
   ```

3. Run k6 tests in another terminal:
   ```bash
   npm run k6
   # or
   k6 run loadtest/script.js
   ```

## CI/CD Pipeline

The GitHub Actions workflow includes the following jobs:

### 1. Lint Job
- Runs ESLint to check code quality
- Fails if any linting errors are found

### 2. Test Job  
- Runs Jest unit tests with coverage
- Uploads coverage reports to Codecov

### 3. SonarQube Analysis
- Performs static code analysis
- Requires `SONAR_TOKEN` and `SONAR_HOST_URL` secrets

### 4. k6 Smoke Test
- Runs performance tests against the application
- Tests basic API endpoints under load

### 5. Build and Push (main branch only)
- Builds Docker image
- Pushes to DockerHub
- Requires `DOCKERHUB_USERNAME` and `DOCKERHUB_TOKEN` secrets

## Required GitHub Secrets

Configure these secrets in your GitHub repository:

- `DOCKERHUB_USERNAME` - Your DockerHub username
- `DOCKERHUB_TOKEN` - Your DockerHub access token  
- `SONAR_TOKEN` - SonarQube authentication token
- `SONAR_HOST_URL` - SonarQube server URL
- `PAT` - GitHub Personal Access Token (if needed for additional integrations)

## API Endpoints

- `GET /` - Health check
- `GET /notes` - List all notes
- `GET /notes/:id` - Get specific note
- `POST /notes` - Create new note
- `PUT /notes/:id` - Update existing note
- `DELETE /notes/:id` - Delete note

## Docker

Build and run with Docker:

```bash
docker build -t notes-app .
docker run -p 3000:3000 notes-app
```
