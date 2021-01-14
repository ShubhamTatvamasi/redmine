# redmine

deploy redmine:
```bash
kubectl create deployment redmine --image=redmine
kubectl expose deployment redmine --port=3000 --name=redmine
```
> user: `admin` pass: `admin`

delete everything:
```bash
kubectl delete deploy/redmine svc/redmine ing/redmine
```

create ingress value:
```bash
kubectl apply -f - << EOF
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: redmine
spec:
  tls:
    - hosts:
      - redmine.k8s.shubhamtatvamasi.com
      secretName: letsencrypt
  rules:
    - host: redmine.k8s.shubhamtatvamasi.com
      http:
        paths:
        - path: /
          backend:
            serviceName: redmine
            servicePort: 3000
EOF
```
