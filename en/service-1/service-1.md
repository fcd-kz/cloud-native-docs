# Service 1 Documentation

This folder contains the documentation for **Service 1** of Freedom Cloud.  
Here you will find an overview, usage instructions, API references, and examples.  

## Overview
Service 1 provides a core feature of the Freedom Cloud platform.  
It allows clients to provision, manage, and monitor resources through a unified interface.

## Getting Started
1. Make sure you have access to the Freedom Cloud portal.  
2. Navigate to **Service 1** in the catalog.  
3. Follow the quick-start guide to create your first resource.  

## API Reference
Service 1 exposes REST endpoints via the **public API**:  

- `POST /v1/service-1/resources` — create a new resource  
- `GET /v1/service-1/resources/{id}` — get resource details  
- `DELETE /v1/service-1/resources/{id}` — remove a resource  
- `DELETE /v1/service-1/resources/{id}` — remove a resource  


## Examples
```bash
# Create a new resource
curl -X POST https://api.freedom-cloud.io/v1/service-1/resources \
  -H "Authorization: Bearer <token>" \
  -d '{"name": "my-resource"}'