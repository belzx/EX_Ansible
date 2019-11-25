执行命令 ansible-playbook playbooks/reuse_tasks.yml

写调用一个 shell 模块的 playbook,
路径为 playbooks/shell.yml

eg: ansible-playbook 调用如下
playbook 路径 playbook/copy.yml

template 模块是用来做差异化文件推送的，ansible 调用 jinja2 模板引擎，所以编辑源文件需要遵循 Jinja2 语法格式。所需参数与 copy 模块类似，src 文件源路径；dest 文件在远程主机的路径；owner 推送后的用户所属；group 推送后的属组；mode 推送后的权限；backup 是否备份原文件。
eg:
编辑 template 文件，路径为
playbooks/templates/nginx_vhost.j2

playbook 文件如下，
文件路径为 playbooks/template.yml

注意：在开发插件之前我们得先保证我们现在有一个可用的 redis 地址，所以我们利用第一节课的 playbook 启动一个 redis 实例
playbook 文件 playbooks/redis_opt.yml

对于很多系统而言，我们登陆使用的是一个普通用户，执行任务可能需要 root 权限，也可能需要再次切换到其他用户；具体在 playbook 中使用如下
become: yes 是否进行切换 root 操作
become_method: 'sudo' 切换 root 的命令，有些系统设置切换命令为 su
文件 playbooks/sudo.yml

when 语句
when 用来判断 tasks 是否执行
文件 playbooks/when.yml

ignore_errors 忽略错误
文件 playbooks/ignore_errors.yml
loop 循环与条件
文件 playbooks/loop.yml

register 对结果进行处理
文件 playbooks/register.yml

until 任务重试
文件 playbooks/until.yml

循环 inventor
文件 playbooks/lookup_inventory.yml

blocks
文件 playbooks/blocks.yml

failed_when 主动触发失败

changed _when 修改状态
文件 playbooks/failed_when.yml

any_errors_fatal 退出进程任务
文件 playbooks/any_errors_fatal.yml

run_once 任务只执行一次
文件 playbooks/run_once.yml

lookup 插件是一种查询外部数据源的方法，比如 shell 命令，甚至键值存储。
文件 playbooks/lookup.yml

from_yaml 将 yaml 数据转成列表或字典
from_json 将 json 数据转成列表或字典
default 变量不存在时提供一个默认值
文件 playbooks/filters.yml


omit 忽略参数
文件 playbooks/omit.yml

handler 当任务修改时触发操作
文件 playbooks/handlers.yml

listen 多任务关联 文件 playbooks/listen.yml

include 和 import 语句非常相似，但是 Ansible executor 引擎对它们的处理非常不同。
所有 import* 语句都是在解析剧本时进行预处理的。
所有 include* 语句都是在执行剧本时遇到时处理的。
include_ import_ 使用
文件 tasks.yml

文件 playbooks/reuse_tasks.yml

ansible-playbook playbooks/role_tasks.yml
创建一个 playbook 使用 nginx 角色进行安装操作，
文件为 playbooks/role_tasks.yml

include_role 导入模块执行
文件 playbooks/include_role.yml

最常用的魔术变量是 hostvars，groups，group_names 和 inventory_hostname。
hostvars 允许访问另一个主机的变量，包括已收集到的有关该主机的 ansible_facts 。可以在剧本中的任何一点访问主机变量。
groups inventory 中所有组（和主机）的列表。这可用于枚举组中的所有主机。
group_names 当前主机所在的所有组的列表（数组）。可以在使用 Jinja 2 语法的模板中使用，使模板源文件基于主机的组成员（或角色）而有所不同。
inventory_hostname Ansible 的 inventory 主机文件中配置的主机名。如果禁用了 ansible_facts 收集，或者不想依赖已发现的主机名，这可能很有用。
ansible_hostname 如果主机有一个长的 FQDN，可以使用 inventory_hostname_short，它包含直到第一个句点的部分，而不包含域的其余部分。
文件 playbooks/magic_variables.yml

我们将 wordpress 项目也作为一个 role
文件 playbooks/roles/wordpress/tasks/main.yml ，