# OTelCol Context

The OTelCol Context exposes data passed through the OpenTelemetry Collector by its components, including client details, request information, and incoming gRPC metadata.
Access these paths under the top-level `otelcol` segment, optionally followed by one or more sub-segments.
This data is only available inside the OpenTelemetry Collector and is not included by default in telemetry exported from the Collector.

## Paths

The following paths are supported.

| path                               | field accessed                                                                                                            | type                                                                    |
|------------------------------------|---------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| otelcol.client.addr                | the remote address string from the client info                                                                            | string                                                                  |
| otelcol.client.metadata            | client metadata attached to the request via `go.opentelemetry.io/collector/client`                                        | pcommon.Map                                                             |
| otelcol.client.metadata[""]        | the value for a specific metadata key                                                                                     | string or nil                                                           |
| otelcol.client.auth.attributes     | map of all auth attributes values extracted from `client.Info.Auth`. Unsupported value types are mapped as empty string   | pcommon.Map                                                             |
| otelcol.client.auth.attributes[""] | the value for a specific auth attribute key                                                                               | string, bool, int64, float64, pcommon.Map, pcommon.Slice, []byte or nil |
| otelcol.grpc.metadata              | incoming gRPC metadata from the context                                                                                   | pcommon.Map                                                             |
| otelcol.grpc.metadata[""]          | values slice for a specific incoming gRPC metadata key                                                                    | string or nil                                                           |


> [!NOTE]
This context is read-only; any attempt to set these paths returns an error.