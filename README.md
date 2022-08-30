# Siphonz 内网穿透工具

Siphonz是一个功能强大的隧道代理服务器，可以将提供各种内网的系统、服务暴露于外网可以访问的能力，可以直接访问内网的相关服务。  
欢迎提出问题、新特性、新场景，欢迎大家交流。 
## 部分使用场景

> 1、部署发布于内网内的服务，如web服务、远程桌面服务等，可以被从外网直接访问，方便开发测试。  
>
> 2、在外网直接对内网服务器进行远程维护。  
>
> 3、小型企业低成本部署企业产品与服务。  
>
> 4、现有企业内部系统上云，或与云上系统互动等。  
>
## 原理图
下图是反向代理服务器的原理图，如nginx等：  
![image](https://github.com/whitezdm/siphon/blob/main/images/reverse_proxy.png)  
1、用户发送请求到反向代理服务。  
2、反向代理服务将请求转发到具体服务来相应请求。  
3、发现代理服务是可以访问到具体服务，相互之间是互通的。  
 如果反向代理服务器无法直接访问到具体服务，那就需要使用到隧道代理服务。隧道代理可以提供内网到server的隧道连接，将服务转发到内网中。  
下图是隧道代理服务器的原理图：  
![image](https://github.com/whitezdm/siphon/blob/main/images/tunnel_proxy.png)  
1、隧道代理client从内网连接到位于公网的隧道代理server，并登录。  
2、用户发送请求到隧道代理服务。  
3、隧道代理服务服务将请求通过隧道转发到隧道代理client上。  
4、隧道代理client将请求转发到同处于内网的具体服务来相应请求。  

## 简单入门使用

>首先我们需要有一台能够外网访问的服务器，作为我们访问的入口server端，其他的在任何位置，可以访问到server端的设备都可以作为client端来转发服务。
>1、server端  
>	
>下载对应的操作系统支持的server程序，默认配置文件为server_conf.json，与server应用同目录，执行server即可。  
>	
1、client端  
>
>下载对应的操作系统支持的client程序，默认配置文件为client_conf.json，与client应用同目录，执行client即可。  
>  
## 配置文件
配置文件格式采用的json5标准，也就是可以添加注释的json格式。
以下简单说明
```
{
    "server": {
        "tcp": {
            "srv0": {
                "listen": [
                    "6100", "[::]:6100"
                ],
                "routes": [{
                        "handler": "routes",
                        "routes": [{
                                "handler": "tunnel_proxy",
                                "client": "5f092b7ca8ccd2992cde0817ed0b7e66",
                                "address": "127.0.0.1:80"
                            }
                        ]
                    }
                ]
            }
        }
    },
    "access": {
        "listen": [
            "6200", "[::]:6200"
        ],
        "client": {
            "5f092b7ca8ccd2992cde0817ed0b7e66": {
                "valid": true,
                "password": "123456"
            }
        }
    }
}
```

## 特性和核心功能清单

## 支持平台与形式

## 其他
开发语言为c++&c混合。原则上各种平台是都OK的。  
目前是以独立服务形式，提供了windows_x64、linux_x64的版本，其他的平台的版本陆续会提供。  
未来会提供调用包的形式，如jar包、dll、so、npm包等多种可调用形式，提供服务。  
以上的版本，暂未提供，如有需要可以直接联系。  
## 待开发的任务


## 联系方式 
E-mail：siphonz@hotmail.com  
wechat：siphonz
QQ群：579270417