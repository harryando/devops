## [Setup Kubernetes Dashboard](https://koinworks.atlassian.net/wiki/spaces/DEV/pages/254444721/Setup+Kubernetes+Dashboard)

## [Edit Access for Cluster Role](https://koinworks.atlassian.net/wiki/spaces/DEV/pages/254346555/Create+Service+Account+to+Only+View+Logs+Delete+Pods+in+Cluster+Kubernetes)

## [How to use Kubernetes Dashboard](https://koinworks.atlassian.net/wiki/spaces/DEV/pages/226525297/Kubernetes+Dashboard)

## Setting Basic Auth

1. create htaccess
    - `htpasswd -c auth (your user)`
2. create secret from file
    - `kubectl create secret generic basic-auth --from-file=auth -n kubernetes-dashboard`
3. add this in to your kubernetes-dashboard ingress
    - `nginx.ingress.kubernetes.io/auth-realm: Authentication Required`
    - `nginx.ingress.kubernetes.io/auth-secret: basic-auth`
    - `nginx.ingress.kubernetes.io/auth-type: basic`



## Troubleshoot Kubernetes Dashboard

1. [Error Authenticate Kubernetes Dashboard](https://koinworks.atlassian.net/wiki/spaces/DOPS/pages/1387692422/Solve+error+authenticate+kubernetes+dashboard)
