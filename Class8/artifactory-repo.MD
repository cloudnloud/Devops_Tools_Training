## Configure google artifact registry

- go to your artifact registry in google cloud console -- > click configure instructions -> paste that entry into your pom.xml file and save it to github repo


## in  jenkins server
- install gcloud cli # https://cloud.google.com/sdk/docs/install#rpm

- authenticate your google cloud from jenkins vm.test from your jenkins server with below command to make sure your jenkins server are talking to your cloud without any permission issues


- gcloud storage buckets create gs://rangabkdba --project=eng-genius-423708-p9 --default-storage-class=STORAGE_CLASS --location=BUCKET_LOCATION --uniform-bucket-level-access

## verify with below command to see your artifact repo


- gcloud config set project eng-genius-423708-p9

- gcloud artifacts repositories list

- gcloud artifacts packages list --repository=devopsrepo --location us 

## set up the github maven pipeline in jenkins

## now run the jenkins pipeline and check weather war file is getting created.

- now we need to push the war file to google artifact registry

## need a gcloud command to push the war file to google artifact registry
