

可以使用cloudflare的workers来`中转流量`，配置为：  

addEventListener(  
&emsp;&emsp;"fetch",event => {  
&emsp;&emsp;&emsp;&emsp;let url=new URL(event.request.url);  
&emsp;&emsp;&emsp;&emsp;url.hostname="xx.herokuapp.com";//你的heroku域名    
&emsp;&emsp;&emsp;&emsp;let request=new Request(url,event.request);  
&emsp;&emsp;&emsp;&emsp;event. respondWith(  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;fetch(request)  
&emsp;&emsp;&emsp;&emsp;)  
&emsp;&emsp;}  
)  


        let url=new URL(event.request.url);

        url.hostname=host;

        let request=new Request(url,event.request);

        event. respondWith(

            fetch(request)

        )

    }

)

```



</details>



<details>

<summary>CloudFlare Workers每五天轮换一遍式反代代码</summary>





```js

const Day0 = 'app0.herokuapp.com'

const Day1 = 'app1.herokuapp.com'

const Day2 = 'app2.herokuapp.com'

const Day3 = 'app3.herokuapp.com'

const Day4 = 'app4.herokuapp.com'

addEventListener(

    "fetch",event => {

    

        let nd = new Date();

        let day = nd.getDate() % 5;

        if (day === 0) {

            host = Day0

        } else if (day === 1) {

            host = Day1

        } else if (day === 2) {

            host = Day2

        } else if (day === 3){

            host = Day3

        } else if (day === 4){

            host = Day4

        } else {

            host = Day1

        }

        

        let url=new URL(event.request.url);

        url.hostname=host;

        let request=new Request(url,event.request);

        event. respondWith(

            fetch(request)

        )

    }

)

```



</details>



<details>

<summary>CloudFlare Workers一周轮换反代代码</summary>





