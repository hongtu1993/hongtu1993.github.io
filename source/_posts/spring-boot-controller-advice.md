---
title: spring boot controller advice
author: 毛宇鹏
date: 2018-12-17 15:48:43
subtitle:
showTitle: SpringBoot 全局异常处理
description: Spring boot 项目全局异常处理控制器
tags:
    - spring boot
categories:
    - spring
---


```java
package cn.com.szzt.tms.ops.server.web.controllers;

import club.maoyupeng.utils.result.ResponseModel;
import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;
import org.springframework.http.HttpStatus;
import org.springframework.validation.BindingResult;
import org.springframework.validation.ObjectError;
import org.springframework.web.HttpMediaTypeNotAcceptableException;
import org.springframework.web.HttpMediaTypeNotSupportedException;
import org.springframework.web.HttpRequestMethodNotSupportedException;
import org.springframework.web.bind.MethodArgumentNotValidException;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.bind.annotation.ResponseStatus;
import org.springframework.web.servlet.NoHandlerFoundException;

import java.util.List;

/**
 * <b>标题:  全局异常处理  </b><br />
 * <pre>
 * </pre>
 *
 * @author 毛宇鹏
 * @date 创建于 下午1:56 2018/9/27
 */
@ControllerAdvice
public class ErrorController extends BaseCore {
    private static final Logger log = LogManager.getLogger(ErrorController.class);

    @ExceptionHandler(Exception.class)
    @ResponseBody
    @ResponseStatus(HttpStatus.INTERNAL_SERVER_ERROR)
    public ResponseModel systemException(Exception e) {
        log.error("System error");
        return result.error(HttpStatus.INTERNAL_SERVER_ERROR.value(), e.getMessage());
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    @ResponseBody
    @ResponseStatus(HttpStatus.UNSUPPORTED_MEDIA_TYPE)
    public ResponseModel methodNotSupported(MethodArgumentNotValidException e) {
        BindingResult bindingResult = e.getBindingResult();
        List<ObjectError> allErrors = bindingResult.getAllErrors();
        if (allErrors != null && !allErrors.isEmpty()) {
            return result.error(HttpStatus.UNSUPPORTED_MEDIA_TYPE.value(), allErrors.get(0).getDefaultMessage());
        }
        return result.error(HttpStatus.UNSUPPORTED_MEDIA_TYPE.value(), "Argument Not Valid");
    }

    @ExceptionHandler(NoHandlerFoundException.class)
    @ResponseBody
    @ResponseStatus(HttpStatus.NOT_FOUND)
    public ResponseModel methodNotSupported(NoHandlerFoundException e) {
        log.error("method not found : 404");
        return result.error(HttpStatus.NOT_FOUND.value(), e.getMessage());
    }

    @ExceptionHandler(HttpRequestMethodNotSupportedException.class)
    @ResponseBody
    @ResponseStatus(HttpStatus.METHOD_NOT_ALLOWED)
    public ResponseModel methodNotSupported(HttpRequestMethodNotSupportedException e) {
        log.error("method not support : 405");
        return result.error(HttpStatus.METHOD_NOT_ALLOWED.value(), e.getMessage());
    }

    @ExceptionHandler(HttpMediaTypeNotSupportedException.class)
    @ResponseBody
    @ResponseStatus(HttpStatus.UNSUPPORTED_MEDIA_TYPE)
    public ResponseModel mediaTypeNotSupported(HttpMediaTypeNotSupportedException e) {
        log.error("media type not support : 415");
        return result.error(HttpStatus.UNSUPPORTED_MEDIA_TYPE.value(), e.getMessage());
    }

    @ExceptionHandler(HttpMediaTypeNotAcceptableException.class)
    @ResponseBody
    @ResponseStatus(HttpStatus.NOT_ACCEPTABLE)
    public ResponseModel mediaTypeNotAcceptable(HttpMediaTypeNotAcceptableException e) {
        log.error("media type not acceptable : 406");
        return result.error(HttpStatus.NOT_ACCEPTABLE.value(), e.getMessage());
    }
}
```
