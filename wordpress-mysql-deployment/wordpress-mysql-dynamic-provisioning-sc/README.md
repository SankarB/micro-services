# Deploy wordpress and mysql on existing GKE Cluster

## 1. Deploy mysql DB and wordpress Application(secret.yaml used for wordpress & mysql)

    # Use below commands to deploy required resources/objects
       1. kubectl apply -f 01-mysql-sc-pd-standard.yaml
       2. kubectl apply -f 02-mysql-pvc.yaml
       3. kubectl apply -f 03-mysql-service.yaml
       4. kubectl apply -f 04-secret.yaml
       5. kubectl apply -f 05-mysql-deployment.yaml
       6. kubectl apply -f 06-wp-sc-pd-ssd.yaml
       7. kubectl apply -f 07-wp-pvc.yaml
       8. kubectl apply -f 08-wp-service.yaml
       9. kubectl apply -f 09-wp-deployment.yaml

## 2. Check list prior to access Application

    # Check Storage Classess, should be available 2 
        kubect get sc
    # Check Storage Classess, should be available 2, Storage Class will create PersistentVolume dynamicaly
        kubect get pv
    # Check PersistentVolumeClaim, should be available 2
        kubectl get pvc
    # Check Secret, should be available 1 
        kubect get secret
    # Check Service, should be available 2 
        kubect get svc
    # Check Deployment, should be available 2 
        kubect get deploy
    # Check Pods, should be available 2, both should be running state
        kubect get pods

## 3. Verify on https://console.cloud.google.com/ load balancing section for Load Balancer which creates by Auto using Wordpress Service type: LoadBalancer 

## 4. Using Load Balaner newly created IP access your Application.

## 5. Clean up
    
    # clean up the cluster, all deployments, Services, PVC's, PV's and SC
        kubectl delete deployment <deploy-name>
        kubectl delete service <service-name>
        kubectl delete pvc <pvc-name>
        kubectl delete pv <pv-name>
        kubectl delete sc <sc-name>