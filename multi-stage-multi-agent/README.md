# Jenkins Pipeline for Back-end and Front-end

## Overview
This Jenkins pipeline automates the build process for a project that has separate **Back-end** (Java/Maven) and **Front-end** (Node.js) components. The pipeline uses **Docker** to provide isolated environments for each stage.

## Pipeline Structure
The pipeline consists of two stages:

1. **Back-end Stage**
   - Runs inside a Docker container with the **Maven (3.8.1) and OpenJDK 11** environment.
   - Verifies the Maven installation.

2. **Front-end Stage**
   - Runs inside a Docker container with **Node.js (16-alpine)**.
   - Verifies the Node.js installation.

## Pipeline Script
```groovy
pipeline {
  agent none
  stages {
    stage('Back-end') {
      agent {
        docker { image 'maven:3.8.1-adoptopenjdk-11' }
      }
      steps {
        sh 'mvn --version'
      }
    }
    stage('Front-end') {
      agent {
        docker { image 'node:16-alpine' }
      }
      steps {
        sh 'node --version'
      }
    }
  }
}
```

## Why Use Multiple Stages?
- **Separation of Concerns**: Each component (Back-end & Front-end) runs in its own stage.
- **Better Debugging**: Errors are isolated per stage.
- **Parallel Execution (Optional)**: Can be modified to run stages in parallel.
- **Resource Optimization**: Each stage runs in a clean Docker environment.

## Prerequisites
- Jenkins installed with **Docker support**.
- Docker installed and running.
- Access to **Maven** and **Node.js** images from Docker Hub.

## How to Use
1. Save the pipeline script in your Jenkins project.
2. Run the pipeline.
3. Verify the output to ensure both stages execute successfully.

## Expected Output
- Back-end stage: Displays Maven version.
- Front-end stage: Displays Node.js version.

## Future Enhancements
- Add **unit tests** for both back-end and front-end.
- Implement **artifact storage** for the built applications.
- Introduce **parallel execution** for efficiency.

---

For any issues, feel free to raise a discussion or open an issue!

t

