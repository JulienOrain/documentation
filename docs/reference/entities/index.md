---
title: Common Properties
excerpt: The definition of properties common to all entities
categories: []
status: published
type: overview
---
# Common Properties

All ReliablyHQ manifests share certain common properties. They are described below.

## Structure

```yaml
apiVersion: <string>
metadata:
    labels: {}
    relatedTo: {}
spec: {}
```

## APIVersion

Defines the APIVersion that this entity is compatible with.

### Structure

```yaml
apiVerison: <string>
```

## Kind

Defines the kind of entity this manifest describes.

### Structure

```yaml
kind: <string>
```

## Metadata

Metadata is used to describe the information in the manifest. It is used to help identify individual manifests, as well as describe things that this manifest relates to.

### Structure

```yaml
metadata:
    labels: {}
    relatedTo: {}
```

### Properties

| ref | description |
|---|---|
| labels | A dict<string,string> that describes the purpose of this manifest. Common properties include `name`, `owner`, `service`, `region`, etc.
| relatedTo | A dict<string,string> that describes labels that this manifest relates to. For instance, `metadata.relatedTo.service: awesome-service` would form a relationship to all other manifests that have a `metadata.labels.service: awesome-service`. This relationship is can then be visualised in the ReliablyHQ apps and utilised by behaviour to invoke some functionality. |

## Spec

Spec is an object that is specific to the manifest. It contains all manifest-specific data.

### Structure

```yaml
spec: {}
```

## Selectors

Selectors are used compare elements of the `spec` of one manifest with the `labels` of another manifest.

### Structure
```yaml
spec:
    ***Selector:
        <string>: <string>
```

### Rules
* each property of a selector must match a label of the target manifest.
* a target manifest may have more labels than a selector requires.
* a target manifest may not have fewer labels than a selector requires.

### Structure

```yaml
metadata:
    labels: {}
    relatedTo: {}
```

### Properties

| ref | description |
|---|---|
| labels | A dict<string,string> that describes the purpose of this manifest. Common properties include `name`, `owner`, `service`, `region`, etc.
| relatedTo | A dict<string,string> that describes labels that this manifest relates to. For instance, `metadata.relatedTo.service: awesome-service` would form a relationship to all other manifests that have a `metadata.labels.service: awesome-service`. This relationship is can then be visualised in the ReliablyHQ apps and utilised by behaviour to invoke some functionality. |