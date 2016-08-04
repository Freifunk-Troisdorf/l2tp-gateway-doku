.. _radvd:

RAdvD
=====

Damit die Clients im Netz auch in den Genuss von öffentlichem IPv6 kommen, müssen die Public IPv6-Prefixe zusätzlich zu den ULA-Prefixes per Router Advertisements bekannt gegeben werden. Dazu ergänzt man die Public IPv6-Prefixe in der /etc/radvd.conf:

	interface bat0 {
	        AdvSendAdvert on;
	        IgnoreIfMissing on;
	        MaxRtrAdvInterval 200;
	        RDNSS 2a03:2260:121::255:5 {};
	        prefix 2a03:2260:121::/64 {
	                AdvOnLink on;
	                AdvAutonomous on;
	                AdvRouterAddr on;
	        };
	};

