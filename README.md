# tilt

local development

# Usage

Install `helm`, `kind`, `ctlptl`, and `tilt`

```shell
brew install helm
brew install kind
brew install tilt-dev/tap/ctlptl
brew install tilt-dev/tap/tilt
```

Create a new cluster

```shell
ctlptl apply -f cluster.yaml
```

- Ensure you have the repos from the git organization (Joshua-FeatureFlag) cloned alongside this repository

  - Your structure should look like this

    Development / Work / Etc./
    ├─ tilt/
    │ ├─ Tiltfile
    ├─ frontend/
    │ ├─ Tiltfile
    ... etc

start tilt

```shell
tilt up
```

# Shutting down & cleaning up tilt

```shell
tilt down
ctlptl delete -f cluster.yaml
```
