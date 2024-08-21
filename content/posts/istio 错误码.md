HTTP and TCP

|Long name|Short name|Description|
|---|---|---|
|**NoHealthyUpstream**|**UH**|No healthy upstream hosts in upstream cluster in addition to 503 response code.|
|**UpstreamConnectionFailure**|**UF**|Upstream connection failure in addition to 503 response code.|
|**UpstreamOverflow**|**UO**|Upstream overflow ([circuit breaking](https://www.envoyproxy.io/docs/envoy/latest/intro/arch_overview/upstream/circuit_breaking#arch-overview-circuit-break)) in addition to 503 response code.|
|**NoRouteFound**|**NR**|No [route configured](https://www.envoyproxy.io/docs/envoy/latest/intro/arch_overview/http/http_routing#arch-overview-http-routing) for a given request in addition to 404 response code or no matching filter chain for a downstream connection.|
|**UpstreamRetryLimitExceeded**|**URX**|The request was rejected because the [upstream retry limit (HTTP)](https://www.envoyproxy.io/docs/envoy/latest/api-v3/config/route/v3/route_components.proto#envoy-v3-api-field-config-route-v3-retrypolicy-num-retries) or [maximum connect attempts (TCP)](https://www.envoyproxy.io/docs/envoy/latest/api-v3/extensions/filters/network/tcp_proxy/v3/tcp_proxy.proto#envoy-v3-api-field-extensions-filters-network-tcp-proxy-v3-tcpproxy-max-connect-attempts) was reached.|
|**NoClusterFound**|**NC**|Upstream cluster not found.|
|**DurationTimeout**|**DT**|When a request or connection exceeded [max_connection_duration](https://www.envoyproxy.io/docs/envoy/latest/api-v3/config/core/v3/protocol.proto#envoy-v3-api-field-config-core-v3-httpprotocoloptions-max-connection-duration) or [max_downstream_connection_duration](https://www.envoyproxy.io/docs/envoy/latest/api-v3/extensions/filters/network/tcp_proxy/v3/tcp_proxy.proto#envoy-v3-api-field-extensions-filters-network-tcp-proxy-v3-tcpproxy-max-downstream-connection-duration).|

HTTP only

|Long name|Short name|Description|
|---|---|---|
|**DownstreamConnectionTermination**|**DC**|Downstream connection termination.|
|**FailedLocalHealthCheck**|**LH**|Local service failed [health check request](https://www.envoyproxy.io/docs/envoy/latest/intro/arch_overview/upstream/health_checking#arch-overview-health-checking) in addition to 503 response code.|
|**UpstreamRequestTimeout**|**UT**|Upstream request timeout in addition to 504 response code.|
|**LocalReset**|**LR**|Connection local reset in addition to 503 response code.|
|**UpstreamRemoteReset**|**UR**|Upstream remote reset in addition to 503 response code.|
|**UpstreamConnectionTermination**|**UC**|Upstream connection termination in addition to 503 response code.|
|**DelayInjected**|**DI**|The request processing was delayed for a period specified via [fault injection](https://www.envoyproxy.io/docs/envoy/latest/configuration/http/http_filters/fault_filter#config-http-filters-fault-injection).|
|**FaultInjected**|**FI**|The request was aborted with a response code specified via [fault injection](https://www.envoyproxy.io/docs/envoy/latest/configuration/http/http_filters/fault_filter#config-http-filters-fault-injection).|
|**RateLimited**|**RL**|The request was ratelimited locally by the [HTTP rate limit filter](https://www.envoyproxy.io/docs/envoy/latest/configuration/http/http_filters/rate_limit_filter#config-http-filters-rate-limit) in addition to 429 response code.|
|**UnauthorizedExternalService**|**UAEX**|The request was denied by the external authorization service.|
|**RateLimitServiceError**|**RLSE**|The request was rejected because there was an error in rate limit service.|
|**InvalidEnvoyRequestHeaders**|**IH**|The request was rejected because it set an invalid value for a [strictly-checked header](https://www.envoyproxy.io/docs/envoy/latest/api-v3/extensions/filters/http/router/v3/router.proto#envoy-v3-api-field-extensions-filters-http-router-v3-router-strict-check-headers) in addition to 400 response code.|
|**StreamIdleTimeout**|**SI**|Stream idle timeout in addition to 408 or 504 response code.|
|**DownstreamProtocolError**|**DPE**|The downstream request had an HTTP protocol error.|
|**UpstreamProtocolError**|**UPE**|The upstream response had an HTTP protocol error.|
|**UpstreamMaxStreamDurationReached**|**UMSDR**|The upstream request reached max stream duration.|
|**OverloadManagerTerminated**|**OM**|Overload Manager terminated the request.|
|**DnsResolutionFailed**|**DF**|The request was terminated due to DNS resolution failure.|
|**DropOverload**|**DO**|The request was terminated in addition to 503 response code due to [drop_overloads](https://www.envoyproxy.io/docs/envoy/latest/api-v3/config/endpoint/v3/endpoint.proto#envoy-v3-api-field-config-endpoint-v3-clusterloadassignment-policy-drop-overloads).|