# mysql-kubernetes

Before deploying MysQl service, We need to configure storage to persistent data.

* Create a storage class.
```
kubectl create -f storage-class.yaml
```

* Create a `PersistentVolumeClaim`
```
kubectl create -f pvc.yaml
```
Now, We have created storage for database, We need to create a kubernetes secret to store mysql root password.

* Create a secret.

Before creating a secret we need to encode the password and update encoded password into the kubernetes secret.
```
echo -n 'yourpassword' | base64
```
Copy the output and update it in `secret.yaml` file and create a secret.
```
kubectl create -f secret.yaml
```
We have stored the MysQl root password into the kubernetes secret. Now we can create a deployment of MysQl service.

* Create a Deployment.
I have update `secret` in as `env` in `eployment.yaml` and also updated storage information. Let's create a deployment
```
kubectl create deployment.yaml
```
Now we have deployed MysQl service on Kuberntes, We have to expose that to access the service.

* Expose MysQl to the Load balancer
```
kubectl create -f service.yaml
```
After creating `service.yaml` file you will get the load balancer IP, You can access mysql using it.



