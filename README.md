# Simplepush for C#/.NET

Using the simplepush.io notification from C# 


```csharp
using System.Collections.Generic;
using System.Net.Http;
using System.Net.Http.Json;
using System.Text;
using System.Threading.Tasks;
using Newtonsoft.Json;

namespace simplepush_csharp_net48
{
    class Program
    {
        static async Task Main(string[] args)
        {
            using (var client = new HttpClient())
            {
                string serviceUrl = "https://api.simplepush.io/send";

                var data = new Dictionary<string, string>
                {
                    { "key",    "HuxgBB" },
                    { "title",  "title" },
                    { "msg",    "message" },
                    { "event",  "event" }
                };


                // -------------------------------------------------------------------------------
                // using regular HttpClient and Json.NET for serializing the data
                data["msg"] = "message using regular HttpClient";
                var json = JsonConvert.SerializeObject(data);
                var postdata = new StringContent(json, Encoding.UTF8, "application/json");
                var response = await client.PostAsync(serviceUrl, postdata);
                response.EnsureSuccessStatusCode();


                // -------------------------------------------------------------------------------
                // Another way using System.Net.Http.Json
                data["msg"] = "message using System.Net.Http.Json PostAsJsonAsync";
                response = await client.PostAsJsonAsync(serviceUrl, data);
                response.EnsureSuccessStatusCode();
            }
        }
    }
}

```