# NDO-Contracts
Ansible playbook to configure Filters, Contratcs and EPG relations using Nexus Dashboard Orchestrator NDO.

## Requirements
- Ansible v2.9 or newer

## Install
Ansible must be installed
```
sudo pip install ansible
```

Install the collection
```
ansible-galaxy collection install cisco.mso
```

Install the Nexus Dashboard (ND) collection when Cisco ACI Multi-Site is installed on Nexus Dashboard (v3.2+) or when using this collection with Nexus Dashboard Orchestrator (v3.6+)
```
ansible-galaxy collection install cisco.nd
```

Docs: https://docs.ansible.com/ansible/latest/collections/cisco/mso/index.html

## Usage

1. Edit host.yml file with the NDO information.

2. Edit the CSV files with your information:

- **aci_build_mso_filters.csv**: Filter related information, use same schema and template as Contract objects
- **aci_build_mso_contracts.csv**: Contracts related information
- **aci_build_mso_epg_contracts_relations.csv**: Application EPGs Contract relations (provider/consumer). This configuration is for enforcement east/west traffic.

> [!NOTE]
> First column of CSV is a dummy because: https://github.com/ansible-collections/community.general/issues/544

3. Run the ansible-playbook command: `ansible-playbook -i host.yml NDO-Contracts.yml --tag all-conf`

`--tag` options:
- `all-conf`: runs all tasks in the playbook
- `filters`: runs the task associated with filters config
- `contracts`: runs the task associated with contracts config
- `relations`: runs the task associated with Contract-EPG relations config (consumer/provider)

`--skip-tags` options:
- `stats`: omit statistics and checks task

> [!NOTE]
> Mac OS users may need to use the environmental variable `OBJC_DISABLE_INITIALIZE_FORK_SAFETY=YES` when running `ansible-playbook`.

The CSV status supports the following keywords:
- `present`
- `absent`
- `query`
- `done`
- `ignored`

In case one or more objects failed, you can ignore all the objects that were correctly configured and run the specific task using the tags.
