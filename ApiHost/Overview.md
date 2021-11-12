# Overview
The `ApiHost` class can be constructed to create fast, and efficient API servers.<br />
Let's start by creating a basic server

```cs
using Exolix.ApiHost
using System;

namespace ApiHostTest {
	public class ServerLogMessage {
		public string Text = "No Text Provided";
	}

	public class Application {
		public static void Main(string[] args) {
			// Create the server
			ApiHost api = new ApiHost(new ApiHostSettings 
			{
				Port = 8080	
			});
			
			// Add server events
			api.OnReady(() => {
				Console.WriteLine($" [ Server ] Listening at \"{api.ListeningAddress}\"");
				
				api.OnOpen((connection) => {
					Console.WriteLine($" [ Server ] New connection opened");
					
					connection.OnMessage("log:console", (rawMessage) => {
						ServerLogMessage message = JsonHandler.Parse<ServerLogMessage>(rawMessage);
					});
				});
			});
			
			// Start the API listener
			api.Run();
		}
	}
}
