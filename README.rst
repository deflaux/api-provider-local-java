api-provider-local-java  |Build Status|_
==============================

.. |Build Status| image:: https://travis-ci.org/googlegenomics/api-provider-local-java.png?branch=master
.. _Build Status: https://travis-ci.org/googlegenomics/api-provider-local-java


Note: this repo supports v0.1 of the GA4GH APIs. There is a different 
`python server <https://github.com/ga4gh/server>`_ that will support v0.5 
and will make this repo obsolete.

.....

Getting started  
---------------

To use, first build the code using `Apache Maven <http://maven.apache.org/download.cgi>`_::

  cd api-provider-local-java
  mvn package

Once built, use the jar file to start a local server::

  java -cp target/api-provider-local-java-v1beta-jar-with-dependencies.jar com.google.cloud.genomics.localrepo.Server --dataset=testdata:testdata

There are two command line flags available:

``--port=<portnum>``:
  Sets the port that the server listens on for incoming connections. If
  unspecified, the default is 5000.

``--dataset=<id>:<directory>``:
  This flag can occur zero or more times. With each instance of this flag, you
  supply a dataset ID and a path to a directory on your local filesystem. When
  the server is started, each directory is recursively traversed, and all ``.bam``
  files with a corresponding sibling ``.bai`` file are included into the data
  with the given dataset ID. For example, if you have the following directory
  layout::

    my_directory/
      my_subdirectory/
        foo.bam
        foo.bam.bai
      another_subdirectory/
        bar.bam
      baz.bam
      baz.bam.bai

  and you passed the flag ``--dataset=my_data:/path/to/my_directory``, then
  ``my_directory/my_subdirectory/foo.bam`` and ``my_directory/baz.bam`` would be
  included into a dataset with ID ``my_data``, but
  ``my_directory/another_subdirectory/bar.bam`` would be excluded, due to not
  having its sibling ``.bai`` file.

Go to ``http://localhost:<portnum>/datasets`` to see your data.  


Project status
--------------

This repository has been replaced by the work on `ga4gh/server <http://github.com/ga4gh/server>`_.
