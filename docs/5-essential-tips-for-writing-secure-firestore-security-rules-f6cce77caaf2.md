# 编写安全 Firestore 安全规则的 5 个基本技巧

> 原文：<https://levelup.gitconnected.com/5-essential-tips-for-writing-secure-firestore-security-rules-f6cce77caaf2>

![](img/7f79312038e59e31b52e712b8ced4db3.png)

# 介绍

欢迎阅读我们的安全 Firestore 安全规则编写指南！如果你正在使用 Firestore，谷歌云的 NoSQL 数据库，那么你就知道保证你的数据安全是多么重要。做到这一点的一个关键方法是通过编写安全规则来控制对数据的访问，并确保以授权和适当的方式使用和修改数据。

但是编写安全的安全规则可能具有挑战性，尤其是如果您是 Firestore 的新手，或者如果您有一个复杂或高度定制的数据库。在这篇博客中，我们将为您提供编写安全 Firestore 安全规则的五个基本提示，以及一些示例和最佳实践，以帮助您在自己的项目中应用这些提示。

在我们深入了解这些技巧之前，让我们快速了解一下 Firestore 是什么以及它是如何处理安全性的。Firestore 是一个完全托管的云原生 NoSQL 数据库，可实时存储和同步数据。它设计灵活、可扩展且易于使用，内置了对安全性和数据保护的支持。

Firestore 保护您数据的一个重要方法是使用安全规则。这些规则是用一种称为 Firestore 安全规则语言的特殊语法编写的，它们定义了用户如何访问和修改数据库中的数据。您可以使用安全规则来控制对特定路径或数据集合的访问，在将数据写入数据库之前验证数据，以及实现其他与安全相关的逻辑。

现在你对 Firestore 是什么以及它如何使用安全规则有了一个基本的了解，让我们来看看编写安全的安全规则的五个基本技巧。这些提示将帮助您确保您的数据不会受到未经授权的访问和滥用，并且您的安全规则易于维护和故障排除。

# 技巧 1:小心使用通配符

通配符是 Firestore 安全规则中的一个强大工具，但如果不小心使用，它们也会很危险。通配符允许您匹配包含变量或未知元素的路径或数据，这对于实现动态或通用规则非常有用。但是，如果不小心，还可能意外地允许未经授权的人访问您的数据，或者创建难以维护或排除故障的规则。

那么，通配符在 Firestore 安全规则中是如何工作的呢？通配符由`*`字符表示，可以用来匹配任何路径或数据元素。例如，您可以使用通配符来匹配集合中的任何文档，如下所示:

```
match /users/{userId} {
  allow read: if request.auth.uid == userId;
  allow write: if request.auth.uid == userId;
}

match /posts/{postId} {
  allow read: if request.auth.uid == resource.data.authorId;
  allow write: if request.auth.uid == resource.data.authorId;
}

match /comments/{commentId} {
  allow read: if request.auth.uid == resource.data.authorId;
  allow write: if request.auth.uid == resource.data.authorId;
}

// Allow anyone to read public posts
match /publicPosts/{postId} {
  allow read: true;
  allow write: if request.auth.uid == resource.data.authorId;
}
```

在本例中，`{userId}`、`{postId}`和`{commentId}`通配符用于匹配相应路径段中的任何字符串。这使得规则可以应用于各自集合中的任何用户、帖子或评论。

虽然通配符对于创建通用或动态规则很有用，但小心使用它们以避免意想不到的后果也很重要。以下是在 Firestore 安全规则中使用通配符的一些最佳实践:

*   尽量少用通配符:通配符可以让你的规则更通用，更不具体，这使得它们更难理解和维护。通常，只有在需要匹配真正可变或未知的路径或数据时，才使用通配符是个好主意。
*   请注意通配符的范围:通配符可以匹配任何路径或数据元素，这意味着它们也可能暴露敏感或私有数据。请确保您了解通配符的范围以及它们可能如何影响您的数据。
*   彻底测试您的通配符规则:通配符规则可能特别难以测试和调试，因为它们可以匹配许多不同的路径和数据元素。确保您彻底测试了您的通配符规则，以确保它们按预期工作。

通过遵循这些最佳实践，您可以在 Firestore 安全规则中有效地使用通配符，而不会使您的数据面临不必要的风险。

# 技巧#2:在写入数据库之前验证数据

在将数据写入数据库之前对其进行验证是一项重要的安全措施，有助于保护您的数据不被未经授权的用户或恶意输入修改或破坏。在 Firestore 中，您可以在将数据写入数据库之前使用安全规则来验证数据，从而确保只有经过正确格式化和授权的数据才能存储在数据库中。

那么，在将数据写入数据库之前，如何使用安全规则来验证数据呢？Firestore 安全规则允许您指定将数据写入数据库时必须满足的条件。您可以使用这些条件来验证数据，方法是检查特定的值、模式或您希望允许或禁止的其他特征。

下面是一个示例，说明在将数据写入数据库之前，如何使用安全规则来验证数据:

```
match /users/{userId} {
  allow write: if request.auth.uid == userId &&
               request.resource.data.age > 18 &&
               request.resource.data.username is string &&
               request.resource.data.username.size() <= 20;
}
```

在本例中，仅当满足以下条件时，安全规则才允许将数据写入到`/users/{userId}`路径:

*   请求的认证用户 ID ( `request.auth.uid`)匹配`userId`路径段。这确保了只有拥有数据的用户才能修改它。
*   正在写入的数据中的`age`字段必须大于 18。这确保了只有 18 岁以上的用户才能写入数据库。
*   `username`字段必须是字符串，长度不得超过 20 个字符。这确保了`username`字段被正确格式化，并且不超过最大允许长度。

现在，让我们看看在 Firestore 安全规则中实现数据验证的一些最佳实践。首先，确保验证所有写入数据库的数据。这包括您直接编写的数据，以及由您的应用程序或服务器端函数生成或修改的数据。

另一个重要的最佳实践是在适当的粒度级别验证数据。这意味着您应该在尽可能靠近数据源的地方验证数据，而不是依赖安全规则来捕捉所有错误或无效数据。例如，如果您有一个允许用户输入数据的表单，您应该在将数据发送到服务器之前在客户端验证数据。这有助于防止无效数据被写入数据库，并可以减轻安全规则的负担。

使用安全规则来加强数据约束和数据关系也是一个好主意。例如，您可以使用安全性规则来确保某些数据字段是必需的，或者通过确保数据项以特定方式相关来强制数据完整性。

以下是一些常见数据验证场景的示例，以及您如何在 Firestore 安全规则中处理它们:

*   验证数据类型:您可以在安全规则中使用`is`操作符来确保数据是特定的类型。例如，您可以使用`request.resource.data.age is int`来确保`age`字段是一个整数。
*   验证数据值:您可以在安全规则中使用比较运算符，如`<`、`>`、`<=`和`>=`，以确保数据值在特定的范围内。例如，您可以使用`request.resource.data.age >= 18 && request.resource.data.age <= 65`来确保`age`字段介于 18 和 65 之间。
*   验证数据模式:您可以在安全规则中使用正则表达式来确保数据匹配特定的模式。例如，您可以使用`request.resource.data.email is string && request.resource.data.email.matches(".+@.+\..+")`来确保`email`字段是一个有效的电子邮件地址。

总的来说，数据验证是保护 Firestore 数据库的一个重要部分。通过在将数据写入数据库之前使用安全规则来验证数据，可以确保只有经过正确格式化和授权的数据才存储在数据库中，从而降低出错或安全漏洞的风险。

以下是在 Firestore 安全规则中实施数据验证时需要记住的一些最佳实践:

*   彻底测试您的安全规则，以确保它们按预期工作。这可能涉及编写单元测试或使用 Firebase 模拟器在模拟环境中测试您的规则。
*   使用描述性错误消息帮助您解决安全规则的问题。这可以更容易地确定错误的原因并快速修复它。
*   考虑在安全规则中使用自定义函数来封装复杂的验证逻辑。这可以使您的规则更具可读性，更易于维护。
*   不要依赖安全规则来验证所有数据。最好也在客户端和服务器端验证数据，以确保数据得到正确的格式化和授权。

# 技巧 3:明智地使用条件表达式

条件表达式是 Firestore 安全规则语言的一个重要特征，允许您根据特定条件控制对数据的访问。它们可以很好地定制您的安全规则并使它们更具动态性，但是如果您不小心的话，它们也会带来安全漏洞。

那么，Firestore 安全规则中的条件表达式是如何工作的呢？条件表达式是根据一个或多个变量或表达式的值计算出`true`或`false`的语句。您可以在安全规则中使用条件表达式来指定访问或修改数据时必须满足的条件。

以下是如何在安全规则中使用条件表达式的示例:

```
match /users/{userId} {
  allow read: if request.auth.uid == userId || request.auth.uid == resource.data.managerId;
  allow write: if request.auth.uid == userId;
}
```

在本例中，安全规则允许拥有数据的用户(`request.auth.uid == userId`)或用户的经理(`request.auth.uid == resource.data.managerId`)读取`/users/{userId}`路径中的数据。`||`操作符用于指定要应用的规则必须满足任一条件。

现在，让我们看看在 Firestore 安全规则中使用条件表达式的一些最佳实践。首先，一定要清楚地定义每条规则必须满足的条件。这将帮助您确保您的规则得到正确实施，并且它们正在实施您想要的访问控制。

另一个重要的最佳实践是尽量减少复杂条件表达式的使用。复杂的表达式可能难以阅读和理解，也更容易出错或出现安全漏洞。只要有可能，尽量使用简单、直接、易于理解和维护的表达方式。

在条件表达式中使用描述性变量和函数名也是一个好主意。这可以使您的规则更具可读性，更容易理解，特别是当您与其他开发人员一起工作时。

以下是一些常见条件表达式场景的示例，以及您可能如何在 Firestore 安全规则中处理它们:

*   基于用户角色控制访问:您可以使用安全性规则根据用户的角色或权限授予或拒绝对数据的访问。例如，您可以使用类似于`request.auth.token.admin == true`的条件表达式向角色为`admin`的用户授予访问权限。
*   实施数据约束:您可以使用安全性规则来实施数据约束，例如最小值、最大值或必需的数据字段。例如，您可以使用类似于`request.resource.data.age >= 18`的条件表达式来确保用户至少年满 18 岁。
*   验证数据模式:您可以在安全规则中使用正则表达式来确保数据匹配特定的模式。例如，您可以使用`request.resource.data.email.matches(".+@.+\..+")`来确保`email`字段是一个有效的电子邮件地址。

总的来说，条件表达式是控制 Firestore 数据库中数据访问的强大工具。通过明智地使用它们并遵循最佳实践，您可以确保您的安全规则是有效和安全的。

# 技巧 4:保持你的安全规则简单和可维护

编写清晰和可维护的安全规则是保护 Firestore 数据库的重要部分。好的安全规则易于理解，易于修改，并且在出错时易于调试。另一方面，写得不好或组织得不好的安全规则可能难以理解、难以维护，并且更容易出现错误或安全漏洞。

那么，如何为 Firestore 数据库编写清晰且可维护的安全规则呢？以下是一些需要记住的最佳实践:

*   让您的安全规则尽可能简单。复杂的规则更难理解和维护，也更容易出错。只要有可能，尽量使用简单、直接、易于理解和修改的规则。
*   使用描述性的变量和函数名。描述性的名称可以使您的规则更易读、更容易理解，尤其是当您与其他开发人员一起工作时。
*   以逻辑和一致的方式组织您的安全规则。这使得在需要时更容易找到和修改特定的规则。
*   彻底记录您的安全规则。好的文档可以帮助您理解安全规则是如何工作的，也可以让其他开发人员更容易地使用您的规则。

现在，让我们来看一些组织和整理您的安全规则的技巧。保持规则有条理的一个方法是按照功能或目的对它们进行分组。例如，您可能有不同的规则来控制对数据的访问、实施数据约束和验证数据模式。

保持规则有序的另一种方法是使用注释和空格将规则分成逻辑部分。这可以使您的规则更容易阅读和理解，特别是如果您有大量的规则或复杂的规则。

以下是组织和维护安全规则的一些提示:

*   使用版本控制跟踪安全性规则的更改。这可以帮助您确定何时以及为什么进行了更改，并且如果需要，还可以使回滚更改变得更容易。
*   彻底测试您的安全规则，以确保它们按预期工作。这可能涉及编写单元测试或使用 Firebase 模拟器在模拟环境中测试您的规则。
*   使用描述性错误消息帮助您解决安全规则的问题。这可以更容易地确定错误的原因并快速修复它。
*   如果需要，不要害怕重构或重新组织您的安全规则。随着数据库的增长或访问控制需求的变化，您的安全规则可能也需要发展。通过保持规则的简单性和可维护性，您将更好地准备根据需要进行这些更改。

总的来说，保持您的安全规则简单和可维护是保护您的 Firestore 数据库的一个重要部分。通过遵循这些最佳实践，您可以确保您的规则是有效的，并且易于理解和维护。

# 技巧 5:测试和调试你的安全规则

测试和调试您的安全规则是保护您的 Firestore 数据库的一个重要部分。通过测试您的规则，您可以确保它们如预期的那样工作，并且它们正在实施您预期的访问控制。

那么，如何测试和调试您的安全规则呢？一种方法是使用 Firebase 模拟器，这是一种允许您在本地环境中模拟 Firestore 数据库行为和安全规则的工具。模拟器对于在模拟环境中测试您的安全规则非常有用，而且在将规则部署到生产环境之前，它也是测试您的规则的好方法。

要使用模拟器，您需要安装 Firebase CLI 并设置一个本地开发环境。您还需要指定要在模拟器配置文件中测试的规则和数据。

下面是一个如何使用模拟器测试安全规则的示例:

```
firebase emulators:start --only firestore

firebase emulators:exec "firebase firestore:rules:run"
```

第一个命令启动模拟器，第二个命令针对模拟器数据运行您的安全规则。如果您的规则有任何问题，模拟器将输出错误消息，帮助您解决问题。

现在，让我们来看一些排除安全规则常见问题的提示。一个常见的问题是规则语法错误，如果规则中有打字错误或其他错误，就会出现这种情况。要修复语法错误，您需要仔细检查您的规则并寻找错误。

另一个常见的问题是规则过于宽松或过于严格。如果您的规则过于宽松，它们可能无法实施您想要的访问控制。另一方面，如果您的规则过于严格，它们可能会阻止授权用户访问他们需要的数据。要解决这些问题，您需要仔细检查您的规则，并根据需要进行调整。

最后，让我们看一些随着时间的推移维护和更新安全规则的最佳实践。随着数据库的增长或访问控制需求的变化，您的安全规则可能也需要发展。要使您的规则保持最新，请考虑以下最佳实践:

*   使用版本控制跟踪安全性规则的更改。这可以帮助您确定何时以及为什么进行了更改，并且如果需要，还可以使回滚更改变得更容易。
*   彻底测试您的安全规则，以确保它们按预期工作。这可能涉及编写单元测试或使用 Firebase 模拟器在模拟环境中测试您的规则。
*   使用描述性错误消息帮助您解决安全规则的问题。这可以更容易地确定错误的原因并快速修复它。
*   如果需要，不要害怕重构或重新组织您的安全规则。随着数据库的增长或访问控制需求的变化，您的安全规则可能也需要发展。通过保持规则的简单性和可维护性，您将更好地准备根据需要进行这些更改。

总的来说，测试和调试您的安全规则是保护您的 Firestore 数据库的一个重要部分。

# 结论

在这篇博文中，我们介绍了编写安全 Firestore 安全规则的 5 个基本技巧:

1.  小心使用通配符
2.  在写入数据库之前验证数据
3.  明智地使用条件表达式
4.  保持您的安全规则简单且可维护
5.  测试和调试您的安全规则

通过遵循这些提示，您可以确保您的 Firestore 安全规则是有效和安全的。您将能够更有效地控制对数据的访问，强制实施数据约束，并防止对数据的未授权访问或篡改。

如果你想了解更多关于 Firestore 安全规则的信息，网上有很多资源。Firebase 文档是一个很好的起点，还有许多在线教程、博客帖子和其他资源可以帮助您了解更多关于 Firestore 安全规则的信息。

要在您自己的项目中应用这些技巧，您需要熟悉为 Firestore 编写安全规则的基础知识。一旦您很好地理解了安全规则的基本语法和结构，您就可以开始将这些技巧应用到您自己的规则中，以确保您的 Firestore 数据库的安全性。

总的来说，Firestore 安全规则是控制数据访问和确保数据库安全的强大工具。通过遵循这些基本提示，您可以为您的 Firestore 数据库编写安全有效的安全规则。因此，这些是你可以遵循的提示，使你的 Firestore 数据库安全。

**不要错过我即将推出的内容和技术指南:**

[](https://medium.com/@nicchong/subscribe) [## 每当 Nic Chong 发布时收到电子邮件。

### 每当 Nic Chong 发布时收到电子邮件。注册后，如果您还没有，您将创建一个中型帐户…

medium.com](https://medium.com/@nicchong/subscribe) 

如果你有什么问题，我在这里帮忙，在评论区等你:)