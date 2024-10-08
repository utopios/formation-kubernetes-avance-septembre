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

## Code de webapp_types.go

```go
/*
Copyright 2024.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
*/

package v1

import (
	metav1 "k8s.io/apimachinery/pkg/apis/meta/v1"
)

// EDIT THIS FILE!  THIS IS SCAFFOLDING FOR YOU TO OWN!
// NOTE: json tags are required.  Any new fields you add must have json tags for the fields to be serialized.

// WebAppSpec defines the desired state of WebApp
type WebAppSpec struct {
	// INSERT ADDITIONAL SPEC FIELDS - desired state of cluster
	// Important: Run "make" to regenerate code after modifying this file

	// Foo is an example field of WebApp. Edit webapp_types.go to remove/update
	AppName          string `json:"appName"`
	Image            string `json:"image"`
	DBImage          string `json:"dbImage"`
	Replicas         int32  `json:"replicas"`
	DBSize           string `json:"dbSize"`
	AutoScaleEnabled bool   `json:"autoScaleEnabled"`
	TrafficThreshold int32  `json:"trafficThreshold"`
}

// WebAppStatus defines the observed state of WebApp
type WebAppStatus struct {
	// INSERT ADDITIONAL STATUS FIELD - define observed state of cluster
	// Important: Run "make" to regenerate code after modifying this file
	AvailableReplicas int32 `json:"availableReplicas"`
}

// +kubebuilder:object:root=true
// +kubebuilder:subresource:status

// WebApp is the Schema for the webapps API
type WebApp struct {
	metav1.TypeMeta   `json:",inline"`
	metav1.ObjectMeta `json:"metadata,omitempty"`

	Spec   WebAppSpec   `json:"spec,omitempty"`
	Status WebAppStatus `json:"status,omitempty"`
}

// +kubebuilder:object:root=true
// +kubebuilder:subresource:status
// +kubebuilder:printcolumn:name="AppName",type="string",JSONPath=".spec.appName"
// +kubebuilder:printcolumn:name="Replicas",type="integer",JSONPath=".spec.replicas"
// +kubebuilder:printcolumn:name="AutoScale",type="boolean",JSONPath=".spec.autoScaleEnabled"

// WebAppList contains a list of WebApp
type WebAppList struct {
	metav1.TypeMeta `json:",inline"`
	metav1.ListMeta `json:"metadata,omitempty"`
	Items           []WebApp `json:"items"`
}

func init() {
	SchemeBuilder.Register(&WebApp{}, &WebAppList{})
}

```

### Etape 3 => génération des CRDs 

```bash
make manifests
```

### Etape 4 => déployer les crds dans le cluster
kubectl apply -f <path/to/crd>

```bash
kubectl apply -f config/crd/bases/utopios.net.utopios.net_webapps.yaml 
```

### Etape 5 => implémenter le controller pour les CRs

##  Etape 6 => build de l'application controller
```
make install
make run
```

## Etape 7 => déployer une cr
kubectl apply -f config/samples/utopios.net_v1_webapp.yaml



# API Aggregation

Endpoint sous le format 
apis/apiregistration.k8s.io/v1/apiservices/{name}

Pour y accéder 

kubectl get --raw /apis/aggregator.example.com/v1