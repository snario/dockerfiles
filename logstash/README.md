# MapCentia ELK stack for GC2 Dockerfile

Full ELK stack (Logstash 1.5.4, Elasticsearch 1.7.1 and Kibana 4.1.1) with a NodeJS proxy for GC2. The container is set up to index Apache access logs with client IP geo-location.

## How to use this image

Start a Logstash container like this:

    sudo docker run \
        --name logstash \
        -p 5043:5043 \
        -p 1337:1337 \
        -e "LOGSTASH_DOMAIN=example.com" \
        -t -d \
        mapcentia/logstash
    
Change the DNS hostname "example.com" to the hostname of your ELK server. You can also use "LOGSTASH_IP=1.2.3.4" but there is some issues with certificates based on IPs and Logstash. So better use a DNS hostname. 

When a container is created a certificate is generated. Copy the certificate out from the container:

    sudo docker cp logstash:/certs/logstash.crt ~/certs/
    
Use the certificate for [Logstashforwarder](https://hub.docker.com/r/mapcentia/logstash-forwarder) on the GC2 servers.

![MapCentia](https://geocloud.mapcentia.com/assets/images/MapCentia_geocloud_200.png)

[www.mapcentia.com/en/geocloud](http://www.mapcentia.com/en/geocloud/)