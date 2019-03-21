---
title: springboot常用面试题
date: 2019-2-13
author: alanJiang
tags:
    - SpringBoot
categories:
    - 面试
thumbnail:  /img/thumbnail/hello.jpg
blogexcerpt: springboot常用面试题
---

## spring程序启动前接口
继承CommandLineRunner，实现run方法
```java
import org.springframework.boot.CommandLineRunner;

public class Runtime implements CommandLineRunner {
    @Override
    public void run(String... args) throws Exception {
        System.out.println("启动前运行");
    }
}
```
## 如何获取指定接口所有实现类bean
```java
import org.springframework.context.ApplicationContextAware;
import org.springframework.stereotype.Component;

import java.util.Map;
@Component
public class Runtime implements ApplicationContextAware {
    /**
     * 获取应用上下文并获取相应的接口实现类
     *
     * @param applicationContext
     * @throws 
     */
    @Override
    public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {
        //根据接口类型返回相应的所有bean
        Map<String, Job> map = applicationContext.getBeansOfType(Job.class);
        map.get("job_A").console();
        map.get("job_B").console();
        System.out.println(map);
    }
}
```
## Spring Boot 拦截器、过滤器、切片 执行顺序

1)过滤器启动
2)拦截器启动
（拦截器 preHandle）
3)切片启动
(切片执行)
4)方法体执行
5)切片结束
6)拦截器结束
7)过滤器结束

看一张图

![alt](img/mianshi/2378651-9f551f4bb069e299.png)

### 过滤器（Filter） ：可以拿到原始Http请求和响应的信息
定义
```java
@Order(1)//值越小越优先
@WebFilter(urlPatterns = "/auth/**",filterName = "uidFilter")
public class UrlParamsFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
    }
    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        MyRequert myRequert = new MyRequert((HttpServletRequest) request);
        chain.doFilter(myRequert, response);
    }
    @Override
    public void destroy() {
    }
}
```

### 拦截器（interceptor）: 可以拿到原始Http请求和响应的信息 也可拿到请求的方法的信息
定义
```java
@Component
public class AuthInterceptor implements HandlerInterceptor {
    @Autowired
    TokenUtil tokenUtil;
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        Long uid = tokenUtil.tokenIsValidaty(request);
        System.out.println(">>>MyInterceptor1>>>>>>>在请求处理之前进行调用（Controller方法调用之前）");
        return true;// 只有返回true才会继续向下执行，返回false取消当前请求
    }
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println(">>>MyInterceptor1>>>>>>>请求处理之后进行调用，但是在视图被渲染之前（Controller方法调用之后）");
    }
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println(">>>MyInterceptor1>>>>>>>在整个请求结束之后被调用，也就是在DispatcherServlet 渲染了对应的视图之后执行（主要是用于进行资源清理工作）");
    }
}
//注册拦截器
@Configuration
@RestController
public class MyWeb_Interceptor_Config extends WebMvcConfigurerAdapter {
    @Autowired
    AuthInterceptor authInterceptor;
    @Autowired
    EncryptInterceptor encryptInterceptor;
    @Autowired
    CommonInterceptor commonInterceptor;
    @Override
    @ResponseBody
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(commonInterceptor).addPathPatterns(InterceptorCFF.COMMON_URL);
        registry.addInterceptor(authInterceptor).addPathPatterns(InterceptorCFF.AUTH_URL);
        registry.addInterceptor(encryptInterceptor).addPathPatterns(InterceptorCFF.ENCRYPT_URL);
        //拦截器顺序为添加的顺序
    }
}
```

### 异常拦截器（ControllerAdvice）：可以用于定义@ExceptionHandler、@InitBinder、@ModelAttribute，并应用到所有@RequestMapping中，另外有@RestControllerAdvice
定义
```java
@ControllerAdvice
public class MyControllerAdvice {
    /**
     * 应用到所有@RequestMapping注解方法，在其执行之前初始化数据绑定器
     * @param binder
     */
    @InitBinder
    public void initBinder(WebDataBinder binder) {}
    /**
     * 把值绑定到Model中，使全局@RequestMapping可以获取到该值
     * @param model
     */
    @ModelAttribute
    public void addAttributes(Model model) {
        model.addAttribute("author", "Magical Sam");
    }
    /**
     * 全局异常捕捉处理
     * @param ex
     * @return
     */
    @ResponseBody
    @ExceptionHandler(value = Exception.class)
    public Map errorHandler(Exception ex) {
        Map map = new HashMap();
        map.put("code", 100);
        map.put("msg", ex.getMessage());
        return map;
    }
}
```
使用
获取@ModelAttribute定义值
```java
class test{
    @RequestMapping("/home")
    public String home(ModelMap modelMap) {
        System.out.println(modelMap.get("author"));
    }
    
    //或者 通过@ModelAttribute获取
    
    @RequestMapping("/home")
    public String home(@ModelAttribute("author") String author) {
        System.out.println(author);
    }
}
```

### aop切面（aspect）：可以在方法执行前后控制方法
[测试学习地址](https://github.com/alanjiang1129/springboot_aop_interface)

## spring bean生命周期
1.首先启动spring 容器
2.调用构造函数创建bean的实例化对象
3.然后进行invokeInitMethods的初始化











#

---
{% raw %}
<style>
qq {
     padding: 2px 4px;
     font-size: 90%;
     color: #c7254e;
     background-color: #f9f2f4;
     border-radius: 4px;
 }
</style>
{% endraw %}
