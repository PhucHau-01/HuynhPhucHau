Provide your solution here:
Troubleshooting High Memory Usage on NGINX Load Balancer

Step 1: Identify the Root Cause

Check overall memory usage

Run the command: free -h
This will show if the system is swapping or running out of memory.
Analyze running processes

Run: top -o %MEM
Identify which processes consume the most memory.
Check NGINX worker processes

Run: ps aux --sort=-%mem | head -10
Determine if NGINX is consuming excessive memory.
Check NGINX error logs

Run: cat /var/log/nginx/error.log | tail -50
Look for memory-related errors.
Analyze open connections

Run: netstat -anp | grep nginx | wc -l
High connection counts may indicate excessive load.
Check system logs

Run: dmesg | tail -50
Identify potential memory leaks or out-of-memory (OOM) killer actions.
Step 2: Possible Causes & Solutions

High traffic load

Impact: Memory exhaustion due to too many connections.
Solution: Optimize NGINX configuration (keepalive, buffers).
Memory leak in NGINX modules

Impact: Continuous increase in memory usage.
Solution: Disable unnecessary modules, update NGINX.
Log files consuming memory

Impact: Excessive logging leading to memory issues.
Solution: Rotate logs using logrotate.
System swap usage

Impact: High memory usage causing performance drops.
Solution: Increase swap space, optimize memory usage.
Misconfiguration (e.g., worker_processes too high)

Impact: Unoptimized resource allocation.
Solution: Adjust worker_processes based on CPU cores.
Step 3: Recovery & Optimization

Restart NGINX to release memory

Run: systemctl restart nginx
Optimize NGINX Configuration

Reduce worker processes:
worker_processes auto;
worker_connections 1024;
Enable caching and compression:
gzip on;
proxy_cache_path /var/cache/nginx levels=1:2 keys_zone=cache:10m inactive=60m;
Use a Load Balancer in front of NGINX
Deploy AWS ALB/NLB or HAProxy to distribute traffic.
