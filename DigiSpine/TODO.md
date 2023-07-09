## Obvious TODOs

- [ ] validate data/log storage so that they are stored in a separate volume and exist after update/location rotation ins swarm 
- [ ] Validate produce/consumer against updates/failure
  - https://kafka.apache.org/documentation/#upgrade_350_kraft
- [ ] https://github.com/lensesio/stream-reactor
  - Validate supported 
- [ ] Document decisions 
- [ ] Secure external connection protocols?!

## Decisions so far
- [x] Which image -> Confluent due to their support time and possibility to commercial support  
  - Note: Versioning of confluent
    - https://docs.confluent.io/platform/current/installation/versions-interoperability.html 
