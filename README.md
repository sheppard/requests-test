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
