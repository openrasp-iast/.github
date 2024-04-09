# iast-scanner

## 目录结构

```bash
.
├── doc
│   └── img
│       └── architecture.png
├── iast_scanner
│   ├── config.default.yaml
│   ├── conftest.py
│   ├── core
│   │   ├── components
│   │   │   ├── audit_tools
│   │   │   │   ├── checker.py
│   │   │   │   ├── context.py
│   │   │   │   ├── __init__.py
│   │   │   │   ├── mutant_helper.py
│   │   │   │   ├── request_data.py
│   │   │   │   └── session.py
│   │   │   ├── authorizer.py
│   │   │   ├── cloud_api.py
│   │   │   ├── cloud_console.py
│   │   │   ├── common.py
│   │   │   ├── communicator.py
│   │   │   ├── config.py
│   │   │   ├── exceptions.py
│   │   │   ├── fork_proxy.py
│   │   │   ├── logger.py
│   │   │   ├── plugin
│   │   │   │   ├── auth_plugin_base.py
│   │   │   │   ├── dedup_plugin_base.py
│   │   │   │   └── scan_plugin_base.py
│   │   │   ├── rasp_result.py
│   │   │   ├── result_receiver.py
│   │   │   ├── runtime_info.py
│   │   │   ├── scanner_manager.py
│   │   │   ├── util.py
│   │   │   └── web_console.py
│   │   ├── launcher.py
│   │   ├── model
│   │   │   ├── base_model.py
│   │   │   ├── config_model.py
│   │   │   ├── new_request_model.py
│   │   │   └── report_model.py
│   │   └── modules
│   │       ├── base.py
│   │       ├── __init__.py
│   │       ├── monitor.py
│   │       ├── preprocessor.py
│   │       └── scanner.py
│   ├── main.py
│   ├── main.spec
│   ├── plugin
│   │   ├── authorizer
│   │   │   └── default.py
│   │   ├── deduplicate
│   │   │   └── default.py
│   │   └── scanner
│   │       ├── command_basic.py
│   │       ├── directory_basic.py
│   │       ├── eval_basic.py
│   │       ├── fileupload_basic.py
│   │       ├── include_basic.py
│   │       ├── readfile_basic.py
│   │       ├── sql_basic.py
│   │       ├── ssrf_basic.py
│   │       ├── writefile_basic.py
│   │       └── xxe_basic.py
│   ├── requirements.txt
│   ├── test
│   │   ├── helper.py
│   │   ├── modules
│   │   │   ├── conftest.py
│   │   │   ├── monitor
│   │   │   │   ├── conftest.py
│   │   │   │   └── test_monitor.py
│   │   │   └── preprocessor
│   │   │       ├── conftest.py
│   │   │       └── test_preprocessor.py
│   │   ├── scan_plugin
│   │   │   ├── conftest.py
│   │   │   ├── test_command_basic.py
│   │   │   ├── test_directory_basic.py
│   │   │   ├── test_fileUpload_basic.py
│   │   │   ├── test_include_basic.py
│   │   │   ├── test_readFile_basic.py
│   │   │   ├── test_sql_basic.py
│   │   │   ├── test_ssrf_basic.py
│   │   │   ├── test_writeFile_basic.py
│   │   │   └── test_xxe_basic.py
│   │   ├── test_launcher.py
│   │   └── test_util.py
│   └── VERSION
├── LICENSE
├── Makefile
├── MANIFEST.in
├── pyproject.toml
├── README.md
└── setup.py

```

## 配置模版

```yaml
# OpenRASP-IAST 默认配置文件模板, 不要在这里修改配置

# 预处理模块
preprocessor.http_port: 25931                        # http服务监听端口
preprocessor.process_num: 2                          # http服务进程数
preprocessor.request_lru_size: 1000                  # 每个进程的每个扫描目标对应一个LRU，总大小: 进程数 * 扫描目标数 * lru_size
preprocessor.api_path: /openrasp-result              # OpenRASP iast插件发送数据的目标 url path
preprocessor.max_buffer_size: 104857600              # http服务器接受数据的缓冲区大小, 单位Bytes, 默认100M
preprocessor.plugin_name: default                    # 使用的去重插件名

# 监控模块
monitor.schedule_interval: 1.000                      # 扫描速率自动调整策略执行间隔(s)
monitor.max_cpu: 98                                   # cpu使用率超过限制会降低并发扫描速率
monitor.min_cpu: 85                                   # cpu使用率低于该值会增加并发扫描速率
monitor.console_port: 18664                           # 管理后台端口

# 扫描配置
scanner.max_concurrent_request: 20                    # 单个扫描任务最大扫描并发线程数
scanner.min_request_interval: 0                       # 每个线程最小扫描请求间隔(ms)
scanner.max_request_interval: 1000                    # 每个线程最大扫描请求间隔(ms)
scanner.request_timeout: 5                            # 扫描请求超时时间(s)
scanner.retry_times: 3                                # 扫描请求失败重试次数
scanner.max_module_instance: 16                       # 最大并发扫描任务数量

# 云控配置
cloud_api.enable: True                                # 是否上传结果到云控
cloud_api.backend_url: "http://127.0.0.1:8087"        # 云控地址
cloud_api.app_secret: "secret"                        # 云控secret_key
cloud_api.app_id: "app"                               # 云控app_id

# 绑定核心(仅支持linux)
affinity.enable: False                                # 是否以绑定CPU核心的方式运行
affinity.core_num: 1                                  # 绑定的核心数量

# 日志配置
log.level: INFO                                       # log级别，可选: DEBUG INFO WARNING ERROR CRITICAL
log.path: ""                                          # log文件路径, 为空时使用 /home/user/openrasp-iast/log
log.rotate_size: 5                                    # 触发rotate的日志大小，单位MB
log.rotate_num: 2                                     # rotate文件最多保存份数不包括当前日志文件

# MySQL 配置
database.host: localhost                              # 数据库地址
database.port: 3306                                   # 端口
database.username: root                               # 连接用户名
database.password: ''                                 # 连接密码, 纯数字需使用引号包裹 如'123456'
database.db_name: openrasp                            # 数据库名

```

## 快速开始

```bash
python iast_scanner/main.py start -f
```
