mkdir -p apache/
cd apache/

wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=1zpbjIhA6sBVOh8Y81wocGqTndnVtu-ZS' -O index.php
wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=1mDsUcMVphKWZpccapaGNLXJzG8PgQyT3' -O haproxy.cfg

chmod +x start-apache2.sh
docker build -t apacheslave3 .

docker tag apache-image localhost:5000/ubuntu
docker run -d -p 5000:5000 --restart=always --name local-registry registry:2
docker push localhost:5000/ubuntu
