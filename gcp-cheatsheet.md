# Google Cloud CLI Cheatsheet

> The Google Cloud CLI manages Google Cloud resources, configuration, and operational workflows from the command line.

## Table of Contents
- [Config & Auth](#config--auth)
- [Projects](#projects)
- [Compute Engine](#compute-engine)
- [Cloud Storage](#cloud-storage)
- [GKE](#gke)
- [IAM](#iam)
- [Networking](#networking)
- [Cloud Functions](#cloud-functions)
- [Pub/Sub](#pubsub)
- [Logging](#logging)

## Config & Auth

| Command | Description |
| --- | --- |
| `gcloud auth login` | Sign in with a Google user account. |
| `gcloud auth application-default login` | Create local Application Default Credentials. |
| `gcloud auth list` | List authenticated accounts and the active account. |
| `gcloud config list` | Display the active gcloud configuration. |
| `gcloud config set project my-project-id` | Set the default project for subsequent commands. |
| `gcloud config configurations create staging` | Create a named gcloud configuration. |

## Projects

| Command | Description |
| --- | --- |
| `gcloud projects list` | List projects visible to the active account. |
| `gcloud projects create my-project-id --name="My Project"` | Create a Google Cloud project. |
| `gcloud projects describe my-project-id` | Display project metadata. |
| `gcloud projects get-iam-policy my-project-id` | Retrieve a project's IAM policy. |
| `gcloud services list --enabled` | List APIs enabled for the active project. |
| `gcloud services enable compute.googleapis.com` | Enable a Google Cloud API. |

## Compute Engine

| Command | Description |
| --- | --- |
| `gcloud compute instances list` | List Compute Engine VM instances. |
| `gcloud compute instances create vm-app --zone=us-central1-a --machine-type=e2-medium --image-family=debian-12 --image-project=debian-cloud` | Create a VM from a public image family. |
| `gcloud compute instances start vm-app --zone=us-central1-a` | Start a stopped VM instance. |
| `gcloud compute instances stop vm-app --zone=us-central1-a` | Stop a running VM instance. |
| `gcloud compute ssh vm-app --zone=us-central1-a` | Open an SSH session to a VM. |
| `gcloud compute instances delete vm-app --zone=us-central1-a` | Delete a VM instance. |

## Cloud Storage

| Command | Description |
| --- | --- |
| `gcloud storage buckets list` | List Cloud Storage buckets. |
| `gcloud storage buckets create gs://my-bucket --location=us-central1` | Create a Cloud Storage bucket. |
| `gcloud storage ls gs://my-bucket/` | List objects in a bucket. |
| `gcloud storage cp file.txt gs://my-bucket/` | Upload a local file to Cloud Storage. |
| `gcloud storage rsync --recursive ./site gs://my-bucket/site` | Synchronize a local directory to a bucket prefix. |
| `gsutil iam get gs://my-bucket` | Display a bucket's IAM policy. |

## GKE

| Command | Description |
| --- | --- |
| `gcloud container clusters list` | List GKE clusters. |
| `gcloud container clusters create-auto app-cluster --region=us-central1` | Create an Autopilot GKE cluster. |
| `gcloud container clusters describe app-cluster --region=us-central1` | Display GKE cluster configuration. |
| `gcloud container clusters get-credentials app-cluster --region=us-central1` | Configure kubectl access to a GKE cluster. |
| `gcloud container clusters resize app-cluster --node-pool=default-pool --num-nodes=3 --region=us-central1` | Resize a Standard cluster node pool. |
| `gcloud container clusters delete app-cluster --region=us-central1 --quiet` | Delete a GKE cluster without prompting. |

## IAM

| Command | Description |
| --- | --- |
| `gcloud projects get-iam-policy my-project-id --format=json` | Export a project's IAM policy as JSON. |
| `gcloud projects add-iam-policy-binding my-project-id --member=user:user@example.com --role=roles/viewer` | Grant a project role to a principal. |
| `gcloud projects remove-iam-policy-binding my-project-id --member=user:user@example.com --role=roles/viewer` | Revoke a project role from a principal. |
| `gcloud iam service-accounts list` | List service accounts in the active project. |
| `gcloud iam service-accounts create deployer --display-name="CI Deployer"` | Create a service account. |
| `gcloud iam service-accounts keys list --iam-account=deployer@my-project-id.iam.gserviceaccount.com` | List user-managed service account keys. |

## Networking

| Command | Description |
| --- | --- |
| `gcloud compute networks list` | List VPC networks. |
| `gcloud compute networks create app-vpc --subnet-mode=custom` | Create a custom-mode VPC network. |
| `gcloud compute networks subnets create app-subnet --network=app-vpc --region=us-central1 --range=10.10.0.0/24` | Create a VPC subnet. |
| `gcloud compute firewall-rules list` | List VPC firewall rules. |
| `gcloud compute firewall-rules create allow-https --network=app-vpc --allow=tcp:443 --source-ranges=10.0.0.0/8` | Create an ingress firewall rule. |
| `gcloud compute addresses list --regions=us-central1` | List regional external IP addresses. |

## Cloud Functions

| Command | Description |
| --- | --- |
| `gcloud functions list --gen2` | List second-generation Cloud Functions. |
| `gcloud functions describe hello --gen2 --region=us-central1` | Display a second-generation function's configuration. |
| `gcloud functions deploy hello --gen2 --runtime=nodejs20 --region=us-central1 --source=. --entry-point=hello --trigger-http --allow-unauthenticated` | Deploy an HTTP-triggered second-generation function. |
| `gcloud functions call hello --gen2 --region=us-central1 --data='{"name":"Ada"}'` | Invoke a second-generation function synchronously. |
| `gcloud functions logs read hello --gen2 --region=us-central1 --limit=50` | Read recent function log entries. |
| `gcloud functions delete hello --gen2 --region=us-central1 --quiet` | Delete a second-generation function. |

## Pub/Sub

| Command | Description |
| --- | --- |
| `gcloud pubsub topics list` | List Pub/Sub topics. |
| `gcloud pubsub topics create events` | Create a Pub/Sub topic. |
| `gcloud pubsub subscriptions create events-worker --topic=events` | Create a pull subscription for a topic. |
| `gcloud pubsub topics publish events --message="deployment complete"` | Publish a message to a topic. |
| `gcloud pubsub subscriptions pull events-worker --auto-ack --limit=10` | Pull and acknowledge available messages. |
| `gcloud pubsub subscriptions list` | List Pub/Sub subscriptions. |

## Logging

| Command | Description |
| --- | --- |
| `gcloud logging logs list` | List log names in the active project. |
| `gcloud logging read 'severity>=ERROR' --limit=50 --format=json` | Query recent error-level log entries. |
| `gcloud logging read 'resource.type="gce_instance"' --limit=20` | Query log entries from Compute Engine resources. |
| `gcloud logging sinks list` | List configured log sinks. |
| `gcloud logging sinks create archive-sink storage.googleapis.com/my-log-bucket --log-filter='severity>=WARNING'` | Create a sink that exports warning and higher logs. |
| `gcloud logging metrics list` | List logs-based metrics. |
