# Quickstart- run nginx

## Steps : 

### Step 1:

```
cd docs\terraform-quickstart
mkdir terraform-docker-demo && cd $_
```

### Step 2: main.tf
```
terraform {
  required_providers {
    docker = {
      source = "terraform-providers/docker"
    }
  }
}

provider "docker" {
  host    = "npipe:////.//pipe//docker_engine"
}

resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = false
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "tutorial"
  ports {
    internal = 80
    external = 8000
  }
}

```
### Step 3: Initialize the project, which downloads a plugin that allows Terraform to interact with Docker.
```
terraform init
```

### Step 4: Provision the NGINX server container with apply
```
terraform apply
```

### Step 5: verify
```
Verify the existence of the NGINX container by visiting localhost:8000 in your web browser or 
running docker ps to see the container.
```

### Step 6: To stop the container
```
terraform destroy
```


## Reference
```
https://learn.hashicorp.com/tutorials/terraform/install-cli
```

## Next Step 
Create real infrastructure in the cloud

### Amazon Web Services (AWS) - https://learn.hashicorp.com/tutorials/terraform/aws-build
### Azure	- https://learn.hashicorp.com/tutorials/terraform/azure-build
### Google Cloud Platform (GCP)	- https://learn.hashicorp.com/tutorials/terraform/google-cloud-platform-build