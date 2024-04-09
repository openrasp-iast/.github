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

## 快速开始

```bash
python iast_scanner/main.py start -f
```
