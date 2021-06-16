官方建议的目录结构

production        # inventory file for production.
staging           # inventory file for staging.

site.yml          # master playbook
webservers.yml    # playbook for webserver tier
dbservers.yml     # playbook for dbserver tier


roles/
  common/         # role name
    tasks/        #   
      main.yml    # main tasks file.
    handlers/     #
      main.yml    # handlers file.
    templates/    #
      ntp.conf.j2 # templates end in .j2.
    files/        #   
      bar.txt     # files
      foo.sh      # script files
    vars/         #
      main.yml    # variables with this role.
    defaults/     #
      main.yml    # default variables.
    meta/         #
      main.yml    # role dependencies



https://gitee.com/chunanyong/zorm
关于事务传播

$ tree .
.
└── example_role
    ├── README.md     # 说明文件
    ├── defaults
    │   └── main.yml  # 可被覆写的变数。
    ├── files         # 需复制到 Managed node 的档案。
    ├── handlers
    │   └── main.yml  # 主要的 handler。
    ├── meta
    │   └── main.yml
    ├── tasks
    │   └── main.yml  # 主要的 task。
    ├── templates     # 集中存放 Jinja2 模板的目录。
    ├── tests
    │   ├── inventory
    │   └── test.yml
    └── vars
        └── main.yml  # 不该被覆写的变数。