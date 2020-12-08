# acme.sh.4.GoDaddy.managed.domain

[Configure LetsEncrypt and Acme.sh](https://github.com/acmesh-official/acme.sh)

- As more and more solutions are built using microservices architecture, it is very important to have all your public endpoints encrypted. The good news is that you can achieve it without spending any additional penny. LetsEncrypt is one such project which is a free and open Certificate Authority and you can easily integrate it with your setup to automatically generate SSL certificates free of cost, FOREVER…

- The domain `pcf4u.com` is being managed by GoDaddy, so we're going to use the GoDaddy Instructions.

- Start by getting API keys from: https://developer.godaddy.com/keys/

```
export GD_Key="dKP1FBK7baAM_65SEvX9AdM8j9kBqEgfiKj"
export GD_Secret="GuaFk14UNPB5k7hJPx2ucs"
```

- If you don't have `acme.sh` yet, you can get it using the following commands:

```
cd /work
git clone https://github.com/acmesh-official/acme.sh.git
cd ./acme.sh
./acme.sh --install
```
- Here's what the `install` responded:

```
Cloning into 'acme.sh'...
remote: Enumerating objects: 10909, done.
remote: Total 10909 (delta 0), reused 0 (delta 0), pack-reused 10909
Receiving objects: 100% (10909/10909), 4.21 MiB | 6.85 MiB/s, done.
Resolving deltas: 100% (6477/6477), done.
[Mon Jul  6 12:26:26 EDT 2020] Installing to ~/.acme.sh
[Mon Jul  6 12:26:26 EDT 2020] Installed to ~/.acme.sh/acme.sh
[Mon Jul  6 12:26:26 EDT 2020] Installing alias to '~/.zshrc'
[Mon Jul  6 12:26:26 EDT 2020] OK, **Close and reopen your terminal to start using acme.sh**
[Mon Jul  6 12:26:26 EDT 2020] Installing cron job
[Mon Jul  6 12:26:34 EDT 2020] Good, bash is found, so change the shebang to use bash as preferred.
[Mon Jul  6 12:26:35 EDT 2020] OK
```

- Note that acme.sh will save GD_Key and GD_Secret in ~/.acme.sh/account.conf and will reuse when needed.

- Just one command left to execute:

```
cd ~/.acme.sh
./acme.sh --issue --dns dns_gd -d '*.pcf4u.com' -d '*.sys.pcf4u.com' -d '*.pks.pcf4u.com' -d '*.apps.pcf4u.com' -d '*.login.sys.pcf4u.com' -d '*.uaa.sys.pcf4u.com'
```

- Just for ease of cut-&-paste, if the desired domain is `ourpcf.com` them the command lines are:

```
cd ~/.acme.sh
./acme.sh --issue --dns dns_gd -d '*.ourpcf.com' -d '*.sys.ourpcf.com' -d '*.pks.ourpcf.com' -d '*.apps.ourpcf.com' -d '*.login.sys.ourpcf.com' -d '*.uaa.sys.ourpcf.com'
```

- Note: to renew a cert use: `acme.sh --renew -d pcf4u.com --force`

- After the `acme.sh` does its magic... you will eventually see:

```
[Mon Jul  6 12:40:22 EDT 2020] Your cert is in  ~/.acme.sh/pcf4u.com/pcf4u.com.cer 
[Mon Jul  6 12:40:22 EDT 2020] Your cert key is in  ~/.acme.sh/pcf4u.com/pcf4u.com.key 
[Mon Jul  6 12:40:22 EDT 2020] The intermediate CA cert is in  ~/.acme.sh/pcf4u.com/ca.cer 
[Mon Jul  6 12:40:22 EDT 2020] And the full chain certs is there:  ~/.acme.sh/pcf4u.com/fullchain.cer 
```

- You can use https://www.sslshopper.com/certificate-decoder.html to decode the cert at ~/.acme.sh/pcf4u.com/pcf4u.com.cer :

```
Certificate Information:
Common Name: pcf4u.com
Subject Alternative Names: *.apps.pcf4u.com, *.login.sys.pcf4u.com, *.pcf4u.com, *.pks.pcf4u.com, *.sys.pcf4u.com, *.uaa.sys.pcf4u.com, pcf4u.com
Valid From: July 6, 2020
Valid To: October 4, 2020
Issuer: Let's Encrypt Authority X3, Let's Encrypt Write review of Let's Encrypt
Serial Number: 034bb58c7a7792bda6479b56e49840b1a7f7
```

- Contents of ~/.acme.sh/pcf4u.com/pcf4u.com.cer 

```
-----BEGIN CERTIFICATE-----
MIIFtzCCBJ+gAwIBAgISA0u1jHp3kr2mR5tW5JhAsaf3MA0GCSqGSIb3DQEBCwUA
MEoxCzAJBgNVBAYTAlVTMRYwFAYDVQQKEw1MZXQncyBFbmNyeXB0MSMwIQYDVQQD
ExpMZXQncyBFbmNyeXB0IEF1dGhvcml0eSBYMzAeFw0yMDA3MDYxNTQwMjFaFw0y
MDEwMDQxNTQwMjFaMBQxEjAQBgNVBAMTCXBjZjR1LmNvbTCCASIwDQYJKoZIhvcN
AQEBBQADggEPADCCAQoCggEBAOQsrBxJEDYYd72ECW1Wecgio/hnIFAPWireZcfW
Mo5QvZDfJzLrGa0qwPFarlT4gd/1Mhn+iIuvNwPUz4nPIcxp/IcwT7QafWVRU/aN
pzrXRYKTxfobki9+FkigzYIFHav0XudLsSdFp2zHJRedJPMX/DGudiacHQu70ofj
HFBTakIAiEzuTVanIhEaNgm4eDfap2DRGBd/Rn/1/78x3SOXjE2SpA3GrOpkOHra
x2583roMnRC63BYFaZDDDYqjQjKZ/LqudjyYX2B8l8ht4z7i2Tuqg0HEpKs6jsS3
OcZv/1LA47Lr9mXyyjGdDATuw18v1FWQXPhIEb00y+MBBocCAwEAAaOCAsswggLH
MA4GA1UdDwEB/wQEAwIFoDAdBgNVHSUEFjAUBggrBgEFBQcDAQYIKwYBBQUHAwIw
DAYDVR0TAQH/BAIwADAdBgNVHQ4EFgQUmNPIByGn29vNABSBR9LAkUmDO9gwHwYD
VR0jBBgwFoAUqEpqYwR93brm0Tm3pkVl7/Oo7KEwbwYIKwYBBQUHAQEEYzBhMC4G
CCsGAQUFBzABhiJodHRwOi8vb2NzcC5pbnQteDMubGV0c2VuY3J5cHQub3JnMC8G
CCsGAQUFBzAChiNodHRwOi8vY2VydC5pbnQteDMubGV0c2VuY3J5cHQub3JnLzCB
gQYDVR0RBHoweIIQKi5hcHBzLnBjZjR1LmNvbYIVKi5sb2dpbi5zeXMucGNmNHUu
Y29tggsqLnBjZjR1LmNvbYIPKi5wa3MucGNmNHUuY29tgg8qLnN5cy5wY2Y0dS5j
b22CEyoudWFhLnN5cy5wY2Y0dS5jb22CCXBjZjR1LmNvbTBMBgNVHSAERTBDMAgG
BmeBDAECATA3BgsrBgEEAYLfEwEBATAoMCYGCCsGAQUFBwIBFhpodHRwOi8vY3Bz
LmxldHNlbmNyeXB0Lm9yZzCCAQMGCisGAQQB1nkCBAIEgfQEgfEA7wB1APCVpFny
ANGCQBAtL5OIjq1L/h1H45nh0DSmsKiqjrJzAAABcyT/9zYAAAQDAEYwRAIgYLrE
2cmhUOoI5g+yFKFkIer6XNQBH+874NUvSVNFgJECIBMD8vWaHnFIBYMdCtjMGCB0
13mJbaaeqt36T6bGMFVoAHYAsh4FzIuizYogTodm+Su5iiUgZ2va+nDnsklTLe+L
kF4AAAFzJP/3QAAABAMARzBFAiA8K0KeFPttT7m2cpbk4n6+1ZUBGxvAMRjn/KV9
xRvgAQIhANK6JQ+76s9tGqkJ5Q/bC1erOZLZRKOHUxjKC4wl2q3yMA0GCSqGSIb3
DQEBCwUAA4IBAQAGhTcxgQhJ12uX8G5djHa8XVKwK3WQT0HEZ5zevsq6qo5uXI/x
ws9AqZhw9W4PMK+gn1Gjc8Jp/1j2QTFm+PPPbebcSVIM6+1i3P8gSWweMYm7Wqh2
idK9EUeKfpnZCksgROrcb8cP1EydsmqZDU8dw6eMtFt4r24lYKZfVnGXSMdzhN8w
S0fEVUqn1Db2qZrcc9Opk4QiwZPlYTRYog6Mx60AAEMPuqx69LcjRwSxTDKB/fYM
+mS2OvQ9UjSQ6gkLyaggE/YH9d8xytzsUoHgYVfcLzDbSgm0N0bNXJkr7l8x/lyS
OerbVHxsS1Xr6qvGs695DMqrDTWGS6EPaCWe
-----END CERTIFICATE-----
```

- Contents of ~/.acme.sh/pcf4u.com/pcf4u.com.key :

```
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEA5CysHEkQNhh3vYQJbVZ5yCKj+GcgUA9aKt5lx9YyjlC9kN8n
MusZrSrA8VquVPiB3/UyGf6Ii683A9TPic8hzGn8hzBPtBp9ZVFT9o2nOtdFgpPF
+huSL34WSKDNggUdq/Re50uxJ0WnbMclF50k8xf8Ma52JpwdC7vSh+McUFNqQgCI
TO5NVqciERo2Cbh4N9qnYNEYF39Gf/X/vzHdI5eMTZKkDcas6mQ4etrHbnzeugyd
ELrcFgVpkMMNiqNCMpn8uq52PJhfYHyXyG3jPuLZO6qDQcSkqzqOxLc5xm//UsDj
suv2ZfLKMZ0MBO7DXy/UVZBc+EgRvTTL4wEGhwIDAQABAoIBAHI4pqO2M4ZQ80gM
m8d/HZGBPcHwpe1N8h45nIvP/xjc9DhcbTwBEqZsG4/2jAR/LkyVatI2Z9Y9DPY/
BvF+nfW9LKvkFFIdXJ5meviWapt6/hHitZ2BRcm+fZs33Ah1VSgqOYPhkToOlURP
4JKUmNWUMSwRoJWtWqDwEfDyUM8oMLFgiV/NjIedYi5n6j2MzJFq5TX9XS2H1/HA
PBqj8Borf93h73WmB/5ogI63nzHxxZzMGs5DyPpLcmGmXXW6pKz4nYPwejf8XUUl
Wpo68LYu/Tk5ClegJPlS2ou7wiCdErnRgNe9pexeBx4KsBiNTZYN/ukoHYWxSh9V
8yyPMeECgYEA9BuA3K7P+FOYtAwo735UZ4lsCIQqNatXKQAa28+qI8pOzpyYYjZi
/vT12TBMT6hb5R/j+C98z8OevNJgNRer7P4phJD7IHYok2gCv06E1/Fi7yWpZT6O
H4zdXf2UvZ0+tfxgzUwbAcyzTgfY7jfJjxM3tGty1KewCkbaALV2HbcCgYEA70p0
QZe+bZE/R4sWNf+Am7+gdGvQHYZcFra8D7HyZ1wMsenNVtfSkONo3wkyBh2gYatP
+7AN2oVqSErMkgQ83TXFe0mjnj9txBPcQP7lcIRpyAP2Fj4/jypd4NRR3AE/DnaH
1PhDqFJ1JtefiKwaeUo7fXVPEd0Rmso3GQjNXbECgYByvX7LvGvLCNhNQS34rMPV
yvV5503D3l7gycjWK32Ixy5V1auW9oN/3fq1dQtZogRX5a6NWRzst8Gkdap9KjxI
8IrpYhB4iLG33/rym2C79B2R1X0TNt0tHVRsOqawnfn9Jr0FotFK/kIF2pBwIM7g
LqNPbfYS2SNZIUaVcLYtbwKBgHVMrByTRBf1wW1SsvqZWvP+RauMRiKTAIVp4lpX
QpqENvznvW66sU+xCnF60njJARufnL+mF8Rs7iKt+AYD6coOV9YNzRT/xtD9Y1TB
Hru/TRNtTa6tqP6HKCnUKqSMP9rZI9C0OoZClYcK3/thUkDusKbZYH9DPSQByGyP
MgyhAoGASc2HHO0/4D+W3EE09/U64b+V756lZOcHMWoU7ERyTCOnKCRbpsYkDnDo
Pt0iF0tS1qVwwydOMnZMNOLNJu5rdvWLv21d//VBEv1GxAcQV+1al5wAPJ1McGax
ZkiyzbTi/xtm49A1g4ZbdPIf6G3/ZPeU+95lyG/wy+nR5/IetcU=
-----END RSA PRIVATE KEY-----
```

- Contents of ~/.acme.sh/pcf4u.com/ca.cer  :

```
-----BEGIN CERTIFICATE-----
MIIEkjCCA3qgAwIBAgIQCgFBQgAAAVOFc2oLheynCDANBgkqhkiG9w0BAQsFADA/
MSQwIgYDVQQKExtEaWdpdGFsIFNpZ25hdHVyZSBUcnVzdCBDby4xFzAVBgNVBAMT
DkRTVCBSb290IENBIFgzMB4XDTE2MDMxNzE2NDA0NloXDTIxMDMxNzE2NDA0Nlow
SjELMAkGA1UEBhMCVVMxFjAUBgNVBAoTDUxldCdzIEVuY3J5cHQxIzAhBgNVBAMT
GkxldCdzIEVuY3J5cHQgQXV0aG9yaXR5IFgzMIIBIjANBgkqhkiG9w0BAQEFAAOC
AQ8AMIIBCgKCAQEAnNMM8FrlLke3cl03g7NoYzDq1zUmGSXhvb418XCSL7e4S0EF
q6meNQhY7LEqxGiHC6PjdeTm86dicbp5gWAf15Gan/PQeGdxyGkOlZHP/uaZ6WA8
SMx+yk13EiSdRxta67nsHjcAHJyse6cF6s5K671B5TaYucv9bTyWaN8jKkKQDIZ0
Z8h/pZq4UmEUEz9l6YKHy9v6Dlb2honzhT+Xhq+w3Brvaw2VFn3EK6BlspkENnWA
a6xK8xuQSXgvopZPKiAlKQTGdMDQMc2PMTiVFrqoM7hD8bEfwzB/onkxEz0tNvjj
/PIzark5McWvxI0NHWQWM6r6hCm21AvA2H3DkwIDAQABo4IBfTCCAXkwEgYDVR0T
AQH/BAgwBgEB/wIBADAOBgNVHQ8BAf8EBAMCAYYwfwYIKwYBBQUHAQEEczBxMDIG
CCsGAQUFBzABhiZodHRwOi8vaXNyZy50cnVzdGlkLm9jc3AuaWRlbnRydXN0LmNv
bTA7BggrBgEFBQcwAoYvaHR0cDovL2FwcHMuaWRlbnRydXN0LmNvbS9yb290cy9k
c3Ryb290Y2F4My5wN2MwHwYDVR0jBBgwFoAUxKexpHsscfrb4UuQdf/EFWCFiRAw
VAYDVR0gBE0wSzAIBgZngQwBAgEwPwYLKwYBBAGC3xMBAQEwMDAuBggrBgEFBQcC
ARYiaHR0cDovL2Nwcy5yb290LXgxLmxldHNlbmNyeXB0Lm9yZzA8BgNVHR8ENTAz
MDGgL6AthitodHRwOi8vY3JsLmlkZW50cnVzdC5jb20vRFNUUk9PVENBWDNDUkwu
Y3JsMB0GA1UdDgQWBBSoSmpjBH3duubRObemRWXv86jsoTANBgkqhkiG9w0BAQsF
AAOCAQEA3TPXEfNjWDjdGBX7CVW+dla5cEilaUcne8IkCJLxWh9KEik3JHRRHGJo
uM2VcGfl96S8TihRzZvoroed6ti6WqEBmtzw3Wodatg+VyOeph4EYpr/1wXKtx8/
wApIvJSwtmVi4MFU5aMqrSDE6ea73Mj2tcMyo5jMd6jmeWUHK8so/joWUoHOUgwu
X4Po1QYz+3dszkDqMp4fklxBwXRsW10KXzPMTZ+sOPAveyxindmjkW8lGy+QsRlG
PfZ+G6Z6h7mjem0Y+iWlkYcV4PIWL1iwBi8saCbGS5jN2p8M+X+Q7UNKEkROb3N6
KOqkqm57TH2H3eDJAkSnh6/DNFu0Qg==
-----END CERTIFICATE-----
```

- The CERT shown above decodes as:

```
Certificate Information:
Common Name: Let's Encrypt Authority X3
Organization: Let's Encrypt
Country: US
Valid From: March 17, 2016
Valid To: March 17, 2021
Issuer: DST Root CA X3, Digital Signature Trust Co.
Serial Number: 0a0141420000015385736a0b85eca708
```

- More details re: `acme.sh` are available at https://github.com/acmesh-official/acme.sh




