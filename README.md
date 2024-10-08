# kube_dashboard

https://fantastic-meme-xqgppp4wjrwhqxg-8001.app.github.dev/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login

minikube start

kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
kubectl create serviceaccount dashboard-admin-sa -n kubernetes-dashboard
kubectl create clusterrolebinding dashboard-admin-sa-binding --clusterrole=cluster-admin --serviceaccount=kubernetes-dashboard:dashboard-admin-sa
kubectl get secret $(kubectl get serviceaccount dashboard-admin-sa -n kubernetes-dashboard -o jsonpath="{.secrets[0].name}") -n kubernetes-dashboard -o jsonpath="{.data.token}" | base64 --decode
kubectl proxy

kubectl apply -f dashboard-admin.yaml
kubectl -n kubernetes-dashboard get serviceaccount
kubectl -n kubernetes-dashboard get clusterrolebinding
kubectl -n kubernetes-dashboard get secret
kubectl apply -f admin-user-token.yaml
kubectl -n kubernetes-dashboard describe secret admin-user-token

eyJhbGciOiJSUzI1NiIsImtpZCI6Ikl2Y2I0cWZOOEtCcnlva29ydnNzbXd0dEFqYlJHcDBpNktuWGdwZ0RXa28ifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJhZG1pbi11c2VyLXRva2VuIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImFkbWluLXVzZXIiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiI0ZjFlNWVhZC0wZjRmLTQwNTgtYjlkNC0xMDZlZDcwN2Q1Y2EiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZXJuZXRlcy1kYXNoYm9hcmQ6YWRtaW4tdXNlciJ9.EcJQ_nUh67jn7cevQGrB_k9vF2YDunx71D-HPfUtG3QNlU9q8v157tRo9UzjSmGEZbyPw4qZ4L-4gxI-KSBXoz1YuQNbcsbz7cLhm9gn-nstcurLOQlUOEkt1myU8nvA36GheJ2q9T-Lcmcly5OsyJr3AvAczhQZ5cI0Fl0ZwM-6Usdn3H_pwenbBCtJx5Au3DFFMQV5aDeKyZ_epio6MwR9f_Tg25p6P58TDB8ij73fjoojIvmlG1FcIghydCrPZyk51-YxY1FtSLNGGaD1g-qUclyex7HFXA63_8SgZ3CJCgpRdgNBccrscVZ1Wpf7ufyXvjFtbXoWpkeL7IoQSw

kubectl apply -f rabbitmq-deployment.yaml
kubectl apply -f producer-deployment.yaml
kubectl apply -f consumer-deployment.yaml

kubectl apply -f producer-service.yaml

kubectl port-forward service/producer 3001:3001