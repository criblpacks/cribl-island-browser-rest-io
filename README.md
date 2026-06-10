# Island Browser REST Collector IO
----
## About this Pack

This pack is built as a complete SOURCE + DESTINATION solution (identified by the IO suffix). Data collection and delivery happen entirely within the Pack's context - you can choose how data arrives at a DESTINATION:
*  *Send to Worker Group Routes* (the default): data is sent to the top-level Worker Group Routes.
*  *Default Destination*: data is sent to the Worker Group's [Default Destination](https://docs.cribl.io/stream/destinations-default/). 
*  *In-Pack Destination*: data is sent to one or more Destinations configured within the Pack.
  
This Pack is designed to collect, process, and output Island Browser data via the Island Browser REST API. It currently supports the following endpoints:

* **Island Audits V2 (unified)** — collects **all** Island audit types (browser, admin, system, and future types) from the unified Island SIEM Audit API in a single feed. **If you enable this collector, none of the other audit endpoints below are needed** — it supersedes them.
* Audit Logs (Legacy) — do not connect this if you connected Island Audits V2.
* Admin Actions (Legacy) — do not connect this if you connected Island Audits V2.

## Deployment

* Every bundled Source within this pack adds a hidden field: `__packsource`. This field allows for simplified routing based on the Pack source.
* This pack is configured by default to use the Destination *Send to Worker Group Routes*. You *must* add either a Worker Group Route or rely on the Default Destination.
* To explicitly use the Worker Group's *Default Destination*, change the Pack's Routes to *default:default*. The Pack will then route the data to the destination currently set as the Default on the Worker Group.

### Configure the Collectors

* Obtain an `API URL` and `API Key` from your Island Browser Administrator and update the Pack variables with these values (see below for details).
* Perform a **Commit & Deploy** (required for Preview to work) and then **Run > Preview** of each Collector to verify that they work correctly.
* Schedule the Collectors, adjusting the schedule as needed.

### Configure your Destination/Update Pack Routes
To ensure proper data routing, you must make a choice: retain the current setting to use the Default Destination defined by your Worker Group, or define a new Destination directly inside this pack and adjust the pack's route accordingly.

### Commit and Deploy
Once everything is configured, perform a Commit & Deploy to enable data collection.

### Variables

The Pack has the following variables:
* `island_audit_integration_id`: The per-integration UUID used in the `/Audits/{id}` path (required)
* `island_audit_api_key`: Bearer API key for the Island SIEM Audit API (required)


## Legacy

This pack retains a number of variables and pipelines from previous versions for backward compatibility with existing deployments. These are not needed for new setups — if you are starting fresh, configure only the `island_audit_*` variables and enable the **Island Audits V2** collector. Do not configure the legacy components alongside Island Audits V2.

## Upgrades

Upgrading certain Cribl Packs using the same Pack ID can have unintended consequences. See [Upgrading an Existing Pack](https://docs.cribl.io/stream/packs#upgrading) for details.

## Release Notes

### Version 3.0.0
* Added **Island Audits V2** unified collector — collects all Island audit types (browser, admin, system, and future types) from the Island SIEM Audit API in a single feed. Supersedes the per-type legacy collectors.

### Version 2.0.0
* Updated Route Destinations to "Send to Worker Group Routes". See above for details.

### Version 1.0.0
- Initial release

## Contributing to the Pack

To contribute to the Pack, please connect with us on [Cribl Community Slack](https://cribl-community.slack.com/). You can suggest new features or offer to collaborate.

## License
This Pack uses the following license: [Apache 2.0](https://github.com/criblio/appscope/blob/master/LICENSE).