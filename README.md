##drunomics CI-system docker images##
This is the docker part of the drunomics ci system.  

You can fetch the readily built docker images directly from our [Docker HUB](https://registry.hub.docker.com/u/drunomics/) Automated Build Repository

The Images are built using ansible. Currently we provide 4 different base Images with different feature set. Detailed information about the configuration and the used ansible roles you can find in the respective Readme.

* [LAMP](/lamp/README.md)
* [LAMP + REDIS](/lamp-redis/README.md)
* [LAMP + REDIS + Apache SOLR](/lamp-redis-solr/README.md)
* [LAMP + REDIS + ElasticSearch](/lamp-redis-elasticsearch/README.md)


(c) 2015 drunomics GmbH. /  MIT License 