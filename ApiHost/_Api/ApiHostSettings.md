# Class: `ApiHostSettings`

# Information
 - Imported from: `Exolix.ApiHost`

# Public Properties
| Key           | Type                                             | Default   | Explained                                            |
| ------------- | ------------------------------------------------ | --------- | ---------------------------------------------------- |
| `Port`        | `int?`                                           | `null`    | Server port, use null for no port                    |
| `Host`        | `string`                                         | `"0.0.0.0"` | Server hostname without port                         |
| `Certificate` | [`ApiHostCertificate?`](./ApiHostCertificate.md) | `null`    | API SSL certificate information, use null for no SSL |
| `PeerNodes`   | [`ApiPeerNode[ ]?`](./ApiPeerNode.md)            | `null`    | API host peer nodes                                  |

```cs
public class ApiHostSettings
	{
		public string Host = "0.0.0.0";
		public int? Port = null;
		public ApiHostCertificate? Certificate = null;
		public ApiPeerAuth? PeerAuth = null;
		public List<ApiPeerNode>? PeerNodes = null;
	}
 ```

<!-- Axeri Document-End -->
[Next (ApiHostCertificate)](./ApiHostCertificate.md)
