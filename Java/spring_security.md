

```
@EnableConfigurationProperties

```



Spring注解@Component、@Repository、@Service、@Controller区别

1. `@Service` 用于标注业务层组件
2. `@Controller` 用于标注控制层组件（如struts中的action）
3. `@Repository` 用于标注数据访问组件，即DAO组件
4. `@Component` 泛指组件，当组件不好归类的时候，我们可以使用这个注解进行标









http://localhost:8080/oauth/authorize?client_id=c1&client_secret=secret&response_type=code

http://localhost:8080/oauth/token?client_id=c1&client_secret=secret&grant_type=authorization_code&code=688aQr

http://localhost:8080/oauth/check_token?token=bcadb979-9849-4d28-b3ae-7c9449b2fc23

### OAuth2.0 流程

```mermaid
sequenceDiagram
participant 用户
participant 应用网页端
participant 应用服务
participant OAuth服务
participant 资源服务
用户->>应用网页端:访问网站
应用网页端->>OAuth服务: 携带回调url参数打开OAuth授权页面
OAuth服务->>OAuth服务:验证用户
OAuth服务-->>用户:给用户展示授权页面(若未登录则返回登录页面)
用户->>OAuth服务:同意授权
OAuth服务->>OAuth服务:验证用户
OAuth服务->>应用服务:添加code参数跳转应用服务的回调地址
应用服务->>OAuth服务:用code获取access_token和refresh_token
应用服务->>+资源服务:用access_token获取用户信息
资源服务->>+OAuth服务:验证access_token是否有效
OAuth服务-->>-资源服务:access_token有效
资源服务-->>-应用服务:返回用户信息
应用服务->>应用服务:设置用户已登录状态
应用服务-->>应用网页端:跳转到应用网页端
应用网页端-->>用户:呈现已登录页面
```



