### Image docker pour le webhook pour la conversion du TP 1 (slide 55)
superutopios/formationkubernetestp1

### Commande de correction 

```bash
# Déploiement du webhook
kubectl apply -f k8s.yaml

# Déploiement du crd
kubectl apply -f crd.yaml

# Déploiement des ressources
kubectl apply -f v1.yaml
kubectl apply -f v2.yaml

kubectl get acfg.v1.myorg.com -o yaml 
```