FROM gcr.io/etcd-development/etcd:latest
LABEL description="The image will create etcd cluster andn provide service"
RUN CPUCOUNT=$(cat /proc/cpuinfo | grep '^processor.*:' | wc -l)
