### Image pour Kubebuilder 
superutopios/kubebuilder

### démarrer un conteneur avec l'image kubebuilder 
docker run -v $(pwd)/tp-operator:/workspace -it superutopios/kubebuilder bash


### Étape 1: Initialisation du Projet avec Kubebuilder
```bash
kubebuilder init --domain utopios.net --repo github.com/utopios/webapp
```

## Etape 2: Création de l'api pour la gestion de ressources

```bash
kubebuilder create api --group utopios.net --version v1 --kind WebApp
```
