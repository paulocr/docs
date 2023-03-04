---
title: Exposing Your App
---

Before your application can say hello, Railway needs to know the IP and port that your application is listening on, in order to expose it to the internet.

The easiest way to get up and running is to have your application listen on `0.0.0.0:$PORT`, where `PORT` is a Railway-provided environment variable. 

Alternatively, you can manually override the `PORT` environment variable by adding `PORT` to your projects variables page. (Command + K and type `Variables` or you can use the keyboard shortcut: `G` + `V` under your selected project)

## Railway-Provided Domain

Railway services don't obtain a domain automatically, but you'll be notified to set one up as soon as we detect a deployment is listening correctly (as described above). Simply follow the prompts to generate a domain and your app will be exposed to the internet!

<Image
src="https://res.cloudinary.com/railway/image/upload/v1654560212/docs/add-domain_prffyh.png"
alt="Screenshot of adding Service Domain"
layout="responsive"
width={1396} height={628} quality={80} />

## Custom Domains

One or more custom domains can be added to a Railway service (tied to a specific environment).

Here's how it works:

1. Navigate to the Settings tab of your desired service
2. Add a custom domain and type in the name
3. Add the `CNAME` record to the DNS settings for your domain
4. Wait for Railway to verify your `CNAME` record

<Image
src="https://res.cloudinary.com/railway/image/upload/v1654563209/docs/domains_uhchsu.png"
alt="Screenshot of Custom Domain"
layout="responsive"
width={1338} height={808} quality={80} />

**NOTE!:** Changes to DNS settings may take up to 72 hours to propagate
worldwide.

**NOTE:**: freenom is not allowed, and not supported.

## Let's Encrypt SSL Certificates

Once a custom domain has been correctly configured, Railway will automatically
generate and apply a Let's Encrypt certificate. This means that any custom
domain on Railway will automatically be accessible
via `https://`.

## Provider Specific Instructions

If you have proxying enabled on Cloudflare (the orange cloud), you MUST set your
SSL/TLS settings to full or above.

<Image src="https://res.cloudinary.com/railway/image/upload/v1631917785/docs/cloudflare_zgeycj.png"
alt="Screenshot of Custom Domain"
layout="responsive"
width={1205} height={901} quality={80} />

If proxying is not enabled, Cloudflare will not associate the domain with your Railway project with the following error.  

```
ERR_TOO_MANY_REDIRECTS
```

Also note that if proxying is enabled, you can NOT use a domain deeper than a first level subdomain without Cloudflare's Advanced Certificate Manager. For example, anything falling under \*.yourdomain.com can be proxied through Cloudflare without issue, however if you have a custom domain under \*.subdomain.yourdomain.com, you MUST disable Cloudflare Proxying and set the CNAME record to DNS Only (the grey cloud), unless you have Cloudflare's Advanced Certificate Manager. 

### Redirecting a Root Domain Workarounds

Some domain registrars don't fully support CNAME records. As a result - when you add an `@` record for a CNAME, the domain registrar will create an invalid `A` record.

Registrars that are known to not fully support CNAME records for the root domain include:
- Freenom
- GoDaddy
- Ionos

**Workaround 1 - Cloudflare Proxy**

You may also configure Cloudflare proxying for your domain to redirect your domain.

After a custom domain is added to the Railway service follow [the instructions listed on Cloudflare's documentation to configure the proxy.](https://support.cloudflare.com/hc/en-us/articles/205893698-Configure-Cloudflare-and-Heroku-over-HTTPS)

**Workaround 2 - Changing your Domain's Nameservers**

You can also change your domain's nameservers to point to Cloudflare's nameservers. This will allow you to use a CNAME record for the root domain. Follow the instructions listed on Cloudflare's documentation to [change your nameservers.](https://developers.cloudflare.com/dns/zone-setups/full-setup/setup/)