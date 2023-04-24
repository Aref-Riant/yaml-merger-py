# yaml-merger-py
Python script to merge YAML files together

this script could merge partial yaml files into bigger ones
specially to deep merge patial values.yaml helm files (used in `helm install --values`) into complete values files (used in `helm install -f`)
with best effort to preserve comments, formatting, and order of items.

# Example:

### values.yaml:
```
# Default values for kube-prometheus-stack.
# This is a YAML-formatted file.
# Declare variables to be passed into your templates.

## Provide a name in place of kube-prometheus-stack for `app:` labels
##
nameOverride: ""

## Override the deployment namespace
##
namespaceOverride: ""

## Provide a k8s version to auto dashboard import script example: kubeTargetVersionOverride: 1.16.6
##
kubeTargetVersionOverride: ""
.
.
.
```

### values-partial.yaml:
```
namespaceOverride: "monitoring"
```

### Command:
```
python yaml-merger.py values.yaml values-partial.yaml > values-merged.yaml
```

### values-merged.yaml:
```
# Default values for kube-prometheus-stack.
# This is a YAML-formatted file.
# Declare variables to be passed into your templates.

## Provide a name in place of kube-prometheus-stack for `app:` labels
##
nameOverride: ""

## Override the deployment namespace
##
namespaceOverride: "monitoring"

## Provide a k8s version to auto dashboard import script example: kubeTargetVersionOverride: 1.16.6
##
kubeTargetVersionOverride: ""

## Allow kubeVersion to be overridden while creating the ingress
##
kubeVersionOverride: ""
.
.
.
```

# Requirements:
`pip install ruamel.yaml`

# 
