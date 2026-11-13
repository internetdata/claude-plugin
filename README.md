# [<img src="https://s3.internetdata.io/internetdata-public/brand/mark.svg" alt="InternetData" height="28"/>](https://internetdata.io/) InternetData Claude Plugin

[![version](https://img.shields.io/github/package-json/v/internetdata/claude-plugin?filename=.claude-plugin%2Fplugin.json)](CHANGELOG.md)
[![license](https://img.shields.io/github/license/internetdata/claude-plugin)](LICENSE)

The official [InternetData](https://internetdata.io) plugin for [Claude](https://claude.com).

InternetData answers what its data says about any IP address, AS or domain, and publishes the databases behind it. With this plugin you can ask about an address, a list of them, a domain or an AS: where an address is, whose network it's on, whether it's a VPN, a proxy, Tor or a hosting provider, a domain's DNS records and an AS's prefixes. You can also ask about the databases: which ones your organization holds, what is inside each, whether a copy you downloaded is intact, and what happened to a download that failed. It works in Claude on the web, desktop and mobile, in Cowork and in Claude Code.

## Getting Started

On claude.ai, in the desktop app or in Cowork, add InternetData from the directory, then connect it on the plugin's Connectors tab.

In Claude Code:

```console
/plugin marketplace add internetdata/claude-plugin
/plugin install internetdata@internetdata
```

The first time a tool runs, you'll be asked to sign in with your InternetData account and pick the API key Claude should use. Claude never sees the key: our MCP server uses it on your behalf. Any key answers lookups, with every field on a paid plan and in the free plan's first 100 lookups each day; the database tools need the `db.download` scope, which your organization's `Default` key has. Databases are licensed by contract. The Open ones, `tor_ip_v1` among them, are licensed to every organization from the start and are free under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). For the rest, [request an evaluation](https://internetdata.io/contact?purpose=evaluation&subject=Evaluation+license).

To disconnect Claude, remove it under Connected applications at https://app.internetdata.io/settings/account/sessions. Access ends within about a minute.

## What's in it

- The InternetData MCP server at `https://mcp.internetdata.io/mcp`, with nine read-only tools: `lookup_ip`, `lookup_ips`, `lookup_asn`, `lookup_domain` and `my_entitlement` for lookups, and `list_databases`, `database_metadata`, `database_checksum` and `list_downloads` for the databases.
- Five skills that say how to use them well:
  - `check-ips` looks up one address or a list: where each is, whose network, and whether it's a VPN, a proxy, Tor or a hosting provider.
  - `review-traffic` screens an export or a log for anonymized traffic, keeping each answer next to its record.
  - `investigate-domain-or-as` looks into a domain's DNS, ranges and disposable flag, or an AS's operator and prefixes.
  - `database-files` answers which databases you hold, how big they are, whether your copy is intact and why a download failed.
  - `analyze-database` explains a database's columns and sample rows, and in Claude Code analyzes a downloaded copy.

## Try it

- "Where is 8.8.8.8, and whose network is it on?"
- "Check these addresses for VPNs, proxies and Tor: 45.83.91.1, 185.220.101.1, 8.8.8.8"
- "Does example.com have a mail server, and is it a disposable email domain?"
- "Who operates AS15169?"
- "What columns does vpn_ip_v1 have? Show me a few sample rows."
- "Our download failed last night. What happened?"

## What it sends

The plugin runs nothing on your machine. Claude sends the addresses, domains, AS numbers and database IDs you ask about to `https://mcp.internetdata.io/mcp`, which calls the InternetData API with the key you picked and returns the answer. Each request is logged against that key as any API call is. Our privacy policy is at https://internetdata.io/privacy, and questions go to support@internetdata.io.

## Other Libraries

There are official InternetData client libraries available for many languages including PHP, Python, Go, Java, and Ruby. See our GitHub at https://github.com/internetdata for more.

## About InternetData

Trusted IP data and domain intelligence: an API to look up any address, AS or domain, and databases you hold.

[<img src="https://s3.internetdata.io/internetdata-public/brand/mark.svg" alt="InternetData" height="64"/>](https://internetdata.io/)

## License

This project is licensed under the [MIT License](LICENSE).
