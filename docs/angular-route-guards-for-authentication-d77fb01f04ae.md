# 用于认证的角形路由保护

> 原文：<https://levelup.gitconnected.com/angular-route-guards-for-authentication-d77fb01f04ae>

## 如何限制应用内导航？

![](img/527d7888a10bd92da3e8371e2a9e2e85.png)

在您的 angular web 应用程序中，您可能需要限制某些用户对某些页面的访问，或者换句话说，您可能正在寻找一种方法来验证来自客户端的应用程序内导航。这就是棱角分明的路线警卫会让你的生活变得轻松。**角度路线守卫是一个接口，可以执行该接口来决定是否可以激活路线。那么，事不宜迟，让我们开始吧！**

Angular 中有 5 种类型的防护，即 **CanActivate、CanActivateChild、CanDeactivate、Resolve** 和 **CanLoad。**让我们来看看**可以激活的防护装置**，它是常用的防护装置之一，它会让您更好地了解如何在 Angular 中使用防护装置。

***只需 3 步！***

## 步骤 1:创建认证服务

在这个例子中，我将使用 [JSON Web 令牌(JWT)](https://jwt.io/) ，这是最流行的认证用户的方法之一。首先，让我们创建 *auth.service.ts* 来处理认证。`ng g service auth`将帮助您生成认证服务。

**isLoggedIn()** 函数将从本地存储中获取令牌，并根据到期时间检查令牌有效负载的有效性。

## 步骤 2:创建路线守卫

使用以下命令生成保护。

`ng g guard auth`

这将创建实现 CanActivate 接口的 *auth.guard.ts* 。

*canActivate()* 方法将使用认证服务的实例，并返回用户是否登录。如果未登录，用户将被重定向至`/login`路线。

## 第三步:使用路线内的警卫

角度路由有一个名为 **canActivate** 的属性，该属性接受一个防护阵列，在路由到特定路由之前会对其进行检查。

现在，如果令牌过期，用户将无法访问`/home`路线，他将被重定向到`/login`路线。

很明显，路由守卫不仅对基于令牌的路由认证有用。如果购物车中没有商品，您可以在电子商务网站中使用 route guards 来限制用户访问结帐页面。

最后，我必须说，有经验的开发人员可以绕过路由防护。与用作安全功能相比，它在提供更好的用户体验方面更有用。

希望在另一篇文章中再见到你。在那之前，编码快乐！💻