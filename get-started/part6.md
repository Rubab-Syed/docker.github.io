---
title: "Get Started, Part 6: Deploy your app"
---
{% include_relative nav.html selected="6" %}

## Prerequisites

- [Install Docker](/engine/installation/).
- Read the orientation in [Part 1](index.md).
- Learn how to create containers in [Part 2](part2.md).
- Make sure you have pushed the container you created to a registry, as
  instructed; we'll be using it here.
- Ensure your image is working by
  running this and visiting `http://localhost/` (slotting in your info for
  `username`, `repo`, and `tag`):

  ```
  docker run -p 80:80 username/repo:tag
  ```
- Have a copy of your `docker-compose.yml` from [Part 5](part5.md) handy.

## Introduction

You've been editing the same Compose file for this entire tutorial. Well, we
have good news: that Compose file works just as well in production as it does
on your machine. Here, we go through some options for running your
Dockerized application.

## Choose an option

{% capture cloud %}
If you're okay with using Docker Community Edition in
production, you can use Docker Cloud to help manage your app on popular
cloud providers such as Amazon Web Services, DigitalOcean, and Microsoft Azure.

To set up and deploy:

- Connect Docker Cloud with your preferred provider, granting Docker Cloud permission
  to automatically provision and "Dockerize" VMs for you.
- Use Docker Cloud to create your computing resources and create your swarm.
- Deploy your app.

> **Note**: We will be linking into the Docker Cloud documentation here; be sure
  to come back to this page after completing each step.

### Connect Docker Cloud

First, link Docker Cloud with your cloud provider:

* [Amazon Web Services setup guide](/docker-cloud/cloud-swarm/link-aws-swarm/)
* [DigitalOcean setup guide](/docker-cloud/infrastructure/link-do.md)
* [Microsoft Azure setup guide](/docker-cloud/infrastructure/link-azure.md)
* [Packet setup guide](/docker-cloud/infrastructure/link-packet.md)
* [SoftLayer setup guide](/docker-cloud/infrastructure/link-softlayer.md)
* [Use the Docker Cloud Agent to Bring your Own Host](/docker-cloud/infrastructure/byoh.md)

### Create your swarm

After your cloud provider is all set up, create a Swarm:

* If you're on AWS you
  can [automatically create a
  swarm](/docker-cloud/cloud-swarm/create-cloud-swarm/).
* Otherwise, [create your nodes](/docker-cloud/getting-started/your_first_node/)
  in the Docker Cloud UI, and run the `docker swarm init` and `docker swarm join`
  commands you learned in [part 4](part4.md) over [SSH via Docker
  Cloud](/docker-cloud/infrastructure/ssh-into-a-node/). Finally, [enable Swarm
  Mode](/docker-cloud/cloud-swarm/using-swarm-mode/) by clicking the toggle at
  the top of the screen, and [register the
  swarm](/docker-cloud/cloud-swarm/register-swarms/) you just made.

### Deploy your app

[Connect to your swarm via Docker
Cloud](/docker-cloud/cloud-swarm/connect-to-swarm/). This opens a terminal whose
context is your local machine, but whose Docker commands are routed up to the
swarm running on your cloud provider.This is a little different from the
paradign you've been following, where you were slinging commands via SSH; now,
you can directly access both your local file system and your remote swarm,
enabling some very tidy-looking commands:

```
docker stack deploy -c docker-compose.yml getstartedlab
```

That's it! Your app is running in production and is managed by Docker Cloud.
{% endcapture %}
{% capture enterpriseboilerplate %}
Customers of Docker Enterprise Edition run a stable, commercially-supported
version of Docker Engine, and as an add-on they get our first-class management
software, Docker Datacenter. You can manage every aspect of your application
via UI using Universal Control Plane, run a private image registry with Docker
Trusted Registry, integrate with your LDAP provider, sign production images with
Docker Content Trust, and many other features.

[Take a tour of Docker Enterprise Edition](https://www.docker.com/enterprise-edition){: class="button outline-btn"}
{% endcapture %}
{% capture enterprisedeployapp %}
Once you're all set up and Datacenter is running, you can [deploy your Compose
file from directly within the UI](/datacenter/ucp/2.1/guides/user/services/).

![Deploy an app on DDC](/datacenter/ucp/2.1/guides/images/deploy-app-ui-1.png)

After that, you'll see it running, and can change any aspect of the application
you choose, or even edit the Compose file itself.

![Managing app on DDC](/datacenter/ucp/2.1/guides/images/deployed_visualizer.png)
{% endcapture %}
{% capture enterprisecloud %}
{{ enterpriseboilerplate }}

The bad news is: the only cloud providers with official Docker
Enterprise editions are Amazon Web Services and Microsoft Azure.

The good news is: there are one-click templates to quickly deploy Docker
Enterprise on each of these providers:

* [Docker Enterprise for AWS](https://store.docker.com/editions/enterprise/docker-ee-aws?tab=description)
* [Docker Enterprise for Azure](https://store.docker.com/editions/enterprise/docker-ee-azure?tab=description)

> **Note**: Having trouble with these? View [our setup guide for AWS](/datacenter/install/aws/).
> You can also [view the WIP guide for Microsoft Azure](https://github.com/docker/docker.github.io/pull/2796).

{{ enterprisedeployapp }}
{% endcapture %}
{% capture enterpriseonprem %}
{{ enterpriseboilerplate }}

Bringing your own server to Docker Enterprise and setting up Docker Datacenter
essentially involves two steps:

1. [Get Docker Enterprise Edition for your server's OS from Docker Store](https://store.docker.com/search?offering=enterprise&type=edition).
2. Follow the [instructions to install Datacenter on your own host](/datacenter/install/linux/).

> **Note**: Running Windows containers? View our [Windows Server setup guide](/docker-ee-for-windows/install/).

{{ enterprisedeployapp }}
{% endcapture %}

<ul class="nav nav-tabs">
  <li class="active"><a data-toggle="tab" href="#cloud">Community Edition (Cloud provider)</a></li>
  <li><a data-toggle="tab" href="#enterprisecloud">Enterprise Edition (Cloud provider)</a></li>
  <li><a data-toggle="tab" href="#enterpriseonprem">Enterprise Edition (On-premise)</a></li>
</ul>
<div class="tab-content">
  <div id="cloud" class="tab-pane fade in active" markdown="1">{{ cloud }}</div>
  <div id="enterprisecloud" class="tab-pane fade" markdown="1">{{ enterprisecloud }}</div>
  <div id="enterpriseonprem" class="tab-pane fade" markdown="1">{{ enterpriseonprem }}</div>
</div>

## Congratulations!

You've taken a full-stack, dev-to-deploy tour of the entire Docker platform.

There is much more to the Docker platform than what was covered here, but you
have a good idea of the basics of containers, images, services, swarms, stacks,
scaling, load-balancing, volumes, and placement constraints.

Want to go deeper? Here are some resources we recommend:

- [Samples](/samples/): Our samples include multiple examples of popular software
  running in containers, and some good labs that teach best practices.
- [User Guide](/engine/userguide/): The user guide has serveral examples that
  explain networking and storage in greater depth than was covered here.
- [Admin Guide](/engine/admin/): Covers how to manage a Dockerized production
  environment.
- [Training](https://training.docker.com/): Official Docker courses that offer
  in-person instruction and virtual classroom environments.
- [Blog](https://blog.docker.com): Covers what's going on with Docker lately.