hrbson
======

This was forked from https://github.com/py-bson/bson, because it's name would
clash with pymongo, which also installs a bson library.

.. image:: https://img.shields.io/pypi/v/bson.svg
   :target: https://pypi.python.org/pypi/bson
.. image:: https://img.shields.io/travis/py-bson/bson.svg
   :target: https://travis-ci.org/py-bson/bson
.. image:: https://img.shields.io/pypi/pyversions/bson.svg
   :target: https://github.com/py-bson/bson
   

Independent BSON codec for Python that doesn't depend on MongoDB. The bson
ObjectId implementation is forked from the PyMongo project, licensed under
the Version 2.0 Apache License.

Installation
------------

.. sourcecode:: bash

   ~ $ poetry add git+https://github.com/helloretail/hrbson.git


Quick start
-----------

.. sourcecode:: python

   >>> import hrbson
   >>> a = hrbson.dumps({"A":[1,2,3,4,5,"6", u"7", {"C":u"DS"}]})
   >>> b = hrbson.loads(a)
   >>> b
   {'A': [1, 2, 3, 4, 5, '6', u'7', {'C': u'DS'}]}


Sending and receiving BSON objects to and from network sockets.


.. sourcecode:: python

   >>> from gevent import monkey, socket
   >>> monkey.patch_all()
   >>>
   >>> import hrbson
   >>> hrbson.patch_socket()
   >>> s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
   >>> s.connect(("127.0.0.1", 12345))
   >>> s.sendobj({u"message" : "hello!"})
