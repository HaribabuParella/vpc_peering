pipeline{
  agent any
  stages{
     stage('Create VPC') {
       steps{
          sh 'gcloud compute networks create vpc1-custom --project=hari-gcp-learning-project  --subnet-mode=custom'
          sh 'gcloud compute networks create vpc2-custom --project=hari-gcp-learning-project  --subnet-mode=custom'
      }
    }
    stage('Create subnets') {
       steps{
           sh 'gcloud compute networks subnets create vpc1-custom-subnets1 --project=hari-gcp-learning-project --range=10.2.0.0/24 --network=vpc1-custom  --region=us-west1'
           sh 'gcloud compute networks subnets create vpc1-custom-subnets2 --project=hari-gcp-learning-project --range=10.3.0.0/24 --network=vpc1-custom  --region=us-west2'
           sh 'gcloud compute networks subnets create vpc1-custom-subnets3 --project=hari-gcp-learning-project --range=10.4.0.0/24 --network=vpc1-custom  --region=us-west4'

           sh 'gcloud compute networks subnets create vpc2-custom-subnets1 --project=hari-gcp-learning-project --range=10.5.0.0/24 --network=vpc2-custom  --region=us-east1'
           sh 'gcloud compute networks subnets create vpc2-custom-subnets2 --project=hari-gcp-learning-project --range=10.6.0.0/24 --network=vpc2-custom  --region=us-east4'
           sh 'gcloud compute networks subnets create vpc2-custom-subnets3 --project=hari-gcp-learning-project --range=10.7.0.0/24 --network=vpc2-custom  --region=us-east5'
      }
    }
    stage('Create vpc peering') {
       steps{
           sh 'gcloud compute networks peerings create vpc1-custom-to-custom --network=vpc1-custom --peer-network=vpc2-custom --export-custom-routes --import-custom-routes --export-subnet-routes-with-public-ip --import-subnet-routes-with-public-ip'
           sh 'gcloud compute networks peerings create vpc2-custom-to-custom --network=vpc2-custom --peer-network=vpc1-custom --export-custom-routes --import-custom-routes --export-subnet-routes-with-public-ip --import-subnet-routes-with-public-ip'
       }
    }
  }
}
