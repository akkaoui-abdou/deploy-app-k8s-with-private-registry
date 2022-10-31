# Pull Image from Private Docker Registry in Kubernetes cluster


  kubectl create secret docker-registry my-registry-key \
--docker-server=https://index.docker.io/v1/ \
--docker-username=<your-registry-username> \
--docker-password=<your-password> \
--docker-email=<your-email@gmail.com>
