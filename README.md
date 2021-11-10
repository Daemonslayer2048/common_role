## Requirements
### ansible-galaxy
  - community.general

## Variables
| Variable | Type | Required | Default | Example |
|    -     |   -  |     -    |    -    |    -    |
| selinux_state | string | True | enforcing | permissive |
| selinux_policy | string | True | targeted | targeted |
| install_zsh | bool | True | true | true |
| users | dict | False | N/A |  |

### Variable Summaries:
__selinux_state:__  
This variable determines what state selinux will be set to run in (i.e. permissive or enforcing).

__selinux_policy:__  
This variable sets selinux policy for more details on what this actually sets see the docs [here](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/security-enhanced_linux/chap-security-enhanced_linux-targeted_policy). Typically this can be be left as targeted.

__install_zsh:__  
This boolean definies whether or not [zsh](https://www.zsh.org/) and [oh_my_zsh](https://ohmyz.sh/) should be installed. This is set to be updated as it sets the ansible user's, shell to [zsh](https://www.zsh.org/) and enables [oh_my_zsh](https://ohmyz.sh/) for said user.  

__users:__  
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
