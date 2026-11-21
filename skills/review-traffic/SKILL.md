---
name: review-traffic
description: Screen a batch of signups, logins, orders, reviews or log lines for anonymized or automated traffic with InternetData, keeping each result next to the record it came from. Use when someone shares an export, a CSV, a table or a log file and asks which entries came from VPNs, proxies, Tor or hosting, which countries or networks they came from, or asks for help spotting fraud, abuse or account sharing by network.
---

# Review traffic with InternetData

1. Find the IP address in each record, and keep whatever identifies the record (user, email, order ID, timestamp) beside it. If a record has more than one address, use the client address, not a server or proxy hop, and say which column you used.
2. Look up every distinct address with a single `lookup_ips` call. A batch needs a key on a paid plan: on any other key, a list of more than 10 addresses comes back refused on every address, so say a review that size needs a paid plan and offer to check the 10 records the person cares about most. Read `coverage` first: a category the key's plan does not include was not checked, so never report those records as clean on that category. An answer with `cap_reached: true` came after its organization's overage cap was reached and has only the free plan's fields: say how many records that left unchecked, and that raising or removing the cap in Billing checks them.
3. Join the results back onto the records and sort them into what they are:
   - `is_resproxy`, `is_mobproxy`: residential or mobile proxy. The address looks like a home or phone connection but is resold, which is the strongest signal of the set.
   - `is_vpn`, `is_tor`: a VPN or a Tor node. Deliberate anonymization, common among ordinary privacy-minded users too.
   - `is_dcproxy`, `is_hosting`: a datacenter proxy or a hosting range. Usually automation, scripts or servers rather than a person at a device.
   - `is_pubproxy`: a public proxy, one anyone can use for free, so read it like a datacenter proxy.
   - `is_relay`: a privacy relay such as iCloud Private Relay: ordinary people with a privacy setting on. Weigh it lightly.
   - `is_cdn`: a CDN range. Usually a service fetching on someone's behalf.
   - `is_ssh`, `is_smtp`, `is_web`, `is_dns_resolver`: an SSH, mail or web server, or an open DNS resolver, answered on the address. A person's own connection rarely runs one, so read it with `is_hosting`: a server, not a person at a device.
   - `is_anycast`: the address is announced from many places at once, as a public DNS resolver's or a CDN's edge is. A person's own connection is not.
   - `is_carrier`, `is_satellite`: a mobile carrier's or a satellite operator's space, named in `carrier.name` or `satellite.provider_name`. Many people share one address there, so several accounts behind one such address is expected, not a pattern. Neither is anonymization.
   - `is_bittorrent`: a BitTorrent client was seen on the address in the last 90 days. Common on home connections; on a hosting range, a seedbox or a server. `bittorrent.indexer` true means a DHT indexer rather than people.

   Every result also carries `hostname` (the reverse DNS name), `location` (the country, its continent and timezone), `asn` (the network: its number and name) and `company` (who uses the address), with a key or without one. None of them is a verdict, but they group the records: a country that doesn't match the account's, one network or one company behind many accounts.
4. Report a count per category, then a table of the flagged records with the identifying fields, the address, the category, the provider where known, and the country, network and company. Then call out patterns that only show up across records: one provider, one network or one address behind many accounts, bursts in time, or several accounts sharing an address.
5. Offer the full joined table as CSV if the person wants to act on it.

Keep the conclusions to what the data shows. A flag says the network is anonymized, not that the person is acting in bad faith, so present the evidence and let the person asking make the call unless they ask you to recommend one.
