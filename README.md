# load-testing

## Vegeta attack!!!

Now this is cool, different from all the ab|siege|jmeter and others. It actually focus on sustaining the load over a time period, which is awesome for API testing. 

You need to install Go lang before and set some default folder, then you can pull the repo and build:
```
export GOPATH=$HOME/go
go get -u github.com/tsenart/vegeta
```

Run 50 concurent requests for 10 mins with url defined in your target.txt, get the result after and report:
```
./vegeta attack -duration=600s -rate=50 -targets=target.txt | tee results.bin | ./vegeta report
```

The target.txt (I'm sending a raw json body over POST to get some shit - and don't ask me why...):
```
POST http://some-website
@/home/gjanak/Desktop/trash/edf_sm/post.json
```

Quite new tool for me, a bit simpler but does the job:
```
wrk -t 4 -c 1000 -d 60 –latency –timeout 3s http://your-own-web/
```

apache ab, sending post request:
```
ab -l -p path/post.json -T application/json -c 5 -n 5 http://your-own-web/
```

Bees with machine guns are using ab and AWS to spin up some instances and hit your server.
https://github.com/newsapps/beeswithmachineguns

Quite nice service if you want to pay for a proper testing:
 Loader.io

To optimize your rest api:
https://www.subbu.org/blog/2011/03/performance-of-restful-apps

note for myself:
optimize its connection handling to resource servers to reduce TCP handshake and slowstart overhead
Make sure to include Content-Length or use Transfer-Encoding: chunked so that the recipient of a HTTP message can know when one HTTP request/response message ends and when the next one starts.
https://www.mnot.net/blog/2006/05/16/web_2_caching

AB + shell:
https://blog.ikvasnica.com/entry/load-test-multiple-api-endpoints-concurrently-use-this-simple-shell-script

Distributed tracking system: http://zipkin.io/pages/quickstart

