# Anisble Server Common Role  
[toc]  

## Requirements
### ansible-galaxy
  - community.general

## Variables
| Variable | Type | Required | Default | Example |
|    -     |   -  |     -    |    -    |    -    |
| selinux_state | string | True | enforcing | permissive |
| selinux_policy | string | True | targeted | targeted |
| install_zsh | bool | True | true | true |
| users | dict | False | N/A | [Example](#users) |
| timezone | string | False | N/A | America/Chicago |
| dns | dict | False | N/A | [Example](#dns) |

### Variable Summaries:
#### selinux_state
This variable determines what state selinux will be set to run in (i.e. permissive or enforcing).

#### selinux_policy
This variable sets selinux policy for more details on what this actually sets see the docs [here](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/security-enhanced_linux/chap-security-enhanced_linux-targeted_policy). Typically this can be be left as targeted.

#### install_zsh
This boolean definies whether or not [zsh](https://www.zsh.org/) and [oh_my_zsh](https://ohmyz.sh/) should be installed. This is set to be updated as it sets the ansible user's, shell to [zsh](https://www.zsh.org/) and enables [oh_my_zsh](https://ohmyz.sh/) for said user.  

#### users  
This dictionary allows the user to create multiple users on the remote system, below is an example yaml:
``` yaml
users:
  - name: user
  - name: user2
    comment: "A user who just NEEDS to be cool and use ZSH"
    shell: /bin/zsh
  - name: admin
    password: $6$UkAmkRMIknoOijJ8$o9f7KjoDXW0/yvwVf2rzshiPe7f0uBY99Ve9tn2uyIt1/U5RyV67k37tJY72TfBxzYCgk2vXWNo439jAgMyS41
    comment: "Admin User"
    shell: /bin/zsh
    groups: wheel
```
The only required item is the users names, and groups should be a comma seperated list of groups the user will belong to.

#### timezone
Sets the servers timezone

#### dns  
| Variable | Type | Required |
|    -     |   -  |     -    |
| searchdomains | list | False |
| nameservers | list | False |  
| hosts | list of dicts | False |

Search domains and nameservers are not required, however they will be left blank if they are not defined and the `dns` variable is defined.

__Example:__
``` yaml
dns:
  searchdomains:
    - test.lan
  nameservers:
    - 1.1.1.1
    - 9.9.9.9
  hosts:
    - ip: 192.168.1.20
      names:
        - test
        - test.local
    - ip: 192.168.1.21
      names:
        - test1
        - test1.local
```
If the hosts list is not included the following will be the default file:
```
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
```
