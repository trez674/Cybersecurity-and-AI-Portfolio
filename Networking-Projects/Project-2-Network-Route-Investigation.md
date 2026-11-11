# Project 2: Network Route Investigation

## Objective

To investigate how network traffic travels from my Windows PC towards different public internet services and understand how traceroute can help troubleshoot network connectivity.

## Tools Used

- Windows Command Prompt
- `tracert`
- Cloudflare Public DNS (1.1.1.1)
- Google Public DNS (8.8.8.8)

## Test 1: Tracing a Route to Cloudflare

**Command:** `tracert 1.1.1.1`

**Observations:**
- The trace displayed my Sky router and several other network hops.
- The command finished with "Trace complete".
- This test provided information about the network path towards Cloudflare.

**What I learned:**

Traceroute displays numbered hops along a network path. These results can help investigate how traffic travels between networks.

## Test 2: Tracing a Route to Google

**Command:** `tracert 8.8.8.8`

**Results:**
- Numbered hops: 8
- Final responding hop: 8.8.8.8
- Trace reached the destination successfully.

**What I learned:**

My PC was able to trace a route towards Google's public DNS service. The eight numbered hops showed the positions along the network path to the destination.

## Test 3: Comparing the Two Routes

I compared the results of `tracert 1.1.1.1` and `tracert 8.8.8.8`.

**Observation:** The two traces showed different network routes.

**What I learned:**

Internet traffic can travel through different network paths depending on the destination and network routing decisions.

## Cybersecurity Relevance

Network tracing is useful when investigating connectivity problems and understanding network paths. Security professionals can combine traceroute information with other tools and logs during network investigations.

## Skills Demonstrated

- Windows Command Prompt
- Network route tracing
- Understanding network hops
- Comparing routes to different destinations
- Basic network troubleshooting
- Technical documentation

## Conclusion

I successfully investigated network routes to two public DNS services using Windows Command Prompt.

The trace to Google's DNS service reached 8.8.8.8 in eight numbered hops. The route differed from the trace towards Cloudflare.

This project helped me understand how traffic travels across networks and how traceroute can support network troubleshooting.

## Next Steps

Learn how to capture and examine network packets using Wireshark.
