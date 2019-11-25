其中 nginx 时该 role 的根目录，

tasks - 包含角色执行的任务的主列表
handlers - 包含 notify 修改任务
defaults - 角色的默认参数
vars - 角色的其他参数
files- 包含角色部署的文件
templates - 包含角色的模板文件
meta - 包含角色定义的元数据

tasks/main.yml 目录是一个 role 必须的文件，其他目录及文件不是必须

我们创建一个可重复使用的 nginx 角色

要求：该 role 可重复使用，可在不同系统中使用，可控制是否使用

创建 playbooks/roles/nginx/tasks/main.yml 文件