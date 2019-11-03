## Manually performace test results using performance.getEntries() from console of Chrome for Canvas_Sin.html
This is further investigation for [Big different window.performance.timing results for repeat test on the same page](https://github.com/GoogleChrome/puppeteer/issues/5110)

Last time, with the simplest server:
```
var http = require('http');

var server = http.createServer(function(req, res) {
    res.writeHead(200);
    res.end('Hi everybody!');
});
server.listen(8080);
```
This time, open [Canvas_Sin.htmll](https://github.com/rubyzhao/Sin-Wave-with-Basic-Canvas/blob/master/Canvas_Sin.html) with live server. [^1] 

For each **Loop**=20,200 and 2000, refresh the website http://127.0.0.1:5500/Canvas_Sin.html, run JSON.stringify(performance.getEntries()) and save as the result in the conslole a few times. 

The below is part of performance result for Loop=20:

NAV_duration | NAV_connectEnd | NAV_responseEnd | NAV_domContentLoadedEventEnd | NAV_domComplete | FP_startTime | LogFileTime
---|---|---|---|---|---|---
168.4 | 0.8 | 12.5 | 67.2 | 167.0 | 149.5 | 03-11-2019-03-38-01
152.5 | 3.2 | 19.2 | 74.8 | 151.8 | 78.0 | 03-11-2019-03-38-29
129.9 | 1.8 | 17.6 | 61.5 | 129.3 | 64.3 | 03-11-2019-03-38-44

The below is part of performance result for Loop=200:

NAV_duration | NAV_connectEnd | NAV_responseEnd | NAV_domContentLoadedEventEnd | NAV_domComplete | FP_startTime | LogFileTime
---|---|---|---|---|---|---
155.3 | 2.0 | 20.2 | 87.2 | 154.7 | 90.3 | 03-11-2019-03-31-12
125.9 | 0.9 | 19.1 | 65.1 | 125.3 | 69.1 | 03-11-2019-03-31-39
121.1 | 1.2 | 7.3 | 50.0 | 120.5 | 54.7 | 03-11-2019-03-32-02

The below is part of performance result for Loop=2000:

NAV_duration | NAV_connectEnd | NAV_responseEnd | NAV_domContentLoadedEventEnd | NAV_domComplete | FP_startTime | LogFileTime
---|---|---|---|---|---|---
139.3 | 0.8 | 22.5 | 69.3 | 138.5 | 72.7 | 03-11-2019-03-35-44
148.9 | 0.8 | 17.3 | 77.7 | 148.3 | 81.4 | 03-11-2019-03-36-10
78.5 | 0.7 | 17.7 | 62.7 | 77.0 | 64.8 | 03-11-2019-03-36-22

The variance is even big. For example, NAV_domComplete=77, 1.92 times less than 148.3 at Loop=2000 is even lower than 167 in Loop=20. 

**Tell us about your environment:**

- [^1]: Live Server: v5.6.1
- Chrome: Version 78.0.3904.87 (Official Build) (64-bit)
- Windows: W10X64 1803
- Node.js version: v12.11.1




