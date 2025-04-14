## Setup procedure
Head over to your databricks workspace.
Click your profile > Settings > Developer > Access Tokens [Manage]
Create an access token, this will be your `DATABRICKS_TOKEN`. Save the token in a secure way.

### Storing DATABRICKS_TOKEN
On Mac: 
- store: `security add-generic-password -a <user-email> -s <name-for-service>`
- retrieve `export DATABRICKS_TOKEN=$(security find-generic-password -s <name-for-service> -w -g`


```bash
uv sync
databricks configure -t <DATABRICKS_TOKEN>
```

### profiles.yml

#### Set up with wizard
```bash
dbt init <project_name>
```

You will be prompted for databricks host, enter `https://<hostname>` 
where `hostname` is found in `Compute`/`SQL Warehouses` tab in your workspace 
along with `http_path` which will also be prompted for. Finally the `token` (`DATABRICKS_TOKEN`) will be
requested which you paste in.

#### Set up manually
```yaml
example_project:
  target: local
  outputs:
    local:
      catalog: <dev-catalog>
      host: <host>
      http_path: <http_path>
      threads: 1
      token: "{{ env_var('DATABRICKS_TOKEN') }}"
      type: databricks
    dev:
      catalog: <dev-catalog>
      host: <host>
      http_path: <http_path>
      threads: 1
      token: "{{ env_var('DATABRICKS_TOKEN') }}" # other auth method perhaps?
      type: databricks
    uat:
      catalog: <uat-catalog>
      host: <host>
      http_path: <http_path>
      threads: 1
      token: "{{ env_var('DATABRICKS_TOKEN') }}"
      type: databricks
    prod:
      catalog: <prod-catalog>
      host: <host>
      http_path: <http_path>
      threads: 1
      token: "{{ env_var('DATABRICKS_TOKEN') }}"
      type: databricks
```
`http_path` corresponds to the compute you wish to use.

### Why this project layout?
#### Sharing catalogs


You should now be able to run dbt commands 
```bash
dbt <command> --project-dir <project_name> --profile-dir <project_name>
```

TODO:
- [ ] CI for creating important resource lifetime operations 
    - [ ] DE operations CI
    - [ ] Analytics team operations CI


## Resources
[Resources for Databricks](https://github.com/reisdebora/awesome-databricks?tab=readme-ov-filehttps://github.com/reisdebora/awesome-databricks?tab=readme-ov-file)
[Eventhub streaming](https://learn.microsoft.com/en-us/azure/databricks/connect/streaming/kafka)
