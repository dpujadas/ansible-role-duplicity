duplicity
=========

This role installs [duplicity](http://duplicity.nongnu.org/) and (optionally) its wrapper [duply](http://duply.net/) and manages duply profiles using S3 as backend.

Role Variables
--------------

- `duplicity_user`: User that will run backups (default: 'root')
- `duplicity_use_duply`: Install and use duply or not (default: True)
- `duplicity_duply_profiles`: Dict of duply profiles to manage (default: '{}')
- `duplicity_archive_dir`: If defined, sets the folder that holds unencrypted meta data of the backup
- `duplicity_gpg_pass`: GPG pass to encrypt backups (Ex: 'SecretPass')
- `duplicity_aws_bucket`: AWS bucket endpoint where backups will be uploaded (Ex: 's3-eu-west-1.amazonaws.com/duplicity-bucket')
- `duplicity_aws_user`: If defined, sets the ACCESS_KEY_ID with read/write privileges to the bucket
- `duplicity_aws_pass`: If defined, sets the SECRET_ACCESS_KEY with read/write privileges to the bucket

Dependencies
------------

- dpujadas/ansible-role-python-pip

Example Playbook
----------------

    - hosts: servers
      vars:
        duplicity_duply_profiles:
          www:
            source: '/var/www'
            max_age: '1M'
            max_fullbkp_age: '1W'
            cron: 'daily'
            exclude:
              - '- dir/bar/foo'
              - '+ dir/bar'
      roles:
        - {
            role: duplicity,
            duplicity_gpg_pass: 'SecretPass',
            duplicity_aws_bucket: 's3-eu-west-1.amazonaws.com/duplicity-bucket',
            duplicity_aws_user: '{{ aws_access_key_id }}',
            duplicity_aws_pass: '{{ aws_secret_access_key }}'
        }

License
-------

MIT

[![Build Status](https://travis-ci.org/dpujadas/ansible-role-duplicity.svg?branch=master)](https://travis-ci.org/dpujadas/ansible-role-duplicity)
