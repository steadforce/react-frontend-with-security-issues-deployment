# React frontend Deployment

Repository containing manifests for
[react-frontend](https://github.com/steadforce/react-frontend-with-security-issues)
deployment. Never install the content of this repo on our clusters manually. This is all done by argo-cd.

## Dependencies

This chart has no defined dependencies yet. 
If you add dependencies in there, you need to then run

    $ helm dependency update

in order to have the chart downloaded to the `charts` directory
and then also commit that new version alongside with the altered
`Chart.yaml` file.

See the [Helm docs](https://helm.sh/docs/topics/charts/#chart-dependencies)
for details.


## Render helm charts locally

The following command renders the charts like argo-cd does to validate the content.

### local

```
 helm template --release-name react-frontend-deployment -n react-frontend --skip-tests \
  --output-dir _render .
```

You can use this command to check if the output is as you expect. The `-a` parameters are needed since we use the
helm feature `.Capabilities.APIVersions.Has` to determine if a `CR` is installable in the cluster or not. Since
helm templating is designed to work offline we have to list the supported `CR`. Using `.Capabilities.APIVersions.Has`
feature in templating prevents sync errors in argo-cd if a `CR` can't be applied since its `CRD` isn't ready.