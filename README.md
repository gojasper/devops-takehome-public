```
       _                             _____                            
      | |                           |  __ \                           
      | | __ _ ___ _ __   ___ _ __  | |  | | _____   _____  _ __  ___ 
  _   | |/ _` / __| '_ \ / _ \ '__| | |  | |/ _ \ \ / / _ \| '_ \/ __|
 | |__| | (_| \__ \ |_) |  __/ |    | |__| |  __/\ V / (_) | |_) \__ \
  \____/ \__,_|___/ .__/ \___|_|    |_____/ \___| \_/ \___/| .__/|___/
                  | |                                      | |        
                  |_|                                      |_|        
```

# DevOps Engineer Take Home Exercise

Thank you for your interest in Jasper! This exercise is designed to assess your profeciency with Docker and Kubernetes.

## Overview

You'll be provided with a Docker image that runs a custom backend service.
This backend service provides Satellite Data (think Hubble) and can do the following:
1. Reports on satellite configuration.
2. Reports on satellite mirror status.

### Task Overview

1. Run the service locally via Docker.
2. Deploy the service to a local Kubernetes cluster.
3. Create a CronJob that periodically checks and logs the satellite status.

## Prerequisites

- Docker installed and running
- A local Kubernetes cluster (minikube, kind, k3d, or similar)
- `kubectl` configured to work with your local cluster
- `helm` installed (v3.x)

## The Satellite Service

- Listens on port `8080` for GET requests (for example `curl localhost:8080/`)
- Listens for GET requests on `/satellite/status`

## Exercise Tasks

### Task 1: Run the Satellite Service Docker Image Locally

**Objective**: Run the Docker container locally. The container will fail to start initially
due to configuration errors. You need to debug and fix the startup issues.

**Requirements**:
- Clone this repository locally
  - `cd devops-takehome-public`
  - Mac arm64: `docker load -i devops-takehome-arm64.tar`
  - Windows/Linux: `docker load -i devops-takehome-arm64.tar`
- Run the Docker container
  - Mac arm64: `docker run satellite-server:arm64`
  - Windows/Linux: `docker run satellite-server:amd64`
- Identify why the container fails to start
- Fix the issue(s) and get the service running
- Verify the service is accessible at `http://localhost:8080`

**Hints**:
- Look at container logs

### Task 2: Deploy to Kubernetes with Helm

**Objective**: Deploy the satellite service to your local Kubernetes cluster using a Helm chart.

**Requirements**:
- Create a Helm chart for the satellite service
- The chart should include:
  - Deployment with appropriate resource limits and requests
  - Service to expose the application
  - Proper labels and selectors
  - Environment variables
- Deploy the chart to your cluster
- Verify the service is accessible within the cluster

**Considerations**:
- Use Kubernetes best practices
- Make the configuration maintainable and extensible
- Consider how you would handle different environments (dev, staging, prod)

### Task 3: Create a CronJob for Status Monitoring

**Objective**: Create a Kubernetes CronJob that periodically queries the `/satellite/status` endpoint and monitors for satellite health.

**Requirements**:
- Create a CronJob that runs every 2 minutes
- The job should:
  - Query the `/satellite/status` endpoint
  - Log the response
  - (**Bonus**) Report Healthy or Unhealthy based on the different mirror statuses
- Include the CronJob in your Helm chart
- Verify the CronJob runs successfully and logs appear

**Considerations**:
- How will the CronJob access the service?
- What happens if the service is temporarily unavailable?
- How would you monitor the CronJob's success/failure?

## Deliverables

Please provide a **public** github repo url with the following sections.

*email your Jasper recruiter with the github link*

1. **Working Docker setup** - Documentation on how to run the Docker image with the correct configuration
2. **Helm chart** - Complete Helm chart in a `helm/` directory with:
   - `Chart.yaml`
   - `values.yaml`
   - `templates/` directory with all necessary Kubernetes manifests
3. **Documentation** - A brief markdown document explaining:
   - How to run the Docker image with the correct configuration
   - How to deploy using Helm
   - How to verify everything is working
   - Screenshots of the deployment in minikube and http response from the running pod
   - Any additional functionality you added

## Evaluation Criteria

We'll be evaluating:

- **Understanding of Docker**: How you debug and resolve issues
- **K8s proficiency**: Understanding of K8s resources, networking, and best practices
- **Helm proficiency**: Chart structure, templating, and config management

You can use your own creative judgement to expand upon each task if it would help to demonstrate a more thorough understanding of k8s, Helm, and Docker.

## Time Estimate

This exercise should take less than 3 hours to complete.

## Questions

If you run into any issues preventing work on this take home exercise, reach out to us.
