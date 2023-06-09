# 缓存那些 API 令牌(专长。Gfycat):优化 Django:第 6 部分

> 原文：<https://levelup.gitconnected.com/cache-those-api-tokens-feat-gfycat-optimising-django-part-6-cf493d978ef1>

![](img/4ad7cc21c670e249378030fa321f9714.png)

约什·格劳泽在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

连接到第三方 API 时的一个常见任务是必须处理 API 令牌。通常，这些令牌最容易通过对 API 的单个客户端身份验证调用来获得。此外，它们有固定的寿命，需要你定期更新。如果没有任何缓存，您很可能会为每个服务调用创建一个新的令牌，从而导致许多冗余的令牌请求，进而在不必要的 API 调用上浪费时间。

在本文中，我将解释如何设置一个健壮的系统，该系统可以在您的服务器上自动缓存和更新 API 令牌。为此，我将使用 Gfycat 作为我的示例，因为它使用基于令牌的身份验证，并且其令牌的生命周期很短，只有一个小时(在撰写本文时)。想了解更多关于 Gfycat 开发者 API 的信息，你可以查看他们的网站，[developers.gfycat.com](https://developers.gfycat.com/api/)。

# 在我们继续之前…

本文假设您已经知道如何在 Django 服务器中缓存数据。如果你想了解更多，我已经在这里写了一篇关于这个的文章！撇开这个不谈，让我们开始吧。

# 那么要点是什么呢？(适用于懒人)

我知道你们中的一些人可能会先复制粘贴要点(我知道我会的)，所以在这里。不要担心，如果你对它的工作方式感兴趣，我会进一步解释，并确保它按照你需要的方式运行。

# 这是怎么回事？

您会注意到该脚本被分解为 3 个函数:

1.  获取和缓存令牌。我们大部分的注意力都会在这里。
2.  形成 Gfycat 头，它从第一个函数中获取令牌，以及
3.  一个简单的 Gfycat API 调用，通过它的 ID 获取 Gfycat 的数据，从第二个函数中获取所需的 Gfycat 头。

让我们更仔细地检查一下`get_gfycat_auth_header`。

```
def get_gfycat_auth_header():
    token = cache.get(GFYCAT_TOKEN_CACHE_KEY)
    if not token:
        # Get the token!
        data = {
            'client_id': settings.GFYCAT_API_KEY,
            'client_secret': settings.GFYCAT_API_SECRET,
            'grant_type': 'client_credentials'
        }
        resp = requests.post(GFYCAT_TOKEN_URL,
                             data=json.dumps(data))
        if resp.status_code < 300:
            resp_data = resp.json()
            token = resp_data['access_token']
            cache.set(GFYCAT_TOKEN_CACHE_KEY, token,
                      resp_data['expires_in'])
        else:  # bad things have happened, error handling goes here.
            return None
    return {'Authorization': 'Bearer {}'.format(token)}
```

该函数执行以下操作:

1.  如果缓存的令牌已经存在，请尝试获取它。如果令牌在那里，就返回它。如果没有，
2.  使用 API 密钥和秘密，对 Gfycat 进行适当的 API 调用。如果调用有效，缓存令牌并返回它。

如果由于某种原因，错误经常发生，您可能希望添加错误处理。否则你应该完成这一部分。

正在执行的一个关键操作是缓存超时。这是从客户端 auth 响应中获得的，通常以秒为单位(在 Gfycat 的例子中，超时值是在`'expires_in'`键下给出的。

```
cache.set(GFYCAT_TOKEN_CACHE_KEY,  # Cache key
          token,                   # Token value
          resp_data['expires_in']) # Timeout (taken from response)
```

设置超时值可确保令牌仅在前一个过期后生成。

令牌超时通常以秒为单位给出，但是如果它以其他形式给出，比如时间戳，或者根本没有给出，那么您必须相应地调整这个段。

# 什么使这成为一个好的解决方案？

首先，获得令牌的网络成本虽然很小，但也不是微不足道的。生成一个令牌可能不需要整整一分钟(如果您每小时都在重建一个大的缓存，可能会出现这种情况！)，但是如果没有这个解决方案，您每次调用第三方 API 的往返时间会增加大约 20-100ms。

通过添加一个小的缓存值，我们可以消除大部分额外的开销。为这样的效率提高付出一点点代价绝对值得努力实现，尤其是如果您的服务频繁使用 API 的话。

# 感谢您阅读本文！

正如您在“第 6 部分”中看到的，我已经写了几篇关于如何提高 Django 服务器性能的文章。如果你想知道如何提高你的 Django 管理性能，[点击这里。](/dealing-with-multiple-massive-tables-in-a-single-admin-optimizing-django-part-3-2c4ee2fec142?source=friends_link&sk=96a35d8e435719670b356ca4c4606c1c)或者如果你想了解 n+1 问题以及如何解决它，[点击这里！](/dealing-with-the-n-1-problem-optimising-django-part-4-f02010c7931d?source=your_stories_page-------------------------------------)