Automated Web Server Management Using Ansible + Semaphore


Host mappings allow Semaphore to use different credentials for different Git hosts or repository dependencies such as Git submodules, or repositories hosted on GitHub, GitLab, and Bitbucket.

Host Config in Semaphore is used to map SSH credentials to Git hosts or repository URLs. This is particularly useful when Ansible repositories use private Git dependencies, submodules, private roles, or collections stored across multiple Git platforms such as GitHub, GitLab, and Bitbucket. Semaphore automatically selects the appropriate SSH key based on the configured mapping.

The Integration URL exposes a webhook endpoint that allows external systems such as GitHub, Jenkins, ServiceNow, monitoring tools, or custom applications to trigger Semaphore task templates and workflows programmatically. This enables event-driven automation and GitOps workflows without requiring users to log in to the Semaphore UI.

Token authentication protects the integration endpoint from unauthorized execution. External systems such as Jenkins, GitHub Actions, ServiceNow, or internal portals can securely trigger Semaphore task templates by sending the correct authentication token in a custom HTTP header.

The Repository feature defines the Git repository that Semaphore clones and executes from. 
Host Config, on the other hand, maps SSH credentials to specific Git hosts or repository URLs. 
Repository answers "which repository should be used," while Host Config answers "which SSH key should be used when accessing a particular Git host or dependency." 
Host Config becomes useful when repositories use private submodules, Ansible Galaxy roles, or collections hosted across multiple Git platforms such as GitHub, GitLab, and Bitbucket.

Group Mapping is used when Semaphore is integrated with an external identity provider such as LDAP, Azure AD, GitHub OAuth, or GitLab. It automatically maps users from external groups to Semaphore teams, enabling centralized access management and role-based access control without manually assigning users to teams. For a small local-user deployment, Group Mapping is typically not required.

API Tokens are used to authenticate requests to the Semaphore REST API. They allow external systems such as Jenkins, GitHub Actions, ServiceNow, custom portals, or scripts to manage Semaphore resources, trigger tasks, retrieve execution history, and automate administrative operations without using the web interface.

Local stores secrets directly in the Semaphore database and is commonly used for SSH keys, passwords, and tokens. 
Storage is used for file-based artifacts such as kubeconfig files, certificates, or Ansible Vault password files. 
ENV reads values from operating system environment variables.
while File reads values from files present on the Semaphore host. 



**Cluster:
**
Load Balancer
                        |
     -------------------------------------
     |                |                 |

Semaphore-1     Semaphore-2      Semaphore-3
     |                |                 |
     -------------------------------------
                    |
                PostgreSQL


**Runners:
**
                 Semaphore
                      |
     -----------------------------------
     |                |               |
     |                |               |

 Runner-1       Runner-2       Runner-3
     |                |               |

 Web01/Web02     Other Hosts     Other Hosts


Runner-1 → Operations Tasks
Runner-2 → Deployment Tasks
Runner-3 → Infrastructure Tasks

readme

