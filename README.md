Usage
-----

*Renamed from `django-redirects-file`*

Import this in urls.py and assign it to urlpatterns
BEFORE custom urls. (redirects should be hit first)
e.g:

``` python
from django_redirects_file import load_redirects

urlpatterns = load_redirects()
urlpatterns += patterns(...)
```

Format of redirects.json
------------------------

The json format is simply key/value pairs, from source to destination:

``` javascript
// redirects.json
{
    "getubuntu/download_static": "http://www.ubuntu.com/netbook/get-ubuntu/download",
    "testing/quantal/alpha1":    "https://wiki.ubuntu.com/QuantalQuetzal/TechnicalOverview/Alpha1"
}
```

To convert old "double spaced" redirects.txt:

``` python
json.dumps(dict([
    i.split('  ')[0:2] #ignore the 3rd item, in-line comments
    for i in open('/path/to/redirects.txt').readlines()
    if len(i.split('  ')) >= 2 #ignore whole comment lines
]))
```

For example, using [this script](https://gist.github.com/nottrobin/4a4f0162be577703cf851fbbe77f411b).
