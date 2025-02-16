# go-bitbucket

<a class="repo-badge" href="https://godoc.org/github.com/rcompos/go-bitbucket"><img src="https://godoc.org/github.com/rcompos/go-bitbucket?status.svg" alt="go-bitbucket?status"></a>
<a href="https://goreportcard.com/report/github.com/rcompos/go-bitbucket"><img class="badge" tag="github.com/rcompos/go-bitbucket" src="https://goreportcard.com/badge/github.com/rcompos/go-bitbucket"></a>

> Bitbucket-API library for golang.

Support Bitbucket API v2.0. 

And the response type is json format defined Bitbucket API.

- Bitbucket API v2.0 <https://developer.atlassian.com/bitbucket/api/2/reference/resource/>
- Swagger for API v2.0 <https://api.bitbucket.org/swagger.json>

## Install

```sh
go get github.com/rcompos/go-bitbucket
```

## Usage

```go
package main

import (
        "fmt"

        "github.com/rcompos/go-bitbucket" 
)

func main() {

        c := bitbucket.NewBasicAuth("username", "password")

        opt := &bitbucket.PullRequestsOptions{
                Owner:             "your-team",
                RepoSlug:          "awesome-project",
                SourceBranch:      "develop",
                DestinationBranch: "master",
                Title:             "fix bug. #9999",
                CloseSourceBranch: true,
        }

        res, err := c.Repositories.PullRequests.Create(opt)
        if err != nil {
                panic(err)
        }

        fmt.Println(res) 
}
```

## FAQ

### Support Bitbucket API v1.0 ?

It does not correspond yet. Because there are many differences between v2.0 and v1.0.

- Bitbucket API v1.0 <https://confluence.atlassian.com/bitbucket/version-1-423626337.html>

It is officially recommended to use v2.0.  
But unfortunately Bitbucket Server (formerly: Stash) API is still v1.0.   
And The API v1.0 covers resources that the v2.0 API and API v2.0 is yet to cover.

## Development

### Install dependencies

It's using dep.

```sh
go get github.com/golang/dep/...
git clone https://github.com/rcompos/go-bitbucket 
cd ./go-bitbucket
dep ensure 
```

### How to testing

Set your available user account to Global Env.

```sh
export BITBUCKET_TEST_USERNAME=<your_username> 
export BITBUCKET_TEST_PASSWORD=<your_password> 
export BITBUCKET_TEST_OWNER=<your_repo_owner>  
export BITBUCKET_TEST_REPOSLUG=<your_repo_name>
```

Refs; URL Syntax is `https://<your_username>:<your_password>@bitbucket.org/<your_repo_owner>/<your_repo_name>.git`. 

And just run,

```sh
make test
```

## License

[Apache License 2.0](./LICENSE)

## Author

[rcompos](https://github.com/rcompos)
