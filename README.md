你好！
很冒昧用这样的方式来和你沟通，如有打扰请忽略我的提交哈。我是光年实验室（gnlab.com）的HR，在招Golang开发工程师，我们是一个技术型团队，技术氛围非常好。全职和兼职都可以，不过最好是全职，工作地点杭州。
我们公司是做流量增长的，Golang负责开发SAAS平台的应用，我们做的很多应用是全新的，工作非常有挑战也很有意思，是国内很多大厂的顾问。
如果有兴趣的话加我微信：13515810775  ，也可以访问 https://gnlab.com/，联系客服转发给HR。
# devto-go
[![Go Report Card](https://goreportcard.com/badge/github.com/ShiraazMoollatjie/devtogo?style=flat-square)](https://goreportcard.com/report/github.com/ShiraazMoollatjie/devtogo)
[![Go Doc](https://img.shields.io/badge/godoc-reference-blue.svg?style=flat-square)](http://godoc.org/github.com/ShiraazMoollatjie/devtogo)
[![Build status](https://ci.appveyor.com/api/projects/status/qiyndko2krd4ltep?svg=true)](https://ci.appveyor.com/project/ShiraazMoollatjie/devtogo)

devto-go is a REST API Wrapper for the dev.to api written in go.

# Usage

Import the package into your go file:

```go
import "github.com/ShiraazMoollatjie/devtogo"
```

Thereafter, create a client and specify your API token:
```go
cl := devtogo.NewClient(devtogo.WithApiKey("MY_API_KEY"))
```

It is also possible to not use an API key for anonymous operations.

## Retrieving articles
To retrieve a list of articles, simply use the `GetArticles` function:
```go
articles, err := cl.GetArticles(devtogo.Defaults())
```
It is also possible for us to add query parameters. For example, it's useful to retrieve articles for a specific `tag`.
The way to do this would be:
```go
al, err := cl.GetArticles(devtogo.Arguments{
		"tag": "go",
	})
```

To retrieve a single article, you need to specify the `article id`:
```go
article, err := client.GetArticle("167919")
```

## Retrieving your own articles

It is possible to retrieve your own articles using this API wrapper. There are four endpoints for this:

`GetMyArticles` returns all the articles created by you. `GetAllMyArticles` does the same thing.
```go
al, err := cl.GetMyArticles(devtogo.Defaults())
	if err != nil {
		panic(err)
	}
```

`GetMyPublishedArticles` returns all your published articles: 
```go
al, err := cl.GetMyPublishedArticles(devtogo.Defaults())
	if err != nil {
		panic(err)
	}
```

`GetMyUnpublishedArticles` returns all your draft articles.
```go
al, err := cl.GetMyUnpublishedArticles(devtogo.Defaults())
	if err != nil {
		panic(err)
	}
```

## Create a post
To create a post, use the `CreateArticle`:
```go
np, err := cl.CreateArticle(devtogo.CreateArticle{
  Title:        "My new dev.to post",
  Tags:         []string{"go"},
  BodyMarkdown: "my long markdown article that is preferably read from a file",
})
```
This will create a post with a title, tags and some content. We can also use the `Published` field to automatically
publish articles to dev.to.

## Update an article
Articles can be updated using the  `UpdateArticle` function:
```go
ua, err := cl.UpdateArticle(np.ID, devtogo.CreateArticle{
		Title:        "My updates dev.to post using the API",
		BodyMarkdown: "my new updated content",
		Published:    true,
	})
```

# Reference
https://docs.dev.to/api/
