# tta-0710

Argo CD로 nginx만 배포하는 최소 예제입니다.

## 구조

```text
.
├── apps
│   └── nginx
│       ├── deployment.yaml
│       ├── kustomization.yaml
│       ├── namespace.yaml
│       └── service.yaml
└── argocd
    └── nginx-application.yaml
```

## 배포 방법

Argo CD가 설치된 클러스터에서 아래 매니페스트를 적용합니다.

```bash
kubectl apply -f argocd/nginx-application.yaml
```

Argo CD는 이 저장소의 `apps/nginx` 경로를 바라보고 nginx 리소스만 동기화합니다.

```yaml
source:
  repoURL: https://github.com/seungbaeji/tta-0710.git
  targetRevision: main
  path: apps/nginx
```

다른 저장소나 브랜치를 사용할 경우 [argocd/nginx-application.yaml](/Users/seungbaeji/Workspace/tta-0710/argocd/nginx-application.yaml)의 `repoURL` 또는 `targetRevision` 값을 바꾸면 됩니다.

## 확인

```bash
kubectl -n argocd get applications.argoproj.io nginx
kubectl -n nginx get deploy,svc,pod
```
