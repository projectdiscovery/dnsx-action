<h1 align="center">
  <img src="https://github.com/projectdiscovery/dnsx/blob/master/static/dnsx-logo.png" alt="dnsx" width="200px"></a>
  <br>
</h1>

<h4 align="center"><a href="https://github.com/projectdiscovery/dnsx-action">dnsx Action</a> makes it easy to orchestrate <a href="https://github.com/projectdiscovery/dnsx">dnsx</a> with GitHub Action.</h4>



Example Usage
-----

**GitHub Action running dnsx on list of hosts**

```yaml
      - name: 💥 dnsx - DNS Resolver
        uses: projectdiscovery/dnsx-action@main
        with:
          list: hosts.txt
```

**Example workflow** - `.github/workflows/dnsx.yml`


```yaml
name: 💥 dnsx - DNS Resolver

on:
    schedule:
      - cron: '0 0 * * *'
    workflow_dispatch:

jobs:
  dnsx-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-go@v2
        with:
          go-version: 1.15

      - name: 💥 dnsx - DNS Resolver
        uses: projectdiscovery/dnsx-action@main
        with:
          list: hosts.txt

      - name: GitHub Workflow artifacts
        uses: actions/upload-artifact@v2
        with:
          name: dnsx.log
          path: dnsx.log
```


Available Inputs
------

| Key      | Description                                          | Required |
| -------- | ---------------------------------------------------- | -------- |
| `list`   | List of hosts to perform DNS resolution              | true     |
| `output` | File to save output result (default - dnsx.log)      | false    |
| `json`   | Write results in JSON format                         | false    |
| `flags`  | Additional dnsx CLI flags to use                     | false    |
