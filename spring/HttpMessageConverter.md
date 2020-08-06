# HttpMessageConverter

- 它负责将请求信息转化为一个对象，或者将对象输出为响应信息
- 被RequestMappingHandlerAdapter（HandlerAdapter的实现类）使用

**实现类**

StringHttpMessageConverter

ByteArrayHttpMessageConverter

SourceHttpMessageConverter

AllEncompassingFormHttpMessageConverter

**如何使用？**

1. 使用@RquestBody、@ResponseBody标记参数、方法
2. 使用类型HttpEntity、ResponseEntity作为方法的入参和返回值的类型

**如何确定请求消息和响应消息的格式？**

​	通过消息头的ContentType和Accept确定