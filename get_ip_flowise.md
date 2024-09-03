### How to obtain the end-user's IP address and leverage it for personalized greetings

1. **Client-side IP Address Acquisition**

Retrieving the end-user's IP address requires a client-side approach. This can be done by embedding a JS snippet within the webpage hosting the Flowise chatbot. The snippet utilizes the fetch API to query a free third-party service like `Ipify`, which provides the user's public IP address. This IP is then stored in as a variable `IP_ADDRESS`.

![image](https://github.com/user-attachments/assets/16dfd436-aa7a-49cf-be0f-ec2c24719264)

2. **Integrating the IP_ADDRESS variable within Flowise**
   
To utilize the captured IP within the Flowise environment, it needs to be passed as a variable during chatbot initialization. Then, the IP can be accessed within the Flowise flow as `vars.IP_ADDRESS`.

![image](https://github.com/user-attachments/assets/0be7520d-bc34-4c7c-baf3-57c3da8e187d)


3. **Enhancing User Engagement with Geolocation**
   
One obvious use we can do with this is greeting the customer, knowing their location, and providing the weather for their city.

![image](https://github.com/user-attachments/assets/aa5bd540-665c-466d-81e9-d7def86077f6)

4. **Files**
   
Here I am including the script for the IP, the custom tool to use it in Flowise, the custom tool for getting the weather, and a simple flow with a custom prompt to make it work.

>     <script type="module">
>         import Chatbot from "https://cdn.jsdelivr.net/npm/flowise-embed/dist/web.js";
> 
>         async function getIpAddress() {
>             try {
>                 const response = await fetch('https://api.ipify.org?format=json');
>                 const data = await response.json();
>                 return data.ip;
>             } catch (error) {
>                 console.error('Error fetching IP address:', error);
>                 return 'unknown'; // Fallback value
>             }
>         }
> 
>         // Initialize the chatbot after getting the IP address
>         async function initializeChatbot() {
>             const ipAddress = await getIpAddress();
> 
>             Chatbot.init({
>                 chatflowid: "HERE",
>                 apiHost: "HERE",
>                 chatflowConfig: {
>                     vars: {
>                         "USER": "myuser",
>                         "IP_ADDRESS": ipAddress
>                     }
>                 },
>                 theme: {
>    
>                 },
>             });
>         }
> 
>         // Initialize the chatbot
>         initializeChatbot();
>     </script>



[Example Chatflow.json](https://github.com/user-attachments/files/16850714/Example.Chatflow.json)
[user_location-CustomTool.json](https://github.com/user-attachments/files/16850717/user_location-CustomTool.json)
[weather_retriever_wttrin-CustomTool.json](https://github.com/user-attachments/files/16850718/weather_retriever_wttrin-CustomTool.json)
