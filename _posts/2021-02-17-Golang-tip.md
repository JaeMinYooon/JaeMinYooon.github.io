---
layout: post
title:  "Golang 사용중인 ip 확인하는 코드"
date:   2021-02-17T14:25:52-05:00
author: Jaemin
categories: Golang
---

<h2>Golang 사용중인 ip 확인하는 코드</h2>

```golang
import (
	"net"
	"os"
)

func main() {
	addrs, err := net.InterfaceAddrs()
	if err != nil {
		os.Stderr.WriteString("Oops: " + err.Error() + "\n")
		os.Exit(1)
	}

	for _, a := range addrs {
		if ipnet, ok := a.(*net.IPNet); ok && !ipnet.IP.IsLoopback() {
			if ipnet.IP.To4() != nil {
				os.Stdout.WriteString(ipnet.IP.String() + "\n")
			}
		}
	}
}
```
