install: https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started-install.html

Tutorial: https://www.elastic.co/guide/en/elastic-stack-get-started/7.5/get-started-elastic-stack.html

===============================================================

B1: Version
> java -version

B2: Install ES

- core
brew tap elastic/tap: https://www.elastic.co/guide/en/elasticsearch/reference/current/brew.html
> brew install elastic/tap/elasticsearch-full

- kibana: https://www.elastic.co/guide/en/kibana/current/brew.html
> brew install elastic/tap/kibana-full


- version
> elasticsearch --version


- start es: localhost:9200
> elasticsearch

- start kibana: localhost:5601/app/kibana
> kibana

===============================================================

GET http://localhost:9200/_all
