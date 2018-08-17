Bitbucket
=========

A Role to install and manage Bitbucket Server configuration on rhel/CentOS servers atm.

Requirements
------------

There's no special requirement as long as you use variable `bitbucket_java_install` to auto-install Java OpenJDK. Otherwise, you will need to install Java JRE before running this role.

Role Variables
--------------

Available variables are listed below, along with default values (see defaults/main.yml):

    bitbucket_java_install

Defines wether role has to auto-install Java OpenJDK within the system

    bitbucket_java_version
    bitbucket_version

Define the versions to install from. Both are somewhat related as bitbucket releases depend on specific JAVA version. Refer to [bitbucket server's platform requirements](https://confluence.atlassian.com/bitbucketserver/supported-platforms-776640981.html).

    bitbucket_java_home

Defines java's home. Overwrite this variable if you manage your own java stack and disabled `bitbucket_java_install`.

    bitbucket_group
    bitbucket_user
    bitbucket_datadir
    bitbucket_workdir

Define bitbucket server user and workspace. `_datadir` locate where bitbucket will be installed within its configuration. `_workdir` locates where bitbucket will generate all its files and repositories.

    bitbucket_archive: "atlassian-bitbucket-{{ bitbucket_version }}.tar.gz"
    bitbucket_url: "https://downloads.atlassian.com/software/stash/downloads/{{ bitbucket_archive }}"

Define default download url. This variable can be overwrite if you manage your own package repository internally.

    bitbucket_hostname
    bitbucket_server_port
    bitbucket_connector_port
    bitbucket_connector_redirect_port
    bitbucket_connection_timeout
    bitbucket_context_path
    bitbucket_proxy_name
    bitbucket_scheme

Bitbucket Server comes with a pre-configured servlet container (Apache Tomcat). Thoses variables allow you to update its configuration to match with your infrastructure requirements.

    bitbuckte_db_driver
    bitbucket_db_uri
    bitbucket_db_user
    bitbucket_db_passwd

Define database engine location and credentials.

    bitbucket_properties

Defines bitbucket server's configuration and behavior. Refer to [bitbucket server's config properties](https://confluence.atlassian.com/bitbucketserver/bitbucket-server-config-properties-776640155.html) for all possible entries.
See defautl/main.xml for how to pass config properties to this variable.

Dependencies
------------

None.

Example Playbook
----------------

Here's an example playbook with few variables:

```yaml
- hosts: servers
  vars:
    bitbucket_java_install: true
    bitbucket_version: "5.3.2"
    bitbuckte_db_driver: "org.postgresql.Driver"
    bitbucket_db_uri: "jdbc:postgresql://db01.domain.tld/bitbucket"
    bitbucket_db_user: "bitbucket"
    bitbucket_db_passwd: "mysuperduperpassword"

  roles:
     - name: bitbucket
       tags:
        - bitbucket
```

License
-------

MIT
