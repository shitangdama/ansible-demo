通过 -e 参数将 dynamic_word 覆写成 ansible。
$ ansible-playbook template_demo.yml -e "dynamic_word=ansible"



 3.执行playbook，并通过 -e 切换各个环境。