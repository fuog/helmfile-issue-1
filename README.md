# helmfile-issue-1

This is a DEMO repo that showcases an helmfile rendering issue [#1971](https://github.com/helmfile/helmfile/issues/1971) regarding `skipSchemaValidation: true` with `transformers: ...` on helmfile version `1.0.0-rc.12`

## Link to helmfile Issue

==> following

## Demo

```
❯ helmfile version

▓▓▓ helmfile

  Version            1.0.0-rc.12
  Git Commit         b921fa6
  Build Date         13 Mar 25 13:57 CET (1 week ago)
  Commit Date        13 Mar 25 13:54 CET (1 week ago)
  Dirty Build        no
  Go version         1.24.1
  Compiler           gc
  Platform           linux/amd64
❯ helmfile --file helmfile.yaml template
Adding repo externaldns https://kubernetes-sigs.github.io/external-dns/
"externaldns" has been added to your repositories

in ./helmfile.yaml: [exit status 1

COMMAND:
  helm template --debug=false --output-dir=/tmp/chartify3963036156/system-externaldns/foooooo/external-dns/helmx.1.rendered foooooo /tmp/chartify3963036156/system-externaldns/foooooo/external-dns -f /tmp/chartify3963036156/system-externaldns/foooooo/external-dns/values.yaml -f /tmp/helmfile800032762/system-externaldns-foooooo-values-7d4df7954 --namespace system-externaldns

OUTPUT:
  Error: values don't meet the specifications of the schema(s) in the following chart(s):
  external-dns:
  - fullnameOverride: Invalid type. Expected: null, given: string]
```

Removing `transformers: ..` will make the render work..

NOTE: the error itself is NOT the fault of `helmfile` but the fact that `skipSchemaValidation: true` is ignored with `transformers: ...`
