1.запустить бд
docker run -d --name postgres-db -e POSTGRES_USER=user -e POSTGRES_PASSWORD=pass -e POSTGRES_DB=mydb -p 5432:5432 postgres
2.Запустить миникуб
minikube start --driver=docker
3.Применить манифесты кубернетеса
kubectl apply -f .
4.запустить сервис для фронтенда
minikube service frontend --url

Запуск мониторинга
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo update

kubectl create namespace monitoring

helm install prometheus prometheus-community/kube-prometheus-stack --namespace monitoring

kubectl port-forward -n monitoring svc/prometheus-grafana 3001:80

login:    admin
Password:
 kubectl get secret --namespace monitoring -l app.kubernetes.io/component=admin-secret -o jsonpath="{.items[0].data.admin-password}" | % { [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($_)) }

 В настройках Графаны импортировать дашборд  id 12486 Full node exporter