# Hyper-parameter tuning in GCP

## 1. Install google cloud and login https://cloud.google.com/sdk/docs
```
gcloud auth login
```

## 2. If the above installaton shows error- gcloud not found, then run below commond
```
curl https://sdk.cloud.google.com | bash
```

## 3. Also it is important to configure your docker with gcloud, otherwise it will show permission error
```
gcloud auth configure-docker
```
