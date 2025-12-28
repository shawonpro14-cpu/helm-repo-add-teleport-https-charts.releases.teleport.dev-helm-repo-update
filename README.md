cat << EOF > prod-cluster-values.yaml
roles: kube,app,discovery
authToken: 29a15d0164560dfffeb5a53f96c4ca21
proxyAddr: tribals.teleport.sh:443
kubeClusterName: https://tribals.io/
labels:
    teleport.internal/resource-id: e1f2aafe-69d1-4abd-93c8-b89c85885269

enterprise: true
updater:
    enabled: true
    releaseChannel: "stable/cloud"
highAvailability:
    replicaCount: 2
    podDisruptionBudget:
        enabled: true
        minAvailable: 1
EOF

helm install teleport-agent teleport/teleport-kube-agent -f prod-cluster-values.yaml --version 18.5.1 \
--create-namespace --namespace tribals
