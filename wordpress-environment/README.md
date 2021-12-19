# WordPress Environment

- [Setup WordPress Locally](#setup-wordpress-locally)
- [Staging and Production](#staging-and-production)

## Setup WordPress Locally

The easiest way to use WordPress locally is using softwares like [ServerPress](https://serverpress.com/) or [Local](https://localwp.com/).

<br/>
<div align="right">
  <b><a href="#wordpress-environment">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Staging and Production

- A **Production Site** is our live site people visit.
- A **Staging Site** is a hosted site used for testing.
- The **Local Setup** is used for development only.

The workflow should can be summaried as following steps:

1. Pull from production to staging to local for latest version of our site.
2. Push from local to staging for testing.
3. Make and test any changes we need in staging.
4. Push from staging to production.

The production & staging handled by hosting (e.g. BlueHost... etc), and the local to staging handled by plugins (e.g. [All-in-One WP Migration](https://wordpress.org/plugins/all-in-one-wp-migration/)).

<br/>
<div align="right">
  <b><a href="#wordpress-environment">[ ↥ Back To Top ]</a></b>
</div>
<br/>