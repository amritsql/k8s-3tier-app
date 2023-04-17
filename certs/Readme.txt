### open ssl cet creation ###
# generate private key #
openssl genrsa -out key.pem 2048
# generate csr #
openssl req -new -key key.pem -out csr.pem
# generate cert #
openssl x509 -req -days 365 -in csr.pem -signkey key.pem -out cert.pem
# create k8s secret #
kubectl create secret tls my-tls-secret --cert=./cert.pem --key=./key.pem




