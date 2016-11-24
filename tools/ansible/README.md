
# Inviqa's Ansible Seed
## Description
This is a collection of Ansible roles, tasks, playbook, vars and samples to be used as seed in projects, to be used in conjunctions with the '[ansible-provisioning][ansible-provisioning]' script.

## Roles
- Roles that only define Galaxy roles dependencies should be stored in the `roles` directory

- Roles that wrap another Galaxy roles AND include default values or tasks should be integrated as modules of `ansible-config-driven-helper` role

- Roles that do not wrap another Galaxy role (even if they might depend on other roles) and that do specific installation tasks should be made a inviqa git role (eventually a Galaxy role) or replaced by other Galaxy roles

- Roles tailored specifically for a project will be included in the `tools/ansible/roles` directory AFTER the project has been seeded with the 'ansible-seed-inviqa' repo

## Vaults
The seed includes the Vault file `group_vars/all/vault.yml` (which password is available only to the Devops/Support team) and it contains secrets to connect to the most used cloud services in the Inviqa organization.
If you need to add additial secrets, use separate Vaults, possibly organised by groups.

## Attributes
### Digital Ocean attributes that can be set
To provision a host or a group of hosts in Digital Ocean set `provider` to `digitalocean`
All the attributes have a default value set
to override the default values add the following attributes as a group_var or host_var
```
  digital_ocean_api_token:          
  digital_ocean_size_id:            
  digital_ocean_image_id:           
  digital_ocean_name:               
  digital_ocean_region_id:          
  digital_ocean_unique_name:        
  digital_ocean_backups_enabled:    
  digital_ocean_private_networking:
  digital_ocean_ssh_key_ids:        
```
### Digital Ocean Floating IP
To be set in the host_vars
```
  digitalocean_floating_ip_enable: true
  digital_ocean_floating_ip: "123.456.789.123"
```

### AWS EC2 attributes
to provision a host or a group of hosts in AWS EC2 set `provider` to `aws-ec2`
```
  provider: aws-ec2
```
to override the default values add the following attributes as a group_var or host_var

```
  ec2_region:
  ec2_availability_zone:
  ec2_instance_type:
  ec2_image:
  ec2_keypair:
  ec2_security_group:
  ec2_instance_tags:
    Name: tag1
    Name: tag2
  ec2_count_tag: "{{ ec2_instance_tags }}"
  ec2_exact_count:

  # This is required because EC2 instances do not allow root ssh by default
  ansible_user: ec2-user

  # exclusively used by EC2 instances
  ansible_ssh_private_key_file: ~/.ssh/your_pem_file_for_ec2.pem
```

### JumpCloud
If defining `jumpcloud_enable = yes` you will need to define the `jumpcloud_tags` as follow:
```ruby```
vars:
  jumpcloud_tags:
    - 'tag_one'
    - 'tag_two'
``````
mind that the tags names need to be already existing in your JC account

### CloudFlare
```ruby```
vars:
  cloudflare_hostname: (optional, if not defined then it would be same as hostname)
    - 'domain1'
    - 'domain2'
``````

## License
[MIT][license]

## Author Information
------------------
Authors Felicity Ratcliffe, Hardik Gajjarat, Marco Massari Calderone - Inviqa UK Ltd

Based on Barney Hanlon's work on the original [ansible-provisioning][ansible-provisioning] project for [Inviqa][inviqa]

[github]: https://github.com/inviqa/ansible-seed-inviqa "Github location of this role"
[ansible-provisioning]: https://github.com/inviqa/ansible-provisioning "Ansible Provision script"
[inviqa]: https://www.inviqa.com "Inviqa UK Ltd"

[license]: https://raw.githubusercontent.com/inviqa/ansible-jumpcloud/master/LICENSE
