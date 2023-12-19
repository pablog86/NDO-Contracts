# NDO-Contracts
## Ansible playbook to configure Filters, contratcs and EPG relations

1. Edit host.yml file with the NDO information.

2. Edit the CSV files with your information:

- **aci_build_mso_filters.csv**: Filter related information, use same schema and template as Contract objects
- **aci_build_mso_contracts.csv**: Contracts related information
- **aci_build_mso_epg_contracts_relations.csv**: Application EPGs Contract relations (provider/consumer). This configuration is for enforcement east/west traffic.

3. Run the ansible-playbook command: `ansible-playbook -i host.yml NDO-Contracts.yml --tag all-conf`

--tag` options:
- `all-conf`: runs all tasks in the playbook
- `filters`: runs the task associated with filters config
- `contracts`: runs the task associated with contracts config
- `relations`: runs the task associated with Contract-EPG relations config (consumer/provider)

`--skip-tags`:
- `stats`: omit statistics and checks task

> [!NOTE]
> Mac OS users may need to use the environmental variable `OBJC_DISABLE_INITIALIZE_FORK_SAFETY=YES` when running `ansible-playbook`.

The CSV status supports the following keywords:
- `present`
- `absent`
- `query`
- `done`
- `ignored`

In case one or more objects failed, you can ignore all the objects that were configured and run the specific task using the tags.
