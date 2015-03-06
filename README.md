# Strange Bug
This seems to happen when setuptools creates a temporary egg for testing when
requests isn't already installed.

```bash
virtualenv requests
cd requests
. bin/activate
git clone https://github.com/sheppard/requests-test.git
cd requests-test
python setup.py test
```

```pytb
Traceback (most recent call last):
  File "setup.py", line 7, in <module>
    test_suite='tests',
  File "/usr/lib/python2.7/distutils/core.py", line 151, in setup
    dist.run_commands()
  File "/usr/lib/python2.7/distutils/dist.py", line 953, in run_commands
    self.run_command(cmd)
  File "/usr/lib/python2.7/distutils/dist.py", line 972, in run_command
    cmd_obj.run()
  File "/home/username/requests/local/lib/python2.7/site-packages/setuptools/command/test.py", line 138, in run
    self.with_project_on_sys_path(self.run_tests)
  File "/home/username/requests/local/lib/python2.7/site-packages/setuptools/command/test.py", line 118, in with_project_on_sys_path
    func()
  File "/home/username/requests/local/lib/python2.7/site-packages/setuptools/command/test.py", line 164, in run_tests
    testLoader = cks
  File "/usr/lib/python2.7/unittest/main.py", line 94, in __init__
    self.parseArgs(argv)
  File "/usr/lib/python2.7/unittest/main.py", line 149, in parseArgs
    self.createTests()
  File "/usr/lib/python2.7/unittest/main.py", line 158, in createTests
    self.module)
  File "/usr/lib/python2.7/unittest/loader.py", line 130, in loadTestsFromNames
    suites = [self.loadTestsFromName(name, module) for name in names]
  File "/usr/lib/python2.7/unittest/loader.py", line 103, in loadTestsFromName
    return self.loadTestsFromModule(obj)
  File "/home/username/requests/local/lib/python2.7/site-packages/setuptools/command/test.py", line 35, in loadTestsFromModule
    tests.append(self.loadTestsFromName(submodule))
  File "/usr/lib/python2.7/unittest/loader.py", line 91, in loadTestsFromName
    module = __import__('.'.join(parts_copy))
  File "/home/username/requests/requests-test/tests/test_requests.py", line 1, in <module>
    import requests_test
  File "/home/username/requests/requests-test/requests_test/__init__.py", line 1, in <module>
    import requests
  File "/home/username/requests/requests-test/requests-2.5.3-py2.7.egg/requests/__init__.py", line 53, in <module>
    from .packages.urllib3.contrib import pyopenssl
  File "/tmp/easy_install-bPx0HA/requests-2.5.3/requests/packages/__init__.py", line 49, in load_module
    
AttributeError: 'NoneType' object has no attribute 'modules'
```
