# Hyper-parameter tuning in GCP

### 1. Install google cloud and login https://cloud.google.com/sdk/docs
```
gcloud auth login
```

### 2. If the above installaton shows error- gcloud not found, then run below commond
```
curl https://sdk.cloud.google.com | bash
```

### 3. Also it is important to configure your docker with gcloud, otherwise it will show permission error
```
gcloud auth configure-docker
```

### 4. Then we will create image, but before that we will export some values

```
#Make a new bucket for your project, and assign that name to BUCKET_NAME
export BUCKET_NAME=hptuning2
#Project id will be ai-project-231602
export PROJECT_ID=ai-project-231602
export JOB_DIR=gs://$BUCKET_NAME/hp_job_dir
export IMAGE_REPO_NAME=scartch_tuning_container
export IMAGE_TAG=scratch_tuning
export IMAGE_URI=gcr.io/$PROJECT_ID/$IMAGE_REPO_NAME:$IMAGE_TAG
export REGION=us-west1
export JOB_NAME=hp_tuning_scratch_container_job_$(date +%Y%m%d_%H%M%S)

```

### 5. git clone this code, in order to use the Dockerfile and hyper_tuning.config file
#feat/AICAR-325-hyperparameter-tuning-scratch branch
```
git clone https://github.com/gaurav67890/Detectron2 detectron2_repo -b feat/AICAR-325-hyperparameter-tuning-scratch
```
