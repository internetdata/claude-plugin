---
name: investigate-domain-or-as
description: "Look into a domain or an autonomous system with InternetData: whether a domain is registered, which DNS records it has and what they point to, the IP ranges its organization holds and whether it's a disposable email domain; an AS's operator, country, registry, size, Whois record and the prefixes it announces with their RPKI status. Use when someone asks about a domain, the domain of an email address, an AS number such as AS15169, or the network operator behind one."
---

# Look into a domain or an AS with InternetData

1. Work out what you were given. An AS is a number, with or without `AS` in front: call `lookup_asn` with the number. A domain, or an email address whose domain is what matters: call `lookup_domain` with the domain alone, lower-case, without a scheme or a path. An IP address belongs to the `check-ips` skill.
2. Read `coverage` before you conclude anything. A field listed in `coverage.not_included` was not returned because of the plan behind the API key, which is not the same as "no". Without a paid plan, a domain answers only whether it is registered and which record types it has, and an AS its operator, country, registry, allocation date and domain. `my_entitlement` shows the plan.
3. For a domain, report:
   - Whether it is registered, and which of A, AAAA, MX, NS and CNAME it has. No MX means it receives no mail.
   - Where the plan covers them, the records themselves with when each was last seen, the IP ranges its organization holds, and `is_disposable` with the services behind it. A disposable domain is the strongest sign an email address was made to be thrown away.
   - The answer comes from InternetData's latest snapshots, not a live DNS query, so say so if the person needs the state this minute.
4. For an AS, report its operator, country, registry and allocation date, and where the plan covers them, its size (IPv4 addresses and prefixes announced), its Whois record and its RPKI counts. A big AS announces thousands of prefixes: summarize them (counts per RPKI status, the largest few) rather than listing them all, unless asked.
5. An AS no database knows comes back as its number with empty values: say it is unknown, not that it is clean. If a call is refused with `unauthorized`, the connection needs signing in again; if it is refused for going over the plan's allowance, check `my_entitlement` and say when it resets.

Keep to what the data shows: a domain's records and an AS's prefixes describe infrastructure, not who is behind a message or what they intend.
