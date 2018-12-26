---
layout: post
star: false
; projects: true
; category: projects
category: blog
image: 
headerImage: false

title: "SpringBoot Validation + Kotlin校验无效的解决方法"
date: 2018-12-26
author: dawsonlee
tag:
- Kotlin
- SpringBoot

---

  [1]: /assets/posts/***/***.png
  
## DTO
    
{% highlight c++ %}
package dawsonlee1790.springboot_validation_kotlin_demo.dto

import javax.validation.constraints.Max
import javax.validation.constraints.Pattern

/**
 * @author dawsonlee1790
 * @email dawsonlee1790@gamil.com
 * @date 2018-12-26
 */
data class LoginDTO(
        @field:Pattern(regexp = "[a-zA-Z0-9]+", message = "姓名只能由数字和大小写字母组成")
        val name: String,
        @get:Max(18, message = "居然超过18岁了，可怕，不允许")
        val age: Int
)

/*
//============springboot validation 不生效============
data class LoginDTO(
        @Pattern(regexp = "[a-zA-Z0-9]+", message = "姓名只能由数字和大小写字母组成")
        val name: String,
        @Max(18, message = "居然超过18岁了，可怕，不允许")
        val age: Int
)
*/
{% endhighlight %}    

    

## controller

    package dawsonlee1790.springboot_validation_kotlin_demo.controller
    
    import dawsonlee1790.springboot_validation_kotlin_demo.dto.LoginDTO
    import org.springframework.validation.annotation.Validated
    import org.springframework.web.bind.annotation.PostMapping
    import org.springframework.web.bind.annotation.RequestBody
    import org.springframework.web.bind.annotation.RequestMapping
    import org.springframework.web.bind.annotation.RestController
    
    /**
     * @author dawsonlee1790
     * @email dawsonlee1790@gamil.com
     * @date 2018-12-26
     */
    @RestController
    @RequestMapping("/loginController")
    class LoginController {
    
        @PostMapping("/login")
        fun login(@RequestBody @Validated loginDTO: LoginDTO) {
            println("Hello ${loginDTO.name}!")
        }
    
    }
    
## 原因分析

* 在 java 中，将 validation 注解到实体类属性或者 get/set 方法上，但是在 kotlin 中，属性直接写在构造函数中，validation 注解并没有作用到属性上。

## 解决方案

* 使用 `@field:` 标识符，field标识符只允许在属性的访问器函数内使用。它能够 validation 校验注解作用与属性。
* 使用 `@get:` 标识符，表示注解用在属性getter的方法上

## 项目源码

* [springboot_validation_kotlin_demo](https://github.com/dawsonlee1790/springboot_validation_kotlin_demo)
