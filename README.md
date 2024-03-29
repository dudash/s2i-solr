# SOLR source-to-image

<h1> THIS IS IN PROGRESS - COMING SOON </h1>

<img src="https://www.openshift.com/images/logos/openshift/Logotype_RH_OpenShift_wLogo_RGB_Gray.svg" alt="OCP logo" height="70" >

This repository contains source code and instructions for building a builder. You can use the builder to package SOLR with schema configuration as reproducible Docker container images using [source-to-image](https://github.com/openshift/source-to-image).


For more information about using these images with OpenShift, please see the
official [OpenShift Documentation](https://docs.openshift.org/latest/architecture/core_concepts/builds_and_image_streams.html#source-build).

For more information about the open source SOLR search engine goto the [Apache website](http://lucene.apache.org/solr/).

<h3>Below you can read how to build and how to use.  FYI, you don't have to build this repo, you can use a prebuilt image - it's available on docker hub.<h3>

## Versions/targets available

SOLR versions available
* 7.2.1

Target versions available
* redhat = RHEL 7 based OpenJDK from access.redhat.com
* jboss = CentOS 7 based OpenJDK for community development use


## Using this image

You'll need to have the [s2i tool](https://github.com/openshift/source-to-image).

### Find and get the image you want (version and target)

```shell
$ docker search dudash/solr
$ docker pull dudash/solr-<version>-<target>:<tag>
```

### Using with github projects

Use the `s2i` tool to build the final image that contains your SOLR search service

* Hello SOLR from github example
```shell
$ s2i build https://github.com/dudash/openshiftexamples-solr.git dudash/solr-66-jboss:latest demo-solr
$ docker run demo-solr
```

### How to structure your code

**TBD**

### Using in Open Shift

You can install the S2I SOLR imagestreams from a template:
```shell
$ oc create -n openshift -f https://raw.githubusercontent.com/dudash/s2i-solr/master/openshift-resources/solr-all-rhel7-imagestreamlist.json
```

Note: Drop the ```-n openshift``` if you don't have admin rights... or ask your admin to create it.

## Environment variables
---------------------
To set environment variables, you can place them as a key value pair into a `.s2i/environment`
file inside your source code repository.

* TBD

## Building this repo yourself

### Build 
To prepare the s2i builder image:
```shell
$ git clone https://github.com/dudash/s2i-solr.git
$ cd s2i-solr
$ make build VERSION=<version> TARGET=<target>
```

### Repo organization
<pre>
**[solr-version]/Dockerfile**: Dockerfile to build container images from
**[solr-version]/Dockerfile.xxx**: Dockerfile to build alternative container images
**[solr-version]/test/test-app**: Sample application used for tests
**hack/**: Folder containing scripts which are responsible for the build and test actions performed by the Makefile
**s2i/**: Build scripts which will be injected into the builder image and executed during application source code builds
</pre>

