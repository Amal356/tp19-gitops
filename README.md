# tp19-gitops : dépôt GitOps (source de vérité) du TP19

> Cours DevOps & Cloud de M. Wahid, Partie 7 : GitOps avec Argo CD. Étudiante : Amal Jemli.
> Rendu du TP : [devops-partie7](https://github.com/Amal356/devops-partie7).

Ce dépôt décrit **l'état désiré** du cluster. Argo CD le compare en permanence au cluster et le réconcilie. On ne fait plus de `kubectl apply` à la main : **chaque changement passe par un commit ou une Pull Request**.

```
base/                 Deployment + Service + ConfigMap (whoami)
envs/dev/             1 réplica, version promue en premier
envs/staging/         2 réplicas
envs/prod/            3 réplicas, synchronisation manuelle
argocd/               Application (dev) et ApplicationSet (dev, staging, prod)
```

La version d'un environnement est la ligne `images: newTag` de son `kustomization.yaml` : **promouvoir = modifier cette ligne par Pull Request**, sans reconstruire l'image.
