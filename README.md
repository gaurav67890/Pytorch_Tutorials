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

### 5. Create the image using the Dockerfile from the above code.
```
docker build --no-cache --build-arg USER_ID=$UID -f Dockerfile -t $IMAGE_URI ./
```

### 5. Get the image id for the above image, and use it to push the docker image to gcp
```
docker tag image_ID $IMAGE_URI
docker push $IMAGE_URI

```

### 6. We are almost done, now we just need to run this below command and start the gcp training
```
gcloud ai-platform jobs submit training $JOB_NAME --job-dir $JOB_DIR --region $REGION --master-image-uri $IMAGE_URI --config hyper_tuning.yaml
```
### 7. See the status of job using
```
gcloud ai-platform jobs describe hp_tuning_scratch_container_job_20200819_204006

#this will generate the url for the job status and log which you can click. 
```
### 8. Mission accomplished, Have fun tuning !

![alt-text][https://github.com/gaurav67890/Detectron2/blob/feat/AICAR-325-hyperparameter-tuning-scratch/landscape-1467725698-leonardo-di-caprio-great-gatsby.gif]


