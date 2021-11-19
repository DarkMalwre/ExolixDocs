# Exolix.ApiHost
The Exolix.ApiHost starts a server on your localhost. You can host your API

### Setting up a server
You can simply set up a server using the ApiHost.

ApiHostSettings Options:
* Port: The port the server will run on
* Host: The host, which the server will run on, defaults to 0.0.0.0

```cs
using Exolix.ApiHost;
using Exolix.Terminal;

class Program 
{
    ApiHost server = new ApiHost(new ApiHostSettings
    {
        Port = 8080
    });
}
```

### Want node clusters?
This is a single node cluster, this server will use itself as a peer node

**NOTE**: This function is **NOT** fully tested and not recommended to use for public APIs

Example:
```cs
using Exolix.ApiHost;
using Exolix.Terminal;

class Program 
{
    ApiHost server = new ApiHost(new ApiHostSettings
    {
        Port = 8080,
        PeerNodes = new List<ApiPeerNode> {
            new ApiPeerNode {
                Port = 8080,
                Key1 = "k1-secret",
                Key2 = "k2-secret"
            }
        },
        PeerAuth = new ApiPeerAuth {
            Key1 = "k1-secret",
            Key2 = "k1-secret"
        }
    });
}
```

### Adding an OnReady() event
Now, when you have your server created, you can add an OnReady() event. It will fire once the ApiHost server is ready!

Arguments:
* None

```cs
using Exolix.ApiHost;
using Exolix.Terminal;

class Program 
{
    ApiHost server = new ApiHost(new ApiHostSettings
    {
        Port = 8080
    });
    
    server.OnReady(() => 
    {
      // The code that will execute once your server is ready
      Logger.Success("ApiHost server is ready!");
    });
    
    server.Run()
}
```

### Adding an OnOpen() event to the server
Since you have the OnReady() event setup, you can now put some events in there! Here there is an example for the OnOpen() event. This event will automatically fire when a connection is made to your server.

Argumetns:
* Connection: `ApiHost.ApiConnection` object

```cs
using Exolix.ApiHost;
using Exolix.Terminal;

class Program 
{
    ApiHost server = new ApiHost(new ApiHostSettings
    {
        Port = 8080
    });
    
    server.OnReady(() => 
    {
      Logger.Success("ApiHost server is ready!");
      api.OnOpen((connection) => 
      {
        // This code will execute when a connection is made to your server
        Logger.Info("Connection added")
        
      }
      
    });
    
    server.Run()
}
```

### Adding an OnClose() event to the server
The OnClose() event will be put into the OnOpen() event, so make sure you have the OnOpen() event setup correctly. This event will fire, once the connection closes or breaks.

Arguments:
* None

```cs
using Exolix.ApiHost;
using Exolix.Terminal;

class Program 
{
    ApiHost server = new ApiHost(new ApiHostSettings
    {
        Port = 8080
    });
    
    server.OnReady(() => 
    {
      Logger.Success("ApiHost server is ready!");
      api.OnOpen((connection) => 
      {
        connection.OnClose(() =>
        {
          // This code will execute once the connection closes or breaks
          Logger.Warning("Connection lost")
        });
        Logger.Info("Connection added")
        
      }
      
    });
    
    server.Run()
}
```

Any Questions? Join our discord support server!
https://discord.gg/KF5XV7Yq
