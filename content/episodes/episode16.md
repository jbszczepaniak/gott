---
title: "#16 - Optional parameters"
date: 2020-01-16  
summary: "They exist."
---

## [get pdf here](/gott/episode16.pdf) 🖨

Java offers type overloading. In Python keyword arguments can be passed to functions. Go doesn't allow either, yet passing optional arguments to the function can be handy from time to time. Let's see how this can be achieved with Go's type system. We will create some sort of `Client​` without a need to pass the parameters.

{{< highlight go >}}
type Client struct {
  Insecure bool
  Timeout int
}

// Set of Options like that will be applied to the Client.
// Since function receives pointer as a parameter it can
// change Client's state.
type Option func(*Client)

// Return an anonymous function of type Option, that
// changes value of `Insecure` field on the Client.
func AllowInsecure() Option { ​
  return func(c *Client) { ​
    c.Insecure = true
  }
}

// Do the same here, but this time pass a timeout parameter.
func WithTimeout(timeout int) Option { ​
  return func(c *Client) { ​
    c.Timeout = timeout
  }
}


// Here magic happens. The `constructor` accepts 0 or many Options
// (which are functions). Then it creates new client, loops over
// the Options and apply them by invoking them.
func NewClient(opts... Option) *Client {
  c := &Client{}
  for _, opt := range opts {​
    opt(c)
  }
  return c
}

func main() {}
  // New Client with default parameters.
  t1 := NewClient()
  // New Client that allows insecure connections
  // and have connection timeout 10s.
  t2 := NewClient(AllowInsecure(), WithTimeout(10))
}
{{< / highlight >}}