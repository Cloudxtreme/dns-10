# @(#) $Tau: dns/Makefile $

## ------------------------------------------------------------------------- ##
##                          T A U    P R O J E C T                           ##
## ------------------------------------------------------------------------- ##
##                                                                           ##
##  Licensed under the Apache License, Version 2.0 (the "License");          ##
##  you may not use this file except in compliance with the License.         ##
##                                                                           ##
##  You may obtain a copy of the License at:                                 ##
##                                                                           ##
##      http://www.apache.org/licenses/LICENSE-2.0                           ##
##                                                                           ##
##  Unless required by applicable law or agreed to in writing, software      ##
##  distributed under the License is distributed on an "AS-IS" BASIS,        ##
##  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. ##
##  See the License for the specific language governing permissions and      ##
##  limitations under the License.                                           ##
##                                                                           ##
## ------------------------------------------------------------------------- ##

FROM tauproject/core:shimmer

RUN DEBIAN_FRONTEND=noninteractive \
	apt-get update -qq -y && \
	apt-get install -qq -y bind9

EXPOSE 53/tcp
EXPOSE 53/udp

RUN mkdir -p /app/etc /app/config /app/config/zones /app/cache /run/named && \
	chgrp bind /app/cache /run/named && \
	chmod 775 /app/cache /run/named
COPY scripts/docker/entrypoint /app/entrypoint
COPY docker/dns/named.conf /app/etc/named.conf
COPY zones/*.zonefile /app/config/zones/

CMD [ "run" ]

ENTRYPOINT [ "/app/entrypoint" ]
