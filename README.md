# Summary
A simple PoC for WordPress RCE (author priviledge), refer to CVE-2019-8942 and CVE-2019-8943.

# Test Environment
## Docker Image
* `docker pull avfisherdocker/wordpress:4.9.8`
* `docker run -d -p 80:80 avfisherdocker/wordpress:4.9.8`

## Mysql & WordPress Info
|Type|Username|Password|
|---|---|---|
|mysql|root|root|
|wordpress|admin|admin4wp498
|wordpress|author|author4wp498

# Proof of Concepts
TBD

# Reference
* <https://blog.ripstech.com/2019/wordpress-image-remote-code-execution/>
* <https://nvd.nist.gov/vuln/detail/CVE-2019-8942>
* <https://nvd.nist.gov/vuln/detail/CVE-2019-8943>
