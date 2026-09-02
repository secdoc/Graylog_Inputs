# graylog

Graylog Inputs

The inputs.json file contains the input configurations for the following input types:

 - DHCPD
 - Maltrail
 - NAXSI
 - Netflow
 - OPNsense
 - Pihole/Unbound DNS/DNSMasq
 - Suricata
 - Zenarmor


## License

Dual-licensed, **attribution required** under both:

- **Code & configuration** (scripts, rules, decoders, pipelines, configs): [Apache License 2.0](LICENSE)
- **Docs, guides & diagrams** (README, docs, diagrams): [CC BY 4.0](LICENSE-docs)

See [`LICENSING.md`](LICENSING.md) and [`NOTICE`](NOTICE). Credit: Lester E. Nichols III, secdoc.tech.

## GitLab CI baseline

GitLab CI runs repository integrity validation and centralized ClamAV scanning on the isolated `phase4-untrusted` runner. The baseline validates tracked Python syntax, shell syntax, and JSON parsing without direct Internet access. Repository-specific build and test gates remain additive to this baseline.

