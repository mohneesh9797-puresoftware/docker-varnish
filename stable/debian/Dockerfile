FROM debian:stretch
ENV SIZE 100M

RUN set -ex; \
	fetchDeps=" \
		dirmngr \
		gnupg \
	"; \
	apt-get update; \
	apt-get install -y --no-install-recommends varnish; \
	apt -a show varnish; \
	apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false $fetchDeps; \
	rm -rf /var/lib/apt/lists/*


WORKDIR /etc/varnish

COPY docker-varnish-entrypoint /usr/local/bin/
ENTRYPOINT ["docker-varnish-entrypoint"]

EXPOSE 80 8443
CMD varnishd -F -f /etc/varnish/default.vcl -a http=:80,HTTP -a proxy=:8443,PROXY -s malloc,$SIZE
