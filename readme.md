## About the Repo
An attempt to create a linked pipeline where multiple repos are involved. Following three repos are related.
- [skc-dperf-1](https://github.com/sayankc/skc-dperf-1)
- [skc-dsec-1](https://github.com/sayankc/skc-dsec-1)
- [skc-acc-1](https://github.com/sayankc/skc-dacc-1)

## Tools 
Google cloud SDK

## How to simulate
1. Create these three repos in the google cloud code repo.
2. use the YAML files to start the chain pipeline. the flow is like below.

**Trigger First Pipeline [PERF] > [if ok] > Run next Pipeline [SEC] > [if ok] > Run next Pipeline [ACC]**

Note : For now, Dummy file content validation is kept. It can be replaced with actual job / test run tasks.


## Commands
### when all fails
```
gcloud builds submit . --config=cloudbuild.yaml 
```

### when first pipeline passes next 2 fails
```
gcloud builds submit . --config=cloudbuild.yaml --substitutions _PERF="performance",_SEC="XYZ",_ACC="accesibility"
```

### when 2 pipeline passes last one fails

```
gcloud builds submit . --config=cloudbuild.yaml --substitutions _PERF="performance",_SEC="security",_ACC="XYZ"
```

### when all pipeline passes 

```
gcloud builds submit . --config=cloudbuild.yaml --substitutions _PERF="performance",_SEC="security",_ACC="accesibility"
```
