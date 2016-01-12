FROM nginx:1.7
MAINTAINER Moreno, Carlos Santiago <ingcsmoreno@gmail.com>

COPY nginx.service /etc/service/nginx/run
COPY consul-template.service /etc/service/consul-template/run
COPY nginx.conf /etc/consul-templates/nginx.conf

ENV CT_URL https://github.com/hashicorp/consul-template/releases/download/v0.10.0/consul-template_0.10.0_linux_amd64.tar.gz

RUN DEBIAN_FRONTEND=noninteractive \
    apt-get update -qq && \
    apt-get -y install curl runit && \
    rm -rf /var/lib/apt/lists/*; \
    curl -L $CT_URL | tar -C /usr/local/bin --strip-components 1 -zxf - ; \
    chmod +x /etc/service/nginx/run /etc/service/consul-template/run; \
    rm -v /etc/nginx/conf.d/*;

CMD ["/usr/bin/runsvdir", "/etc/service"]
