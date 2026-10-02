# [<img src="https://s3.internetdata.io/internetdata-public/brand/mark.svg" alt="InternetData" height="28"/>](https://internetdata.io/) InternetData Claude Plugin

[![version](https://img.shields.io/github/package-json/v/internetdata/claude-plugin?filename=.claude-plugin%2Fplugin.json)](CHANGELOG.md)
[![license](https://img.shields.io/github/license/internetdata/claude-plugin)](LICENSE)

The official [InternetData](https://internetdata.io) plugin for [Claude](https://claude.com).

InternetData publishes IP and ASN databases: geolocation, anonymity, ownership and network data, as gzipped CSV and as MMDB. With this plugin you can ask Claude about the ones your organization is licensed for: which ones you hold, what is inside each, sample rows, sizes and build dates, whether a copy you downloaded is intact, and what happened to a download that failed. It works in Claude on the web, desktop and mobile, in Cowork and in Claude Code.

## Getting Started

On claude.ai, in the desktop app or in Cowork, add InternetData from the directory, then connect it on the plugin's Connectors tab.

In Claude Code:

```console
/plugin marketplace add internetdata/claude-plugin
/plugin install internetdata@internetdata
```

The first time a tool runs, you'll be asked to sign in with your InternetData account and pick the API key Claude should use. Claude never sees the key: our MCP server uses it on your behalf. The key needs the `db.download` scope, which your organization's `Default` key has. Databases are licensed by contract; if your organization doesn't have one yet, [request an evaluation](https://internetdata.io/contact?purpose=evaluation&subject=Evaluation+license).

To disconnect Claude, remove it under Connected applications at https://app.internetdata.io/settings/account/sessions. Access ends within about a minute.

## What's in it

- The InternetData MCP server at `https://mcp.internetdata.io/mcp`, with four read-only tools: `list_databases`, `database_metadata`, `database_checksum` and `list_downloads`.
- Two skills that tell Claude how to use them well:
  - `database-files` answers which databases you hold, how big they are, whether your copy is intact and why a download failed.
  - `analyze-database` explains a database's columns and sample rows, and in Claude Code analyzes a downloaded copy.

## Try it

- "Which IP databases are we licensed for, and when were they last built?"
- "What columns does vpn_ip_v1 have? Show me a few sample rows."
- "Does the checksum of my vpn_ip_v1.csv.gz match the published one?"
- "Our download failed last night. What happened?"

## What it sends

The plugin runs nothing on your machine. Claude sends the database ids you ask about to `https://mcp.internetdata.io/mcp`, which calls the InternetData API with the key you picked and returns the answer. Each request is logged against that key as any API call is. Our privacy policy is at https://internetdata.io/privacy, and questions go to support@internetdata.io.

## Other Libraries

There are official InternetData client libraries available for many languages including PHP, Python, Go, Java, and Ruby. See our GitHub at https://github.com/internetdata for more.

## About InternetData

Geolocation, anonymity, ownership and network databases for IP addresses and AS numbers, licensed as files you download and query yourself.

[<img src="https://s3.internetdata.io/internetdata-public/brand/mark.svg" alt="InternetData" height="64"/>](https://internetdata.io/)

## License

This project is licensed under the [MIT License](LICENSE).
