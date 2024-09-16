# How To Nullify Lazy Sting Ops

A semi-famous cybersecurity professional from Eastern Europe asked me to help with a project. I got connected through another cybersecurity expert I had done minor OSINT work for in the past, which is why I considered the request. The task was to regularly collect DNS A/AAAA, CNAME, and MX records for over 100,000 domains linked to malware and cybercrime. The goal was to turn it into a subscription service. I'm skilled in dev ops, coding, and math, so I saw it as a chance to gather data and perform basic analysis and cluster detection.

The general idea is to detect:

* Which domains are changing their IP addresses within similar or patterned time windows
* Identifying which network prefixes are preferred for these kinds of operations
* Build timelines of this change activity for in-depth historical analysis

I'm good at finding things that aren't meant to be found. AI has made this even easier, to the point where [I can figure out a person’s height from the oval shape at the top of a cup in a picture](https://x.com/TyrantsMuse/status/1830514185165234531). I could use the income, so I agreed to help. However, Eastern Europe is a historically volatile region, and with NATO and Russian spies all over the place—especially now with the Ukraine War—I suspected this could be a setup. If so, the goal would likely be to show intent to obtain malware, and the simplest way to do that would be to have me routinely query 100,000+ malware domains. This is especially risky for me, since my most well-known epistemic weapon design, [Blackmail Inflation](https://www.youtube.com/watch?v=xlmhhh9HYqc), is still a sensitive topic for those who might be affected by it. It’s like setting up a junior nuclear researcher to query 100,000+ domains selling products with trace amounts of nuclear material, then twisting it to claim intent to buy fissile material. I realized this early on, but being short on money, it's hard to turn down jobs.

I should also mention there was no contract, which means that while the idea came from his needs, without payment, the intellectual property of the code and the data it generates belongs to me. The lack of a contract or NDA was also a red flag for a potential setup.

So, I hedged my bets. I figured if it was a setup, the clearest sign would be his inability to pay. I broke the project into payment-based checkpoints to test for this red flag and off-ramp quickly if needed. I also made sure to never run the DNS queries from home (which I couldn't anyway since my home IP gets throttled after about 175 queries).

It took around 30 hours to build a service that could efficiently query 100,000+ domains from a single machine. Most would turn to cloud solutions for that level of network I/O, but that would increase long-term costs. Avoiding these expenses while delivering a fast proof-of-concept is a win for business operations.  Querying that many DNS records at once is a challenge, but I found decent solutions to make it work. Overall, the project was a success and can be applied to more than just cyber warfare.

### How It Works

I now check the DNS records every 30 minutes, gathering AS records to determine geolocation and ISP data for each domain’s IP. A simple web server lets clients access what they need from the data.

For example, this command tells us how many unique domains are being checked:

```bash
curl -s http://localhost:3000/domains/count
```

```json
[
    {
        "total_domains": 101585
    }
]
```

This one tells us how many times specific reasons for DNS query failure have happened:

```bash
curl -s http://localhost:3000/failures/types
```

```json
[
    {
        "error_reason": "NXDOMAIN",
        "total_value": 42892
    },    {
        "error_reason": "SERVFAIL",
        "total_value": 2859
    },    {
        "error_reason": "REFUSED",
        "total_value": 3
    }
]
```

And my personal favorite, this one tells us how many domains are originating from specific network prefixes:

```bash
curl -s http://localhost:3000/resolved/networkPrefixBuckets
```

```json
[
   {
        "count": 2057,
        "first_three_segments": "146.112.61..x"
    },    {
        "count": 1269,
        "first_three_segments": "185.230.63..x"
    },    {
        "count": 1262,
        "first_three_segments": "3.33.13.x"
    },    {
        "count": 1253,
        "first_three_segments": "15.197.148.x"
    },    {
        "count": 617,
        "first_three_segments": "162.0.2.x"
    },    {
        "count": 546,
        "first_three_segments": "198.185.159.x"
    },    {
        "count": 529,
        "first_three_segments": "199.59.24.x"
    },    {
        "count": 520,
        "first_three_segments": "198.49.23.x"
    },    {
        "count": 471,
        "first_three_segments": "192.124.249.x"
    },    {
        "count": 462,
        "first_three_segments": "3.64.16.x"
    },    {
        "count": 458, 
       "first_three_segments": "76.223.67..x"
    },    {
      ...    
    }
]
```

### Help Me Defeat The World's Laziest Sting Op

In short, this is the start of a very useful project that can work for any domain names you choose. The Eastern European cybersecurity professional doesn't have access to any of the code—no pay, no code. Since I can't completely rule out the possibility that he might be part of an entrapment operation (which is more common in cybersecurity than you'd think), I'm offering the chance for anyone to invest in making this service legitimate. Being able to cluster DNS query data can be incredibly powerful for identifying motives behind geopolitical events, influence operations by bot farms, malware teams (and state actors), and crypto groups needing public-facing web presences.

If you are interested in funding such an operation and turning it into a profitable SaaS, please contact me at [psysecgroup+dns@proton.me](mailto:psysecgroup+dns@proton.me)
