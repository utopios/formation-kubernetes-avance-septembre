### Image pour Kubebuilder 
superutopios/kubebuilder

### démarrer un conteneur avec l'image kubebuilder 
docker run -v $(pwd)/tp-operator:/workspace -it superutopios/kubebuilder bash


### Étape 1: Initialisation du Projet avec Kubebuilder
```bash
kubebuilder init --domain utopios.net --repo github.com/utopios/webapp
```