# GitHub Actions Setup Instructions

This guide will walk you through setting up GitHub Actions workflows for your AI-Powered Rasta Reggae Radio project. These workflows will automate the deployment process to AWS, Azure, and Vercel.

## Step 1: Create the Workflow Directory Structure

First, you need to create the `.github/workflows` directory in your repository:

```bash
mkdir -p .github/workflows
```

## Step 2: Add the Workflow Files

Create the following three workflow files in the `.github/workflows` directory:

### 1. Azure Deployment Workflow (.github/workflows/azure-deploy.yml)

This workflow handles deployment of AI components to Azure.

### 2. AWS Deployment Workflow (.github/workflows/aws-deploy.yml)

This workflow handles deployment of streaming infrastructure to AWS.

### 3. Frontend Deployment Workflow (.github/workflows/frontend-deploy.yml)

This workflow handles deployment of the React.js frontend to Vercel.

## Step 3: Configure GitHub Secrets

For security, you need to add the following secrets to your GitHub repository:

1. Go to your repository on GitHub
2. Click on "Settings" > "Secrets and variables" > "Actions"
3. Click on "New repository secret"
4. Add the following secrets:

### AWS Secrets
- `AWS_ACCESS_KEY_ID`: Your AWS access key
- `AWS_SECRET_ACCESS_KEY`: Your AWS secret key
- `AWS_REGION`: AWS region (e.g., us-east-1)
- `AWS_KEY_NAME`: Name of your EC2 key pair
- `AWS_KEY_PATH`: Path to your EC2 key pair file
- `AWS_HOSTED_ZONE_ID`: Route 53 hosted zone ID for your domain

### Azure Secrets
- `AZURE_CREDENTIALS`: JSON credentials for Azure service principal
- `AZURE_RESOURCE_GROUP`: Name of your Azure resource group
- `AZURE_LOCATION`: Azure region (e.g., eastus)
- `AZURE_CONTAINER_REGISTRY`: URL of your Azure Container Registry
- `AZURE_REGISTRY_USERNAME`: Username for ACR
- `AZURE_REGISTRY_PASSWORD`: Password for ACR
- `AZURE_FUNCTION_APP_NAME`: Name of your Azure Function App

### Vercel Secrets
- `VERCEL_TOKEN`: Vercel API token
- `VERCEL_ORG_ID`: Vercel organization ID
- `VERCEL_PROJECT_ID`: Vercel project ID
- `API_URL`: URL for the backend API
- `STREAMING_URL`: URL for the streaming server
- `SUPABASE_URL`: URL for your Supabase project
- `SUPABASE_ANON_KEY`: Anon key for Supabase authentication

## Step 4: Create a Service Principal for Azure

To create an Azure service principal and get the credentials JSON:

```bash
az ad sp create-for-rbac --name "RastaRadioDeployment" --role contributor \
                          --scopes /subscriptions/{subscription-id}/resourceGroups/{resource-group} \
                          --sdk-auth
```

The output JSON should be stored as the `AZURE_CREDENTIALS` secret.

## Step 5: Get Vercel Project Information

To get your Vercel organization ID and project ID:

1. Install Vercel CLI: `npm i -g vercel`
2. Run `vercel login`
3. Run `vercel link` in your project directory
4. Check the `.vercel/project.json` file for your project ID
5. Get your organization ID from the Vercel dashboard

## Step 6: Test the Workflows

After setting up the workflows and secrets, you can manually trigger them:

1. Go to the "Actions" tab in your repository
2. Select the workflow you want to run
3. Click "Run workflow" > "Run workflow"

This will start the deployment process according to the workflow configuration.
