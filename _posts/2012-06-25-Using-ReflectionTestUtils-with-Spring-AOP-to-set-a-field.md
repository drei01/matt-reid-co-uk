---
layout: post
title: Using ReflectionTestUtils with Spring AOP to set a field
---

When using spring"s handy ReflectionTestUtils to set a field on an AOP
proxied object, it has trouble setting fields on the proxy object
(complaining that "field not found"). In this case you need to unwrap
the original object from the proxy.








    private  Object unwrapProxy(Class clazz, Object proxy) {
             if(AopUtils.isAopProxy(proxy) && proxy instanceof Advised) {
                 try{
                     Object target = ((Advised)proxy).getTargetSource().getTarget();
                     return target;
                 }catch (Exception e) {}
              }
             return proxy;
        }

(adapted from [this](http://stackoverflow.com/a/9034022/513564)) this
can then be used to set call a setter like so:










    ReflectionTestUtils.setField((ActualClass)unwrapProxy(ActualClass.class, proxiedClass), "someField", fieldValue);



 









