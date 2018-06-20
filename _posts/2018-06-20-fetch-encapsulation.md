---
yout:     post
title:      Fetch Encapsulation
subtitle:   encapsulate Fetch
date:       2018-06-20
author:     Allen
catalog: true
tags:
    - fetch encapsulation
---

### Simple encapsulation of the fetch.



In order to better to use the fetch, I am trying to encapsulate the fetch as a fetchSevce in an Object. 

```

let fetchService  = {

  let notAuthorizedCounter = 0

  fetch: (url,method,header,body) => {

    if(!header){

      header ={}

    }

    return fetchService[method.toLowerCase()](url,header,body).catch(exe => {

      loggerService.log('fetchService failed': exe)

      //token expired 

      if(exe.code === '401' || exe.code === '403'){

        notAuthorizedCounter++

        //max attempts 3

        if(notAuthorizedCounter > 2){

          notAuthorizedCounter = 0;

          loggerService.warn("401 or 403 received. Max attemps reached")

          return

        }else{

          return fetchService.fetch(url, method, header, body)

        }

      }

    })

  }

  get: (url, header){

    return fetch(url, {

      method: 'GET',

      headers: header

    }).then((response) => response.json())

  }

  post: (url.header, body){

    header['Content-Type'] = 'application/json'

    return fetch(url, {

      method: 'POST',

      headers: header,

      body: JSON.stringify(body)

    }).then(response => response.json())

  }

}

```

As we can see as above, the fetchService return a `fetchService[method].toLowerCase()` which is a method in `fetchService` Class. The `get` and `post` method return `fetch()` which is a promise. Hence, Through the `fetchService[method](url,header,body)`, we are able to get a `resolve(response)`. If there are some errors when fetching the data, the `catch` function will get invoked. User can customize the header as a `object`. In addition, there a max attempts for users to fetch. If the fail number is greater than 2, user will receive a warning message. 



Finally, we can use `fetchService.fetch(url,method,header,body)`
